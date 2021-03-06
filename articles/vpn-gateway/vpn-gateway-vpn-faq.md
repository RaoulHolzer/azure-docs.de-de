---
title: "Häufig gestellte Fragen zu VPN Gateway und virtuellen Netzwerken | Microsoft Docs"
description: "Häufig gestellte Fragen zum VPN-Gateway. Häufig gestellte Fragen zu standortübergreifenden Verbindungen, Verbindungen mit Hybridkonfiguration und VPN-Gateways von Microsoft Azure Virtual Network"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2016
ms.author: yushwang
translationtype: Human Translation
ms.sourcegitcommit: dcda8b30adde930ab373a087d6955b900365c4cc
ms.openlocfilehash: e7d0fa43001268fc4747bbf40d3dc209aa037a67


---
# <a name="vpn-gateway-faq"></a>Häufig gestellte Fragen zum VPN-Gateway
## <a name="connecting-to-virtual-networks"></a>Herstellen einer Verbindung mit virtuellen Netzwerken
### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>Kann ich Verbindungen zwischen virtuellen Netzwerken in verschiedenen Azure-Regionen herstellen?
Ja. Es gelten keine regionsbedingten Einschränkungen. Verbindungen können sowohl zwischen virtuellen Netzwerken in der gleichen Region als auch zwischen virtuellen Netzwerken in unterschiedlichen Azure-Regionen hergestellt werden. 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>Kann ich Verbindungen zwischen virtuellen Netzwerken in unterschiedlichen Abonnements herstellen?
Ja.

