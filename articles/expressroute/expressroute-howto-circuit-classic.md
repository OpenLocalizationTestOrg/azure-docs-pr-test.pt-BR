---
title: "Criar e modificar um circuito ExpressRoute: PowerShell: Azure clássico | Microsoft Docs"
description: "Este artigo o orienta pelas etapas de saudação para criar e provisionar um circuito de rota expressa. Este artigo também mostra como toocheck Olá status, atualizar, ou excluir e desprovisionar o circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a>Criar e modificar um circuito da ExpressRoute usando o PowerShell (clássico)
> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [CLI do Azure](howto-circuit-cli.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-circuit-classic.md)
>

Este artigo orienta Olá etapas toocreate um circuito de rota expressa do Azure usando o modelo de implantação clássico hello e cmdlets do PowerShell. Este artigo também mostra como toocheck Olá status, atualizar, ou excluir e cancelar o provisionamento de um circuito de rota expressa.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


**Sobre modelos de implantação do Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a>Antes de começar
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a>Etapa 1. Analisar os pré-requisitos de saudação e artigos de fluxo de trabalho
Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a>Etapa 2. Instalar versões mais recentes de saudação de módulos do PowerShell de gerenciamento de serviço do Azure (SM) Olá
Siga as instruções de saudação em [Introdução aos cmdlets do PowerShell do Azure](/powershell/azure/overview) para obter orientação passo a passo sobre como tooconfigure os módulos do computador toouse hello Azure PowerShell.

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a>Etapa 3. Faça logon no tooyour conta do Azure e selecione uma assinatura
1. Abra o console do PowerShell com direitos elevados e conecte-se a conta de tooyour. Use Olá toohelp de exemplo que você se conectar a seguir:

        Login-AzureRmAccount

2. Verificar as assinaturas de saudação para conta de saudação.

        Get-AzureRmSubscription

3. Se você tiver mais de uma assinatura, selecione a assinatura de saudação que você deseja toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Em seguida, use Olá tooadd cmdlet a seguir tooPowerShell sua assinatura do Azure para o modelo de implantação clássico hello.

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a>Criar e provisionar um circuito do ExpressRoute
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a>Etapa 1. Importar os módulos do PowerShell de saudação do ExpressRoute
 Se você ainda não tiver feito isso, você deve importar os módulos do Azure e rota expressa Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello. Importar os módulos de saudação do hello local que estavam instalados tooon seu computador local. Dependendo do método hello usado tooinstall módulos de hello, local Olá pode ser diferente de saudação mostrado no exemplo a seguir. Modificar o exemplo hello se necessário.  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>Etapa 2. Obter lista de saudação de provedores suportados, locais e larguras de banda
Antes de criar um circuito de rota expressa, você precisa de lista de saudação de provedores com suporte de conectividade, locais e as opções de largura de banda.

Olá cmdlet do PowerShell `Get-AzureDedicatedCircuitServiceProvider` retorna essas informações, que você usará em etapas posteriores:

    Get-AzureDedicatedCircuitServiceProvider

Verifique toosee se seu provedor de conectividade está listado. Anote Olá informações a seguir porque você precisará dele mais tarde quando você criar um circuito:

* Nome
* PeeringLocations
* BandwidthsOffered

Agora você está pronto toocreate um circuito de rota expressa.         

### <a name="step-3-create-an-expressroute-circuit"></a>Etapa 3. Criar um circuito do ExpressRoute
saudação de exemplo a seguir mostra como toocreate uma rota expressa de 200 Mbps de circuito por meio de Equinix no Vale do Silício. Se estiver usando um provedor diferente e configurações diferentes, substitua essas informações ao fazer a solicitação.

> [!IMPORTANT]
> O circuito de rota expressa será cobrado do momento Olá que uma chave de serviço é emitida. Certifique-se de que você executar esta operação quando o provedor de conectividade de saudação circuito de saudação tooprovision pronto.
> 
> 

a seguir Olá é um exemplo de solicitação de uma nova chave de serviço:

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

Ou, se você quiser toocreate um circuito de ExpressRoute com o complemento do premium Olá, use Olá exemplo a seguir. Consulte toohello [perguntas frequentes sobre o rota expressa](expressroute-faqs.md) para obter mais detalhes sobre o complemento do premium Olá.

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


