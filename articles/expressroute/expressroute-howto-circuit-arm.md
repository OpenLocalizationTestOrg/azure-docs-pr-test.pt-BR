---
title: 'Criar e modificar um circuito ExpressRoute: PowerShell: Azure Resource Manager | Microsoft Docs'
description: Este artigo descreve como toocreate, provisionar, verifique se, atualizar, excluir e cancelar o provisionamento de um circuito de rota expressa.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a>Criar e modificar um circuito do ExpressRoute usando o PowerShell
> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [CLI do Azure](howto-circuit-cli.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-circuit-classic.md)
>

Este artigo descreve como toocreate uma rota expressa do Azure de circuito usando o modelo de implantação de Gerenciador de recursos do Azure de saudação e cmdlets de PowerShell. Este artigo também mostra como toocheck Olá status do circuito hello, atualizá-lo, ou excluir e seu provisionamento.

## <a name="before-you-begin"></a>Antes de começar
* Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Gerenciador de recursos do Azure. Para obter mais informações, consulte [Visão geral do Azure PowerShell](/powershell/azure/overview).
* Saudação de revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.


## <a name="create-and-provision-an-expressroute-circuit"></a>Criar e provisionar um circuito do ExpressRoute
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Entre no tooyour conta do Azure e selecione sua assinatura
toobegin sua configuração, entrar tooyour conta do Azure. Use Olá toohelp exemplos que você se conectar a seguir:

```powershell
Login-AzureRmAccount
```

Verificar as assinaturas de saudação conta hello:

```powershell
Get-AzureRmSubscription
```

Selecione a assinatura de saudação que você deseja toocreate uma rota expressa de circuito para:

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Obter lista de saudação de provedores suportados, locais e larguras de banda
Antes de criar um circuito de rota expressa, você precisa de lista de saudação de provedores com suporte de conectividade, locais e as opções de largura de banda.

Olá cmdlet do PowerShell **Get-AzureRmExpressRouteServiceProvider** retorna essas informações, que você usará em etapas posteriores:

```powershell
Get-AzureRmExpressRouteServiceProvider
```

Verifique toosee se seu provedor de conectividade está listado. Anote Olá informações a seguir. Você precisará delas mais tarde ao criar um circuito.

* Nome
* PeeringLocations
* BandwidthsOffered

Agora você está pronto toocreate um circuito de rota expressa.   

### <a name="3-create-an-expressroute-circuit"></a>3. Criar um circuito do ExpressRoute
Se você ainda não tiver um grupo de recursos, deverá criar um antes de criar o circuito do ExpressRoute. Você pode fazer isso executando Olá comando a seguir:

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


saudação de exemplo a seguir mostra como toocreate uma rota expressa de 200 Mbps de circuito por meio de Equinix no Vale do Silício. Se estiver usando um provedor diferente e configurações diferentes, substitua essas informações ao fazer a solicitação. a seguir Olá é um exemplo de solicitação de uma nova chave de serviço:

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

Certifique-se de que você especifique a camada SKU correta hello e família SKU:

* A camada da SKU determina se um complemento padrão ou premium do ExpressRoute está habilitado. Você pode especificar *padrão* tooget Olá SKU standard ou *Premium* para o complemento do premium Olá.
* A família SKU determina o tipo de cobrança de saudação. Você pode especificar *Metereddata* para um plano de dados limitado e *Unlimiteddata* para um plano de dados ilimitado. Você pode alterar o tipo de cobrança de saudação do *Metereddata* muito*Unlimiteddata*, mas você não pode alterar o tipo de saudação do *Unlimiteddata* muito*Metereddata* .

> [!IMPORTANT]
> O circuito de rota expressa será cobrado do momento Olá que uma chave de serviço é emitida. Certifique-se de que você executar esta operação quando o provedor de conectividade de saudação circuito de saudação tooprovision pronto.
> 
> 

resposta de Olá contém a chave de serviço de saudação. Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá comando a seguir:

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a>4. Listar todos os circuitos do ExpressRoute
tooget Olá de uma lista de todos os circuitos do ExpressRoute que você criou, execute Olá **AzureRmExpressRouteCircuit Get** comando:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

