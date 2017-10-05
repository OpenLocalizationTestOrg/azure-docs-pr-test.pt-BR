---
title: "Criar e modificar um circuito ExpressRoute: PowerShell: Azure clássico | Microsoft Docs"
description: "Este artigo fornece uma orientação sobre as etapas de criação e de provisionamento de um circuito do ExpressRoute. Este artigo também mostra como verificar o status, atualizar ou excluir e desprovisionar seu circuito."
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
ms.openlocfilehash: 3b12bbb21ebf6a0160227c4a281c420cf192d6f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="f0a8d-104">Criar e modificar um circuito da ExpressRoute usando o PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="f0a8d-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0a8d-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f0a8d-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="f0a8d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0a8d-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="f0a8d-107">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f0a8d-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="f0a8d-108">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f0a8d-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="f0a8d-109">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="f0a8d-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="f0a8d-110">Este artigo fornece uma orientação pelas etapas de criação de um circuito da Azure ExpressRoute usando cmdlets do PowerShell e o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-110">This article walks you through the steps to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the classic deployment model.</span></span> <span data-ttu-id="f0a8d-111">Este artigo também mostra a você como verificar o status, atualizar ou excluir e desprovisionar um circuito da ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-111">This article also shows you how to check the status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="f0a8d-112">**Sobre modelos de implantação do Azure**</span><span class="sxs-lookup"><span data-stu-id="f0a8d-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="f0a8d-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f0a8d-113">Before you begin</span></span>
### <a name="step-1-review-the-prerequisites-and-workflow-articles"></a><span data-ttu-id="f0a8d-114">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-114">Step 1.</span></span> <span data-ttu-id="f0a8d-115">Examine os pré-requisitos e artigos de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="f0a8d-115">Review the prerequisites and workflow articles</span></span>
<span data-ttu-id="f0a8d-116">Leia os [pré-requisitos](expressroute-prerequisites.md) e os [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-116">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-the-latest-versions-of-the-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="f0a8d-117">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-117">Step 2.</span></span> <span data-ttu-id="f0a8d-118">Instalar as versões mais recentes dos módulos do PowerShell do SM (Gerenciamento de Serviços) do Azure</span><span class="sxs-lookup"><span data-stu-id="f0a8d-118">Install the latest versions of the Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="f0a8d-119">Siga as instruções em [Introdução aos cmdlets do Azure PowerShell](/powershell/azure/overview) para obter orientações passo a passo sobre como configurar o computador para usar os módulos do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-119">Follow the instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="f0a8d-120">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-120">Step 3.</span></span> <span data-ttu-id="f0a8d-121">Entre em sua conta do Azure e selecione uma assinatura</span><span class="sxs-lookup"><span data-stu-id="f0a8d-121">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="f0a8d-122">Abra o console do PowerShell com direitos elevados e conecte-se à sua conta.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-122">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="f0a8d-123">Use o exemplo a seguir para ajudar a se conectar:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-123">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="f0a8d-124">Verificar as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-124">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="f0a8d-125">Se você tiver mais de uma assinatura, selecione a assinatura que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-125">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="f0a8d-126">Use o cmdlet a seguir para adicionar sua assinatura do Azure ao PowerShell para o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-126">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="f0a8d-127">Criar e provisionar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-the-powershell-modules-for-expressroute"></a><span data-ttu-id="f0a8d-128">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-128">Step 1.</span></span> <span data-ttu-id="f0a8d-129">Importar os módulos do PowerShell para o ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-129">Import the PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="f0a8d-130">Se ainda não tiver feito isso, importe os módulos do Azure e de ExpressRoute na sessão do PowerShell para começar a usar os cmdlets de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-130">If you have not already done so, you must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="f0a8d-131">Importe os módulos do local onde foram instalados para o computador local.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-131">You import the modules from the location that they were installed to on your local computer.</span></span> <span data-ttu-id="f0a8d-132">Dependendo do método usado para instalar os módulos, o local pode ser diferente do exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-132">Depending on the method you used to install the modules, the location may be different than the following example shows.</span></span> <span data-ttu-id="f0a8d-133">Modifique o exemplo, se for necessário.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-133">Modify the example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="f0a8d-134">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-134">Step 2.</span></span> <span data-ttu-id="f0a8d-135">Obtenha a lista de provedores, de locais e de larguras de banda com suporte</span><span class="sxs-lookup"><span data-stu-id="f0a8d-135">Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="f0a8d-136">Antes de criar um circuito de ExpressRoute você precisará de uma lista de provedores de conectividade com suporte, dos locais e de opções de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-136">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="f0a8d-137">O cmdlet do PowerShell `Get-AzureDedicatedCircuitServiceProvider` retornará estas informações, que você usará em etapas posteriores:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-137">The PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="f0a8d-138">Verifique se o provedor de conectividade está listado.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-138">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="f0a8d-139">Anote as informações a seguir, pois você precisará delas mais tarde quando criar um circuito:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-139">Make a note of the following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="f0a8d-140">Nome</span><span class="sxs-lookup"><span data-stu-id="f0a8d-140">Name</span></span>
* <span data-ttu-id="f0a8d-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="f0a8d-141">PeeringLocations</span></span>
* <span data-ttu-id="f0a8d-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="f0a8d-142">BandwidthsOffered</span></span>

<span data-ttu-id="f0a8d-143">Agora você está pronto para criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-143">You're now ready to create an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="f0a8d-144">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-144">Step 3.</span></span> <span data-ttu-id="f0a8d-145">Criar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="f0a8d-146">O exemplo a seguir mostra como criar um circuito do ExpressRoute de 200 Mbps por meio da Equinix, no Vale do Silício.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-146">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="f0a8d-147">Se estiver usando um provedor diferente e configurações diferentes, substitua essas informações ao fazer a solicitação.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0a8d-148">O circuito do ExpressRoute será cobrado a partir do momento em que uma chave de serviço for emitida.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-148">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="f0a8d-149">Execute esta operação quando o provedor de conectividade estiver pronto para provisionar o circuito.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-149">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="f0a8d-150">A seguir, um exemplo de solicitação de uma nova chave de serviço:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-150">The following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="f0a8d-151">Ou então, se quiser criar um circuito do ExpressRoute com o complemento premium, use o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-151">Or, if you want to create an ExpressRoute circuit with the premium add-on, use the following example.</span></span> <span data-ttu-id="f0a8d-152">Confira s [Perguntas frequentes sobre o ExpressRoute](expressroute-faqs.md) para saber mais sobre o complemento premium.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-152">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more details about the premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="f0a8d-153">A resposta conterá a chave de serviço.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-153">The response will contain the service key.</span></span> <span data-ttu-id="f0a8d-154">Você pode obter descrições detalhadas de todos os parâmetros executando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-154">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-the-expressroute-circuits"></a><span data-ttu-id="f0a8d-155">Etapa 4.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-155">Step 4.</span></span> <span data-ttu-id="f0a8d-156">Listar todos os circuitos do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-156">List all the ExpressRoute circuits</span></span>
<span data-ttu-id="f0a8d-157">Você pode executar o comando `Get-AzureDedicatedCircuit` para obter uma lista de todos os circuitos do ExpressRoute que criou:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-157">You can run the `Get-AzureDedicatedCircuit` command to get a list of all the ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="f0a8d-158">A resposta será algo semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-158">The response will be something similar to the following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="f0a8d-159">Você pode recuperar essas informações a qualquer momento usando o cmdlet `Get-AzureDedicatedCircuit` .</span><span class="sxs-lookup"><span data-stu-id="f0a8d-159">You can retrieve this information at any time by using the `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="f0a8d-160">Fazer a chamada sem parâmetros listará todos os circuitos.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-160">Making the call without any parameters lists all the circuits.</span></span> <span data-ttu-id="f0a8d-161">Sua chave de serviço estará listada no campo *ServiceKey* .</span><span class="sxs-lookup"><span data-stu-id="f0a8d-161">Your service key will be listed in the *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="f0a8d-162">Você pode obter descrições detalhadas de todos os parâmetros executando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-162">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="f0a8d-163">Etapa 5.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-163">Step 5.</span></span> <span data-ttu-id="f0a8d-164">Enviar a chave de serviço ao seu provedor de conectividade para obter provisionamento</span><span class="sxs-lookup"><span data-stu-id="f0a8d-164">Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="f0a8d-165">*ServiceProviderProvisioningState* fornece informações sobre o estado atual de provisionamento no lado do provedor de serviço.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-165">*ServiceProviderProvisioningState* provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="f0a8d-166">*Status* fornece o estado no lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-166">*Status* provides the state on the Microsoft side.</span></span> <span data-ttu-id="f0a8d-167">Para saber mais sobre estados de provisionamento do circuito, confira o artigo [Fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states) .</span><span class="sxs-lookup"><span data-stu-id="f0a8d-167">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="f0a8d-168">Quando você criar um novo circuito do ExpressRoute, ele estará no seguinte estado:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-168">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="f0a8d-169">O circuito assumirá o seguinte o estado quando o provedor de conectividade estiver habilitando-o para você:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-169">The circuit will go to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="f0a8d-170">Um circuito do ExpressRoute deverá estar no seguinte estado para você poder usá-lo:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-170">An ExpressRoute circuit must be in the following state for you to be able to use it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="f0a8d-171">Etapa 6.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-171">Step 6.</span></span> <span data-ttu-id="f0a8d-172">Verifique periodicamente o status e o estado da chave do circuito</span><span class="sxs-lookup"><span data-stu-id="f0a8d-172">Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="f0a8d-173">Isso permite que você saiba quando seu provedor habilitou seu circuito.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="f0a8d-174">Após a configuração do circuito, o *ServiceProviderProvisioningState* será exibido como *Provisioned*, como mostrado neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-174">After the circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in the following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="f0a8d-175">Etapa 7.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-175">Step 7.</span></span> <span data-ttu-id="f0a8d-176">Criar sua configuração de roteamento</span><span class="sxs-lookup"><span data-stu-id="f0a8d-176">Create your routing configuration</span></span>
<span data-ttu-id="f0a8d-177">Confira o artigo [Configuração de roteamento do circuito do ExpressRoute (criar e modificar emparelhamentos de circuito)](expressroute-howto-routing-classic.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-177">Refer to the [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0a8d-178">Estas instruções aplicam-se apenas a circuitos criados com provedores de serviço que oferecem serviços de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-178">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="f0a8d-179">Se você estiver usando um provedor de serviços que oferece serviços gerenciados de camada 3 (normalmente um IP VPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="f0a8d-180">Etapa 8.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-180">Step 8.</span></span> <span data-ttu-id="f0a8d-181">Vincular uma rede virtual a um circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-181">Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="f0a8d-182">Em seguida, vincule uma rede virtual a seu circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-182">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="f0a8d-183">Confira [Vincular circuitos do ExpressRoute a redes virtuais](expressroute-howto-linkvnet-classic.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-183">Refer to [Linking ExpressRoute circuits to virtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="f0a8d-184">Se você precisar criar uma rede virtual usando o modelo de implantação clássico para a ExpressRoute, confira [Criar uma rede virtual para o ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="f0a8d-184">If you need to create a virtual network using the classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="f0a8d-185">Obtendo o status de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-185">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="f0a8d-186">Você pode recuperar essas informações a qualquer momento usando o cmdlet `Get-AzureCircuit` .</span><span class="sxs-lookup"><span data-stu-id="f0a8d-186">You can retrieve this information at any time by using the `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="f0a8d-187">Fazer a chamada sem parâmetros listará todos os circuitos.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-187">Making the call without any parameters lists all the circuits.</span></span>

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

<span data-ttu-id="f0a8d-188">Você pode obter informações sobre um circuito do ExpressRoute específico passando a chave do serviço como um parâmetro para a chamada.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-188">You can get information on a specific ExpressRoute circuit by passing the service key as a parameter to the call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="f0a8d-189">Você pode obter descrições detalhadas de todos os parâmetros executando o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-189">You can get detailed descriptions of all the parameters by running the following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="f0a8d-190">Modificando um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="f0a8d-191">Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="f0a8d-192">Você pode fazer o seguinte sem tempo de inatividade:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-192">You can do the following with no downtime:</span></span>

* <span data-ttu-id="f0a8d-193">Como habilitar ou desabilitar o complemento premium do ExpressRoute para seu circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="f0a8d-194">Aumente a largura de banda do circuito de ExpressRoute, desde que haja capacidade disponível na porta.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-194">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="f0a8d-195">Observe que não há suporte para o downgrade da largura de banda de um circuito.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-195">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="f0a8d-196">Altere o plano de medição de Dados Limitados para Dados Ilimitados.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-196">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="f0a8d-197">Observe que a alteração do plano de medição de Dados Ilimitados para Dados Limitados não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-197">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="f0a8d-198">Você pode habilitar e desabilitar *Permitir Operações Clássicas*.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="f0a8d-199">Confira as [Perguntas frequentes sobre o ExpressRoute](expressroute-faqs.md) para saber mais sobre limites e limitações.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-199">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="f0a8d-200">Para habilitar o complemento premium do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-200">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="f0a8d-201">Você pode habilitar o complemento premium do ExpressRoute para o circuito existente usando o seguinte cmdlet do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-201">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="f0a8d-202">O seu circuito agora tem os recursos do complemento premium do ExpressRoute habilitados.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-202">Your circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="f0a8d-203">Observe que passaremos a cobrar pelo recurso do complemento Premium assim que o comando for executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-203">Note that we will start billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="f0a8d-204">Para desabilitar o complemento premium do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-204">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f0a8d-205">Esta operação poderá falhar se você estiver usando recursos que ultrapassem o que é permitido para o circuito padrão.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-205">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="f0a8d-206">Considerações</span><span class="sxs-lookup"><span data-stu-id="f0a8d-206">Considerations</span></span>

* <span data-ttu-id="f0a8d-207">Verifique se o número de redes virtuais vinculadas ao circuito é menor do que 10 antes de fazer o downgrade de Premium para padrão.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-207">You must ensure that the number of virtual networks linked to the circuit is less than 10 before you downgrade from premium to standard.</span></span> <span data-ttu-id="f0a8d-208">Caso contrário, sua solicitação de atualização falhará e você receberá uma cobrança com as taxas premium.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-208">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="f0a8d-209">Você precisa desvincular todas as redes virtuais em outras regiões geopolíticas.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="f0a8d-210">Caso contrário, sua solicitação de atualização falhará e você receberá uma cobrança com as taxas premium.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-210">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="f0a8d-211">Sua tabela de roteamento deve ter menos de 4.000 rotas para o emparelhamento privado.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="f0a8d-212">Se o tamanho da tabela de roteamento for maior que 4.000 rotas, a sessão BGP será descartada e não será reabilitada até que o número de prefixos anunciados fique abaixo de 4.000.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-212">If your route table size is greater than 4,000 routes, the BGP session will drop and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-the-premium-add-on"></a><span data-ttu-id="f0a8d-213">Desabilitar o complemento premium</span><span class="sxs-lookup"><span data-stu-id="f0a8d-213">Disable the premium add-on</span></span>
<span data-ttu-id="f0a8d-214">Você pode desabilitar o complemento premium do ExpressRoute para o circuito existente usando o seguinte cmdlet do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-214">You can disable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="f0a8d-215">Para atualizar a largura de banda do circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-215">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="f0a8d-216">Confira as [Perguntas frequentes sobre o ExpressRoute](expressroute-faqs.md) para obter opções de largura de banda com suporte para seu provedor.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-216">Check the [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="f0a8d-217">Você pode escolher um tamanho maior do que o tamanho do circuito existente, desde que a porta física (na qual o circuito foi criado) permita.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-217">You can pick any size that is greater than the size of your existing circuit as long as the physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0a8d-218">Talvez seja necessário recriar o circuito de ExpressRoute se não houver capacidade adequada na porta existente.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-218">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="f0a8d-219">Você não pode atualizar o circuito não se houver capacidade adicional disponível nesse local.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-219">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="f0a8d-220">Não é possível reduzir a largura de banda de um circuito do ExpressRoute sem interrupções.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-220">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="f0a8d-221">O downgrade da largura de banda exige o desprovisionamento do circuito do ExpressRoute e um reprovisionamento de um novo circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-221">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="f0a8d-222">Redimensionar um circuito</span><span class="sxs-lookup"><span data-stu-id="f0a8d-222">Resize a circuit</span></span>

<span data-ttu-id="f0a8d-223">Após decidir de qual tamanho precisa, você pode usar o seguinte comando para redimensionar o circuito:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-223">After you decide what size you need, you can use the following command to resize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="f0a8d-224">O circuito será sido dimensionado no lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-224">Your circuit will have been sized up on the Microsoft side.</span></span> <span data-ttu-id="f0a8d-225">Entre em contato com seu provedor de conectividade para que ele atualize as configurações a fim de corresponder a essa alteração.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-225">You must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="f0a8d-226">Observe que passaremos a lhe cobrar pela opção de largura de banda atualizada a partir desse momento.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-226">Note that we will start billing you for the updated bandwidth option from this point on.</span></span>

<span data-ttu-id="f0a8d-227">Se você vir o seguinte erro quando aumentar a largura de banda do circuito, isso significa que não há largura de banda suficiente restante na porta física onde o circuito existente foi criado.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-227">If you see the following error when increasing the circuit bandwidth, it means there is no sufficient bandwidth left on the physical port where your existing circuit is created.</span></span> <span data-ttu-id="f0a8d-228">Será necessário excluir este circuito e criar um novo circuito do tamanho que você precisa.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-228">You have to delete this circuit and create a new circuit of the size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available to perform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="f0a8d-229">Desprovisionamento e exclusão de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="f0a8d-230">Considerações</span><span class="sxs-lookup"><span data-stu-id="f0a8d-230">Considerations</span></span>

* <span data-ttu-id="f0a8d-231">Você deve desvincular todas as redes virtuais do circuto do ExpressRoute para que a operação seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-231">You must unlink all virtual networks from the ExpressRoute circuit for this operation to succeed.</span></span> <span data-ttu-id="f0a8d-232">Se essa operação falhar, verifique se você tem redes virtuais vinculadas ao circuito.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-232">Check to see if you have any virtual networks that are linked to the circuit if this operation fails.</span></span>
* <span data-ttu-id="f0a8d-233">Se o estado de provisionamento do provedor de serviço de circuito de ExpressRoute for **Provisionando** ou **Provisionado**, você deverá trabalhar com seu provedor de serviços para que ele desprovisione o circuito.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-233">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="f0a8d-234">Continuaremos a reservar recursos e a cobrar de você até que o provedor de serviços complete o desprovisionamento do circuito e nos notifique.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-234">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="f0a8d-235">Se o provedor de serviços tiver desprovisionado o circuito (o estado de provisionamento do provedor de serviços estiver definido como **Não provisionado**), exclua o circuito.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-235">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="f0a8d-236">Isso interromperá a cobrança do circuito.</span><span class="sxs-lookup"><span data-stu-id="f0a8d-236">This will stop billing for the circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="f0a8d-237">Excluir um circuito</span><span class="sxs-lookup"><span data-stu-id="f0a8d-237">Delete a circuit</span></span>

<span data-ttu-id="f0a8d-238">Você pode excluir o circuito do ExpressRoute executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-238">You can delete your ExpressRoute circuit by running the following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="f0a8d-239">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f0a8d-239">Next steps</span></span>
<span data-ttu-id="f0a8d-240">Depois de criar seu circuito, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f0a8d-240">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="f0a8d-241">Criar e modificar o roteamento do circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="f0a8d-242">Vincular a rede virtual ao circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f0a8d-242">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

