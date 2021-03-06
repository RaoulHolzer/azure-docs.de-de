---
title: Erstellen eines neuen elastischen Pools mit PowerShell | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie mithilfe von PowerShell Ressourcen für Azure SQL-Datenbanken horizontal hochskalieren können, indem Sie für die Verwaltung mehrerer Datenbanken einen skalierbaren elastischen Pool erstellen."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 37a707ee-9223-43ae-8c35-1ccafde8b83e
ms.service: sql-database
ms.custom: multiple databases
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
translationtype: Human Translation
ms.sourcegitcommit: 6c8420a154d998aa95c0220049ee54b3039a872b
ms.openlocfilehash: 679cdacc3782f667635a586df4cd77a9af7884d9


---
# <a name="create-a-new-elastic-pool-with-powershell"></a>Erstellen eines neuen elastischen Pools mit PowerShell
> [!div class="op_single_selector"]
> * [Azure-Portal](sql-database-elastic-pool-create-portal.md)
> * [PowerShell](sql-database-elastic-pool-create-powershell.md)
> * [C#](sql-database-elastic-pool-create-csharp.md)
>
>

Hier erfahren Sie, wie Sie mithilfe von PowerShell-Cmdlets einen [elastischen Pool](sql-database-elastic-pool.md) erstellen.

Häufige Fehlercodes finden Sie unter [SQL-Fehlercodes für SQL-Datenbank-Clientanwendungen: Datenbankverbindungsfehler und andere Probleme](sql-database-develop-error-messages.md).

> [!NOTE]
> Elastische Pools sind in allen Azure-Regionen allgemein verfügbar, mit Ausnahme von „USA, Norden-Mitte“ und „Indien, Westen“. Dort befinden sie sich derzeit in der Vorschauphase.  Die allgemeine Verfügbarkeit von elastischen Pools in diesen Regionen wird so bald wie möglich bereitgestellt. Elastische Pools unterstützen zurzeit keine Datenbanken mit [In-Memory-OLTP oder In-Memory-Analysen](sql-database-in-memory.md).
>
>

Sie müssen Azure PowerShell 1.0 oder höher installiert haben. Weitere Informationen finden Sie unter [Installieren und Konfigurieren von Azure PowerShell](/powershell/azureps-cmdlets-docs).

## <a name="create-a-new-pool"></a>Erstellen eines neuen Pools
Das Cmdlet [New-AzureRmSqlElasticPool](https://msdn.microsoft.com/library/azure/mt619378\(v=azure.300\).aspx) erstellt einen neuen Pool. Die Werte für die eDTUs pro Pool und die Mindest- und Höchstwerte für DTUs werden durch den Wert der Dienstebene (Basic, Standard oder Premium) beschränkt. Siehe hierzu [eDTUs und Speicherbeschränkungen für elastische Pools und elastische Datenbanken](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

    New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100


## <a name="create-a-new-elastic-database-in-a-pool"></a>Erstellen einer neuen elastischen Datenbank in einem Pool
Verwenden Sie das Cmdlet [New-AzureRmSqlDatabase](https://msdn.microsoft.com/library/azure/mt619339\(v=azure.300\).aspx), und legen Sie den **ElasticPoolName**-Parameter auf den Zielpool fest. Informationen dazu, wie Sie eine bestehende Datenbank in einen Pool verschieben, finden Sie unter [Verwalten und Skalieren eines Pools für elastische Datenbanken mit C#](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

    New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"

## <a name="create-a-pool-and-populate-it-with-multiple-new-databases"></a>Erstellen Sie einen Pool, und füllen Sie ihn mit mehreren neuen Datenbanken.
Das Erstellen einer großen Anzahl an Datenbanken in einem Pool kann eine Weile dauern, wenn dies über das Portal oder über PowerShell-Cmdlets erfolgt, die jeweils nur eine Einzeldatenbank erstellen. Zur Automatisierung des Erstellen in einem neuen Pool siehe [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).   

## <a name="example-create-a-pool-using-powershell"></a>Beispiel: Erstellen eines Pools mit PowerShell
Dieses Skript erstellt eine neue Azure-Ressourcengruppe und einen neuen Server. Wenn Sie aufgefordert werden, geben Sie einen Administratornamen und das Kennwort für den neuen Server ein (nicht Ihre Azure-Anmeldeinformationen).

    $subscriptionId = '<your Azure subscription id>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $serverName = '<server name>'
    $poolName = '<pool name>'
    $databaseName = '<database name>'

    Login-AzureRmAccount
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
    New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

    New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

    New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB



## <a name="next-steps"></a>Nächste Schritte
* [Verwalten Ihres Pools](sql-database-elastic-pool-manage-powershell.md)
* [Erstellen elastischer Aufträge](sql-database-elastic-jobs-overview.md) : Elastische Aufträge ermöglichen die Ausführung von T-SQL-Skripts für eine beliebige Anzahl von Datenbanken im Pool.
* [Skalieren mit der Azure SQL-Datenbank](sql-database-elastic-scale-introduction.md): Verwenden Sie elastische Datenbanktools für die horizontale Skalierung.



<!--HONumber=Jan17_HO1-->