resposta de saudação conterá a chave de serviço de saudação. Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá seguinte:

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a>Etapa 4. Lista todos os circuitos de rota expressa Olá
Você pode executar Olá `Get-AzureDedicatedCircuit` comando Olá de tooget uma lista de todos os circuitos do ExpressRoute que você criou:

    Get-AzureDedicatedCircuit

resposta de saudação será algo parecido toohello exemplo a seguir:

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Você pode recuperar essas informações a qualquer momento usando Olá `Get-AzureDedicatedCircuit` cmdlet. Fazer com que o hello chamada sem nenhum parâmetro lista todos os circuitos hello. Sua chave de serviço será listada no hello *ServiceKey* campo.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá seguinte:

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>Etapa 5. Enviar Olá tooyour chave conectividade provedor para provisionamento
*ServiceProviderProvisioningState* fornece informações sobre o estado atual de saudação do provisionamento no lado do provedor de serviços de saudação. *Status* informa o estado de saudação em Olá lado da Microsoft. Para obter mais informações sobre estados de provisionamento do circuito, consulte Olá [fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states) artigo.

Quando você cria um novo circuito de rota expressa, circuito Olá estará em Olá estado a seguir:

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


circuito Olá irá toohello estado a seguir quando o provedor de conectividade Olá está no processo de saudação de habilitá-la para você:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Um circuito de rota expressa deve ser Olá seguindo o estado para você toobe capaz de toouse-lo:

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>Etapa 6. Verifique periodicamente o status de saudação e o estado de saudação da chave de circuito de saudação
Isso permite que você saiba quando seu provedor habilitou seu circuito. Depois que o circuito Olá tiver sido configurado, *ServiceProviderProvisioningState* será exibido como *provisionado* conforme mostrado no exemplo a seguir de saudação:

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a>Etapa 7. Criar sua configuração de roteamento
Consulte toohello [configuração de roteamento de circuito de rota expressa (criar e modificar os emparelhamentos de circuito)](expressroute-howto-routing-classic.md) artigo para obter instruções passo a passo.

