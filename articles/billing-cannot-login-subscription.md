---
title: Ich kann mich nicht anmelden, um mein Azure-Abonnement zu verwalten | Microsoft Docs
description: Informationen zur Problembehandlung bei einigen häufig auftretenden Anmeldeproblemen bei Azure-Abonnements
services: ''
documentationcenter: ''
author: genlin
manager: msmbaldwin
editor: ''
tags: billing

ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: genli

---
# Ich kann mich nicht anmelden, um mein Azure-Abonnement zu verwalten
Dieser Artikel führt Sie durch einige der am häufigsten verwendeten Methoden, um Anmeldungsprobleme zu beheben.

> [!NOTE]
> Wenn Sie bei irgendeinem Verfahren in diesem Artikel weitere Hilfe benötigen, [wenden Sie sich an den Support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), um das Problem schnell zu lösen.
> 
> 

## Die Seite hängt im Ladestatus
Dieses Problem kann mit einem Problem zusammenhängen, das Ihren Internetbrowser betrifft.

Um dieses Problem zu beheben, probieren Sie die folgenden Methoden in der angegebenen Reihenfolge aus. Nachdem Sie jede Methode ausprobiert haben, versuchen Sie erneut, eine Verbindung mit der Anmeldeseite im Portal herzustellen.

* Aktualisieren Sie die Seite.
* Verwenden Sie einen anderen Internetbrowser.
* Wenn Sie Microsoft Internet Explorer verwenden, navigieren Sie im InPrivate-Browsermodus zum Azure-Portal. Gehen Sie dazu folgendermaßen vor:
  
  A: Klicken Sie auf **Extras** ![Schaltfläche „Extras“](./media/billing-cannot-login-subscription/Toolsbutton.png) > **Sicherheit** > **InPrivate-Browsen**.
  
  B. Wechseln Sie zum [Azure-Portal](https://portal.azure.com), und melden Sie sich beim Portal an.

## Fehlermeldung „Keine Abonnements gefunden“
Dieses Problem kann auftreten, wenn das Konto nicht über ausreichende Benutzerrechte verfügt. Ein Kontoadministrator kann nur auf das [Kontocenter](https://account.windowsazure.com/) zugreifen, während Dienstadministratoren und Co-Administratoren nur Zugriff auf das [Azure-Portal](https://portal.azure.com) haben.

**Szenario 1: Fehlermeldung wird im [Azure-Portal](https://portal.azure.com) empfangen**

Zum Beheben dieses Problems [fügen Sie die Co-Administrator- oder Besitzerrolle](billing-add-change-azure-subscription-administrator.md) für das Konto hinzu.

**Szenario 2: Fehlermeldung wird im [Azure-Kontocenter](https://account.windowsazure.com/Subscriptions) empfangen**

Überprüfen Sie, ob das Konto, das Sie verwendet haben, das des Kontoadministrators ist. Gehen Sie folgendermaßen vor, um zu überprüfen, wer der Kontoadministrator ist:

1. Melden Sie sich auf dem [Azure-Portal](https://portal.azure.com) an.
2. Wählen Sie im Menü „Hub“ die Option **Abonnement** aus.
3. Wählen Sie das zu überprüfende Abonnement und dann **Einstellungen** aus.
4. Wählen Sie **Eigenschaften** aus. Der Kontoadministrator des Abonnements wird im Feld **Kontoadministrator** angezeigt.

## Sie werden automatisch als ein anderer Benutzer angemeldet
Dieses Problem kann auftreten, wenn Sie mehr als ein Benutzerkonto in einem Internetbrowser verwenden.

Um dieses Problem zu lösen, probieren Sie eine der folgenden Methoden aus:

* Melden Sie sich vom Portal ab und dann wieder mit dem Konto an, das Sie verwenden möchten.
* Löschen Sie Cache und Internetcookies. Klicken Sie hierzu in Internet Explorer auf **Extras** ![Schaltfläche „Extras“](./media/billing-cannot-login-subscription/Toolsbutton.png) > **Internetoptionen** > **Löschen**, stellen Sie sicher, dass die Kontrollkästchen für temporäre Dateien, Cookies, Kennwort und Verlauf aktiviert sind, und klicken Sie dann auf „Löschen“.
* Setzen Sie die Internet Explorer-Einstellungen zurück, um alle persönlichen Einstellungen wiederherstellen, die Sie vorgenommen haben. Klicken Sie hierzu auf **Extras** ![Schaltfläche „Extras“](./media/billing-cannot-login-subscription/Toolsbutton.png)> **Internetoptionen** > **Erweitert** > wählen Sie das Feld **Persönliche Einstellungen löschen** > **Zurücksetzen**.
* Navigieren Sie im Modus InPrivate-Browsen zum Azure-Portal. Klicken Sie hierzu auf **Extras** ![Schaltfläche „Extras“](./media/billing-cannot-login-subscription/Toolsbutton.png) > **Sicherheit** > **InPrivate-Browsen**.

## Sie müssen sich bei einem Organisationskonto anmelden
Ihr Microsoft-Konto ist die E-Mail-Adresse, die Sie zusammen mit Ihrem Kennwort verwenden, um sich bei Windows Live-Programmen oder -Diensten anzumelden, z. B. bei Outlook, Hotmail, MSN oder OneDrive. Sie können ein Microsoft-Konto mit einer beliebigen E-Mail-Adresse einrichten, z. B. auch mit Ihrer Firmen-E-Mail-Adresse. Weitere Informationen finden Sie unter [www.microsoft.com/account](http://www.microsoft.com/account).

Die Standardanmeldeseite des Azure-Portals ist für ein Microsoft-Konto gedacht. Wenn Ihr Konto mit einem Organisationskonto verknüpft ist, wählen Sie die richtige Anmeldeoption aus (siehe Abbildung unten). Weitere Informationen zur Verwendung eines Organisationskontos finden Sie unter [Als Unternehmen für Azure registrieren](active-directory/sign-up-organization.md).

![Anmeldeseite](./media/billing-cannot-login-subscription/signin.png)

> [!NOTE]
> Wenn Sie weitere Fragen haben, [wenden Sie sich an den Support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), um das Problem schnell zu lösen.
> 
> 

<!---HONumber=AcomDC_0928_2016-->