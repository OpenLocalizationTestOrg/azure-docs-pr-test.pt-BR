---
title: "Configurar o túnel forçado para conexões Site a Site: clássico | Microsoft Docs"
description: "Como tooyour voltar do tráfego de Internet associado do tooredirect ou 'force' todos os no local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a>Configurar o túnel forçado usando o modelo de implantação clássico Olá

Forçado permite redirecionar ou "forçar" todos os direcionado à Internet tráfego tooyour back local através de um túnel VPN Site a Site para inspeção e auditoria de túnel. Esse é um requisito crítico de segurança para a maioria das políticas de TI empresariais. Sem o túnel forçado, o tráfego direcionado à Internet de suas VMs no Azure sempre percorrerá da infraestrutura de rede do Azure diretamente out toohello Internet, sem Olá opção tooallow você tráfego de saudação tooinspect ou auditoria. Acesso não autorizado pode levar a divulgação de tooinformation ou outros tipos de violações de segurança.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Este artigo o orienta pela configuração forçado túnel para redes virtuais criadas usando o modelo de implantação clássico hello. O túnel forçado pode ser configurado usando o PowerShell, não por meio do portal de saudação. Se você quiser tooconfigure encapsulamento para modelo de implantação do Gerenciador de recursos de saudação forçado, selecione artigo clássico Olá lista suspensa a seguir:

> [!div class="op_single_selector"]
> * [PowerShell - clássico](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell – Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a>Requisitos e considerações
O túnel forçado no Azure é configurado por meio de UDR (rotas de definidas pelo usuário) de rede virtual. Redirecionar o tráfego tooan local do site é expressa como um gateway de VPN do Azure toohello rota padrão. Olá, seção a seguir lista limitação atual Olá da tabela de roteamento hello e rotas para uma rede Virtual do Azure:

* Cada sub-rede de rede virtual tem uma tabela de roteamento interna do sistema. tabela de roteamento de sistema Olá tem Olá três grupos de rotas a seguir:

  * **Rotas de rede virtual locais:** diretamente toohello VMs de destino na Olá mesma rede virtual.
  * **Rotas locais:** toohello gateway de VPN do Azure.
  * **Rota padrão:** toohello diretamente da Internet. Pacotes destinados toohello endereços IP privados não cobertos por rotas Olá dois anterior serão removidos.
* Com o lançamento de saudação de rotas definidas pelo usuário, crie um tooadd de tabela de roteamento uma rota padrão e, em seguida, associar Olá roteamento tabela tooyour VNet sub-redes tooenable forçado túnel nessas sub-redes.
* É necessário tooset "site padrão" entre a rede virtual de toohello conectado Olá de sites locais entre locais.
* O túnel forçado deve ser associado a uma Rede Virtual que tem um gateway de VPN de roteamento dinâmico (e não um gateway estático).
* Túnel forçado do ExpressRoute não está configurado por meio desse mecanismo, mas em vez disso, é habilitado por anuncia uma rota padrão por meio de saudação ExpressRoute BGP sessões de emparelhamento. Consulte Olá [documentação de rota expressa](https://azure.microsoft.com/documentation/services/expressroute/) para obter mais informações.

## <a name="configuration-overview"></a>Visão geral de configuração
Em Olá exemplo a seguir, Olá front-end subrede não será forçada encapsulado. cargas de trabalho Olá na sub-rede de front-end Olá podem continuar tooaccept e responde solicitações toocustomer de saudação Internet diretamente. Olá sub-redes de camada intermediária e back-end são forçados encapsulado. Quaisquer conexões de saída da toohello duas sub-redes Internet será tooan forçada ou redirecionado de volta no site local por meio de saudação que encapsulamentos VPN S2S.

Isso permite que você toorestrict e inspecione o acesso à Internet de suas máquinas virtuais ou serviços no Azure, de nuvem enquanto continua tooenable sua arquitetura de serviço de várias camadas necessária. Você também pode aplicar forçado túnel toohello redes virtuais inteiras se não houver nenhuma carga de trabalho para a Internet em suas redes virtuais.

![Túnel forçado](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a>Antes de começar
Verifique se você tem Olá itens antes de começar a configuração a seguir.

* Uma assinatura do Azure. Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Uma rede virtual configurada. 
* versão mais recente de saudação do hello cmdlets do PowerShell do Azure. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.

## <a name="configure-forced-tunneling"></a>Configurar o túnel forçado
Olá procedimento a seguir ajudarão você a especificar um túnel forçado para uma rede virtual. etapas de configuração de saudação correspondem toohello arquivo de configuração de rede de rede virtual.

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

Neste exemplo, a rede virtual de saudação 'MultiTier-VNet' tem três sub-redes: sub-redes 'Front-end', 'Midtier' e 'Back-end', com conexões locais entre quatro: 'DefaultSiteHQ' e três ramificações. 

Olá etapas definir Olá 'DefaultSiteHQ' como conexão de site saudação padrão para túnel forçado e configurar Olá Midtier e Backend sub-redes toouse túnel forçado.

1. Crie uma tabela de roteamento. Use Olá toocreate cmdlet a seguir em sua tabela de rotas.

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. Adicione uma tabela de roteamento de toohello de rota padrão. 

  Olá, exemplo a seguir adiciona uma rota toohello tabela de roteamento padrão criada na etapa 1. Observe que Olá somente rota com suporte é o prefixo de destino de saudação de "0.0.0.0/0" toohello NextHop "VPNGateway".

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. Associe sub-redes de toohello de tabela de roteamento hello. 

  Depois de uma tabela de roteamento é criada e adicionada uma rota, use Olá tooadd de exemplo a seguir ou associar a sub-rede de rede virtual Olá rota tabela tooa. exemplo Hello adiciona Olá rota tabela "MyRouteTable" toohello Midtier e sub-redes de back-end do VNet MultiTier-VNet.

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. Atribua um site padrão ao túnel forçado. 

  Em Olá anterior da etapa, scripts de cmdlet de exemplo hello criado Olá tabela de roteamento em associados Olá tootwo de tabela de rota de sub-redes de rede virtual hello. etapa restante Olá é tooselect um site local entre conexões de vários locais de saudação da rede virtual Olá Olá site ou túnel padrão.

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a>Cmdlets do PowerShell adicionais
### <a name="toodelete-a-route-table"></a>toodelete uma tabela de rotas

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a>toolist uma tabela de rotas

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a>toodelete uma rota de uma tabela de rota

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a>tooremove uma rota de uma sub-rede

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a>tabela de rotas Olá toolist associada a uma sub-rede

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a>tooremove um site padrão de um gateway de VPN VNet

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```