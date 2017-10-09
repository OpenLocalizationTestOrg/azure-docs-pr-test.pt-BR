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
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="201cd-104">Criar e modificar um circuito da ExpressRoute usando o PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="201cd-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="201cd-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="201cd-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="201cd-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="201cd-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="201cd-107">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="201cd-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="201cd-108">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="201cd-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="201cd-109">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="201cd-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="201cd-110">Este artigo orienta Olá etapas toocreate um circuito de rota expressa do Azure usando o modelo de implantação clássico hello e cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="201cd-110">This article walks you through hello steps toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello classic deployment model.</span></span> <span data-ttu-id="201cd-111">Este artigo também mostra como toocheck Olá status, atualizar, ou excluir e cancelar o provisionamento de um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="201cd-111">This article also shows you how toocheck hello status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="201cd-112">**Sobre modelos de implantação do Azure**</span><span class="sxs-lookup"><span data-stu-id="201cd-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="201cd-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="201cd-113">Before you begin</span></span>
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a><span data-ttu-id="201cd-114">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="201cd-114">Step 1.</span></span> <span data-ttu-id="201cd-115">Analisar os pré-requisitos de saudação e artigos de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="201cd-115">Review hello prerequisites and workflow articles</span></span>
<span data-ttu-id="201cd-116">Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="201cd-116">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="201cd-117">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="201cd-117">Step 2.</span></span> <span data-ttu-id="201cd-118">Instalar versões mais recentes de saudação de módulos do PowerShell de gerenciamento de serviço do Azure (SM) Olá</span><span class="sxs-lookup"><span data-stu-id="201cd-118">Install hello latest versions of hello Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="201cd-119">Siga as instruções de saudação em [Introdução aos cmdlets do PowerShell do Azure](/powershell/azure/overview) para obter orientação passo a passo sobre como tooconfigure os módulos do computador toouse hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="201cd-119">Follow hello instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="201cd-120">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="201cd-120">Step 3.</span></span> <span data-ttu-id="201cd-121">Faça logon no tooyour conta do Azure e selecione uma assinatura</span><span class="sxs-lookup"><span data-stu-id="201cd-121">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="201cd-122">Abra o console do PowerShell com direitos elevados e conecte-se a conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="201cd-122">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="201cd-123">Use Olá toohelp de exemplo que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="201cd-123">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="201cd-124">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="201cd-124">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="201cd-125">Se você tiver mais de uma assinatura, selecione a assinatura de saudação que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="201cd-125">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="201cd-126">Em seguida, use Olá tooadd cmdlet a seguir tooPowerShell sua assinatura do Azure para o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="201cd-126">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="201cd-127">Criar e provisionar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="201cd-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a><span data-ttu-id="201cd-128">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="201cd-128">Step 1.</span></span> <span data-ttu-id="201cd-129">Importar os módulos do PowerShell de saudação do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="201cd-129">Import hello PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="201cd-130">Se você ainda não tiver feito isso, você deve importar os módulos do Azure e rota expressa Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="201cd-130">If you have not already done so, you must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="201cd-131">Importar os módulos de saudação do hello local que estavam instalados tooon seu computador local.</span><span class="sxs-lookup"><span data-stu-id="201cd-131">You import hello modules from hello location that they were installed tooon your local computer.</span></span> <span data-ttu-id="201cd-132">Dependendo do método hello usado tooinstall módulos de hello, local Olá pode ser diferente de saudação mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="201cd-132">Depending on hello method you used tooinstall hello modules, hello location may be different than hello following example shows.</span></span> <span data-ttu-id="201cd-133">Modificar o exemplo hello se necessário.</span><span class="sxs-lookup"><span data-stu-id="201cd-133">Modify hello example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="201cd-134">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="201cd-134">Step 2.</span></span> <span data-ttu-id="201cd-135">Obter lista de saudação de provedores suportados, locais e larguras de banda</span><span class="sxs-lookup"><span data-stu-id="201cd-135">Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="201cd-136">Antes de criar um circuito de rota expressa, você precisa de lista de saudação de provedores com suporte de conectividade, locais e as opções de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="201cd-136">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="201cd-137">Olá cmdlet do PowerShell `Get-AzureDedicatedCircuitServiceProvider` retorna essas informações, que você usará em etapas posteriores:</span><span class="sxs-lookup"><span data-stu-id="201cd-137">hello PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="201cd-138">Verifique toosee se seu provedor de conectividade está listado.</span><span class="sxs-lookup"><span data-stu-id="201cd-138">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="201cd-139">Anote Olá informações a seguir porque você precisará dele mais tarde quando você criar um circuito:</span><span class="sxs-lookup"><span data-stu-id="201cd-139">Make a note of hello following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="201cd-140">Nome</span><span class="sxs-lookup"><span data-stu-id="201cd-140">Name</span></span>
* <span data-ttu-id="201cd-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="201cd-141">PeeringLocations</span></span>
* <span data-ttu-id="201cd-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="201cd-142">BandwidthsOffered</span></span>