> [!IMPORTANT]
> Essas instruções se aplicam somente a toocircuits que são criados com provedores de serviços que oferecem serviços da camada 2 de conectividade. Se você estiver usando um provedor de serviços que oferece serviços gerenciados de camada 3 (normalmente um IP VPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a>Etapa 8. Vincular um circuito de rota expressa do tooan de rede virtual
Em seguida, vincule um circuito de rota expressa do tooyour de rede virtual. Consulte também[circuitos de rota expressa vincular redes toovirtual](expressroute-howto-linkvnet-classic.md) para obter instruções passo a passo. Se você precisar toocreate uma rede virtual usando o modelo de implantação clássico Olá para o ExpressRoute, consulte [criar uma rede virtual para o ExpressRoute](expressroute-howto-vnet-portal-classic.md).

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Obter status de saudação de um circuito de rota expressa
Você pode recuperar essas informações a qualquer momento usando Olá `Get-AzureCircuit` cmdlet. Fazer com que o hello chamada sem nenhum parâmetro lista todos os circuitos hello.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Você pode obter informações sobre um circuito de rota expressa específica, passando a chave de serviço hello como uma chamada de toohello do parâmetro.

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá exemplo a seguir:

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a>Modificando um circuito do ExpressRoute
Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade.

Você pode fazer Olá sem tempo de inatividade a seguir:

* Como habilitar ou desabilitar o complemento premium do ExpressRoute para seu circuito do ExpressRoute.
* Aumento de largura de banda de saudação do circuito ExpressRoute fornecido há capacidade disponível na porta hello. Observe que a largura de banda de saudação de um circuito de downgrade não é suportado. 
* Alterar o plano de dados limitados tooUnlimited dados de medição de saudação. Observe que esse plano de medição Olá alteração de dados ilimitada tooMetered que dados não tem suporte.
* Você pode habilitar e desabilitar *Permitir Operações Clássicas*.

Consulte toohello [perguntas frequentes sobre o rota expressa](expressroute-faqs.md) para obter mais informações sobre limitações e limites.

### <a name="tooenable-hello-expressroute-premium-add-on"></a>complemento do premium tooenable Olá rota expressa
Você pode habilitar o complemento do premium Olá rota expressa para o circuito existente usando Olá cmdlet do PowerShell a seguir:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

O circuito terá habilitados dos recursos de complemento de premium Olá rota expressa. Observe que começamos cobrança você para o recurso de complemento premium Olá assim que o comando Olá foi executado com êxito.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>complemento do premium toodisable Olá rota expressa
> [!IMPORTANT]
> Essa operação pode falhar se você estiver usando recursos que são maiores do que o que é permitido para o circuito de saudação padrão.
> 
> 

#### <a name="considerations"></a>Considerações

* Certifique-se de que o número de saudação de redes virtuais vinculadas toohello circuito é inferior a 10 antes de você fazer o downgrade de premium toostandard. Se você não fizer isso, sua solicitação de atualização falhará e você será taxas de premium Olá cobradas.
* Você precisa desvincular todas as redes virtuais em outras regiões geopolíticas. Se você não fizer isso, sua solicitação de atualização falhará e você será taxas de premium Olá cobradas.
* Sua tabela de roteamento deve ter menos de 4.000 rotas para o emparelhamento privado. Se o tamanho da tabela de rota for maior que 4.000 rotas, sessão BGP de saudação será removido e não ser reabilitada até que o número de saudação de prefixos anunciados fica abaixo de 4.000.

#### <a name="disable-hello-premium-add-on"></a>Desabilitar o complemento do premium Olá
Você pode desabilitar o complemento do premium Olá rota expressa para o circuito existente usando Olá cmdlet do PowerShell a seguir:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>largura de banda de circuito ExpressRoute tooupdate Olá
Verificar Olá [perguntas frequentes sobre o rota expressa](expressroute-faqs.md) para opções de largura de banda para o seu provedor de suporte. Você pode escolher qualquer tamanho que seja maior que o tamanho de saudação do circuito existente, desde que a porta física hello (no qual o circuito é criado) permite que.

> [!IMPORTANT]
> Você pode ter o circuito de rota expressa Olá toorecreate se não houver capacidade insuficiente na porta existente Olá. Não é possível atualizar o circuito de saudação se não houver nenhuma capacidade adicional disponível nesse local.
>
> Você não pode reduzir a largura de banda de saudação de um circuito de rota expressa sem interrupções. Downgrade da largura de banda requer que o circuito de rota expressa Olá toodeprovision e, em seguida, Reprovisionar um novo circuito de rota expressa.
> 
> 

#### <a name="resize-a-circuit"></a>Redimensionar um circuito

Depois de decidir qual o tamanho que você precisa, você pode usar Olá tooresize de comando a seguir o circuito:

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

O circuito será ter foi dimensionado para cima no lado do Microsoft hello. Você deve entrar em contato com suas configurações de tooupdate do provedor de conectividade em seu toomatch lado essa alteração. Observe que começamos cobrança você de saudação atualizado opção de largura de banda desse ponto em.

Se você vir Olá erro a seguir ao aumentar a largura de banda de circuito hello, ele significa que não há nenhuma largura de banda suficiente fica na porta física hello, onde o circuito existente é criado. Você tem toodelete este circuito e cria um novo circuito de tamanho de saudação que é necessário. 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Desprovisionamento e exclusão de um circuito do ExpressRoute

### <a name="considerations"></a>Considerações

* Você deve desvincular todas as redes virtuais da saudação circuito de rota expressa para toosucceed esta operação. Verificar toosee se você tiver quaisquer redes virtuais que estão vinculadas toohello circuito se essa operação falhar.
* Se o provedor de serviços de circuito ExpressRoute Olá estado de provisionamento é **provisionamento** ou **provisionado** você deve trabalhar com o circuito de saudação do serviço provedor toodeprovision em seu lado. Vamos continuar tooreserve recursos e cobrar você até que o provedor de serviços Olá Complete desprovisionamento circuito de saudação e nos notifica.
* Se o provedor de serviços de saudação tem desprovisionada circuito hello (provedor de serviços de saudação estado de provisionamento está definido muito**não provisionado**), em seguida, você pode excluir o circuito de saudação. Isso interromperá a cobrança para o circuito de saudação.

#### <a name="delete-a-circuit"></a>Excluir um circuito

Você pode excluir o circuito de rota expressa executando Olá comando a seguir:

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a>Próximas etapas
Depois de criar o circuito, certifique-se de que Olá a seguir:

* [Criar e modificar o roteamento do circuito do ExpressRoute](expressroute-howto-routing-classic.md)
* [Vincular sua rede virtual de tooyour circuito de rota expressa](expressroute-howto-linkvnet-classic.md)

