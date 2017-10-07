---
title: 'Como tooconfigure roteamento (emparelhamento) para um circuito de rota expressa: Gerenciador de recursos: PowerShell: Azure | Microsoft Docs'
description: "Este artigo o orienta pelas etapas de saudação para criar e provisionar Olá privado, público e emparelhamento da Microsoft de um circuito de rota expressa. Este artigo também mostra como status de saudação toocheck, atualizar ou excluir emparelhamentos para o seu circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a>Criar e modificar o emparelhamento de um circuito do ExpressRoute usando o PowerShell

Este artigo ajuda você a criar e gerenciar a configuração de roteamento para um circuito de rota expressa no modelo de implantação do Gerenciador de recursos do hello usando o PowerShell. Você também pode verificar status hello, update ou delete e desprovisionar emparelhamentos de um circuito de rota expressa. Se você quiser toouse toowork um método diferente com o circuito, selecione um artigo de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [CLI do Azure](howto-routing-cli.md)
> * [Vídeo – Emparelhamento privado](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Vídeo – Emparelhamento público](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Vídeo – Emparelhamento da Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Pré-requisitos de configuração

* Você precisará a versão mais recente de saudação do hello cmdlets do PowerShell do Gerenciador de recursos do Azure. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). 
* Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md) página hello [requisitos de roteamento](expressroute-routing.md) página e hello [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração de página.
* Você deve ter um circuito do ExpressRoute ativo. Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-arm.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar. Olá circuito de rota expressa deve estar em um estado habilitado e configurado para você toobe toorun capaz de saudação cmdlets neste artigo.

Essas instruções se aplicam somente a toocircuits criado com provedores de serviço oferece serviços de conectividade de camada 2. Se você estiver usando um provedor de serviços que ofereça serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.

> [!IMPORTANT]
> Estamos atualmente não anuncie emparelhamentos configurados pelos provedores de serviço por meio do portal de gerenciamento de serviços de saudação. Estamos trabalhando para habilitar esse recurso em breve. Verifique com seu provedor de serviços antes de configurar os emparelhamentos via protocolo BGP.
> 
> 

Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito do ExpressRoute. Você pode configurar emparelhamentos em qualquer ordem escolhida. No entanto, você deve garantir que você conclua a configuração de saudação de cada um emparelhamento de cada vez. 

## <a name="azure-private-peering"></a>Emparelhamento privado do Azure

Esta seção ajuda você a criar, obter, atualizar e excluir Olá configuração emparelhamento particular do Azure para um circuito de rota expressa.

### <a name="toocreate-azure-private-peering"></a>toocreate emparelhamento particular do Azure

1. Importe o módulo do PowerShell de saudação do ExpressRoute.

  Você deve instalar o instalador do PowerShell mais recente saudação do [Galeria do PowerShell](http://www.powershellgallery.com/) e importar os módulos do Azure Resource Manager Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello. Você precisará toorun PowerShell como administrador.

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  Importe todos os módulos AzureRM.* Olá Olá conhecido intervalo de versão semântico.

  ```powershell
  Import-AzureRM
  ```

  Você também pode importar um módulo selecione Olá conhecido intervalo de versão semântico.

  ```powershell
  Import-Module AzureRM.Network 
  ```

  Entre na conta de tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Selecione a assinatura de saudação desejado toocreate circuito de rota expressa.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Criar um circuito do ExpressRoute.

  Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-arm.md) e fornecidos pelo provedor de conectividade de saudação.

  Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você. Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello. No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.
3. Verifique toomake de circuito de rota expressa de saudação se ele está configurado e também está habilitado. Use Olá exemplo a seguir:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  resposta de saudação é semelhante toohello exemplo a seguir:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configure o emparelhamento particular do Azure para o circuito de saudação. Certifique-se de que você tenha Olá itens a seguir antes de prosseguir com as próximas etapas hello:

  * Um /30 sub-rede para o link primário hello. subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.
  * Um /30 sub-rede para o link secundário hello. subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.
  * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
  * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes. Você pode usar um número de AS privado para esse emparelhamento. Não use 65515.
  * **Opcional -** um hash MD5 se você escolher toouse um.

  Use hello Azure privado de emparelhamento para o circuito de tooconfigure de exemplo a seguir:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Se você escolher toouse um hash MD5, use Olá exemplo a seguir:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.
  > 
  >

### <a name="tooview-azure-private-peering-details"></a>tooview privado emparelhamento detalhes do Azure

Você pode obter os detalhes de configuração usando Olá exemplo a seguir:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuração emparelhamento particular do Azure

Você pode atualizar qualquer parte da configuração de saudação usando Olá exemplo a seguir. Neste exemplo, Olá VLAN ID de circuito hello está sendo atualizado do too500 100.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a>toodelete emparelhamento particular do Azure

Você pode remover a configuração do emparelhamento executando Olá exemplo a seguir:

> [!WARNING]
> Certifique-se de que todas as redes virtuais são desvinculadas do hello circuito de rota expressa antes de executar este exemplo. 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a>Emparelhamento público do Azure

Esta seção ajuda você a criar, obter, atualizar e excluir Olá a configuração de emparelhamento pública do Azure para um circuito de rota expressa.

### <a name="toocreate-azure-public-peering"></a>toocreate emparelhamento público do Azure

1. Importe o módulo do PowerShell de saudação do ExpressRoute.

  Você deve instalar o instalador do PowerShell mais recente saudação do [Galeria do PowerShell](http://www.powershellgallery.com/) e importar os módulos do Azure Resource Manager Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello. Você precisará toorun PowerShell como administrador.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  Importe todos os módulos AzureRM.* Olá Olá conhecido intervalo de versão semântico.

  ```powershell
  Import-AzureRM
  ```

  Você também pode importar um módulo selecione Olá conhecido intervalo de versão semântico.

  ```powershell
  Import-Module AzureRM.Network
```

  Entre na conta de tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Selecione a assinatura de saudação desejado toocreate circuito de rota expressa.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Criar um circuito do ExpressRoute.

  Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-arm.md) e fornecidos pelo provedor de conectividade de saudação.

  Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você. Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello. No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.
3. Verifique tooensure de circuito de rota expressa Olá provisionado e também está habilitado. Use Olá exemplo a seguir:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  resposta de saudação é semelhante toohello exemplo a seguir:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configure o emparelhamento público do Azure para o circuito de saudação. Certifique-se de que você tenha Olá informações a seguir antes de você continuar.

  * Um /30 sub-rede para o link primário hello. Precisa ser um prefixo IPv4 público válido.
  * Um /30 sub-rede para o link secundário hello. Precisa ser um prefixo IPv4 público válido.
  * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
  * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes.
  * **Opcional -** um hash MD5 se você escolher toouse um.

  Executar hello Azure público de emparelhamento para o circuito de tooconfigure de exemplo a seguir

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Se você escolher toouse um hash MD5, use Olá exemplo a seguir:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.
  > 
  >

### <a name="tooview-azure-public-peering-details"></a>tooview público emparelhamento detalhes do Azure

Você pode obter os detalhes de configuração usando Olá cmdlet a seguir:

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuração de emparelhamento pública do Azure

Você pode atualizar qualquer parte da configuração de saudação usando Olá exemplo a seguir. Neste exemplo, Olá VLAN ID de circuito hello está sendo atualizado do too600 200.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a>toodelete emparelhamento público do Azure

Você pode remover a configuração do emparelhamento executando Olá exemplo a seguir:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a>Emparelhamento da Microsoft

Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento Microsoft hello por um circuito de rota expressa.

> [!IMPORTANT]
> Emparelhamento da Microsoft de circuitos ExpressRoute que foram configurados anterior tooAugust 1, 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft hello, mesmo se os filtros de roteamento não estão definidos. Emparelhamento da Microsoft de circuitos de rota expressa configurados em ou após 1 de agosto de 2017 não terá quaisquer prefixos anunciados até que um filtro de rota é anexado toohello circuito. Para obter mais informações, consulte [Configurar um filtro de rota para o emparelhamento da Microsoft](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate emparelhamento da Microsoft

1. Importe o módulo do PowerShell de saudação do ExpressRoute.

  Você deve instalar o instalador do PowerShell mais recente saudação do [Galeria do PowerShell](http://www.powershellgallery.com/) e importar os módulos do Azure Resource Manager Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello. Você precisará toorun PowerShell como administrador.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  Importe todos os módulos AzureRM.* Olá Olá conhecido intervalo de versão semântico.

  ```powershell
  Import-AzureRM
  ```

  Você também pode importar um módulo selecione Olá conhecido intervalo de versão semântico.

  ```powershell
  Import-Module AzureRM.Network
  ```

  Entre na conta de tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Selecione a assinatura de saudação desejado toocreate circuito de rota expressa.

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Criar um circuito do ExpressRoute.

  Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-arm.md) e fornecidos pelo provedor de conectividade de saudação.

  Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você. Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello. No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.
3. Verifique toomake de circuito de rota expressa de saudação se ele está configurado e também está habilitado. Use Olá exemplo a seguir:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  resposta de saudação é semelhante toohello exemplo a seguir:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configure o emparelhamento do circuito de saudação do Microsoft. Certifique-se de que você tenha Olá seguintes informações antes de continuar.

  * Um /30 sub-rede para o link primário hello. Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.
  * Um /30 sub-rede para o link secundário hello. Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.
  * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
  * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes.
  * Anunciado prefixos: você deve fornecer uma lista de todos os prefixos planejar tooadvertise sobre a sessão BGP de saudação. Somente prefixos de endereços IP públicos são aceitos. Se você planejar toosend um conjunto de prefixos, você pode enviar uma lista separada por vírgulas. Esses prefixos devem ser registrado tooyou em um RIR / IRR.
  * **Opcional -** cliente ASN: se você estiver prefixos de anúncios que não são registrado toohello emparelhamento como número, você pode especificar hello como número toowhich, eles são registrados.
  * Nome de roteamento do registro: Você pode especificar Olá RIR / IRR no qual hello como número e prefixos estão registrados.
  * **Opcional -** um hash MD5 se você escolher toouse um.

   Use Olá exemplo tooconfigure emparelhamento da Microsoft para o circuito a seguir:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a>tooget detalhes de emparelhamento da Microsoft

Você pode obter os detalhes de configuração usando Olá exemplo a seguir:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate configuração de emparelhamento da Microsoft

Você pode atualizar qualquer parte da configuração de saudação usando Olá exemplo a seguir:

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a>toodelete emparelhamento da Microsoft

Você pode remover a configuração do emparelhamento executando Olá cmdlet a seguir:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a>Próximas etapas

Próxima etapa, [vincular um circuito de rota expressa do tooan de VNet](expressroute-howto-linkvnet-arm.md).

* Para saber mais sobre fluxos de trabalho do ExpressRoute, confira [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).
* Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).
* Para saber mais sobre redes virtuais, confira [Visão geral da rede virtual](../virtual-network/virtual-networks-overview.md).
