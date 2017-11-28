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
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="9a94f-103">Criar e modificar um circuito do ExpressRoute usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a94f-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a94f-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9a94f-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="9a94f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a94f-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="9a94f-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9a94f-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="9a94f-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9a94f-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="9a94f-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="9a94f-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="9a94f-109">Este artigo descreve como toocreate uma rota expressa do Azure de circuito usando o modelo de implantação de Gerenciador de recursos do Azure de saudação e cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a94f-109">This article describes how toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="9a94f-110">Este artigo também mostra como toocheck Olá status do circuito hello, atualizá-lo, ou excluir e seu provisionamento.</span><span class="sxs-lookup"><span data-stu-id="9a94f-110">This article also shows you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9a94f-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="9a94f-111">Before you begin</span></span>
* <span data-ttu-id="9a94f-112">Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a94f-112">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="9a94f-113">Para obter mais informações, consulte [Visão geral do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9a94f-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="9a94f-114">Saudação de revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="9a94f-114">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="9a94f-115">Criar e provisionar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9a94f-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="9a94f-116">1. Entre no tooyour conta do Azure e selecione sua assinatura</span><span class="sxs-lookup"><span data-stu-id="9a94f-116">1. Sign in tooyour Azure account and select your subscription</span></span>
<span data-ttu-id="9a94f-117">toobegin sua configuração, entrar tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a94f-117">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="9a94f-118">Use Olá toohelp exemplos que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-118">Use hello following examples toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="9a94f-119">Verificar as assinaturas de saudação conta hello:</span><span class="sxs-lookup"><span data-stu-id="9a94f-119">Check hello subscriptions for hello account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="9a94f-120">Selecione a assinatura de saudação que você deseja toocreate uma rota expressa de circuito para:</span><span class="sxs-lookup"><span data-stu-id="9a94f-120">Select hello subscription that you want toocreate an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="9a94f-121">2. Obter lista de saudação de provedores suportados, locais e larguras de banda</span><span class="sxs-lookup"><span data-stu-id="9a94f-121">2. Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="9a94f-122">Antes de criar um circuito de rota expressa, você precisa de lista de saudação de provedores com suporte de conectividade, locais e as opções de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="9a94f-122">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="9a94f-123">Olá cmdlet do PowerShell **Get-AzureRmExpressRouteServiceProvider** retorna essas informações, que você usará em etapas posteriores:</span><span class="sxs-lookup"><span data-stu-id="9a94f-123">hello PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="9a94f-124">Verifique toosee se seu provedor de conectividade está listado.</span><span class="sxs-lookup"><span data-stu-id="9a94f-124">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="9a94f-125">Anote Olá informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="9a94f-125">Make a note of hello following information.</span></span> <span data-ttu-id="9a94f-126">Você precisará delas mais tarde ao criar um circuito.</span><span class="sxs-lookup"><span data-stu-id="9a94f-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="9a94f-127">Nome</span><span class="sxs-lookup"><span data-stu-id="9a94f-127">Name</span></span>
* <span data-ttu-id="9a94f-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="9a94f-128">PeeringLocations</span></span>
* <span data-ttu-id="9a94f-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="9a94f-129">BandwidthsOffered</span></span>

