---
title: "Verknüpfen eines virtuellen Netzwerks mit einer ExpressRoute-Verbindung über das Resource Manager-Bereitstellungsmodell und das Azure-Portal | Microsoft Docs"
description: "In diesem Dokument erhalten Sie einen Überblick über das Verknüpfen von virtuellen Netzwerken (VNets) mit ExpressRoute-Verbindungen."
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 6a3604b95179d1a88f832ed45d9a6b85931187b1


---
# <a name="link-a-virtual-network-to-an-expressroute-circuit"></a>Verknüpfen eines virtuellen Netzwerks mit einer ExpressRoute-Verbindung
> [!div class="op_single_selector"]
> * [Azure-Portal – Resource Manager](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell – Resource Manager](expressroute-howto-linkvnet-arm.md)
> * [PowerShell – klassisch](expressroute-howto-linkvnet-classic.md)
> 
> 

Dieser Artikel unterstützt Sie beim Verknüpfen virtueller Netzwerke (VNets) mit Azure ExpressRoute-Verbindungen über das Resource Manager-Bereitstellungsmodell und das Azure-Portal. Virtuelle Netzwerke können Teil desselben Abonnements sein oder zu einem anderen Abonnement gehören.

**Informationen zu Azure-Bereitstellungsmodellen**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a>Konfigurationsvoraussetzungen
* Stellen Sie sicher, dass Sie vor Beginn der Konfiguration die Seiten [Voraussetzungen](expressroute-prerequisites.md), [Routinganforderungen](expressroute-routing.md) und [Workflows](expressroute-workflows.md) gelesen haben.
* Sie benötigen eine aktive ExpressRoute-Verbindung.
  
  * Führen Sie die Schritte zum [Erstellen einer ExpressRoute-Verbindung](expressroute-howto-circuit-arm.md) aus, und lassen Sie sie vom Konnektivitätsanbieter aktivieren.
  * Stellen Sie sicher, dass privates Azure-Peering für die Verbindung konfiguriert ist. Informationen zum Routing finden Sie unter [Konfigurieren des Routings](expressroute-howto-routing-portal-resource-manager.md) .
  * Vergewissern Sie sich, dass das private Azure-Peering konfiguriert wurde und das BGP-Peering zwischen Ihrem Netzwerk und Microsoft aktiv ist, damit End-to-End-Konnektivität bereitgestellt werden kann.
  * Vergewissern Sie sich, dass ein virtuelles Netzwerk und ein virtuelles Netzwerkgateway erstellt und vollständig bereitgestellt wurden. Folgen Sie der Anleitung, um ein [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) zu erstellen. (Führen Sie nur die Schritte 1 bis 5 aus.)

Sie können bis zu zehn virtuelle Netzwerke mit einer ExpressRoute-Standardverbindung verknüpfen. Alle virtuellen Netzwerke müssen sich in der gleichen geopolitischen Region befinden, wenn Sie eine ExpressRoute-Standardverbindung verwenden. Wenn Sie das ExpressRoute Premium-Add-On aktiviert haben, können Sie virtuelle Netzwerke außerhalb der geopolitischen Region der ExpressRoute-Verbindung oder eine größere Anzahl von virtuellen Netzwerken mit der Express Route-Verbindung verknüpfen. Weitere Informationen zum Premium-Add-On finden Sie in den [häufig gestellten Fragen](expressroute-faqs.md) .

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a>Herstellen einer Verbindung zwischen einem virtuellen Netzwerk in demselben Abonnement und einer Verbindung
### <a name="to-create-a-connection"></a>So stellen Sie eine Verbindung her
1. Stellen Sie sicher, dass Ihre ExpressRoute-Verbindung und das private Azure-Peering erfolgreich konfiguriert wurden. Befolgen Sie die Anweisungen unter [Erstellen einer ExpressRoute-Verbindung](expressroute-howto-circuit-arm.md) und [Konfigurieren des Routings](expressroute-howto-routing-arm.md). Ihre ExpressRoute-Verbindung sollte in etwa wie in der folgenden Abbildung dargestellt aussehen:
   
    ![Screenshot einer ExpressRoute-Verbindung](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
   > [!NOTE]
   > BGP-Konfigurationsinformationen werden nicht angezeigt, wenn Ihre Peerings vom Layer 3-Anbieter konfiguriert wurden. Wenn sich Ihre Verbindung im bereitgestellten Zustand befindet, sollten Sie Verbindungen erstellen können.
   > 
   > 
2. Jetzt können Sie damit beginnen, eine Verbindung zum Verknüpfen des virtuellen Netzwerkgateways mit Ihrer ExpressRoute-Verbindung bereitzustellen. Klicken Sie auf **Verbindung** > **Hinzufügen**, um das Blatt **Verbindung hinzufügen** zu öffnen, und konfigurieren Sie dann die Werte. Sehen Sie sich das folgende Referenzbeispiel an:

    ![Screenshot zum Hinzufügen der Verbindung](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  


1. Nachdem die Verbindung erfolgreich konfiguriert wurde, zeigt das Verbindungsobjekt die Daten für die Verbindung an.
   
    ![Screenshot des Verbindungsobjekts](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="to-delete-a-connection"></a>So löschen Sie eine Verbindung
Sie können eine Verbindung löschen, indem Sie das Symbol **Löschen** auf dem Blatt für Ihre Verbindung auswählen.

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a>Herstellen einer Verbindung zwischen einem virtuellen Netzwerk in einem anderen Abonnement und einer Verbindung
Zu diesem Zeitpunkt können Sie virtuelle Netzwerke in verschiedenen Abonnements nicht über das Azure-Portal verbinden. Allerdings können Sie PowerShell dazu verwenden. Weitere Informationen hierzu finden Sie im [PowerShell](expressroute-howto-linkvnet-arm.md) -Artikel.

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen über ExpressRoute finden Sie unter [ExpressRoute – FAQ](expressroute-faqs.md).




<!--HONumber=Nov16_HO3-->


