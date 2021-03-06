---
title: 'NoSQL-Tutorial: DocumentDB .NET Core SDK | Microsoft Docs'
description: "Ein NoSQL-Tutorial, in dem eine Onlinedatenbank und eine C#-Konsolenanwendung mit dem DocumentDB .NET Core SDK erstellt werden. DocumentDB ist eine NoSQL-Datenbank für JSON."
keywords: nosql tutorial, online database, c# console application
services: documentdb
documentationcenter: .net
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 12/09/2016
ms.author: arramac
translationtype: Human Translation
ms.sourcegitcommit: 269d0a0c72d6509b91d7cc8fcffb6641006026f4
ms.openlocfilehash: 9323eb95ec014a1cc57daa8433e87f9d68b949f5


---
# <a name="nosql-tutorial-build-a-documentdb-c-console-application-on-net-core"></a>NoSQL-Tutorial: Erstellen einer DocumentDB-C#-Konsolenanwendung unter .NET Core
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Willkommen beim NoSQL-Tutorial für das Azure DocumentDB .NET Core SDK! Im Rahmen dieses Lernprogramms erstellen Sie eine Konsolenanwendung, mit der DocumentDB-Ressourcen erstellt und abgefragt werden können.

Folgende Themen werden behandelt:

* Erstellen eines DocumentDB-Kontos und Verbindungsaufbau
* Konfigurieren Ihrer Visual Studio-Projektmappe
* Erstellen einer Onlinedatenbank
* Erstellen einer Sammlung
* Erstellen von JSON-Dokumenten
* Abfragen der Sammlung
* Ersetzen eines Dokuments
* Löschen eines Dokuments
* Löschen der Datenbank