### <a name="can-i-connect-to-multiple-sites-from-a-single-virtual-network"></a>Kann ich eine Verbindung mit mehreren Standorten eines einzelnen virtuellen Netzwerks herstellen?
Verbindungen mit mehreren Standorten können mit Windows PowerShell und den REST-APIs von Azure hergestellt werden. Weitere Informationen finden Sie im Abschnitt [Mehrere Standorte und VNet-zu-VNet-Verbindungen](#multi-site-and-vnet-to-vnet-connectivity) .

## <a name="what-are-my-cross-premises-connection-options"></a>Welche Optionen stehen mir bei standortübergreifenden Verbindungen zur Verfügung?
Die folgenden standortübergreifende Verbindungen werden unterstützt:

* [Standort zu Standort](vpn-gateway-site-to-site-create.md) : VPN-Verbindung über IPsec (IKE v1 und IKE v2). Für diese Art von Verbindung wird ein VPN-Gerät oder RRAS benötigt.
* [Punkt zu Standort](vpn-gateway-point-to-site-create.md) : VPN-Verbindung über SSTP (Secure Socket Tunneling-Protokoll). Für diese Verbindung wird kein VPN-Gerät benötigt.
* [VNet-zu-VNet](virtual-networks-configure-vnet-to-vnet-connection.md) : Dieser Verbindungstyp entspricht der Standort-zu-Standort-Konfiguration. VNet zu VNet ist eine VPN-Verbindung über IPsec (IKE v1 und IKE v2). Für diese Verbindung wird kein VPN-Gerät benötigt.
* [Mehrere Standorte](vpn-gateway-multi-site.md) : Hierbei handelt es sich um eine Variante der Standort-zu-Standort-Konfiguration, mit der Sie mehrere lokale Standorte mit einem virtuellen Netzwerk verbinden können.
* [ExpressRoute](../expressroute/expressroute-introduction.md) : ExpressRoute ist eine Azure-Direktverbindung mit Ihrem WAN (nicht über das öffentliche Internet). Weitere Informationen finden Sie unter [ExpressRoute – Technische Übersicht](../expressroute/expressroute-introduction.md) sowie unter [ExpressRoute – FAQ](../expressroute/expressroute-faqs.md).

Weitere Informationen zu Verbindungen finden Sie unter [Informationen zu VPN Gateway](vpn-gateway-about-vpngateways.md).

### <a name="what-is-the-difference-between-a-site-to-site-connection-and-point-to-site"></a>Was ist der Unterschied zwischen einer Standort-zu-Standort- und einer Punkt-zu-Standort-Verbindung?
**Standort zu Standort** : Bei diesem Verbindungstyp können Sie eine Verbindung zwischen lokalen Computern und virtuellen Computern oder Rolleninstanzen in Ihrem virtuellen Netzwerk herstellen (abhängig von der Routingkonfiguration). Diese Option eignet sich hervorragend für eine ständig verfügbare, standortübergreifende Verbindung sowie für Hybridkonfigurationen. Dieser Verbindungstyp basiert auf einer (hardware- oder softwarebasierten) IPsec-VPN-Appliance, die am Rand des Netzwerks bereitgestellt werden muss. Wenn Sie eine Verbindung dieses Typs erstellen möchten, benötigen Sie die erforderliche VPN-Hardware und eine extern ausgerichtete IPv4-Adresse.

**Punkt zu Standort** : Mit diesem Verbindungstyp können Sie ortsunabhängig eine Verbindung zwischen einem einzelnen Computer mit einer beliebigen Ressource in Ihrem virtuellen Netzwerk herstellen. Hierbei kommt der in Windows enthaltene VPN-Client zum Einsatz. Im Rahmen der Punkt-zu-Standort-Konfiguration installieren Sie ein Zertifikat und ein VPN-Clientkonfigurationspaket mit den Einstellungen, die es Ihrem Computer ermöglichen, eine Verbindung mit einem beliebigen virtuellen Computer oder einer beliebigen Rolleninstanz innerhalb des virtuellen Netzwerks herzustellen. Dieser Verbindungstyp eignet sich hervorragend, wenn Sie eine Verbindung mit einem virtuellen Netzwerk herstellen möchten, sich aber nicht vor Ort befinden. Er ist auch eine gute Wahl, wenn Ihnen keine VPN-Hardware oder keine extern ausgerichtete IPv4-Adresse zur Verfügung steht (beides Voraussetzungen für eine Standort-zu-Standort-Verbindung).

Sie können Ihr virtuelles Netzwerk für die parallele Verwendung von Standort-zu-Standort- und Punkt-zu-Standort-Verbindungen konfigurieren. Hierzu müssen Sie Ihre Standort-zu-Standort-Verbindung mit einem routenbasierten VPN-Typ für Ihr Gateway erstellen. Routenbasierte VPN-Typen werden im klassischen Bereitstellungsmodell als dynamische Gateways bezeichnet.

### <a name="what-is-expressroute"></a>Was ist ExpressRoute?
ExpressRoute ermöglicht es Ihnen, private Verbindungen zwischen Microsoft-Datencentern und einer Infrastruktur bei Ihnen vor Ort oder in einer Kollokationsumgebung zu erstellen. Mit ExpressRoute können Sie Verbindungen mit Microsoft-Clouddiensten wie Microsoft Azure und Office 365 an einem ExpressRoute-Partnerkollokationsstandort oder direkt über Ihr vorhandenen WAN (etwa über das MPLS-VPN eines Netzwerkdienstanbieters) herstellen.

ExpressRoute-Verbindungen sind sicherer, zuverlässiger und bieten eine höhere Bandbreite sowie eine geringere Latenz als herkömmliche Verbindungen über das Internet. In einigen Fällen können durch die Verwendung von ExpressRoute-Verbindungen zum Übertragen von Daten zwischen einem lokalen Netzwerk und Azure auch drastische Kosteneinsparungen erzielt werden. Wenn Sie aus Ihrem lokalen Netzwerk heraus bereits eine standortübergreifende Verbindung mit Azure hergestellt haben, können Sie eine Migration auf eine ExpressRoute-Verbindung durchführen, während das virtuelle Netzwerk intakt bleibt.

Weitere Informationen finden Sie unter [ExpressRoute – FAQ](../expressroute/expressroute-faqs.md) .

## <a name="site-to-site-connections-and-vpn-devices"></a>Standort-zu-Standort-Verbindungen und VPN-Geräte
### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>Was muss ich bei der Wahl eines VPN-Geräts berücksichtigen?
Wir haben in Zusammenarbeit mit Geräteherstellern eine Reihe von VPN-Geräten für standardmäßige Standort-zu-Standort-Verbindungen getestet. Eine Liste mit kompatiblen VPN-Geräten, entsprechenden Konfigurationsanweisungen oder -beispielen und Gerätespezifikationen finden Sie [hier](vpn-gateway-about-vpn-devices.md). Alle Geräte der als kompatibel angegebenen Gerätefamilien sollten mit Virtual Network verwendet werden können. Hilfreiche Informationen zur Konfiguration des VPN-Gerätes finden Sie im entsprechenden Konfigurationsbeispiel oder unter dem Link für die entsprechende Gerätefamilie.

### <a name="what-do-i-do-if-i-have-a-vpn-device-that-isnt-in-the-known-compatible-device-list"></a>Was kann ich tun, wenn mein VPN-Gerät nicht in der Liste bekannter kompatibler Geräte enthalten ist?
Wenn Ihr Gerät nicht in der Liste bekannter kompatibler VPN-Geräte enthalten ist und Sie das Gerät für Ihre VPN-Verbindung verwenden möchten, vergewissern Sie sich [hier](vpn-gateway-about-vpn-devices.md), dass es für die unterstützten IPsec-/IKE-Konfigurationsoptionen und -parameter geeignet ist. Geräte, die die Mindestanforderungen erfüllen, sollten problemlos mit VPN-Gateways verwendet werden können. Zusätzliche Unterstützung und Konfigurationsanweisungen erhalten Sie vom Gerätehersteller.

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a>Warum fällt mein richtlinienbasierter VPN-Tunnel aus, wenn kein Datenverkehr stattfindet?
Dabei handelt es sich um einen Standardvorgang bei richtlinienbasierten (auch als „statisches Routing“ bezeichnet) VPN-Gateways. Wenn im Tunnel länger als 5 Minuten kein Datenverkehr stattfindet, wird der Tunnel geschlossen. Bei erneut einsetzendem Datenverkehr wird der Tunnel umgehend wiederhergestellt. Die Richtung des Datenverkehrs ist dabei unerheblich.

### <a name="can-i-use-software-vpns-to-connect-to-azure"></a>Kann ich VPN-Softwarelösungen verwenden, um eine Verbindung mit Azure herzustellen?
Für die standortübergreifende Standort-zu-Standort-Konfiguration werden Routing- und RAS-Server unter Windows Server 2012 unterstützt.

Auch andere VPN-Softwarelösungen können mit unserem Gateway verwendet werden, sofern sie über branchenübliche IPsec-Implementierungen verfügen. Konfigurations- und Supportinformationen erhalten Sie vom Anbieter der Software.

## <a name="point-to-site-connections"></a>Punkt-zu-Standort-Verbindungen
### <a name="what-operating-systems-can-i-use-with-point-to-site"></a>Welche Betriebssysteme kann ich bei Punkt-zu-Standort-Verbindungen verwenden?
Folgende Betriebssysteme werden unterstützt:

* Windows 7 (32 Bit und 64 Bit)
* Windows Server 2008 R2 (nur 64 Bit)
* Windows 8 (32 Bit und 64 Bit)
* Windows 8.1 (32 Bit und 64 Bit)
* Windows Server 2012 (nur 64 Bit)
* Windows Server 2012 R2 (nur 64 Bit)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>Kann ich für Punkt-zu-Standort-Verbindungen einen beliebigen VPN-Softwareclient mit SSTP-Unterstützung verwenden?
Nein. Nur die oben aufgeführten Windows-Betriebssystemversionen werden unterstützt.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>Wie viele VPN-Clientendpunkte kann meine Punkt-zu-Standort-Konfiguration umfassen?
Wir unterstützen bis zu 128 gleichzeitige VPN-Clientverbindungen mit einem virtuellen Netzwerk.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>Kann ich für Punkt-zu-Standort-Verbindungen meine eigene interne PKI-Stammzertifizierungsstelle verwenden?
Ja. Bisher konnten nur selbstsignierte Stammzertifikate verwendet werden. Sie können weiterhin 20 Stammzertifikate hochladen.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>Können Proxys und Firewalls mit der Punkt-zu-Standort-Funktion durchlaufen werden?
Ja. Wir verwenden das Secure Socket Tunneling-Protokoll (SSTP), um eine Tunnelverbindung durch Firewalls zu ermöglichen. Dieser Tunnel wird als HTTPS-Verbindung angezeigt.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-the-vpn-automatically-reconnect"></a>Wird die VPN-Verbindung eines für „Punkt zu Standort“ konfigurierten Clientcomputers nach einem Neustart automatisch wiederhergestellt?
Standardmäßig wird die VPN-Verbindung des Clientcomputers nicht automatisch wiederhergestellt.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-the-vpn-clients"></a>Werden automatische Verbindungswiederherstellung und DDNS bei Punkt-zu-Standort-Verbindungen auf den VPN-Clients unterstützt?
Automatische Verbindungswiederherstellung und DDNS werden in Punkt-zu-Standort-VPNs derzeit nicht unterstützt.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-the-same-virtual-network"></a>Kann ich im gleichen virtuellen Netzwerk sowohl Standort-zu-Standort- als auch Punkt-zu-Standort-Konfigurationen verwenden?
Ja. Beide Lösungen können verwendet werden, wenn Sie über einen routenbasierten VPN-Typ für Ihr Gateway verfügen. Für das klassische Bereitstellungsmodell benötigen Sie ein dynamisches Gateway. Punkt-zu-Standort-Konfigurationen werden für VPN Gateways mit statischem Routing oder Gateways mit „-VpnType = PolicyBased“ nicht unterstützt.

### <a name="can-i-configure-a-point-to-site-client-to-connect-to-multiple-virtual-networks-at-the-same-time"></a>Kann ich einen Punkt-zu-Standort-Client so konfigurieren, dass er gleichzeitig eine Verbindung mit mehreren virtuellen Netzwerken herstellt?
Ja, das ist möglich. Allerdings dürfen sich weder die IP-Präfixe noch die Punkt-zu-Standort-Adressräume der virtuellen Netzwerke überschneiden.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>Wie viel Durchsatz kann ich bei einer Standort-zu-Standort- oder bei einer Punkt-zu-Standort-Verbindung erwarten?
Der genaue Durchsatz der VPN-Tunnel lässt sich nur schwer ermitteln. IPsec und SSTP sind VPN-Protokolle mit hohem Kryptografieaufwand. Außerdem wird der Durchsatz durch die Latenz und die Bandbreite zwischen Ihrem Standort und dem Internet eingeschränkt.

## <a name="gateways"></a>Gateways
### <a name="what-is-a-policy-based-static-routing-gateway"></a>Was ist ein richtlinienbasiertes Gateway mit statischem Routing?
Richtlinienbasierte Gateways implementieren richtlinienbasierte VPNs verwendet. Bei richtlinienbasierten VPNs werden Pakete verschlüsselt und durch IPsec-Tunnel geleitet. Grundlage hierfür sind Kombinationen aus Adresspräfixen zwischen Ihrem lokalen Netzwerk und dem Azure-VNet. Die Richtlinie (auch Datenverkehrsselektor genannt) wird in der Regel als Zugriffsliste in der VPN-Konfiguration definiert.

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a>Was ist ein routebasiertes Gateway mit dynamischem Routing?
Routenbasierte Gateways implementieren die routenbasierten VPNs. Bei routingbasierten VPNs werden Pakete auf der Grundlage der Routen der IP-Weiterleitungs- oder -Routingtabelle an die entsprechenden VPN-Tunnelschnittstellen weitergeleitet. An den Tunnelschnittstellen werden die Pakete dann ver- bzw. entschlüsselt. Die Richtlinie bzw. der Datenverkehrsselektor für routingbasierte VPNs werden im Any-to-Any-Format (bzw. als Platzhalter) konfiguriert.

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>Kann ich die IP-Adresse meines VPN-Gateways vor dessen Erstellung erhalten?
Nein. Die IP-Adresse kann erst nach der Erstellung des Gateways bezogen werden. Wenn Sie das VPN-Gateway löschen und anschließend neu erstellen, ändert sich die IP-Adresse.

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>Wie wird mein VPN-Tunnel authentifiziert?
Beim Azure-VPN erfolgt die Authentifizierung mittels vorinstalliertem Schlüssel (Pre-Shared Key, PSK). Der vorinstallierte Schlüssel wird bei der Erstellung des VPN-Tunnels generiert. Der automatisch generierte PSK kann mit dem PowerShell-Cmdlet „Set Pre-Shared Key“ oder mithilfe der entsprechenden REST-API angepasst werden.

### <a name="can-i-use-the-set-pre-shared-key-api-to-configure-my-policy-based-static-routing-gateway-vpn"></a>Kann ich mit der API „Set Pre-Shared Key“ mein richtlinienbasiertes VPN mit statischem Routing-Gateway konfigurieren?
Ja. Mit der API „Set Pre-Shared Key“ und dem PowerShell-Cmdlet können Sie sowohl richtlinienbasierte (statische) Azure-VPNs als auch routenbasierte (dynamische) VPNs konfigurieren.

### <a name="can-i-use-other-authentication-options"></a>Kann ich andere Authentifizierungsoptionen verwenden?
Für die Authentifizierung können nur vorinstallierte Schlüssel (Pre-Shared Keys, PSKs) verwendet werden.

### <a name="what-is-the-gateway-subnet-and-why-is-it-needed"></a>Was ist das Gatewaysubnetz, und wozu wird es benötigt?
Es gibt einen Gatewaydienst, der ausgeführt wird, um standortübergreifende Verbindungen zu ermöglichen.

Sie müssen ein Gatewaysubnetz für Ihr VNet erstellen, um ein VPN Gateway zu konfigurieren. Alle Gatewaysubnetze müssen den Namen „GatewaySubnet“ haben, damit sie einwandfrei funktionieren. Verwenden Sie für Ihr Gatewaysubnetz keinen anderen Namen. Zudem dürfen keine VMs oder anderen Komponenten im Gatewaysubnetz bereitgestellt werden.

Die Mindestgröße des Gatewaysubnetzes hängt gänzlich von der Konfiguration ab, die Sie erstellen möchten. Obwohl es bei manchen Konfigurationen möglich ist, ein Gatewaysubnetz mit einer Größe von nur /29 zu erstellen, empfehlen wir, ein Gatewaysubnetz von mindestens /28 (/ 28, / 27, /26 usw.) zu erstellen.

### <a name="can-i-deploy-virtual-machines-or-role-instances-to-my-gateway-subnet"></a>Kann ich virtuelle Computer oder Rolleninstanzen in meinem Gatewaysubnetz bereitstellen?
Nein.

### <a name="how-do-i-specify-which-traffic-goes-through-the-vpn-gateway"></a>Wie kann ich angeben, welcher Datenverkehr über das VPN-Gateway abgewickelt werden soll?
Wenn Sie das klassische Azure-Portal verwenden, fügen Sie die einzelnen Bereiche, die über das Gateway für Ihr virtuelles Netzwerk gesendet werden sollen, auf der Seite "Netzwerke" unter "Lokale Netzwerke" hinzu.

### <a name="can-i-configure-forced-tunneling"></a>Kann ich eine erzwungene Tunnelung konfigurieren?
Ja. Weitere Informationen finden Sie unter [Konfigurieren der Tunnelerzwingung](vpn-gateway-about-forced-tunneling.md).

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-to-connect-to-my-on-premises-network"></a>Kann ich in Azure einen eigenen VPN-Server einrichten und damit eine Verbindung mit meinem lokalen Netzwerk herstellen?
Ja. Sie können in Azure eigene VPN-Gateways oder -Server bereitstellen (entweder über Azure Marketplace oder durch Erstellung eines eigenen VPN-Routers). Sie müssen in Ihrem virtuellen Netzwerk benutzerdefinierte Routen konfigurieren, um sicherzustellen, dass der Datenverkehr ordnungsgemäß zwischen Ihren lokalen Netzwerken und den Subnetzen Ihres virtuellen Netzwerks weitergeleitet wird.

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>Warum werden auf meinem VPN-Gateway bestimmte Ports geöffnet?
Sie sind für die Kommunikation mit der Azure-Infrastruktur erforderlich. Sie werden von Azure-Zertifikaten geschützt (gesperrt). Ohne die richtigen Zertifikate werden externe Entitäten, einschließlich der Kunden dieser Gateways, sich nicht auf diese Endpunkte auswirken.

Ein VPN-Gateway ist im Grunde ein mehrfach vernetztes Gerät mit einer NIC, die das private Netzwerk des Kunden nutzt, und einer NIC für das öffentliche Netzwerk. Azure-Infrastrukturentitäten können aus Compliance-Gründen keine privaten Netzwerke von Kunden nutzen, sodass sie öffentliche Endpunkte für die Kommunikation der Infrastruktur nutzen müssen. Die öffentlichen Endpunkte werden in regelmäßigen Abständen mit der Azure-Sicherheitsüberwachung überprüft.

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>Weitere Informationen zu Gatewaytypen, Anforderungen und Durchsatz
Weitere Informationen finden Sie unter [Informationen zu VPN Gateway-Einstellungen](vpn-gateway-about-vpn-gateway-settings.md).

## <a name="multi-site-and-vnet-to-vnet-connectivity"></a>Mehrere Standorte und VNet-zu-VNet-Verbindungen
### <a name="which-type-of-gateways-can-support-multi-site-and-vnet-to-vnet-connectivity"></a>Welche Art von Gateway unterstützt mehrere Standorte sowie VNet-zu-VNet-Verbindungen?
Nur routenbasierte VPNs (mit dynamischem Routing).

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-to-another-vnet-with-a-policybased-vpn-type"></a>Kann ich ein VNet mit einem routenbasierten VPN-Typ (RouteBased) mit einem anderen VNet mit einem richtlinienbasierten VPN (PolicyBased) verbinden?
Nein. Beide virtuellen Netzwerke müssen routenbasierte VPNs (mit dynamischem Routing) verwenden.

### <a name="is-the-vnet-to-vnet-traffic-secure"></a>Ist der Datenverkehr bei VNet-zu-VNet-Verbindungen sicher?
Ja, er wird mittels IPsec-/IKE-Verschlüsselung geschützt.

### <a name="does-vnet-to-vnet-traffic-travel-over-the-azure-backbone"></a>Wird VNet-zu-VNet-Datenverkehr über den Azure-Backbone übertragen?
Ja.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>Mit wie vielen lokalen Standorten und virtuellen Netzwerken kann ein virtuelles Netzwerk verbunden werden?
Max. zehn (kombiniert für Basic- und Standard-Gateways mit dynamischem Routing); 30 bei VPN-Hochleistungsgateways.

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>Kann ich Punkt-zu-Standort-VPNs mit meinem virtuellen Netzwerk und mehreren VPN-Tunneln kombinieren?
Ja. VPNs vom Typ „Punkt zu Standort“ (P2S) können mit den VPN Gateways kombiniert werden, die Verbindungen mit mehreren lokalen Standorten und anderen virtuellen Netzwerken herstellen.

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a>Kann ich mithilfe eines VPNs mit mehreren Standorten mehrere Tunnel zwischen meinem virtuellen Netzwerk und meinem lokalen Standort konfigurieren?
Nein. Redundante Tunnel zwischen einem virtuellen Netzwerk von Azure und einem lokalen Standort werden nicht unterstützt.

### <a name="can-there-be-overlapping-address-spaces-among-the-connected-virtual-networks-and-on-premises-local-sites"></a>Dürfen sich die Adressräume der verbundenen virtuellen Netzwerke und der lokalen Standorte überschneiden?
Nein. Bei einer Überschneidung der Adressräume kann die Netzwerkkonfigurationsdatei nicht hochgeladen und kein virtuelles Netzwerk erstellt werden.

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a>Erhalte ich durch mehr Standort-zu-Standort-VPNs mehr Bandbreite als bei einem einzelnen virtuellen Netzwerk?
Nein. Alle VPN-Tunnel (einschließlich Punkt-zu-Standort-VPNs) verwenden das gleiche Azure-VPN Gateway und die gleiche verfügbare Bandbreite.

### <a name="can-i-use-azure-vpn-gateway-to-transit-traffic-between-my-on-premises-sites-or-to-another-virtual-network"></a>Kann ich mit dem Azure-VPN Gateway Datenverkehr zwischen meinen lokalen Standorten oder an ein anderes virtuelles Netzwerk übertragen?
**Klassisches Bereitstellungsmodell**<br>
Datenverkehr kann bei Verwendung des klassischen Bereitstellungsmodells über das Azure-VPN-Gateway übertragen werden, die Übertragung basiert jedoch auf statisch definierten Adressräumen aus der Netzwerkkonfigurationsdatei. BGP wird bei Azure Virtual Networks und VPN-Gateways, für die das klassische Bereitstellungsmodell verwendet wird, noch nicht unterstützt. Ohne BGP müssen die Adressräume für die Übertragung manuell definiert werden. Dies ist jedoch sehr fehleranfällig und wird daher nicht empfohlen.<br>
**Resource Manager-Bereitstellungsmodell**<br>
Wenn Sie das Resource Manager-Bereitstellungsmodell verwenden, finden Sie weitere Informationen im Abschnitt [BGP](#bgp).

### <a name="does-azure-generate-the-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-the-same-virtual-network"></a>Generiert Azure für alle meine VPN-Verbindungen für das gleiche virtuelle Netzwerk den gleichen vorinstallierten IPsec-/IKE-Schlüssel?
Nein. Azure generiert für unterschiedliche VPN-Verbindungen standardmäßig unterschiedliche vorinstallierte Schlüssel. Mit der REST-API oder dem PowerShell-Cmdlet „Set VPN Gateway Key“ können Sie jedoch den Schlüsselwert nach Ihren Vorstellungen festlegen. Bei dem Schlüssel muss es sich zwingend um eine alphanumerische Zeichenfolge mit einer Länge zwischen einem und 128 Zeichen handeln.

### <a name="does-azure-charge-for-traffic-between-virtual-networks"></a>Fallen bei Azure Kosten für den Datenverkehr zwischen virtuellen Netzwerken an?
Beim Datenverkehr zwischen verschiedenen virtuellen Netzwerken fallen nur Kosten an, wenn sich die Daten zwischen verschiedenen Azure-Regionen bewegen. Die Höhe der Kosten finden Sie auf der Azure-Seite [VPN Gateway Preise](https://azure.microsoft.com/pricing/details/vpn-gateway/) .

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-to-my-expressroute-circuit"></a>Kann ich eine Verbindung zwischen einem virtuellen Netzwerk mit IPsec-VPNs und meiner ExpressRoute-Verbindung herstellen?
Ja, diese Möglichkeit wird unterstützt. Weitere Informationen finden Sie unter [Konfigurieren von gleichzeitig vorhandenen ExpressRoute- und Standort-zu-Standort-VPN-Verbindungen](../expressroute/expressroute-howto-coexist-classic.md).

## <a name="a-namebgpabgp"></a><a name="bgp"></a>BGP
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="cross-premises-connectivity-and-vms"></a>Standortübergreifende Konnektivität und virtuelle Computer
### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-to-the-vm"></a>Wenn sich mein virtueller Computer in einem virtuellen Netzwerk befindet und ich über eine standortübergreifende Verbindung verfüge, wie sollte ich dann die Verbindung mit dem virtuellen Computer herstellen?
Hier haben Sie mehrere Möglichkeiten: Wenn Sie RDP aktiviert und einen Endpunkt erstellt haben, können Sie die Verbindung mit dem virtuellen Computer über die VIP-Adresse herstellen. Geben Sie in diesem Fall die VIP-Adresse und den Port an, mit dem Sie eine Verbindung herstellen möchten. Auf Ihrem virtuellen Computer müssen Sie den Port für den Datenverkehr konfigurieren. In der Regel speichern Sie hierzu die Einstellungen für die RDP-Verbindung mithilfe des klassischen Azure-Portals auf dem Computer. Die Einstellungen enthalten die erforderlichen Verbindungsinformationen.

Wenn Sie ein virtuelles Netzwerk mit standortübergreifender Verbindung konfiguriert haben, können Sie die Verbindung mit Ihrem virtuellen Computer über die interne DIP-Adresse oder über die private IP-Adresse herstellen. Außerdem kann die Verbindung mit dem virtuellen Computer von einem anderen virtuellen Computer im gleichen virtuellen Netzwerk über die interne DIP-Adresse hergestellt werden. Wenn Sie die Verbindung an einem Standort außerhalb Ihres virtuellen Netzwerks herstellen möchten, kann über die DIP-Adresse keine RDP-Verbindung hergestellt werden. Wen Sie also beispielsweise ein virtuelles Netzwerk mit Punkt-zu-Standort-Verbindung konfiguriert haben und die Verbindung nicht von Ihrem Computer aus herstellen, ist keine DIP-basierte Verbindung mit dem virtuellen Computer möglich.

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-the-traffic-from-my-vm-go-through-that-connection"></a>Wenn sich mein virtueller Computer in einem virtuellen Netzwerk mit standortübergreifender Verbindung befindet, wird dann der gesamte Datenverkehr meines virtuellen Computers über diese Verbindung abgewickelt?
Nein. Nur der Datenverkehr mit einer IP-Zieladresse, die innerhalb der angegebenen lokalen Netzwerk-IP-Adressbereiche des virtuellen Netzwerks liegt, wird über das Gateway des virtuellen Netzwerks abgewickelt. Datenverkehr mit einer IP-Zieladresse im virtuellen Netzwerk bleibt innerhalb des virtuellen Netzwerks. Anderer Datenverkehr wird über den Load Balancer an die öffentlichen Netzwerke oder (bei erzwungener Tunnelung) über das Azure-VPN-Gateway gesendet. Bei der Problembehandlung müssen Sie sich vergewissern, dass alle Bereiche, die über das Gateway gesendet werden sollen, in Ihrem lokalen Netzwerk aufgeführt sind. Vergewissern Sie sich, dass sich die Adressbereiche des lokalen Netzwerks nicht mit einem der Adressbereiche im virtuellen Netzwerk überschneiden. Vergewissern Sie sich außerdem, dass der verwendete DNS-Server den Namen zur korrekten IP-Adresse auflöst.

## <a name="virtual-network-faq"></a>FAQs zu virtuellen Netzwerken
Weitere Informationen zu virtuellen Netzwerken finden Sie in den [FAQs zu virtuellen Netzwerken](../virtual-network/virtual-networks-faq.md).



<!--HONumber=Dec16_HO2-->


