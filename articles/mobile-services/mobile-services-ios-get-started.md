---
title: Erste Schritte mit Azure Mobile Services für iOS-Apps | Microsoft Docs
description: Befolgen Sie dieses Lernprogramm für die ersten Schritte bei der Verwendung von Azure Mobile Services für die iOS-Entwicklung.
services: mobile-services
documentationcenter: ios
author: krisragh
manager: dwrede
editor: ''

ms.service: mobile-services
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/21/2016
ms.author: krisragh

---
# <a name="getting-started"></a>Erste Schritte mit Mobile Services
[!INCLUDE [mobile-services-selector-get-started](../../includes/mobile-services-selector-get-started.md)]

&nbsp;

[!INCLUDE [mobile-service-note-mobile-apps](../../includes/mobile-services-note-mobile-apps.md)]

> Informationen zur entsprechenden Mobile Apps-Version dieses Themas finden Sie unter [Erstellen einer iOS-App in Azure Mobile Apps](../app-service-mobile/app-service-mobile-ios-get-started.md).
> 
> 

In diesem Lernprogramm erfahren Sie, wie Sie mit den Azure Mobile Services einen cloudbasierten Back-End-Dienst zu einer iOS-App hinzufügen können.

In diesem Lernprogramm erstellen Sie einen neuen mobilen Dienst und eine einfache *To-Do-Listen*-App, die App-Daten im neuen mobilen Dienst speichert. Der von Ihnen zu erstellende mobile Dienst verwendet JavaScript für die serverseitige Geschäftslogik. Informationen zum Erstellen eines mobilen Diensts mit serverseitiger Geschäftslogik in .NET finden Sie in der [.NET-Back-End-Version] dieses Themas.

> [!NOTE]
> Um dieses Lernprogramm abzuschließen, benötigen Sie ein Azure-Konto. Falls Sie kein Konto besitzen, können Sie sich für eine Azure-Testversion registrieren. So erhalten Sie [kostenlose mobile Dienste, die Sie auch nach Ablauf der Testversion weiter nutzen können](https://azure.microsoft.com/pricing/details/mobile-services/). Einzelheiten finden Sie unter [Kostenlose Azure-Testversion](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AE564AB28&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fde-DE%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started-ios%2F%20).
> 
> 

## <a name="create-new-service"> </a>Erstellen eines neuen mobilen Dienstes
[!INCLUDE [mobile-services-create-new-service](../../includes/mobile-services-create-new-service.md)]

## Erstellen einer neuen iOS-App
Sie können zum Erstellen einer neuen App, die mit Ihrem mobilen Dienst verbunden ist, eine einfache Schnellstartanleitung im klassischen Azure-Portal befolgen:

1. Klicken Sie im [klassischen Azure-Portal] auf **Mobile Services** und anschließend auf den mobilen Dienst, den Sie gerade erstellt haben.
2. Klicken Sie auf der Registerkarte "Schnellstart" unter **Eine Plattform wählen** auf **iOS**, und erweitern Sie die Option **Eine neue iOS-App erstellen**. Dadurch werden die Schritte zum Erstellen einer iOS-App angezeigt, die mit dem mobilen Dienst verbunden wird.
3. Klicken Sie auf **TodoItem-Tabelle erstellen**, um eine Tabelle zum Speichern von App-Daten zu erstellen.
4. Klicken Sie unter **Ihre App herunterladen und ausführen** auf **Download**. Dadurch wird das Projekt für die Beispielanwendung der *To-do-List* heruntergeladen, die zusammen mit dem Mobile Services iOS SDK mit dem mobilen Dienst verbunden ist. Speichern Sie die komprimierte Projektdatei auf Ihrem lokalen Computer, und notieren Sie sich den Speicherort.

## Ausführen der neuen iOS-App
[!INCLUDE [mobile-services-ios-run-app](../../includes/mobile-services-ios-run-app.md)]

<ol start="4"><li><p>Zurück im [klassischen Azure-Portal] klicken Sie auf die Registerkarte **DATEN** und dann auf die Tabelle **TodoItems**. Nun können Sie die von der App in die Tabelle eingefügten Daten durchsuchen.<p></li></ol></p>

## <a name="next-steps"> </a>Nächste Schritte
Erfahren Sie, wie Sie weitere wichtige Aufgaben in Mobile Services durchführen:

* [Erste Schritte mit der Synchronisierung von Offlinedaten] <br/>Erfahren Sie, wie Sie die Offlinedatensynchronisierung nutzen, um eine reaktionsfähige, stabile App zu implementieren.
* [Hinzufügen von Authentifizierung zu einer vorhandenen App] <br/>Informationen über die Authentifizierung von Benutzern der App mit einem Identitätsanbieter.
* [Hinzufügen von Pushbenachrichtigungen zu einer vorhandenen App] <br/>Erfahren Sie, wie Sie eine einfache Pushbenachrichtigung an Ihre App senden können.

[!INCLUDE [app-service-disqus-feedback-slug](../../includes/app-service-disqus-feedback-slug.md)]

<!-- Anchors. -->
[Getting started with Mobile Services]: #getting-started
[Create a new mobile service]: #create-new-service
[Define the mobile service instance]: #define-mobile-service-instance
[Next Steps]: #next-steps

<!-- Images. -->
[6]: ./media/mobile-services-ios-get-started/mobile-portal-quickstart-ios.png
[7]: ./media/mobile-services-ios-get-started/mobile-quickstart-steps-ios.png
[8]: ./media/mobile-services-ios-get-started/mobile-xcode-project.png

[10]: ./media/mobile-services-ios-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/mobile-services-ios-get-started/mobile-data-tab.png
[12]: ./media/mobile-services-ios-get-started/mobile-data-browse.png


<!-- URLs. -->
[Erste Schritte mit der Synchronisierung von Offlinedaten]: mobile-services-ios-get-started-offline-data.md
[Hinzufügen von Authentifizierung zu einer vorhandenen App]: mobile-services-dotnet-backend-ios-get-started-users.md
[Hinzufügen von Pushbenachrichtigungen zu einer vorhandenen App]: mobile-services-dotnet-backend-ios-get-started-push.md


[Mobile Services iOS SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[klassischen Azure-Portal]: https://manage.windowsazure.com/
[XCode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[.NET-Back-End-Version]: mobile-services-dotnet-backend-ios-get-started.md

<!---HONumber=AcomDC_0727_2016-->