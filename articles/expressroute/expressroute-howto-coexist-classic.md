---
title: "Configurar as conexões de VPN ExpressRoute e Site a Site que possam coexistir: clássico: Azure | Microsoft Docs"
description: "Este artigo orienta você pela configuração de uma conexão VPN Site a Site que pode coexistir para o modelo de implantação clássico hello e rota expressa."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a>Configurar as conexões coexistentes do ExpressRoute e do Site a Site (clássico)
> [!div class="op_single_selector"]
> * [PowerShell – Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - clássico](expressroute-howto-coexist-classic.md)
> 
> 

Tendo Olá capacidade tooconfigure VPN Site a Site e ExpressRoute tem várias vantagens. Você pode configurar VPN Site a Site como um caminho de failover seguro para ExressRoute ou usar VPNs Site a Site tooconnect toosites que não estão conectados por meio de rota expressa. Abordaremos Olá etapas tooconfigure ambos os cenários neste artigo. Este artigo se aplica o modelo de implantação clássico toohello. Essa configuração não está disponível no portal de saudação.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Sobre modelos de implantação do Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> Circuitos de rota expressa devem ser configurados previamente antes de seguir as instruções de saudação abaixo. Certifique-se de que você seguiu Olá guias muito[criar um circuito ExpressRoute](expressroute-howto-circuit-classic.md) e [configurar o roteamento](expressroute-howto-routing-classic.md) antes de executar as etapas de saudação abaixo.
> 
> 