<span data-ttu-id="201cd-143">Agora você está pronto toocreate um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="201cd-143">You're now ready toocreate an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="201cd-144">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="201cd-144">Step 3.</span></span> <span data-ttu-id="201cd-145">Criar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="201cd-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="201cd-146">saudação de exemplo a seguir mostra como toocreate uma rota expressa de 200 Mbps de circuito por meio de Equinix no Vale do Silício.</span><span class="sxs-lookup"><span data-stu-id="201cd-146">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="201cd-147">Se estiver usando um provedor diferente e configurações diferentes, substitua essas informações ao fazer a solicitação.</span><span class="sxs-lookup"><span data-stu-id="201cd-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="201cd-148">O circuito de rota expressa será cobrado do momento Olá que uma chave de serviço é emitida.</span><span class="sxs-lookup"><span data-stu-id="201cd-148">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="201cd-149">Certifique-se de que você executar esta operação quando o provedor de conectividade de saudação circuito de saudação tooprovision pronto.</span><span class="sxs-lookup"><span data-stu-id="201cd-149">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="201cd-150">a seguir Olá é um exemplo de solicitação de uma nova chave de serviço:</span><span class="sxs-lookup"><span data-stu-id="201cd-150">hello following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="201cd-151">Ou, se você quiser toocreate um circuito de ExpressRoute com o complemento do premium Olá, use Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="201cd-151">Or, if you want toocreate an ExpressRoute circuit with hello premium add-on, use hello following example.</span></span> <span data-ttu-id="201cd-152">Consulte toohello [perguntas frequentes sobre o rota expressa](expressroute-faqs.md) para obter mais detalhes sobre o complemento do premium Olá.</span><span class="sxs-lookup"><span data-stu-id="201cd-152">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more details about hello premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="201cd-153">resposta de saudação conterá a chave de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="201cd-153">hello response will contain hello service key.</span></span> <span data-ttu-id="201cd-154">Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="201cd-154">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a><span data-ttu-id="201cd-155">Etapa 4.</span><span class="sxs-lookup"><span data-stu-id="201cd-155">Step 4.</span></span> <span data-ttu-id="201cd-156">Lista todos os circuitos de rota expressa Olá</span><span class="sxs-lookup"><span data-stu-id="201cd-156">List all hello ExpressRoute circuits</span></span>
<span data-ttu-id="201cd-157">Você pode executar Olá `Get-AzureDedicatedCircuit` comando Olá de tooget uma lista de todos os circuitos do ExpressRoute que você criou:</span><span class="sxs-lookup"><span data-stu-id="201cd-157">You can run hello `Get-AzureDedicatedCircuit` command tooget a list of all hello ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="201cd-158">resposta de saudação será algo parecido toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="201cd-158">hello response will be something similar toohello following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="201cd-159">Você pode recuperar essas informações a qualquer momento usando Olá `Get-AzureDedicatedCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="201cd-159">You can retrieve this information at any time by using hello `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="201cd-160">Fazer com que o hello chamada sem nenhum parâmetro lista todos os circuitos hello.</span><span class="sxs-lookup"><span data-stu-id="201cd-160">Making hello call without any parameters lists all hello circuits.</span></span> <span data-ttu-id="201cd-161">Sua chave de serviço será listada no hello *ServiceKey* campo.</span><span class="sxs-lookup"><span data-stu-id="201cd-161">Your service key will be listed in hello *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="201cd-162">Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="201cd-162">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="201cd-163">Etapa 5.</span><span class="sxs-lookup"><span data-stu-id="201cd-163">Step 5.</span></span> <span data-ttu-id="201cd-164">Enviar Olá tooyour chave conectividade provedor para provisionamento</span><span class="sxs-lookup"><span data-stu-id="201cd-164">Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="201cd-165">*ServiceProviderProvisioningState* fornece informações sobre o estado atual de saudação do provisionamento no lado do provedor de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="201cd-165">*ServiceProviderProvisioningState* provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="201cd-166">*Status* informa o estado de saudação em Olá lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="201cd-166">*Status* provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="201cd-167">Para obter mais informações sobre estados de provisionamento do circuito, consulte Olá [fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states) artigo.</span><span class="sxs-lookup"><span data-stu-id="201cd-167">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="201cd-168">Quando você cria um novo circuito de rota expressa, circuito Olá estará em Olá estado a seguir:</span><span class="sxs-lookup"><span data-stu-id="201cd-168">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="201cd-169">circuito Olá irá toohello estado a seguir quando o provedor de conectividade Olá está no processo de saudação de habilitá-la para você:</span><span class="sxs-lookup"><span data-stu-id="201cd-169">hello circuit will go toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="201cd-170">Um circuito de rota expressa deve ser Olá seguindo o estado para você toobe capaz de toouse-lo:</span><span class="sxs-lookup"><span data-stu-id="201cd-170">An ExpressRoute circuit must be in hello following state for you toobe able toouse it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="201cd-171">Etapa 6.</span><span class="sxs-lookup"><span data-stu-id="201cd-171">Step 6.</span></span> <span data-ttu-id="201cd-172">Verifique periodicamente o status de saudação e o estado de saudação da chave de circuito de saudação</span><span class="sxs-lookup"><span data-stu-id="201cd-172">Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="201cd-173">Isso permite que você saiba quando seu provedor habilitou seu circuito.</span><span class="sxs-lookup"><span data-stu-id="201cd-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="201cd-174">Depois que o circuito Olá tiver sido configurado, *ServiceProviderProvisioningState* será exibido como *provisionado* conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="201cd-174">After hello circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in hello following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="201cd-175">Etapa 7.</span><span class="sxs-lookup"><span data-stu-id="201cd-175">Step 7.</span></span> <span data-ttu-id="201cd-176">Criar sua configuração de roteamento</span><span class="sxs-lookup"><span data-stu-id="201cd-176">Create your routing configuration</span></span>
<span data-ttu-id="201cd-177">Consulte toohello [configuração de roteamento de circuito de rota expressa (criar e modificar os emparelhamentos de circuito)](expressroute-howto-routing-classic.md) artigo para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="201cd-177">Refer toohello [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="201cd-178">Essas instruções se aplicam somente a toocircuits que são criados com provedores de serviços que oferecem serviços da camada 2 de conectividade.</span><span class="sxs-lookup"><span data-stu-id="201cd-178">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="201cd-179">Se você estiver usando um provedor de serviços que oferece serviços gerenciados de camada 3 (normalmente um IP VPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="201cd-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="201cd-180">Etapa 8.</span><span class="sxs-lookup"><span data-stu-id="201cd-180">Step 8.</span></span> <span data-ttu-id="201cd-181">Vincular um circuito de rota expressa do tooan de rede virtual</span><span class="sxs-lookup"><span data-stu-id="201cd-181">Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="201cd-182">Em seguida, vincule um circuito de rota expressa do tooyour de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="201cd-182">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="201cd-183">Consulte também[circuitos de rota expressa vincular redes toovirtual](expressroute-howto-linkvnet-classic.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="201cd-183">Refer too[Linking ExpressRoute circuits toovirtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="201cd-184">Se você precisar toocreate uma rede virtual usando o modelo de implantação clássico Olá para o ExpressRoute, consulte [criar uma rede virtual para o ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="201cd-184">If you need toocreate a virtual network using hello classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="201cd-185">Obter status de saudação de um circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="201cd-185">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="201cd-186">Você pode recuperar essas informações a qualquer momento usando Olá `Get-AzureCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="201cd-186">You can retrieve this information at any time by using hello `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="201cd-187">Fazer com que o hello chamada sem nenhum parâmetro lista todos os circuitos hello.</span><span class="sxs-lookup"><span data-stu-id="201cd-187">Making hello call without any parameters lists all hello circuits.</span></span>

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

<span data-ttu-id="201cd-188">Você pode obter informações sobre um circuito de rota expressa específica, passando a chave de serviço hello como uma chamada de toohello do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="201cd-188">You can get information on a specific ExpressRoute circuit by passing hello service key as a parameter toohello call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="201cd-189">Você pode obter descrições detalhadas de todos os parâmetros de saudação executando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="201cd-189">You can get detailed descriptions of all hello parameters by running hello following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="201cd-190">Modificando um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="201cd-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="201cd-191">Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="201cd-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="201cd-192">Você pode fazer Olá sem tempo de inatividade a seguir:</span><span class="sxs-lookup"><span data-stu-id="201cd-192">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="201cd-193">Como habilitar ou desabilitar o complemento premium do ExpressRoute para seu circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="201cd-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="201cd-194">Aumento de largura de banda de saudação do circuito ExpressRoute fornecido há capacidade disponível na porta hello.</span><span class="sxs-lookup"><span data-stu-id="201cd-194">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="201cd-195">Observe que a largura de banda de saudação de um circuito de downgrade não é suportado.</span><span class="sxs-lookup"><span data-stu-id="201cd-195">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="201cd-196">Alterar o plano de dados limitados tooUnlimited dados de medição de saudação.</span><span class="sxs-lookup"><span data-stu-id="201cd-196">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="201cd-197">Observe que esse plano de medição Olá alteração de dados ilimitada tooMetered que dados não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="201cd-197">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="201cd-198">Você pode habilitar e desabilitar *Permitir Operações Clássicas*.</span><span class="sxs-lookup"><span data-stu-id="201cd-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="201cd-199">Consulte toohello [perguntas frequentes sobre o rota expressa](expressroute-faqs.md) para obter mais informações sobre limitações e limites.</span><span class="sxs-lookup"><span data-stu-id="201cd-199">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="201cd-200">complemento do premium tooenable Olá rota expressa</span><span class="sxs-lookup"><span data-stu-id="201cd-200">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="201cd-201">Você pode habilitar o complemento do premium Olá rota expressa para o circuito existente usando Olá cmdlet do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="201cd-201">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="201cd-202">O circuito terá habilitados dos recursos de complemento de premium Olá rota expressa.</span><span class="sxs-lookup"><span data-stu-id="201cd-202">Your circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="201cd-203">Observe que começamos cobrança você para o recurso de complemento premium Olá assim que o comando Olá foi executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="201cd-203">Note that we will start billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="201cd-204">complemento do premium toodisable Olá rota expressa</span><span class="sxs-lookup"><span data-stu-id="201cd-204">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="201cd-205">Essa operação pode falhar se você estiver usando recursos que são maiores do que o que é permitido para o circuito de saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="201cd-205">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="201cd-206">Considerações</span><span class="sxs-lookup"><span data-stu-id="201cd-206">Considerations</span></span>

* <span data-ttu-id="201cd-207">Certifique-se de que o número de saudação de redes virtuais vinculadas toohello circuito é inferior a 10 antes de você fazer o downgrade de premium toostandard.</span><span class="sxs-lookup"><span data-stu-id="201cd-207">You must ensure that hello number of virtual networks linked toohello circuit is less than 10 before you downgrade from premium toostandard.</span></span> <span data-ttu-id="201cd-208">Se você não fizer isso, sua solicitação de atualização falhará e você será taxas de premium Olá cobradas.</span><span class="sxs-lookup"><span data-stu-id="201cd-208">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="201cd-209">Você precisa desvincular todas as redes virtuais em outras regiões geopolíticas.</span><span class="sxs-lookup"><span data-stu-id="201cd-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="201cd-210">Se você não fizer isso, sua solicitação de atualização falhará e você será taxas de premium Olá cobradas.</span><span class="sxs-lookup"><span data-stu-id="201cd-210">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="201cd-211">Sua tabela de roteamento deve ter menos de 4.000 rotas para o emparelhamento privado.</span><span class="sxs-lookup"><span data-stu-id="201cd-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="201cd-212">Se o tamanho da tabela de rota for maior que 4.000 rotas, sessão BGP de saudação será removido e não ser reabilitada até que o número de saudação de prefixos anunciados fica abaixo de 4.000.</span><span class="sxs-lookup"><span data-stu-id="201cd-212">If your route table size is greater than 4,000 routes, hello BGP session will drop and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-hello-premium-add-on"></a><span data-ttu-id="201cd-213">Desabilitar o complemento do premium Olá</span><span class="sxs-lookup"><span data-stu-id="201cd-213">Disable hello premium add-on</span></span>
<span data-ttu-id="201cd-214">Você pode desabilitar o complemento do premium Olá rota expressa para o circuito existente usando Olá cmdlet do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="201cd-214">You can disable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="201cd-215">largura de banda de circuito ExpressRoute tooupdate Olá</span><span class="sxs-lookup"><span data-stu-id="201cd-215">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="201cd-216">Verificar Olá [perguntas frequentes sobre o rota expressa](expressroute-faqs.md) para opções de largura de banda para o seu provedor de suporte.</span><span class="sxs-lookup"><span data-stu-id="201cd-216">Check hello [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="201cd-217">Você pode escolher qualquer tamanho que seja maior que o tamanho de saudação do circuito existente, desde que a porta física hello (no qual o circuito é criado) permite que.</span><span class="sxs-lookup"><span data-stu-id="201cd-217">You can pick any size that is greater than hello size of your existing circuit as long as hello physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="201cd-218">Você pode ter o circuito de rota expressa Olá toorecreate se não houver capacidade insuficiente na porta existente Olá.</span><span class="sxs-lookup"><span data-stu-id="201cd-218">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="201cd-219">Não é possível atualizar o circuito de saudação se não houver nenhuma capacidade adicional disponível nesse local.</span><span class="sxs-lookup"><span data-stu-id="201cd-219">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="201cd-220">Você não pode reduzir a largura de banda de saudação de um circuito de rota expressa sem interrupções.</span><span class="sxs-lookup"><span data-stu-id="201cd-220">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="201cd-221">Downgrade da largura de banda requer que o circuito de rota expressa Olá toodeprovision e, em seguida, Reprovisionar um novo circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="201cd-221">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="201cd-222">Redimensionar um circuito</span><span class="sxs-lookup"><span data-stu-id="201cd-222">Resize a circuit</span></span>

<span data-ttu-id="201cd-223">Depois de decidir qual o tamanho que você precisa, você pode usar Olá tooresize de comando a seguir o circuito:</span><span class="sxs-lookup"><span data-stu-id="201cd-223">After you decide what size you need, you can use hello following command tooresize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="201cd-224">O circuito será ter foi dimensionado para cima no lado do Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="201cd-224">Your circuit will have been sized up on hello Microsoft side.</span></span> <span data-ttu-id="201cd-225">Você deve entrar em contato com suas configurações de tooupdate do provedor de conectividade em seu toomatch lado essa alteração.</span><span class="sxs-lookup"><span data-stu-id="201cd-225">You must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="201cd-226">Observe que começamos cobrança você de saudação atualizado opção de largura de banda desse ponto em.</span><span class="sxs-lookup"><span data-stu-id="201cd-226">Note that we will start billing you for hello updated bandwidth option from this point on.</span></span>

<span data-ttu-id="201cd-227">Se você vir Olá erro a seguir ao aumentar a largura de banda de circuito hello, ele significa que não há nenhuma largura de banda suficiente fica na porta física hello, onde o circuito existente é criado.</span><span class="sxs-lookup"><span data-stu-id="201cd-227">If you see hello following error when increasing hello circuit bandwidth, it means there is no sufficient bandwidth left on hello physical port where your existing circuit is created.</span></span> <span data-ttu-id="201cd-228">Você tem toodelete este circuito e cria um novo circuito de tamanho de saudação que é necessário.</span><span class="sxs-lookup"><span data-stu-id="201cd-228">You have toodelete this circuit and create a new circuit of hello size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="201cd-229">Desprovisionamento e exclusão de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="201cd-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="201cd-230">Considerações</span><span class="sxs-lookup"><span data-stu-id="201cd-230">Considerations</span></span>

* <span data-ttu-id="201cd-231">Você deve desvincular todas as redes virtuais da saudação circuito de rota expressa para toosucceed esta operação.</span><span class="sxs-lookup"><span data-stu-id="201cd-231">You must unlink all virtual networks from hello ExpressRoute circuit for this operation toosucceed.</span></span> <span data-ttu-id="201cd-232">Verificar toosee se você tiver quaisquer redes virtuais que estão vinculadas toohello circuito se essa operação falhar.</span><span class="sxs-lookup"><span data-stu-id="201cd-232">Check toosee if you have any virtual networks that are linked toohello circuit if this operation fails.</span></span>
* <span data-ttu-id="201cd-233">Se o provedor de serviços de circuito ExpressRoute Olá estado de provisionamento é **provisionamento** ou **provisionado** você deve trabalhar com o circuito de saudação do serviço provedor toodeprovision em seu lado.</span><span class="sxs-lookup"><span data-stu-id="201cd-233">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="201cd-234">Vamos continuar tooreserve recursos e cobrar você até que o provedor de serviços Olá Complete desprovisionamento circuito de saudação e nos notifica.</span><span class="sxs-lookup"><span data-stu-id="201cd-234">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="201cd-235">Se o provedor de serviços de saudação tem desprovisionada circuito hello (provedor de serviços de saudação estado de provisionamento está definido muito**não provisionado**), em seguida, você pode excluir o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="201cd-235">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="201cd-236">Isso interromperá a cobrança para o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="201cd-236">This will stop billing for hello circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="201cd-237">Excluir um circuito</span><span class="sxs-lookup"><span data-stu-id="201cd-237">Delete a circuit</span></span>

<span data-ttu-id="201cd-238">Você pode excluir o circuito de rota expressa executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="201cd-238">You can delete your ExpressRoute circuit by running hello following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="201cd-239">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="201cd-239">Next steps</span></span>
<span data-ttu-id="201cd-240">Depois de criar o circuito, certifique-se de que Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="201cd-240">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="201cd-241">Criar e modificar o roteamento do circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="201cd-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="201cd-242">Vincular sua rede virtual de tooyour circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="201cd-242">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

