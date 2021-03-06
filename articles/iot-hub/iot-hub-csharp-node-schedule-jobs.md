---
title: "Planen von Aufträgen mit Azure IoT Hub | Microsoft Docs"
description: "In diesem Tutorial wird gezeigt, wie Sie Aufträge planen."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/17/2016
ms.author: juanpere
translationtype: Human Translation
ms.sourcegitcommit: 00746fa67292fa6858980e364c88921d60b29460
ms.openlocfilehash: ebda1823464d6148e5ab9f0276a72ed0f716f757


---
# <a name="tutorial-schedule-and-broadcast-jobs"></a>Tutorial: Planen und Übertragen von Aufträgen
[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

## <a name="introduction"></a>Einführung
Azure IoT Hub ist ein vollständig verwalteter Dienst, mit dem eine Back-End-App Aufträge erstellen und nachverfolgen kann, mit denen für Millionen von Geräten die Planung und Updates durchgeführt werden.  Aufträge können für die folgenden Aktionen verwendet werden:

* Aktualisieren gewünschter Eigenschaften
* Aktualisieren von Tags
* Aufrufen direkter Methoden

Vom Konzept her umschließt ein Auftrag eine dieser Aktionen und verfolgt den Ausführungsfortschritt für eine Gruppe von Geräten nach, die anhand einer Gerätezwillingsabfrage definiert wird.  Mit einem Auftrag kann eine Back-End-App beispielsweise eine Neustartmethode auf 10.000 Geräten aufrufen, die mit einer Gerätezwillingsabfrage angegeben und für einen späteren Zeitpunkt geplant ist.  Diese Anwendung kann dann den Fortschritt nachverfolgen, wenn diese Geräte jeweils die Neustartmethode empfangen und ausführen.

Weitere Informationen zu diesen Funktionen finden Sie in den folgenden Artikeln:

* Gerätezwilling und -eigenschaften: [Get started with device twins][lnk-get-started-twin] (Erste Schritte mit Gerätezwillingen) und [Tutorial: Verwenden der Eigenschaften von Gerätezwillingen][lnk-twin-props]
* Direkte Methoden: [Entwicklerhandbuch – direkte Methoden][lnk-dev-methods] und [Tutorial: Verwenden von direkten Methoden][lnk-c2d-methods]

Dieses Tutorial veranschaulicht folgende Vorgehensweisen:

* Erstellen eines simulierten Geräts mit einer direkten Methode, um die **lockDoor**-Funktion zu ermöglichen, die von der Back-End-App aufgerufen werden kann
* Erstellen einer Konsolenanwendung, die die direkte **lockDoor**-Methode auf der simulierten Geräte-App über einen Auftrag aufruft und die gewünschten Eigenschaften über einen Geräteauftrag aktualisiert

Am Ende dieses Tutorials verfügen Sie über eine Node.js-Konsolen-Geräte-App und eine .NET-Konsolen-Back-End-App (C#):

**simDevice.js**: Stellt mit der Geräteidentität eine Verbindung mit Ihrem IoT Hub her und empfängt eine direkte **lockDoor**-Methode.

**ScheduleJob**: Ruft eine direkte Methode auf der simulierten Geräte-App auf und aktualisiert die gewünschten Eigenschaften des Gerätezwillings per Auftrag.

Für dieses Tutorial benötigen Sie Folgendes:

* Microsoft Visual Studio 2015.
* Node.js Version 0.12.x oder höher, <br/>  Unter [Prepare your development environment][lnk-dev-setup] (Vorbereiten Ihrer Entwicklungsumgebung) wird beschrieben, wie Sie Node.js für dieses Tutorial unter Windows oder Linux installieren.
* Ein aktives Azure-Konto. (Wenn Sie über kein Konto verfügen, können Sie in nur wenigen Minuten ein [kostenloses Konto][lnk-free-trial] erstellen.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a>Planen von Aufträgen zum Aufrufen einer direkten Methode und Aktualisieren der Eigenschaften eines Gerätezwillings
In diesem Abschnitt erstellen Sie eine .NET-Konsolen-App (mit C#), mit der eine **lockDoor**-Remotefunktion auf einem Gerät mit einer direkten Methode initiiert wird, und aktualisieren die Eigenschaften des Gerätezwillings.

1. Fügen Sie in Visual Studio in der aktuellen Projektmappe mithilfe der Projektvorlage **Konsolenanwendung** ein Visual C#-Projekt für den klassischen Windows-Desktop hinzu. Geben Sie dem Projekt den Namen **ScheduleJob**.

    ![Neues Visual C#-Projekt für den klassischen Windows-Desktop][img-createapp]

2. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt **ScheduleJob**, und klicken Sie anschließend auf **NuGet-Pakete verwalten**.
3. Wählen Sie im Fenster **NuGet-Paket-Manager** die Option **Durchsuchen**, suchen Sie nach **microsoft.azure.devices**, wählen Sie zum Installieren des Pakets **Microsoft.Azure.Devices** die Option **Installieren**, und akzeptieren Sie die Nutzungsbedingungen. Bei diesem Verfahren werden das NuGet-Paket für das [Dienst SDK für Microsoft Azure IoT][lnk-nuget-service-sdk] sowie die dazugehörigen Abhängigkeiten heruntergeladen, installiert und mit einem Verweis versehen.

    ![Fenster „NuGet-Paket-Manager“][img-servicenuget]
4. Fügen Sie am Anfang der Datei **Program.cs** die folgenden `using`-Anweisungen hinzu:
   
        using Microsoft.Azure.Devices;
        
5. Fügen Sie der **Program** -Klasse die folgenden Felder hinzu. Ersetzen Sie die mehrfachen Platzhalterwerte durch die Verbindungszeichenfolge für den IoT Hub, den Sie im vorherigen Abschnitt erstellt haben.
   
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        
6. Fügen Sie der **Program** -Klasse die folgende Methode hinzu:
   
        public static async Task MonitorJob(string jobId)
        {
            JobResponse result;
            do
            {
                result = await jobClient.GetJobAsync(jobId);
                Console.WriteLine("Job Status : " + result.Status.ToString());
                Thread.Sleep(2000);
            } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
        }
                
7. Fügen Sie der **Program** -Klasse die folgende Methode hinzu:

        public static async Task StartMethodJob(string jobId)
        {
            CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

            JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
                "SELECT * from DEVICES",
                directMethod,
                DateTime.Now,
                10);

            Console.WriteLine("Started Method Job");
        }

8. Fügen Sie der **Program** -Klasse die folgende Methode hinzu:

        public static async Task StartTwinUpdateJob(string jobId)
        {
            var twin = new Twin();
            twin.Properties.Desired["Building"] = "43";
            twin.Properties.Desired["Floor"] = "3";
            twin.ETag = "*";

            JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
                "SELECT * from DEVICES", 
                twin,
                DateTime.Now,
                10);

            Console.WriteLine("Started Twin Update Job");
        }
 

9. Fügen Sie abschließend der **Main** -Methode die folgenden Zeilen hinzu:
   
        jobClient = JobClient.CreateFromConnectionString(connString);

        string methodJobId = Guid.NewGuid().ToString();

        StartMethodJob(methodJobId);
        MonitorJob(methodJobId).Wait();
        Console.WriteLine("Press ENTER to run the next job.");
        Console.ReadLine();

        string twinUpdateJobId = Guid.NewGuid().ToString();

        StartTwinUpdateJob(twinUpdateJobId);
        MonitorJob(twinUpdateJobId).Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
                   
10. Erstellen Sie die Projektmappe.

## <a name="create-a-simulated-device-app"></a>Erstellen einer simulierten Geräte-App
In diesem Abschnitt erstellen Sie eine Node.js-Konsolen-App, die auf eine von der Cloud aufgerufene direkte Methode antwortet. Diese Methode löst einen Neustart eines simulierten Geräts aus und ermöglicht mithilfe der gemeldeten Eigenschaften Abfragen des Gerätezwillings zum Identifizieren von Geräten und deren letztem Neustart.

1. Erstellen Sie einen leeren Ordner mit dem Namen **simDevice**.  Erstellen Sie im Ordner **simDevice** die Datei „package.json“, indem Sie an der Eingabeaufforderung den unten angegebenen Befehl verwenden.  Übernehmen Sie alle Standardeinstellungen:
   
    ```
    npm init
    ```
2. Führen Sie an der Eingabeaufforderung im Ordner **simDevice** den folgenden Befehl aus, um das Geräte-SDK-Paket **azure-iot-device** und das Paket **azure-iot-device-mqtt** zu installieren:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Erstellen Sie mit einem Text-Editor im Ordner **simDevice** die neue Datei **simDevice.js**.
4. Fügen Sie am Anfang der Datei **simDevice.js** die folgenden require-Anweisungen hinzu:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Fügen Sie die Variable **connectionString** hinzu, und verwenden Sie sie zum Erstellen eines Geräteclients.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Fügen Sie die folgende Funktion zur Behandlung der **lockDoor**-Methode hinzu.
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. Fügen Sie den folgenden Code hinzu, um den Handler für die **lockDoor**-Methode zu registrieren.
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub.  Waiting for reboot direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. Speichern und schließen Sie die Datei **simDevice.js**.

> [!NOTE]
> Der Einfachheit halber wird in diesem Tutorial keine Wiederholungsrichtlinie implementiert. Im Produktionscode sollten Sie Wiederholungsrichtlinien implementieren (z.B. einen exponentiellen Backoff), wie im MSDN-Artikel zum [Transient Fault Handling (Behandeln vorübergehender Fehler)][lnk-transient-faults] beschrieben.
> 
> 

## <a name="run-the-apps"></a>Ausführen der Apps
Sie können die Apps nun ausführen.

1. Führen Sie in der Befehlszeile im Ordner **simDevice** den folgenden Befehl aus, um mit dem Lauschen auf die direkte Methode zum Neustarten zu beginnen.
   
    ```
    node simDevice.js
    ```
2. Führen Sie die C#-Konsolen-App **ScheduleJob** aus – klicken Sie mit der rechten Maustaste auf das **ScheduleJob**-Projekt, wählen Sie **Debuggen** und **Neue Instanz starten**.

3. Sie sehen die Ausgabe von Geräte- und Back-End-App.

## <a name="next-steps"></a>Nächste Schritte
In diesem Tutorial haben Sie einen Auftrag zum Planen einer direkten Methode für ein Gerät und eines Updates der Eigenschaften eines Gerätezwillings verwendet.

Informationen zu den weiteren ersten Schritten mit IoT Hub und Geräteverwaltungsmustern, z.B. drahtloses Firmware-Remoteupdate, finden Sie unter:

[Tutorial: Durchführen eines Firmwareupdates][lnk-fwupdate]

Informationen zu den weiteren ersten Schritten mit IoT Hub finden Sie unter [Erste Schritte mit dem Gateway-SDK][lnk-gateway-SDK].

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-gateway-SDK]: iot-hub-linux-gateway-sdk-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/get_started/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/


<!--HONumber=Nov16_HO5-->