<span data-ttu-id="9a94f-130">Agora você está pronto toocreate um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="9a94f-130">You're now ready toocreate an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="9a94f-131">3. Criar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9a94f-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="9a94f-132">Se você ainda não tiver um grupo de recursos, deverá criar um antes de criar o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9a94f-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="9a94f-133">Você pode fazer isso executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-133">You can do so by running hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="9a94f-134">saudação de exemplo a seguir mostra como toocreate uma rota expressa de 200 Mbps de circuito por meio de Equinix no Vale do Silício.</span><span class="sxs-lookup"><span data-stu-id="9a94f-134">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="9a94f-135">Se estiver usando um provedor diferente e configurações diferentes, substitua essas informações ao fazer a solicitação.</span><span class="sxs-lookup"><span data-stu-id="9a94f-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="9a94f-136">a seguir Olá é um exemplo de solicitação de uma nova chave de serviço:</span><span class="sxs-lookup"><span data-stu-id="9a94f-136">hello following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="9a94f-137">Certifique-se de que você especifique a camada SKU correta hello e família SKU:</span><span class="sxs-lookup"><span data-stu-id="9a94f-137">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="9a94f-138">A camada da SKU determina se um complemento padrão ou premium do ExpressRoute está habilitado.</span><span class="sxs-lookup"><span data-stu-id="9a94f-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="9a94f-139">Você pode especificar *padrão* tooget Olá SKU standard ou *Premium* para o complemento do premium Olá.</span><span class="sxs-lookup"><span data-stu-id="9a94f-139">You can specify *Standard* tooget hello standard SKU or *Premium* for hello premium add-on.</span></span>
* <span data-ttu-id="9a94f-140">A família SKU determina o tipo de cobrança de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a94f-140">SKU family determines hello billing type.</span></span> <span data-ttu-id="9a94f-141">Você pode especificar *Metereddata* para um plano de dados limitado e *Unlimiteddata* para um plano de dados ilimitado.</span><span class="sxs-lookup"><span data-stu-id="9a94f-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="9a94f-142">Você pode alterar o tipo de cobrança de saudação do *Metereddata* muito*Unlimiteddata*, mas você não pode alterar o tipo de saudação do *Unlimiteddata* muito*Metereddata* .</span><span class="sxs-lookup"><span data-stu-id="9a94f-142">You can change hello billing type from *Metereddata* too*Unlimiteddata*, but you can't change hello type from *Unlimiteddata* too*Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a94f-143">O circuito de rota expressa será cobrado do momento Olá que uma chave de serviço é emitida.</span><span class="sxs-lookup"><span data-stu-id="9a94f-143">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="9a94f-144">Certifique-se de que você executar esta operação quando o provedor de conectividade de saudação circuito de saudação tooprovision pronto.</span><span class="sxs-lookup"><span data-stu-id="9a94f-144">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="9a94f-145">resposta de Olá contém a chave de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a94f-145">hello response contains hello service key.</span></span> <span data-ttu-id="9a94f-146">Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-146">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="9a94f-147">4. Listar todos os circuitos do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9a94f-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="9a94f-148">tooget Olá de uma lista de todos os circuitos do ExpressRoute que você criou, execute Olá **AzureRmExpressRouteCircuit Get** comando:</span><span class="sxs-lookup"><span data-stu-id="9a94f-148">tooget a list of all hello ExpressRoute circuits that you created, run hello **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="9a94f-149">resposta de saudação terá aparência semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-149">hello response will look similar toohello following example:</span></span>

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