Sie haben nicht genügend Zeit? Keine Sorge! Die vollständige Lösung ist auf [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)verfügbar. Im Abschnitt [Abrufen der vollständigen Lösung](#GetSolution) finden Sie eine Kurzanleitung.

Bitte verwenden Sie nach Abschluss des Lernprogramms die Abstimmungsschaltflächen am Anfang oder Ende dieser Seite, um uns Ihre Meinung mitzuteilen. Wenn wir mit Ihnen Kontakt aufnehmen sollen, können Sie Ihre E-Mail-Adresse im Kommentar hinterlassen.

Lassen Sie uns anfangen.

## <a name="prerequisites"></a>Voraussetzungen
Stellen Sie sicher, dass Sie über Folgendes verfügen:

* Ein aktives Azure-Konto. Wenn Sie keines besitzen, können Sie sich für ein [kostenloses Konto](https://azure.microsoft.com/free/)registrieren. 
    * Als Alternative können Sie den [Azure DocumentDB-Emulator](documentdb-nosql-local-emulator.md) für dieses Tutorial verwenden.
* [Visual Studio 2015 Update 3](https://go.microsoft.com/fwlink/?LinkId=691129) und [.NET Core 1.0.1 – VS 2015 Tooling Preview 2](https://go.microsoft.com/fwlink/?LinkID=827546)
    * Wenn Sie einen Macintosh- oder Linux-Computer verwenden, können Sie .NET Core-Apps über die Befehlszeile entwickeln, indem Sie das [.NET Core SDK](https://www.microsoft.com/net/core#macos) für die Plattform Ihrer Wahl installieren. 
    * Wenn Sie unter Windows arbeiten, können Sie .NET Core-Apps über die Befehlszeile entwickeln, indem Sie das [.NET Core SDK](https://www.microsoft.com/net/core#windows) installieren. 
    * Sie können Ihren eigenen Editor verwenden oder [Visual Studio Code](https://code.visualstudio.com/) herunterladen (kostenlos und funktioniert unter Windows, Linux und MacOS). 

## <a name="step-1-create-a-documentdb-account"></a>Schritt 1: Erstellen eines DocumentDB-Kontos
In diesem Schritt erstellen Sie ein DocumentDB-Konto. Wenn Sie bereits über ein Konto verfügen, das Sie verwenden möchten, können Sie diesen Schritt überspringen und mit [Einrichten der Visual Studio-Projektmappe](#SetupVS)fortfahren. Wenn Sie den DocumentDB-Emulator verwenden, führen Sie die Schritte unter [Azure DocumentDB-Emulator](documentdb-nosql-local-emulator.md) zum Einrichten des Emulators aus, und fahren Sie dann mit [Einrichten Ihrer Visual Studio-Projektmappe](#SetupVS) fort.

[!INCLUDE [documentdb-create-dbaccount](../../includes/documentdb-create-dbaccount.md)]

## <a name="a-idsetupvsastep-2-setup-your-visual-studio-solution"></a><a id="SetupVS"></a>Schritt 2: Einrichten Ihrer Visual Studio-Projektmappe
1. Öffnen Sie **Visual Studio 2015** auf Ihrem Computer.
2. Wählen Sie im Menü **Datei** die Option **Neu** und anschließend **Projekt** aus.
3. Wählen Sie im Dialogfeld **Neues Projekt** die Option **Vorlagen** / **Visual C#** / **.NET Core**/**Konsolenanwendung (.NET Core)** aus, geben Sie Ihrem Projekt einen Namen, und klicken Sie dann auf **OK**.
   ![Screenshot des Fensters „Neues Projekt“](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)
4. Im **Projektmappen-Explorer**klicken Sie mit der rechten Maustaste auf die neue Konsolenanwendung, die sich unter Ihrer Visual Studio-Projektmappe befindet.
5. Klicken Sie dann, ohne das Menü zu verlassen, auf **NuGet-Pakete verwalten...**
   ![Screenshot des Kontextmenüs für das Projekt](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. Klicken Sie auf der Registerkarte **NuGet** auf **Durchsuchen**, und geben Sie in das Suchfeld **azure documentdb** ein.
7. Suchen Sie in den Ergebnissen nach **Microsoft.Azure.DocumentDB.Core**, und klicken Sie auf **Installieren**.
   Die Paket-ID für die DocumentDB-Clientbibliothek lautet [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).

Prima. Damit ist die Einrichtung abgeschlossen und wir können mit dem Schreiben von Code beginnen. Ein vollständiges Codeprojekt dieses Tutorials finden Sie auf [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).

## <a name="a-idconnectastep-3-connect-to-a-documentdb-account"></a><a id="Connect"></a>Schritt 3: Herstellen einer Verbindung mit einem DocumentDB-Konto
Fügen Sie zunächst in der Datei "Program.cs" am Anfang der C#-Anwendung folgende Verweise hinzu:

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART TO YOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> Um dieses NoSQL-Tutorial abzuschließen, müssen Sie die oben genannten Abhängigkeiten hinzufügen.
> 
> 

Fügen Sie diese beiden Konstanten und Ihre Variable *Client* nun unter der öffentlichen *Program*-Klasse hinzu.

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUri = "<your endpoint URI>";
        private const string PrimaryKey = "<your key>";
        private DocumentClient client;

Navigieren Sie als Nächstes zum [Azure-Portal](https://portal.azure.com) , um Ihren URI und den Primärschlüssel abzurufen. Der DocumentDB-URI und der Primärschlüssel sind erforderlich, damit Ihre Anwendung weiß, womit die Verbindung hergestellt werden soll, und damit DocumentDB weiß, dass die Verbindung Ihrer Anwendung vertrauenswürdig ist.

Navigieren Sie im Azure-Portal zu Ihrem DocumentDB-Konto, und klicken Sie auf **Schlüssel**.

Kopieren Sie den URI vom Portal, und fügen Sie ihn in `<your endpoint URI>` in der Datei „program.cs“ ein. Kopieren Sie anschließend den PRIMÄRSCHLÜSSEL aus dem Portal, und fügen Sie ihn in `<your key>`ein. Nutzen Sie bei Verwendung des Azure DocumentDB-Emulators `https://localhost:443` als Endpunkt und den klar definierten Autorisierungsschlüssel unter [How to develop using the DocumentDB Emulator](documentdb-nosql-local-emulator.md) (Entwickeln mit dem DocumentDB-Emulator).

![Screenshot des Azure-Portals, das vom NoSQL-Tutorial zum Erstellen einer C#-Konsolenanwendung verwendet wird. Zeigt ein DocumentDB-Konto, bei dem der ACTIVE-Hub, die Schaltfläche „SCHLÜSSEL“ auf dem Blatt „DocumentDB-Konto“ sowie auf dem Blatt „Schlüssel“ die Werte URI, PRIMÄRSCHLÜSSEL und SEKUNDÄRSCHLÜSSEL hervorgehoben sind.][keys]

Zu Beginn erstellen wir für die Anwendung zu den ersten Schritten eine neue Instanz von **DocumentClient**.

Fügen Sie unterhalb der **Main**-Methode die neue asynchrone Aufgabe mit der Bezeichnung **GetStartedDemo** hinzu. Sie dient zum Instanziieren des neuen **DocumentClient**-Elements.

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
    }

Fügen Sie den folgenden Code hinzu, um die asynchrone Aufgabe über die **Main** -Methode auszuführen. Mit der **Main** -Methode werden Ausnahmen abgefangen und in die Konsole geschrieben.

    static void Main(string[] args)
    {
            // ADD THIS PART TO YOUR CODE
            try
            {
                    Program p = new Program();
                    p.GetStartedDemo().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }

Drücken Sie F5 **** , um die Anwendung auszuführen.

Glückwunsch! Sie haben die Verbindung mit einem DocumentDB-Konto erfolgreich hergestellt. Als Nächstes sehen wir uns die Verwendung von DocumentDB-Ressourcen an.  

## <a name="step-4-create-a-database"></a>Schritt 4: Erstellen einer Datenbank
Bevor Sie den Code zum Erstellen einer Datenbank hinzufügen, fügen Sie eine Hilfsmethode zum Schreiben in die Konsole hinzu.

Kopieren Sie die **WriteToConsoleAndPromptToContinue**-Methode, und fügen Sie sie unterhalb der **GetStartedDemo**-Methode ein.

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

Ihre [DocumentDB](documentdb-resources.md#databases)-Datenbank kann mithilfe der Methode [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) der **DocumentClient**-Klasse erstellt werden. Eine Datenbank ist ein logischer Container für JSON-Dokumentspeicher, der auf Sammlungen aufgeteilt ist.

Kopieren Sie den folgenden Code, und fügen Sie ihn in die **GetStartedDemo** -Methode unterhalb der Clienterstellung ein. Eine Datenbank mit dem Namen *FamilyDB*wird erstellt.

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });

Drücken Sie F5 **** , um die Anwendung auszuführen.

Glückwunsch! Sie haben die Erstellung einer DocumentDB-Datenbank erfolgreich abgeschlossen.  

## <a name="a-idcreatecollastep-5-create-a-collection"></a><a id="CreateColl"></a>Schritt 5: Erstellen einer Sammlung
> [!WARNING]
> **CreateDocumentCollectionAsync** erstellt eine neue Sammlung mit reserviertem Durchsatz. Dies wirkt sich auf die Kosten aus. Weitere Informationen finden Sie auf unserer [Preisseite](https://azure.microsoft.com/pricing/details/documentdb/).
> 
> 

Eine [Sammlung](documentdb-resources.md#collections) kann mithilfe der [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx)-Methode der **DocumentClient**-Klasse erstellt werden. Eine Sammlung ist ein Container für JSON-Dokumente und die zugehörige JavaScript-Anwendungslogik.

Kopieren Sie den folgenden Code, und fügen Sie ihn unterhalb der Datenbankerstellung in die **GetStartedDemo** -Methode ein. Dadurch wird eine Dokumentsammlung namens *FamilyCollection_oa* erstellt.

        this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

        await this.CreateDatabaseIfNotExists("FamilyDB_oa");

        // ADD THIS PART TO YOUR CODE
        await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

Drücken Sie F5 **** , um die Anwendung auszuführen.

Glückwunsch! Sie haben die Erstellung einer DocumentDB-Dokumentsammlung erfolgreich abgeschlossen.  

## <a name="a-idcreatedocastep-6-create-json-documents"></a><a id="CreateDoc"></a>Schritt 6: Erstellen von JSON-Dokumenten
Ein [Dokument](documentdb-resources.md#documents) kann mithilfe der [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx)-Methode der **DocumentClient**-Klasse erstellt werden. Dokumente sind benutzerdefinierter (beliebiger) JSON-Inhalt. Wir können jetzt eines oder mehrere Dokumente einfügen. Wenn Sie bereits über Daten verfügen, die Sie in der Datenbank speichern möchten, können Sie das [Datenmigrationstool](documentdb-import-data.md)von DocumentDB verwenden.

Zunächst müssen wir eine **Family** -Klasse erstellen, die in diesem Beispiel in DocumentDB gespeicherte Objekte darstellt. Außerdem erstellen wir die Unterklassen **Parent**, **Child**, **Pet** und **Address**, die in **Family** verwendet werden. Beachten Sie, dass Dokumente eine **Id**-Eigenschaft enthalten müssen, die in JSON als **id** serialisiert wird. Erstellen Sie diese Klassen, indem Sie die folgenden internen Unterklassen nach der **GetStartedDemo** -Methode hinzufügen.

Kopieren Sie die Klassen **Family**, **Parent**, **Child**, **Pet** und **Address**, und fügen Sie sie unterhalb der **WriteToConsoleAndPromptToContinue**-Methode ein.

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }

    // ADD THIS PART TO YOUR CODE
    public class Family
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        public string LastName { get; set; }
        public Parent[] Parents { get; set; }
        public Child[] Children { get; set; }
        public Address Address { get; set; }
        public bool IsRegistered { get; set; }
        public override string ToString()
        {
                return JsonConvert.SerializeObject(this);
        }
    }

    public class Parent
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
    }

    public class Child
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
        public string Gender { get; set; }
        public int Grade { get; set; }
        public Pet[] Pets { get; set; }
    }

    public class Pet
    {
        public string GivenName { get; set; }
    }

    public class Address
    {
        public string State { get; set; }
        public string County { get; set; }
        public string City { get; set; }
    }

Kopieren Sie die **CreateFamilyDocumentIfNotExists**-Methode, und fügen Sie sie unterhalb der **CreateDocumentCollectionIfNotExists**-Methode ein.

    // ADD THIS PART TO YOUR CODE
    private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
            this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
                this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
            }
            else
            {
                throw;
            }
        }
    }

Fügen Sie zwei Dokumente ein: eines für die Familie Andersen und eines für die Familie Wakefield.

Kopieren Sie den folgenden Code, und fügen Sie ihn unterhalb der Erstellung der Dokumentsammlung in die **GetStartedDemo** -Methode ein.

    await this.CreateDatabaseIfNotExists("FamilyDB_oa");

    await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

    // ADD THIS PART TO YOUR CODE
    Family andersenFamily = new Family
    {
            Id = "Andersen.1",
            LastName = "Andersen",
            Parents = new Parent[]
            {
                    new Parent { FirstName = "Thomas" },
                    new Parent { FirstName = "Mary Kay" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FirstName = "Henriette Thaulow",
                            Gender = "female",
                            Grade = 5,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Fluffy" }
                            }
                    }
            },
            Address = new Address { State = "WA", County = "King", City = "Seattle" },
            IsRegistered = true
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

    Family wakefieldFamily = new Family
    {
            Id = "Wakefield.7",
            LastName = "Wakefield",
            Parents = new Parent[]
            {
                    new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                    new Parent { FamilyName = "Miller", FirstName = "Ben" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FamilyName = "Merriam",
                            FirstName = "Jesse",
                            Gender = "female",
                            Grade = 8,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Goofy" },
                                    new Pet { GivenName = "Shadow" }
                            }
                    },
                    new Child
                    {
                            FamilyName = "Miller",
                            FirstName = "Lisa",
                            Gender = "female",
                            Grade = 1
                    }
            },
            Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
            IsRegistered = false
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

Drücken Sie F5 **** , um die Anwendung auszuführen.

Glückwunsch! Sie haben die Erstellung von zwei DocumentDB-Dokumenten erfolgreich abgeschlossen.  

![Diagramm zur hierarchischen Beziehung zwischen dem Konto, der Onlinedatenbank, der Sammlung und den Dokumenten, die vom NoSQL-Tutorial zum Erstellen einer C#-Konsolenanwendung verwendet werden.](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a name="a-idqueryastep-7-query-documentdb-resources"></a><a id="Query"></a>Schritt 7: Abfragen von DocumentDB-Ressourcen
DocumentDB unterstützt umfassende [Abfragen](documentdb-sql-query.md) der in jeder Sammlung gespeicherten JSON-Dokumente.  Der folgende Beispielcode zeigt die verschiedenen Abfragen - sowohl mithilfe der SQL-Syntax als auch LINQ -, die wir nun mit den Dokumenten ausführen können, die wir im vorherigen Schritt eingefügt haben.

Kopieren Sie die **ExecuteSimpleQuery**-Methode, und fügen Sie sie unterhalb der **CreateFamilyDocumentIfNotExists**-Methode ein.

    // ADD THIS PART TO YOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find the Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute the same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

Kopieren Sie den folgenden Code, und fügen Sie ihn unterhalb der Erstellung des zweiten Dokuments in die **GetStartedDemo** -Methode ein.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

Drücken Sie F5 **** , um die Anwendung auszuführen.

Glückwunsch! Sie haben die Abfrage einer DocumentDB-Sammlung erfolgreich abgeschlossen.

Das folgende Diagramm veranschaulicht, wie die DocumentDB-SQL-Abfragesyntax gegen die erstellte Sammlung aufgerufen wird. Die gleiche Logik wird auf die LINQ-Abfrage angewendet.

![Diagramm zur Veranschaulichung des Bereichs und der Bedeutung der Abfrage, die vom NoSQL-Tutorial zum Erstellen einer C#-Konsolenanwendung verwendet wird.](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

Das [FROM](documentdb-sql-query.md#from-clause) -Schlüsselwort ist in der Abfrage optional, da DocumentDB Abfragen auf eine Sammlung begrenzt. Aus diesem Grund ist "FROM Familien f" austauschbar mit "FROM Stamm r" oder einem anderen variablen Namen, den Sie auswählen. DocumentDB wird ableiten, dass Familien, Stamm oder der variable Name, den Sie ausgewählt haben, standardmäßig auf die aktuelle Sammlung verweisen.

## <a name="a-idreplacedocumentastep-8-replace-json-document"></a><a id="ReplaceDocument"></a>Schritt 8: Ersetzen eines JSON-Dokuments
DocumentDB unterstützt das Ersetzen von JSON-Dokumenten.  

Kopieren Sie die **ReplaceFamilyDocument**-Methode, und fügen Sie sie unterhalb der **ExecuteSimpleQuery**-Methode ein.

    // ADD THIS PART TO YOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
        try
        {
            await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
            this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
        }
        catch (DocumentClientException de)
        {
            throw;
        }
    }

Kopieren Sie den folgenden Code, und fügen Sie ihn unterhalb der Abfrageausführung in die **GetStartedDemo** -Methode ein. Nach dem Ersetzen des Dokuments wird dieselbe Abfrage erneut ausgeführt, um das geänderte Dokument anzuzeigen.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

Drücken Sie F5 **** , um die Anwendung auszuführen.

Glückwunsch! Sie haben die Ersetzung eines DocumentDB-Dokuments erfolgreich abgeschlossen.

## <a name="a-iddeletedocumentastep-9-delete-json-document"></a><a id="DeleteDocument"></a>Schritt 9: Löschen eines JSON-Dokuments
DocumentDB unterstützt das Löschen von JSON-Dokumenten.  

Kopieren Sie die **DeleteFamilyDocument**-Methode, und fügen Sie sie unterhalb der **ReplaceFamilyDocument**-Methode ein.

    // ADD THIS PART TO YOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
        try
        {
            await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
            Console.WriteLine("Deleted Family {0}", documentName);
        }
        catch (DocumentClientException de)
        {
            throw;
        }
    }

Kopieren Sie den folgenden Code, und fügen Sie ihn unterhalb der zweiten Abfrageausführung in die **GetStartedDemo** -Methode ein.

    await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

Drücken Sie F5 **** , um die Anwendung auszuführen.

Glückwunsch! Sie haben das Löschen eines DocumentDB-Dokuments erfolgreich abgeschlossen.

## <a name="a-iddeletedatabaseastep-10-delete-the-database"></a><a id="DeleteDatabase"></a>Schritt 10: Löschen der Datenbank
Das Löschen der erstellten Datenbank entfernt die Datenbank und alle untergeordneten Ressourcen (Sammlungen, Dokumente usw.).

Kopieren Sie den folgenden Code, und fügen Sie ihn unterhalb des Dokumentlöschvorgangs in die **GetStartedDemo** -Methode ein, um die gesamte Datenbank und alle untergeordneten Ressourcen zu löschen.

    this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

    await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));

Drücken Sie F5 **** , um die Anwendung auszuführen.

Glückwunsch! Sie haben das Löschen einer DocumentDB-Datenbank erfolgreich abgeschlossen.

## <a name="a-idrunastep-11-run-your-c-console-application-all-together"></a><a id="Run"></a>Schritt 11: Ausführen der gesamten C#-Konsolenanwendung
Drücken Sie in Visual Studio F5 , um die Anwendung im Debugmodus zu erstellen.

Die Ausgabe der GetStarted-Anwendung sollte angezeigt werden. Die Ausgabe zeigt die Ergebnisse der hinzugefügten Abfragen an. Sie sollte mit unten stehendem Beispieltext übereinstimmen.

    Created FamilyDB_oa
    Press any key to continue ...
    Created FamilyCollection_oa
    Press any key to continue ...
    Created Family Andersen.1
    Press any key to continue ...
    Created Family Wakefield.7
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key to exit.

Glückwunsch! Sie haben dieses NoSQL-Tutorial abgeschlossen und verfügen über eine funktionierende C#-Konsolenanwendung!

## <a name="a-idgetsolutiona-get-the-complete-nosql-tutorial-solution"></a><a id="GetSolution"></a> Abrufen der vollständigen Projektmappe für das NoSQL-Tutorial
Um die "GetStarted"-Lösung zu erstellen, die alle Beispiele dieses Artikels enthält, ist Folgendes erforderlich:

* Ein aktives Azure-Konto. Wenn Sie keines besitzen, können Sie sich für ein [kostenloses Konto](https://azure.microsoft.com/free/)registrieren.
* Ein [DocumentDB-Konto][documentdb-create-account].
* [GetStarted-Projektmappe](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) (erhältlich auf GitHub)

Um die Verweise auf das DocumentDB .NET Core SDK in Visual Studio wiederherzustellen, klicken Sie mit der rechten Maustaste im Projektmappen-Explorer auf die **GetStarted**-Lösung und klicken dann auf die Option **NuGet-Paketwiederherstellung aktivieren**. Aktualisieren Sie anschließend in der Datei „Program.cs“ die Werte „EndpointUrl“ und „AuthorizationKey“ wie unter [Herstellen einer Verbindung mit einem DocumentDB-Konto](#Connect) beschrieben.

## <a name="next-steps"></a>Nächste Schritte
* Möchten Sie ein komplexeres ASP.NET MVC-NoSQL-Tutorial ausführen? Siehe: [Erstellen einer Webanwendung mit ASP.NET MVC unter Verwendung von DocumentDB](documentdb-dotnet-application.md).
* Möchten Sie Skalierungs- und Leistungstests mit DocumentDB durchführen? Siehe: [Leistungs- und Skalierungstests mit Azure DocumentDB](documentdb-performance-testing.md)
* Sie erfahren, wie Sie ein [DocumentDB-Konto überwachen](documentdb-monitor-accounts.md).
* Fragen Sie unser Beispieldataset im [Query Playground](https://www.documentdb.com/sql/demo)ab.
* Weitere Informationen zum Programmiermodell finden Sie auf der [DocumentDB-Dokumentationsseite](https://azure.microsoft.com/documentation/services/documentdb/)im Abschnitt "Entwickeln".

[documentdb-create-account]: documentdb-create-account.md
[documentdb-manage]: documentdb-manage.md
[keys]: media/documentdb-get-started/nosql-tutorial-keys.png



<!--HONumber=Dec16_HO2-->