## <a name="limits-and-limitations"></a>Limites e limitações
* **Não há suporte para o roteamento do tráfego.** Não é possível fazer o roteamento (por meio do Azure) entre sua rede local conectada via VPN Site a Site e sua rede local conectada via ExpressRoute.
* **Não há suporte para o Ponto a site.** Não é possível habilitar toohello de conexões de VPN ponto a site mesmo VNet tooExpressRoute conectado. VPN de ponto para site e ExpressRoute não podem coexistir para Olá mesmo VNet.
* **Não é possível habilitar o túnel forçado no gateway VPN Site a Site hello.** Você pode apenas "forçar" todos os direcionado à Internet tráfego tooyour Voltar na rede local através de rota expressa.
* **Não há suporte para o gateway SKU básico.** Você deve usar um gateway de SKU não básica para ambos os Olá [gateway de rota expressa](expressroute-about-virtual-network-gateways.md) e hello [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Há suporte para apenas um gateway de VPN baseado em rotas.** Você deve usar uma rota baseada no [Gateway de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **O roteamento estático deve ser configurado para o gateway de VPN.** Se sua rede local está conectada tooboth ExpressRoute e uma Site a Site VPN, você deve ter uma rota estática configurada em sua rede local tooroute Olá Site a Site VPN conexão toohello Internet pública.
* **O gateway de ExpressRoute deve ser configurado primeiro.** Você deve criar o gateway de rota expressa Olá primeiro antes de adicionar o gateway VPN Site a Site hello.

## <a name="configuration-designs"></a>Designs de configuração
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Configurar uma VPN site a site como um caminho de failover para o ExpressRoute
Você pode configurar uma conexão VPN site a site como um backup para o ExpressRoute. Isso se aplica apenas toovirtual redes vinculado toohello caminho de emparelhamento particular do Azure. Não há uma solução de failover com base em VPN para serviços acessíveis por meio de emparelhamentos público do Azure e da Microsoft. Olá circuito de rota expressa é sempre link principal hello. Dados fluirá pelo caminho VPN Site a Site Olá somente se Olá circuito ExpressRoute falhar. 

> [!NOTE]
> Enquanto circuito de rota expressa é preferível por VPN Site a Site quando ambas as rotas são Olá mesmo, o Azure usará hello mais longa correspondência toochoose Olá rota de prefixo para o destino do pacote de saudação.
> 
> 

![Coexistência](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Configurar um toosites tooconnect VPN Site a Site não está conectado por meio de rota expressa
Você pode configurar sua rede onde alguns sites se conectam diretamente tooAzure por VPN Site a Site, e alguns sites se conectam por meio de rota expressa. 

![Coexistência](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> Não é possível configurar uma rede virtual como um roteador de trânsito.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Selecionando Olá etapas toouse
Há dois conjuntos diferentes de toochoose procedimentos de em conexões de tooconfigure de ordem podem coexistir. procedimento de configuração de saudação selecionados por você dependerá se você tiver uma rede virtual existente que você deseja tooconnect para, ou você deseja toocreate uma nova rede virtual.

* Não tem uma rede virtual e precisa toocreate um.
  
    Se você ainda não tiver uma rede virtual, este procedimento irá orientá-lo por meio de criar uma nova rede virtual usando o modelo de implantação clássico hello e criação de novas conexões de VPN Site a Site e rota expressa. tooconfigure, Olá etapas a seguir na seção de artigo Olá [toocreate uma nova rede virtual e conexões coexistentes](#new).
* Eu já tenho uma VNet do modelo de implantação clássico
  
    Talvez você já tenha uma rede virtual implementada com uma conexão de VPN Site a Site ou uma conexão de ExpressRoute existente. Olá seção artigo [tooconfigure coexsiting conexões para uma rede virtual já existente](#add) irá orientá-lo por meio de excluir gateway hello e, em seguida, criar novas conexões VPN Site a Site e rota expressa. Observe que, ao criar novas conexões de hello, Olá etapas devem ser concluídas em uma ordem muito específica. Não use instruções Olá toocreate outros artigos seus gateways e conexões.
  
    Neste procedimento, criação de conexões que podem coexistir será exigem você toodelete seu gateway e, em seguida, configure novos gateways. Isso significa que você terá tempo de inatividade para as conexões entre locais enquanto você excluir e recria o gateway e conexões, mas você não precisará toomigrate qualquer uma das sua VMs ou serviços tooa nova rede virtual. Suas máquinas virtuais e serviços ainda serão toocommunicate capaz de saída por meio do balanceador de carga Olá enquanto você configurar seu gateway se eles estiverem toodo configurado assim.

## <a name="new"></a>conexões coexistentes e toocreate uma nova rede virtual
Este procedimento orientará você na criação de uma Rede Virtual, bem como na criação das conexões site a site e de ExpressRoute que coexistirão.

1. Você precisará tooinstall Olá última versão do hello cmdlets do PowerShell do Azure. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello. Observe que Olá cmdlets que você usará para essa configuração pode ser um pouco diferente do que você talvez esteja familiarizado com. Se toouse Olá cmdlets ser especificado nestas instruções. 
2. Crie um esquema para a sua rede virtual. Para obter mais informações sobre o esquema de configuração hello, consulte [esquema de configuração de rede Virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   
    Quando você criar seu esquema, certifique-se de que usar o hello valores a seguir:
   
   * sub-rede de gateway de saudação para rede virtual Olá deve ser /27 ou um prefixo mais curto (como /26 ou /25).
   * tipo de conexão de gateway de saudação é "dedicado".
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. Depois de criar e configurar o arquivo de esquema xml, carregue o arquivo hello. Isso criará sua rede virtual.
   
    Use Olá tooupload cmdlet a seguir seu arquivo, substituindo o valor de saudação com seus próprios.
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <a name="gw">
            </a>Crie um gateway de ExpressRoute. Ser toospecify se Olá GatewaySKU como *padrão*, *HighPerformance*, ou *UltraPerformance* e Olá GatewayType como *DynamicRouting*.
   
    Use Olá exemplo a seguir, substituindo valores de saudação para seu próprio.
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. Vincule um circuito de rota expressa toohello do gateway de rota expressa hello. Após essa etapa foi concluída, a conexão Olá entre sua rede local e o Azure, por meio do ExpressRoute, é estabelecida.
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <a name="vpngw"></a>Em seguida, crie seu gateway de VPN Site a Site. Olá GatewaySKU devem ser *padrão*, *HighPerformance*, ou *UltraPerformance* e hello GatewayType deve ser *DynamicRouting*.
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    configurações para gateway de rede virtual do hello tooretrieve, incluindo Olá gateway ID e o IP público do hello, usam Olá `Get-AzureVirtualNetworkGateway` cmdlet.
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. Crie uma entidade de gateway de VPN de site local. Esse comando não configura seu gateway de VPN local. Em vez disso, permite configurações de gateway local tooprovide hello, como o IP público hello e hello local espaço de endereço, para que hello gateway VPN do Azure pode se conectar tooit.
   
   > [!IMPORTANT]
   > site local Olá Olá VPN Site a Site não está definido em Olá netcfg. Em vez disso, você deve usar parâmetros cmdlet toospecify Olá site local. Não é possível defini-lo usando o portal ou arquivo de netcfg hello.
   > 
   > 
   
    Use Olá exemplo a seguir, substituindo valores hello com seus próprios.
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > Se sua rede local tiver várias rotas, você poderá passá-las como uma matriz.  $MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")  
   > 
   > 

    configurações para gateway de rede virtual do hello tooretrieve, incluindo Olá gateway ID e o IP público do hello, usam Olá `Get-AzureVirtualNetworkGateway` cmdlet. Consulte Olá exemplo a seguir.

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. Configure seu dispositivo tooconnect toohello novo gateway de VPN local. Use as informações de saudação recuperado na etapa 6, ao configurar seu dispositivo VPN. Para obter mais informações sobre a configuração de dispositivo VPN, consulte [Configuração do Dispositivo VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
2. Gateway VPN Site a Site link Olá no gateway local toohello do Azure.
   
    Neste exemplo, connectedEntityId é a ID de gateway local hello, que você pode encontrar executando `Get-AzureLocalNetworkGateway`. Você pode encontrar virtualNetworkGatewayId usando Olá `Get-AzureVirtualNetworkGateway` cmdlet. Após essa etapa, é estabelecida a conexão Olá entre sua rede local e o Azure via Olá conexão VPN Site a Site.

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <a name="add"></a>tooconfigure coexsiting conexões para uma rede virtual já existente
Se você tiver uma rede virtual existente, verifique o tamanho de sub-rede de gateway hello. Se a sub-rede do gateway Olá for /28 ou /29, primeiro exclua o gateway de rede virtual hello e aumentar o tamanho de sub-rede de gateway de saudação. Olá etapas nesta seção mostram como toodo que.

Se a sub-rede do gateway de saudação é /27 ou maior e rede virtual Olá é conectado por meio de rota expressa, você pode ignorar as etapas de saudação abaixo e prosseguir muito["Etapa 6 – criar um gateway VPN Site a Site"](#vpngw) na seção anterior hello.

> [!NOTE]
> Quando você exclui um gateway existente Olá, seus locais perderá a rede virtual do hello conexão tooyour enquanto você trabalha nessa configuração.
> 
> 

1. Você precisará tooinstall Olá última versão do hello cmdlets do PowerShell do Gerenciador de recursos do Azure. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello. Observe que Olá cmdlets que você usará para essa configuração pode ser um pouco diferente do que você talvez esteja familiarizado com. Se toouse Olá cmdlets ser especificado nestas instruções. 
2. Exclua gateway existente Olá rota expressa ou VPN Site a Site. Use Olá cmdlet a seguir, substituindo valores hello com seus próprios.
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. Exporte o esquema de saudação da rede virtual. Use Olá cmdlet do PowerShell a seguir, substituindo valores hello com seus próprios.
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. Edite esquema de arquivo de configuração de rede Olá para que a sub-rede de gateway de saudação é /27 ou um prefixo mais curto (como /26 ou /25). Consulte Olá exemplo a seguir. 
   
   > [!NOTE]
   > Se você não tiver endereços IP suficientes no tamanho de sub-rede de gateway sua rede virtual tooincrease hello, será necessário tooadd mais espaço de endereço IP. Para obter mais informações sobre o esquema de configuração hello, consulte [esquema de configuração de rede Virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. Se seu gateway anterior era uma VPN Site a Site, você deve também alterar tipo de conexão de saudação muito**dedicado**.
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. Neste ponto, você terá uma VNet sem nenhum gateway. novos gateways do toocreate e concluir as conexões, você pode continuar com a [etapa 4 - criar um gateway de rota expressa](#gw), encontrado em Olá precede o conjunto de etapas.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre a rota expressa, consulte Olá [perguntas frequentes sobre o rota expressa](expressroute-faqs.md)

