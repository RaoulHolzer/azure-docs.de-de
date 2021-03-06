---
title: Herstellen von Verbindungen mit SQL-Datenbanken mithilfe von PHP unter Windows | Microsoft Docs
description: Enthält ein PHP-Beispielprogramm, das eine Verbindung von einem Windows-Client mit Azure SQL-Datenbank herstellt, sowie Links zu den auf dem Client erforderlichen Softwarekomponenten.
services: sql-database
documentationcenter: ''
author: meet-bhagdev
manager: jhubbard
editor: ''

ms.service: sql-database
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 06/16/2016
ms.author: meetb

---
# Herstellen von Verbindungen mit SQL-Datenbanken mithilfe von PHP unter Windows
[!INCLUDE [sql-database-develop-includes-selector-language-platform-depth](../../includes/sql-database-develop-includes-selector-language-platform-depth.md)]

In diesem Thema wird veranschaulicht, wie Sie von einer in PHP geschriebenen Clientanwendung, die unter Windows ausgeführt wird, eine Verbindung mit Azure SQL-Datenbank herstellen können.

## Schritt 1: Konfigurieren der Entwicklungsumgebung
[Configure development environment for PHP development](https://msdn.microsoft.com/library/mt720663.aspx) (Konfigurieren der Entwicklungsumgebung für die PHP-Entwicklung)

## Schritt 2: Erstellen einer SQL-Datenbank
Auf der [Seite für erste Schritte](sql-database-get-started.md) erhalten Sie Informationen zum Erstellen einer Beispieldatenbank. Sie sollten unbedingt die Anleitung zum Erstellen einer **AdventureWorks-Datenbankvorlage** befolgen. Die unten gezeigten Beispiele funktionieren nur mit dem **AdventureWorks-Schema**.

## Schritt 3: Abrufen der Verbindungsdetails
[!INCLUDE [sql-database-include-connection-string-details-20-portalshots](../../includes/sql-database-include-connection-string-details-20-portalshots.md)]

## Schritt 4: Ausführen von Beispielcode
* [Proof of concept connecting to SQL using PHP](https://msdn.microsoft.com/library/mt720665.aspx) (Machbarkeitsstudie für das Herstellen einer Verbindung mit SQL mithilfe von PHP)
* [Connect resiliently to SQL with PHP](https://msdn.microsoft.com/library/mt720667.aspx) (Stabile Verbindung mit SQL mithilfe von PHP)

## Nächste Schritte
* Lesen Sie die [Übersicht über die Entwicklung von SQL-Datenbanken](sql-database-develop-overview.md)
* Weitere Informationen zum [Microsoft PHP-Treiber für SQL Server](https://msdn.microsoft.com/library/dn865013.aspx)
* Weitere Informationen über die Installation und Verwendung von PHP finden Sie unter [Accessing SQL Server Databases with PHP](http://social.technet.microsoft.com/wiki/contents/articles/1258.accessing-sql-server-databases-from-php.aspx) (Zugreifen auf SQL Server-Datenbanken mit PHP, in englischer Sprache).

## Weitere Ressourcen
* [Entwurfsmuster für mehrinstanzenfähige SaaS-Anwendungen und Azure SQL-Datenbank](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* Entdecken Sie alle [Funktionen von SQL-Datenbank](https://azure.microsoft.com/services/sql-database/).

<!---HONumber=AcomDC_0622_2016-->