<span data-ttu-id="9a94f-150">Você pode recuperar essas informações a qualquer momento usando Olá `Get-AzureRmExpressRouteCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a94f-150">You can retrieve this information at any time by using hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="9a94f-151">Fazer com que o hello chamada sem parâmetros lista todos os circuitos hello.</span><span class="sxs-lookup"><span data-stu-id="9a94f-151">Making hello call with no parameters lists all hello circuits.</span></span> <span data-ttu-id="9a94f-152">Sua chave de serviço será listada no hello *ServiceKey* campo:</span><span class="sxs-lookup"><span data-stu-id="9a94f-152">Your service key will be listed in hello *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="9a94f-153">resposta de saudação terá aparência semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-153">hello response will look similar toohello following example:</span></span>

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


<span data-ttu-id="9a94f-154">Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-154">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="9a94f-155">5. Enviar Olá tooyour chave conectividade provedor para provisionamento</span><span class="sxs-lookup"><span data-stu-id="9a94f-155">5. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="9a94f-156">*ServiceProviderProvisioningState* fornece informações sobre o estado atual de saudação do provisionamento no lado do provedor de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a94f-156">*ServiceProviderProvisioningState* provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="9a94f-157">Status fornece o estado de Olá em Olá lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9a94f-157">Status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="9a94f-158">Para obter mais informações sobre estados de provisionamento do circuito, consulte Olá [fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states) artigo.</span><span class="sxs-lookup"><span data-stu-id="9a94f-158">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="9a94f-159">Quando você cria um novo circuito de rota expressa, circuito Olá estará em Olá estado a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-159">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="9a94f-160">circuito Olá alterará toohello estado a seguir quando o provedor de conectividade Olá está no processo de saudação de habilitá-la para você:</span><span class="sxs-lookup"><span data-stu-id="9a94f-160">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="9a94f-161">Para você toobe capaz de toouse um circuito de rota expressa, ele deve ser Olá estado a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-161">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="9a94f-162">6. Verifique periodicamente o status de saudação e o estado de saudação da chave de circuito de saudação</span><span class="sxs-lookup"><span data-stu-id="9a94f-162">6. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="9a94f-163">Verificar o status de saudação e o estado de saudação da chave de circuito Olá permite que você saiba quando seu provedor habilitou o seu circuito.</span><span class="sxs-lookup"><span data-stu-id="9a94f-163">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="9a94f-164">Depois que o circuito Olá tiver sido configurado, *ServiceProviderProvisioningState* aparece como *provisionado*, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="9a94f-164">After hello circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in hello following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="9a94f-165">resposta de saudação terá aparência semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-165">hello response will look similar toohello following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="9a94f-166">7. Criar sua configuração de roteamento</span><span class="sxs-lookup"><span data-stu-id="9a94f-166">7. Create your routing configuration</span></span>
<span data-ttu-id="9a94f-167">Para obter instruções passo a passo, consulte Olá [configuração de roteamento de circuito de rota expressa](expressroute-howto-routing-arm.md) artigo toocreate e modificar os emparelhamentos de circuito.</span><span class="sxs-lookup"><span data-stu-id="9a94f-167">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a94f-168">Essas instruções se aplicam somente a toocircuits que são criados com provedores de serviços que oferecem serviços da camada 2 de conectividade.</span><span class="sxs-lookup"><span data-stu-id="9a94f-168">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="9a94f-169">Se você estiver usando um provedor de serviços que oferece serviços gerenciados de camada 3 (normalmente um IP VPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="9a94f-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="9a94f-170">8. Vincular um circuito de rota expressa do tooan de rede virtual</span><span class="sxs-lookup"><span data-stu-id="9a94f-170">8. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="9a94f-171">Em seguida, vincule um circuito de rota expressa do tooyour de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9a94f-171">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="9a94f-172">Saudação de uso [vinculação virtual redes circuitos tooExpressRoute](expressroute-howto-linkvnet-arm.md) quando você trabalha com o modelo de implantação do Gerenciador de recursos de saudação do artigo.</span><span class="sxs-lookup"><span data-stu-id="9a94f-172">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="9a94f-173">Obter status de saudação de um circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="9a94f-173">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="9a94f-174">Você pode recuperar essas informações a qualquer momento usando Olá **AzureRmExpressRouteCircuit Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a94f-174">You can retrieve this information at any time by using hello **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="9a94f-175">Fazer com que o hello chamada sem parâmetros lista todos os circuitos hello.</span><span class="sxs-lookup"><span data-stu-id="9a94f-175">Making hello call with no parameters lists all hello circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="9a94f-176">resposta de saudação será semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-176">hello response will be similar toohello following example:</span></span>

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


<span data-ttu-id="9a94f-177">Você pode obter informações sobre um circuito de rota expressa específica, passando o nome do grupo de recursos de saudação e o nome do circuito como uma chamada de toohello do parâmetro:</span><span class="sxs-lookup"><span data-stu-id="9a94f-177">You can get information on a specific ExpressRoute circuit by passing hello resource group name and circuit name as a parameter toohello call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="9a94f-178">resposta de saudação terá aparência semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-178">hello response will look similar toohello following example:</span></span>

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


<span data-ttu-id="9a94f-179">Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-179">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="9a94f-180"><a name="modify">
            </a>Modificar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9a94f-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="9a94f-181">Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="9a94f-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="9a94f-182">Você pode fazer Olá sem tempo de inatividade a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-182">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="9a94f-183">Como habilitar ou desabilitar o complemento premium do ExpressRoute para seu circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9a94f-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="9a94f-184">Aumento de largura de banda de saudação do circuito ExpressRoute fornecido há capacidade disponível na porta hello.</span><span class="sxs-lookup"><span data-stu-id="9a94f-184">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="9a94f-185">Não há suporte para a largura de banda de saudação de um circuito de downgrade.</span><span class="sxs-lookup"><span data-stu-id="9a94f-185">Downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="9a94f-186">Alterar o plano de dados limitados tooUnlimited dados de medição de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a94f-186">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="9a94f-187">Alterando Olá plano de dados ilimitado tooMetered não há suporte para dados de medição.</span><span class="sxs-lookup"><span data-stu-id="9a94f-187">Changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="9a94f-188">Você pode habilitar e desabilitar *Permitir Operações Clássicas*.</span><span class="sxs-lookup"><span data-stu-id="9a94f-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="9a94f-189">Para obter mais informações sobre limitações e limites, consulte toohello [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="9a94f-189">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="9a94f-190">complemento do premium tooenable Olá rota expressa</span><span class="sxs-lookup"><span data-stu-id="9a94f-190">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="9a94f-191">Você pode habilitar o complemento do premium Olá rota expressa para o circuito existente usando Olá trecho do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-191">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="9a94f-192">circuito Olá terá habilitados dos recursos de complemento de premium Olá rota expressa.</span><span class="sxs-lookup"><span data-stu-id="9a94f-192">hello circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="9a94f-193">Começaremos a cobrança é para o recurso de complemento premium Olá assim que o comando Olá foi executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="9a94f-193">We will begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="9a94f-194">complemento do premium toodisable Olá rota expressa</span><span class="sxs-lookup"><span data-stu-id="9a94f-194">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9a94f-195">Essa operação pode falhar se você estiver usando recursos que são maiores do que o que é permitido para o circuito de saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="9a94f-195">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="9a94f-196">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9a94f-196">Note hello following:</span></span>

* <span data-ttu-id="9a94f-197">Antes de você fazer o downgrade de premium toostandard, você deve garantir que esse número de saudação de redes virtuais que estão vinculadas toohello circuito é inferior a 10.</span><span class="sxs-lookup"><span data-stu-id="9a94f-197">Before you downgrade from premium toostandard, you must ensure that hello number of virtual networks that are linked toohello circuit is less than 10.</span></span> <span data-ttu-id="9a94f-198">Se você não fizer isso, sua solicitação de atualização falhará e cobraremos com tarifas premium.</span><span class="sxs-lookup"><span data-stu-id="9a94f-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="9a94f-199">Você precisa desvincular todas as redes virtuais em outras regiões geopolíticas.</span><span class="sxs-lookup"><span data-stu-id="9a94f-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="9a94f-200">Se você não fizer isso, sua solicitação de atualização falhará e cobraremos com tarifas premium.</span><span class="sxs-lookup"><span data-stu-id="9a94f-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="9a94f-201">Sua tabela de roteamento deve ter menos de 4.000 rotas para o emparelhamento privado.</span><span class="sxs-lookup"><span data-stu-id="9a94f-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="9a94f-202">Se o tamanho da tabela de rota for maior que 4.000 rotas, a sessão BGP de saudação descarta e não ser reabilitada até que o número de saudação de prefixos anunciados fica abaixo de 4.000.</span><span class="sxs-lookup"><span data-stu-id="9a94f-202">If your route table size is greater than 4,000 routes, hello BGP session drops and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="9a94f-203">Você pode desabilitar o complemento do premium Olá rota expressa para o circuito existente hello usando Olá cmdlet do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-203">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="9a94f-204">largura de banda de circuito ExpressRoute tooupdate Olá</span><span class="sxs-lookup"><span data-stu-id="9a94f-204">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="9a94f-205">Para obter opções de largura de banda com suporte para o seu provedor, verifique Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="9a94f-205">For supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="9a94f-206">Você pode escolher qualquer tamanho maior do que o tamanho de saudação do circuito existente.</span><span class="sxs-lookup"><span data-stu-id="9a94f-206">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a94f-207">Você pode ter o circuito de rota expressa Olá toorecreate se não houver capacidade insuficiente na porta existente Olá.</span><span class="sxs-lookup"><span data-stu-id="9a94f-207">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="9a94f-208">Não é possível atualizar o circuito de saudação se não houver nenhuma capacidade adicional disponível nesse local.</span><span class="sxs-lookup"><span data-stu-id="9a94f-208">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="9a94f-209">Você não pode reduzir a largura de banda de saudação de um circuito de rota expressa sem interrupções.</span><span class="sxs-lookup"><span data-stu-id="9a94f-209">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="9a94f-210">Downgrade da largura de banda requer que o circuito de rota expressa Olá toodeprovision e, em seguida, Reprovisionar um novo circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="9a94f-210">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="9a94f-211">Depois de decidir qual o tamanho que você precisa usar o circuito de Olá tooresize de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-211">After you decide what size you need, use hello following command tooresize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="9a94f-212">O circuito será dimensionado para cima no lado do Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="9a94f-212">Your circuit will be sized up on hello Microsoft side.</span></span> <span data-ttu-id="9a94f-213">Em seguida, você deve contatar suas configurações de tooupdate do provedor de conectividade em seu toomatch lado essa alteração.</span><span class="sxs-lookup"><span data-stu-id="9a94f-213">Then you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="9a94f-214">Depois de fazer essa notificação, começaremos a cobrança você para a opção de largura de banda Olá atualizado.</span><span class="sxs-lookup"><span data-stu-id="9a94f-214">After you make this notification, we will begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="9a94f-215">Olá toomove SKU de toounlimited limitado</span><span class="sxs-lookup"><span data-stu-id="9a94f-215">toomove hello SKU from metered toounlimited</span></span>
<span data-ttu-id="9a94f-216">Você pode alterar Olá SKU de um circuito de rota expressa usando Olá trecho do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-216">You can change hello SKU of an ExpressRoute circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="9a94f-217">toocontrol clássico de toohello de acesso e ambientes do Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="9a94f-217">toocontrol access toohello classic and Resource Manager environments</span></span>
<span data-ttu-id="9a94f-218">Consulte as instruções de saudação em [circuitos ExpressRoute mover de modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9a94f-218">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="9a94f-219">Desprovisionamento e exclusão de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9a94f-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="9a94f-220">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9a94f-220">Note hello following:</span></span>

* <span data-ttu-id="9a94f-221">Você deve desvincular todas as redes virtuais da saudação circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="9a94f-221">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="9a94f-222">Se essa operação falhar, verifique toosee se todas as redes virtuais são vinculados toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="9a94f-222">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="9a94f-223">Se o provedor de serviços de circuito ExpressRoute Olá estado de provisionamento é **provisionamento** ou **provisionado** você deve trabalhar com o circuito de saudação do serviço provedor toodeprovision em seu lado.</span><span class="sxs-lookup"><span data-stu-id="9a94f-223">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="9a94f-224">Vamos continuar tooreserve recursos e cobrar você até que o provedor de serviços Olá Complete desprovisionamento circuito de saudação e nos notifica.</span><span class="sxs-lookup"><span data-stu-id="9a94f-224">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="9a94f-225">Se o provedor de serviços de saudação tem desprovisionada circuito hello (provedor de serviços de saudação estado de provisionamento está definido muito**não provisionado**), em seguida, você pode excluir o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a94f-225">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="9a94f-226">Isso interromperá a cobrança para o circuito Olá</span><span class="sxs-lookup"><span data-stu-id="9a94f-226">This will stop billing for hello circuit</span></span>

<span data-ttu-id="9a94f-227">Você pode excluir o circuito de rota expressa executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-227">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="9a94f-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9a94f-228">Next steps</span></span>

<span data-ttu-id="9a94f-229">Depois de criar o circuito, certifique-se de que Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a94f-229">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="9a94f-230">Criar e modificar o roteamento do circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9a94f-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="9a94f-231">Vincular sua rede virtual de tooyour circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="9a94f-231">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
