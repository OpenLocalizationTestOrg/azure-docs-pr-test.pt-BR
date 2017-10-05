---
title: 'Criar e modificar um circuito ExpressRoute: PowerShell: Azure Resource Manager | Microsoft Docs'
description: Este artigo descreve como criar, provisionar, verificar, atualizar, excluir e desprovisionar um circuito do ExpressRoute.
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
ms.openlocfilehash: 8bfae39d84aaac3b9527084df9dcfbd51f591dfe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="c4303-103">Criar e modificar um circuito do ExpressRoute usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4303-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4303-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c4303-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="c4303-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4303-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="c4303-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c4303-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="c4303-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c4303-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="c4303-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="c4303-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="c4303-109">Este artigo descreve como criar um circuito do Azure ExpressRoute usando os cmdlets do Windows PowerShell e o modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c4303-109">This article describes how to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="c4303-110">Este artigo também mostra como verificar o status do circuito, atualizá-lo ou excluí-lo e desprovisioná-lo.</span><span class="sxs-lookup"><span data-stu-id="c4303-110">This article also shows you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c4303-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c4303-111">Before you begin</span></span>
* <span data-ttu-id="c4303-112">Instale a versão mais recente dos cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c4303-112">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c4303-113">Para obter mais informações, consulte [Visão geral do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c4303-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="c4303-114">Examine os [pré-requisitos](expressroute-prerequisites.md) e os [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="c4303-114">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="c4303-115">Criar e provisionar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="c4303-116">1. Entre na sua conta do Azure e selecione sua assinatura</span><span class="sxs-lookup"><span data-stu-id="c4303-116">1. Sign in to your Azure account and select your subscription</span></span>
<span data-ttu-id="c4303-117">Para iniciar sua configuração, entrar na sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4303-117">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="c4303-118">Use o exemplo a seguir para ajudar a conectar:</span><span class="sxs-lookup"><span data-stu-id="c4303-118">Use the following examples to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="c4303-119">Verifique as assinaturas da conta:</span><span class="sxs-lookup"><span data-stu-id="c4303-119">Check the subscriptions for the account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="c4303-120">Selecione a assinatura para a qual você deseja criar um circuito do ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="c4303-120">Select the subscription that you want to create an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="c4303-121">2. Obtenha a lista de provedores, de locais e de larguras de banda com suporte</span><span class="sxs-lookup"><span data-stu-id="c4303-121">2. Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="c4303-122">Antes de criar um circuito de ExpressRoute você precisará de uma lista de provedores de conectividade com suporte, dos locais e de opções de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="c4303-122">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="c4303-123">O cmdlet do PowerShell **Get-AzureRmExpressRouteServiceProvider** retorna essas informações, que serão usadas em etapas posteriores:</span><span class="sxs-lookup"><span data-stu-id="c4303-123">The PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="c4303-124">Verifique se o provedor de conectividade está listado.</span><span class="sxs-lookup"><span data-stu-id="c4303-124">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="c4303-125">Anote as informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="c4303-125">Make a note of the following information.</span></span> <span data-ttu-id="c4303-126">Você precisará delas mais tarde ao criar um circuito.</span><span class="sxs-lookup"><span data-stu-id="c4303-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="c4303-127">Nome</span><span class="sxs-lookup"><span data-stu-id="c4303-127">Name</span></span>
* <span data-ttu-id="c4303-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="c4303-128">PeeringLocations</span></span>
* <span data-ttu-id="c4303-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="c4303-129">BandwidthsOffered</span></span>

<span data-ttu-id="c4303-130">Agora você está pronto para criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c4303-130">You're now ready to create an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="c4303-131">3. Criar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="c4303-132">Se você ainda não tiver um grupo de recursos, deverá criar um antes de criar o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c4303-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="c4303-133">Faça isso ao executar o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c4303-133">You can do so by running the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="c4303-134">O exemplo a seguir mostra como criar um circuito do ExpressRoute de 200 Mbps por meio da Equinix, no Vale do Silício.</span><span class="sxs-lookup"><span data-stu-id="c4303-134">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="c4303-135">Se estiver usando um provedor diferente e configurações diferentes, substitua essas informações ao fazer a solicitação.</span><span class="sxs-lookup"><span data-stu-id="c4303-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="c4303-136">A seguir, um exemplo de solicitação de uma nova chave de serviço:</span><span class="sxs-lookup"><span data-stu-id="c4303-136">The following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="c4303-137">Especifique a camada da SKU e a família de SKUs corretas:</span><span class="sxs-lookup"><span data-stu-id="c4303-137">Make sure that you specify the correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="c4303-138">A camada da SKU determina se um complemento padrão ou premium do ExpressRoute está habilitado.</span><span class="sxs-lookup"><span data-stu-id="c4303-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="c4303-139">Você pode especificar *Standard* para obter o SKU padrão ou *Premium* para o complemento premium.</span><span class="sxs-lookup"><span data-stu-id="c4303-139">You can specify *Standard* to get the standard SKU or *Premium* for the premium add-on.</span></span>
* <span data-ttu-id="c4303-140">A família da SKU determina o tipo de cobrança.</span><span class="sxs-lookup"><span data-stu-id="c4303-140">SKU family determines the billing type.</span></span> <span data-ttu-id="c4303-141">Você pode especificar *Metereddata* para um plano de dados limitado e *Unlimiteddata* para um plano de dados ilimitado.</span><span class="sxs-lookup"><span data-stu-id="c4303-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="c4303-142">É possível alterar o tipo de cobrança de *Metereddata* para *Unlimiteddata*, mas não é possível alterar o tipo de *Unlimiteddata* para *Metereddata*.</span><span class="sxs-lookup"><span data-stu-id="c4303-142">You can change the billing type from *Metereddata* to *Unlimiteddata*, but you can't change the type from *Unlimiteddata* to *Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4303-143">O circuito do ExpressRoute será cobrado a partir do momento em que uma chave de serviço for emitida.</span><span class="sxs-lookup"><span data-stu-id="c4303-143">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="c4303-144">Execute esta operação quando o provedor de conectividade estiver pronto para provisionar o circuito.</span><span class="sxs-lookup"><span data-stu-id="c4303-144">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="c4303-145">A resposta conterá a chave de serviço.</span><span class="sxs-lookup"><span data-stu-id="c4303-145">The response contains the service key.</span></span> <span data-ttu-id="c4303-146">Você pode obter descrições detalhadas de todos os parâmetros executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c4303-146">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="c4303-147">4. Listar todos os circuitos do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="c4303-148">Para obter uma lista de todos os circuitos do ExpressRoute criados, execute o comando **Get-AzureRmExpressRouteCircuit**:</span><span class="sxs-lookup"><span data-stu-id="c4303-148">To get a list of all the ExpressRoute circuits that you created, run the **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="c4303-149">A resposta será semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="c4303-149">The response will look similar to the following example:</span></span>

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

<span data-ttu-id="c4303-150">Você pode recuperar essas informações a qualquer momento usando o cmdlet `Get-AzureRmExpressRouteCircuit` .</span><span class="sxs-lookup"><span data-stu-id="c4303-150">You can retrieve this information at any time by using the `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="c4303-151">Fazer a chamada sem parâmetros listará todos os circuitos.</span><span class="sxs-lookup"><span data-stu-id="c4303-151">Making the call with no parameters lists all the circuits.</span></span> <span data-ttu-id="c4303-152">Sua chave de serviço estará listada no campo *ServiceKey* :</span><span class="sxs-lookup"><span data-stu-id="c4303-152">Your service key will be listed in the *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="c4303-153">A resposta será semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="c4303-153">The response will look similar to the following example:</span></span>

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


<span data-ttu-id="c4303-154">Você pode obter descrições detalhadas de todos os parâmetros executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c4303-154">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="c4303-155">5. Enviar a chave de serviço ao seu provedor de conectividade para obter provisionamento</span><span class="sxs-lookup"><span data-stu-id="c4303-155">5. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="c4303-156">*ServiceProviderProvisioningState* fornece informações sobre o estado atual de provisionamento no lado do provedor de serviço.</span><span class="sxs-lookup"><span data-stu-id="c4303-156">*ServiceProviderProvisioningState* provides information about the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="c4303-157">Status fornece o estado no lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c4303-157">Status provides the state on the Microsoft side.</span></span> <span data-ttu-id="c4303-158">Para saber mais sobre estados de provisionamento do circuito, confira o artigo [Fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states) .</span><span class="sxs-lookup"><span data-stu-id="c4303-158">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="c4303-159">Quando você criar um novo circuito do ExpressRoute, ele estará no seguinte estado:</span><span class="sxs-lookup"><span data-stu-id="c4303-159">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="c4303-160">O circuito assumirá o estado a seguir quando o provedor de conectividade estiver no processo de habilitá-lo para você:</span><span class="sxs-lookup"><span data-stu-id="c4303-160">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="c4303-161">Para que você consiga usar um circuito do ExpressRoute, ele deverá estar no seguinte estado:</span><span class="sxs-lookup"><span data-stu-id="c4303-161">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="c4303-162">6. Verifique periodicamente o status e o estado da chave do circuito</span><span class="sxs-lookup"><span data-stu-id="c4303-162">6. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="c4303-163">A verificação do status e o estado da chave do circuito informará quando o provedor tiver habilitado seu circuito.</span><span class="sxs-lookup"><span data-stu-id="c4303-163">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="c4303-164">Após a configuração do circuito, o *ServiceProviderProvisioningState* será exibido como *Provisioned*, como mostrado neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="c4303-164">After the circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in the following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="c4303-165">A resposta será semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="c4303-165">The response will look similar to the following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="c4303-166">7. Criar sua configuração de roteamento</span><span class="sxs-lookup"><span data-stu-id="c4303-166">7. Create your routing configuration</span></span>
<span data-ttu-id="c4303-167">Para obter instruções passo a passo, confira o artigo [configuração do roteamento de circuito do ExpressRoute](expressroute-howto-routing-arm.md) para criar e modificar os emparelhamentos de circuito.</span><span class="sxs-lookup"><span data-stu-id="c4303-167">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4303-168">Estas instruções aplicam-se apenas a circuitos criados com provedores de serviço que oferecem serviços de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="c4303-168">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="c4303-169">Se você estiver usando um provedor de serviços que oferece serviços gerenciados de camada 3 (normalmente um IP VPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="c4303-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="c4303-170">8. Vincular uma rede virtual a um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-170">8. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="c4303-171">Em seguida, vincule uma rede virtual a seu circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c4303-171">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="c4303-172">Use o artigo [Vincular redes virtuais a circuitos do ExpressRoute](expressroute-howto-linkvnet-arm.md) ao trabalhar com o modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="c4303-172">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="c4303-173">Obtendo o status de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-173">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="c4303-174">Você pode recuperar essas informações a qualquer momento usando o cmdlet **Get-AzureRmExpressRouteCircuit**.</span><span class="sxs-lookup"><span data-stu-id="c4303-174">You can retrieve this information at any time by using the **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="c4303-175">Fazer a chamada sem parâmetros listará todos os circuitos.</span><span class="sxs-lookup"><span data-stu-id="c4303-175">Making the call with no parameters lists all the circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="c4303-176">A resposta será semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="c4303-176">The response will be similar to the following example:</span></span>

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


<span data-ttu-id="c4303-177">Você pode obter informações sobre um circuito do ExpressRoute específico passando o nome do grupo de recursos e o nome do circuito como um parâmetro para a chamada:</span><span class="sxs-lookup"><span data-stu-id="c4303-177">You can get information on a specific ExpressRoute circuit by passing the resource group name and circuit name as a parameter to the call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="c4303-178">A resposta será semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="c4303-178">The response will look similar to the following example:</span></span>

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


<span data-ttu-id="c4303-179">Você pode obter descrições detalhadas de todos os parâmetros executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c4303-179">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="c4303-180"><a name="modify">
            </a>Modificar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="c4303-181">Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="c4303-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="c4303-182">Você pode fazer o seguinte sem tempo de inatividade:</span><span class="sxs-lookup"><span data-stu-id="c4303-182">You can do the following with no downtime:</span></span>

* <span data-ttu-id="c4303-183">Como habilitar ou desabilitar o complemento premium do ExpressRoute para seu circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c4303-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="c4303-184">Aumente a largura de banda do circuito de ExpressRoute, desde que haja capacidade disponível na porta.</span><span class="sxs-lookup"><span data-stu-id="c4303-184">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="c4303-185">Não há suporte para o downgrade da largura de banda de um circuito.</span><span class="sxs-lookup"><span data-stu-id="c4303-185">Downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="c4303-186">Altere o plano de medição de Dados Limitados para Dados Ilimitados.</span><span class="sxs-lookup"><span data-stu-id="c4303-186">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="c4303-187">Não há suporte para alteração do plano de medição de Dados Ilimitados para Dados Limitados.</span><span class="sxs-lookup"><span data-stu-id="c4303-187">Changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="c4303-188">Você pode habilitar e desabilitar *Permitir Operações Clássicas*.</span><span class="sxs-lookup"><span data-stu-id="c4303-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="c4303-189">Para saber mais sobre limites e limitações, confira as [Perguntas frequentes sobre o ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="c4303-189">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="c4303-190">Para habilitar o complemento premium do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-190">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="c4303-191">Você pode habilitar o complemento premium do ExpressRoute para o circuito existente usando o seguinte trecho do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c4303-191">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="c4303-192">Agora, o circuito terá os recursos de complemento premium do ExpressRoute habilitados.</span><span class="sxs-lookup"><span data-stu-id="c4303-192">The circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="c4303-193">Começaremos a cobrar pela funcionalidade do complemento Premium assim que o comando for executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="c4303-193">We will begin billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="c4303-194">Para desabilitar o complemento premium do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-194">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c4303-195">Esta operação poderá falhar se você estiver usando recursos que ultrapassem o que é permitido para o circuito padrão.</span><span class="sxs-lookup"><span data-stu-id="c4303-195">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

<span data-ttu-id="c4303-196">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c4303-196">Note the following:</span></span>

* <span data-ttu-id="c4303-197">Antes de fazer o downgrade de premium para standard, verifique se o número de redes virtuais vinculadas ao circuito é menor que 10.</span><span class="sxs-lookup"><span data-stu-id="c4303-197">Before you downgrade from premium to standard, you must ensure that the number of virtual networks that are linked to the circuit is less than 10.</span></span> <span data-ttu-id="c4303-198">Se você não fizer isso, sua solicitação de atualização falhará e cobraremos com tarifas premium.</span><span class="sxs-lookup"><span data-stu-id="c4303-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="c4303-199">Você precisa desvincular todas as redes virtuais em outras regiões geopolíticas.</span><span class="sxs-lookup"><span data-stu-id="c4303-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="c4303-200">Se você não fizer isso, sua solicitação de atualização falhará e cobraremos com tarifas premium.</span><span class="sxs-lookup"><span data-stu-id="c4303-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="c4303-201">Sua tabela de roteamento deve ter menos de 4.000 rotas para o emparelhamento privado.</span><span class="sxs-lookup"><span data-stu-id="c4303-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="c4303-202">Se o tamanho da tabela de roteamento for maior que 4.000 rotas, a sessão BGP será descartada e não poderá ser reabilitada até que o número de prefixos anunciados fique abaixo de 4.000.</span><span class="sxs-lookup"><span data-stu-id="c4303-202">If your route table size is greater than 4,000 routes, the BGP session drops and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="c4303-203">Você pode desabilitar o complemento premium do ExpressRoute para o circuito existente usando o seguinte cmdlet do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c4303-203">You can disable the ExpressRoute premium add-on for the existing circuit by using the following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="c4303-204">Para atualizar a largura de banda do circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-204">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="c4303-205">Para obter opções de largura de banda com suporte para seu provedor, confira as [Perguntas frequentes sobre o ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="c4303-205">For supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="c4303-206">Você pode escolher qualquer tamanho maior do que o tamanho do circuito existente.</span><span class="sxs-lookup"><span data-stu-id="c4303-206">You can pick any size greater than the size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4303-207">Talvez seja necessário recriar o circuito de ExpressRoute se não houver capacidade adequada na porta existente.</span><span class="sxs-lookup"><span data-stu-id="c4303-207">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="c4303-208">Você não pode atualizar o circuito não se houver capacidade adicional disponível nesse local.</span><span class="sxs-lookup"><span data-stu-id="c4303-208">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="c4303-209">Não é possível reduzir a largura de banda de um circuito do ExpressRoute sem interrupções.</span><span class="sxs-lookup"><span data-stu-id="c4303-209">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="c4303-210">O downgrade da largura de banda exige o desprovisionamento do circuito do ExpressRoute e um reprovisionamento de um novo circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c4303-210">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="c4303-211">Depois de decidir sobre qual tamanho você precisa, use o seguinte comando para redimensionar o circuito:</span><span class="sxs-lookup"><span data-stu-id="c4303-211">After you decide what size you need, use the following command to resize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="c4303-212">O circuito será dimensionado no lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c4303-212">Your circuit will be sized up on the Microsoft side.</span></span> <span data-ttu-id="c4303-213">Entre em contato com seu provedor de conectividade para que ele atualize as configurações para corresponder a essa alteração.</span><span class="sxs-lookup"><span data-stu-id="c4303-213">Then you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="c4303-214">Depois que você fizer essa notificação, começaremos a cobrar pela opção de largura de banda atualizada.</span><span class="sxs-lookup"><span data-stu-id="c4303-214">After you make this notification, we will begin billing you for the updated bandwidth option.</span></span>

### <a name="to-move-the-sku-from-metered-to-unlimited"></a><span data-ttu-id="c4303-215">Para mover a SKU de limitado para ilimitado</span><span class="sxs-lookup"><span data-stu-id="c4303-215">To move the SKU from metered to unlimited</span></span>
<span data-ttu-id="c4303-216">Você pode alterar a SKU de um circuito de ExpressRoute usando o seguinte trecho de código do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c4303-216">You can change the SKU of an ExpressRoute circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a><span data-ttu-id="c4303-217">Para controlar o acesso aos ambientes clássico e do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c4303-217">To control access to the classic and Resource Manager environments</span></span>
<span data-ttu-id="c4303-218">Confira as instruções em [Mover os circuitos de ExpressRoute do modelo de implantação Clássico para o Resource Manager](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c4303-218">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="c4303-219">Desprovisionamento e exclusão de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="c4303-220">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c4303-220">Note the following:</span></span>

* <span data-ttu-id="c4303-221">Você deve desvincular todas as redes virtuais do circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c4303-221">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="c4303-222">Se essa operação falhar, verifique se há redes virtuais vinculadas ao circuito.</span><span class="sxs-lookup"><span data-stu-id="c4303-222">If this operation fails, check to see if any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="c4303-223">Se o estado de provisionamento do provedor de serviço de circuito de ExpressRoute for **Provisionando** ou **Provisionado**, você deverá trabalhar com seu provedor de serviços para que ele desprovisione o circuito.</span><span class="sxs-lookup"><span data-stu-id="c4303-223">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="c4303-224">Continuaremos a reservar recursos e a cobrar de você até que o provedor de serviços complete o desprovisionamento do circuito e nos notifique.</span><span class="sxs-lookup"><span data-stu-id="c4303-224">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="c4303-225">Se o provedor de serviços tiver desprovisionado o circuito (o estado de provisionamento do provedor de serviços estiver definido como **Não provisionado**), exclua o circuito.</span><span class="sxs-lookup"><span data-stu-id="c4303-225">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="c4303-226">Isso interromperá a cobrança do circuito</span><span class="sxs-lookup"><span data-stu-id="c4303-226">This will stop billing for the circuit</span></span>

<span data-ttu-id="c4303-227">Você pode excluir o circuito do ExpressRoute executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4303-227">You can delete your ExpressRoute circuit by running the following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="c4303-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4303-228">Next steps</span></span>

<span data-ttu-id="c4303-229">Depois de criar seu circuito, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c4303-229">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="c4303-230">Criar e modificar o roteamento do circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="c4303-231">Vincular a rede virtual ao circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c4303-231">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