resposta de saudação terá aparência semelhante toohello exemplo a seguir:

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
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

Você pode recuperar essas informações a qualquer momento usando Olá `Get-AzureRmExpressRouteCircuit` cmdlet. Fazer com que o hello chamada sem parâmetros lista todos os circuitos hello. Sua chave de serviço será listada no hello *ServiceKey* campo:

```powershell
Get-AzureRmExpressRouteCircuit
```


resposta de saudação terá aparência semelhante toohello exemplo a seguir:

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
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá comando a seguir:

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Enviar Olá tooyour chave conectividade provedor para provisionamento
*ServiceProviderProvisioningState* fornece informações sobre o estado atual de saudação do provisionamento no lado do provedor de serviços de saudação. Status fornece o estado de Olá em Olá lado da Microsoft. Para obter mais informações sobre estados de provisionamento do circuito, consulte Olá [fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states) artigo.

Quando você cria um novo circuito de rota expressa, circuito Olá estará em Olá estado a seguir:

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



circuito Olá alterará toohello estado a seguir quando o provedor de conectividade Olá está no processo de saudação de habilitá-la para você:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Para você toobe capaz de toouse um circuito de rota expressa, ele deve ser Olá estado a seguir:

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Verifique periodicamente o status de saudação e o estado de saudação da chave de circuito de saudação
Verificar o status de saudação e o estado de saudação da chave de circuito Olá permite que você saiba quando seu provedor habilitou o seu circuito. Depois que o circuito Olá tiver sido configurado, *ServiceProviderProvisioningState* aparece como *provisionado*, conforme mostrado no exemplo a seguir de saudação:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


resposta de saudação terá aparência semelhante toohello exemplo a seguir:

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

### <a name="7-create-your-routing-configuration"></a>7. Criar sua configuração de roteamento
Para obter instruções passo a passo, consulte Olá [configuração de roteamento de circuito de rota expressa](expressroute-howto-routing-arm.md) artigo toocreate e modificar os emparelhamentos de circuito.

> [!IMPORTANT]
> Essas instruções se aplicam somente a toocircuits que são criados com provedores de serviços que oferecem serviços da camada 2 de conectividade. Se você estiver usando um provedor de serviços que oferece serviços gerenciados de camada 3 (normalmente um IP VPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Vincular um circuito de rota expressa do tooan de rede virtual
Em seguida, vincule um circuito de rota expressa do tooyour de rede virtual. Saudação de uso [vinculação virtual redes circuitos tooExpressRoute](expressroute-howto-linkvnet-arm.md) quando você trabalha com o modelo de implantação do Gerenciador de recursos de saudação do artigo.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Obter status de saudação de um circuito de rota expressa
Você pode recuperar essas informações a qualquer momento usando Olá **AzureRmExpressRouteCircuit Get** cmdlet. Fazer com que o hello chamada sem parâmetros lista todos os circuitos hello.

```powershell
Get-AzureRmExpressRouteCircuit
```


resposta de saudação será semelhante toohello exemplo a seguir:

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


Você pode obter informações sobre um circuito de rota expressa específica, passando o nome do grupo de recursos de saudação e o nome do circuito como uma chamada de toohello do parâmetro:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


resposta de saudação terá aparência semelhante toohello exemplo a seguir:

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


Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá comando a seguir:

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify">
            </a>Modificar um circuito do ExpressRoute
Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade.

Você pode fazer Olá sem tempo de inatividade a seguir:

* Como habilitar ou desabilitar o complemento premium do ExpressRoute para seu circuito do ExpressRoute.
* Aumento de largura de banda de saudação do circuito ExpressRoute fornecido há capacidade disponível na porta hello. Não há suporte para a largura de banda de saudação de um circuito de downgrade. 
* Alterar o plano de dados limitados tooUnlimited dados de medição de saudação. Alterando Olá plano de dados ilimitado tooMetered não há suporte para dados de medição.
* Você pode habilitar e desabilitar *Permitir Operações Clássicas*.

Para obter mais informações sobre limitações e limites, consulte toohello [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>complemento do premium tooenable Olá rota expressa
Você pode habilitar o complemento do premium Olá rota expressa para o circuito existente usando Olá trecho do PowerShell a seguir:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

circuito Olá terá habilitados dos recursos de complemento de premium Olá rota expressa. Começaremos a cobrança é para o recurso de complemento premium Olá assim que o comando Olá foi executado com êxito.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>complemento do premium toodisable Olá rota expressa
> [!IMPORTANT]
> Essa operação pode falhar se você estiver usando recursos que são maiores do que o que é permitido para o circuito de saudação padrão.
> 
> 

Observe o seguinte hello:

* Antes de você fazer o downgrade de premium toostandard, você deve garantir que esse número de saudação de redes virtuais que estão vinculadas toohello circuito é inferior a 10. Se você não fizer isso, sua solicitação de atualização falhará e cobraremos com tarifas premium.
* Você precisa desvincular todas as redes virtuais em outras regiões geopolíticas. Se você não fizer isso, sua solicitação de atualização falhará e cobraremos com tarifas premium.
* Sua tabela de roteamento deve ter menos de 4.000 rotas para o emparelhamento privado. Se o tamanho da tabela de rota for maior que 4.000 rotas, a sessão BGP de saudação descarta e não ser reabilitada até que o número de saudação de prefixos anunciados fica abaixo de 4.000.

Você pode desabilitar o complemento do premium Olá rota expressa para o circuito existente hello usando Olá cmdlet do PowerShell a seguir:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>largura de banda de circuito ExpressRoute tooupdate Olá
Para obter opções de largura de banda com suporte para o seu provedor, verifique Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md). Você pode escolher qualquer tamanho maior do que o tamanho de saudação do circuito existente.

> [!IMPORTANT]
> Você pode ter o circuito de rota expressa Olá toorecreate se não houver capacidade insuficiente na porta existente Olá. Não é possível atualizar o circuito de saudação se não houver nenhuma capacidade adicional disponível nesse local.
>
> Você não pode reduzir a largura de banda de saudação de um circuito de rota expressa sem interrupções. Downgrade da largura de banda requer que o circuito de rota expressa Olá toodeprovision e, em seguida, Reprovisionar um novo circuito de rota expressa.
> 

Depois de decidir qual o tamanho que você precisa usar o circuito de Olá tooresize de comando a seguir:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


O circuito será dimensionado para cima no lado do Microsoft hello. Em seguida, você deve contatar suas configurações de tooupdate do provedor de conectividade em seu toomatch lado essa alteração. Depois de fazer essa notificação, começaremos a cobrança você para a opção de largura de banda Olá atualizado.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>Olá toomove SKU de toounlimited limitado
Você pode alterar Olá SKU de um circuito de rota expressa usando Olá trecho do PowerShell a seguir:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>toocontrol clássico de toohello de acesso e ambientes do Gerenciador de recursos
Consulte as instruções de saudação em [circuitos ExpressRoute mover de modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](expressroute-howto-move-arm.md).  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Desprovisionamento e exclusão de um circuito do ExpressRoute
Observe o seguinte hello:

* Você deve desvincular todas as redes virtuais da saudação circuito de rota expressa. Se essa operação falhar, verifique toosee se todas as redes virtuais são vinculados toohello circuito.
* Se o provedor de serviços de circuito ExpressRoute Olá estado de provisionamento é **provisionamento** ou **provisionado** você deve trabalhar com o circuito de saudação do serviço provedor toodeprovision em seu lado. Vamos continuar tooreserve recursos e cobrar você até que o provedor de serviços Olá Complete desprovisionamento circuito de saudação e nos notifica.
* Se o provedor de serviços de saudação tem desprovisionada circuito hello (provedor de serviços de saudação estado de provisionamento está definido muito**não provisionado**), em seguida, você pode excluir o circuito de saudação. Isso interromperá a cobrança para o circuito Olá

Você pode excluir o circuito de rota expressa executando Olá comando a seguir:

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a>Próximas etapas

Depois de criar o circuito, certifique-se de que Olá a seguir:

* [Criar e modificar o roteamento do circuito do ExpressRoute](expressroute-howto-routing-arm.md)
* [Vincular sua rede virtual de tooyour circuito de rota expressa](expressroute-howto-linkvnet-arm.md)
