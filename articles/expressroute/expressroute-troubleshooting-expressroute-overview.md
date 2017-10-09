---
title: "Verificando a conectividade: Guia de Solução de Problemas do Azure ExpressRoute | Microsoft Docs"
description: "Esta página fornece instruções sobre solução de problemas e validando a conectividade de tooend final de um circuito de rota expressa."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="4e128-103">Verificando a conectividade do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4e128-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="4e128-104">Rota expressa, que se estende uma rede local para o hello nuvem da Microsoft em uma conexão privada que é facilitada por um provedor de conectividade, envolve Olá três zonas de rede distintas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-104">ExpressRoute, which extends an on-premises network into hello Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves hello following three distinct network zones:</span></span>

-   <span data-ttu-id="4e128-105">Rede do Cliente</span><span class="sxs-lookup"><span data-stu-id="4e128-105">Customer Network</span></span>
-   <span data-ttu-id="4e128-106">Rede do Provedor</span><span class="sxs-lookup"><span data-stu-id="4e128-106">Provider Network</span></span>
-   <span data-ttu-id="4e128-107">Microsoft Datacenter</span><span class="sxs-lookup"><span data-stu-id="4e128-107">Microsoft Datacenter</span></span>

<span data-ttu-id="4e128-108">Olá finalidade deste documento é toohelp usuário tooidentify onde (ou até mesmo se) existe um problema de conectividade e em qual zona, assim, tooseek Ajuda do problema de saudação tooresolve equipe apropriada.</span><span class="sxs-lookup"><span data-stu-id="4e128-108">hello purpose of this document is toohelp user tooidentify where (or even if) a connectivity issue exists and within which zone, thereby tooseek help from appropriate team tooresolve hello issue.</span></span> <span data-ttu-id="4e128-109">Se o suporte da Microsoft é um problema de tooresolve necessária, abra um tíquete de suporte com [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="4e128-109">If Microsoft support is needed tooresolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e128-110">Este documento é pretendido toohelp diagnosticar e corrigir problemas simples.</span><span class="sxs-lookup"><span data-stu-id="4e128-110">This document is intended toohelp diagnosing and fixing simple issues.</span></span> <span data-ttu-id="4e128-111">Não é pretendido toobe uma substituição para o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e128-111">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="4e128-112">Abrir um tíquete de suporte com [Microsoft Support] [ Support] se você estiver toosolve não é possível problema de saudação usando Olá diretrizes fornecidas.</span><span class="sxs-lookup"><span data-stu-id="4e128-112">Open a support ticket with [Microsoft Support][Support] if you are unable toosolve hello problem using hello guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="4e128-113">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4e128-113">Overview</span></span>
<span data-ttu-id="4e128-114">Olá diagrama a seguir mostra a conectividade lógica saudação de uma rede de tooMicrosoft de rede do cliente usando o ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4e128-114">hello following diagram shows hello logical connectivity of a customer network tooMicrosoft network using ExpressRoute.</span></span>
<span data-ttu-id="4e128-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="4e128-115">[![1]][1]</span></span>

<span data-ttu-id="4e128-116">Olá precede o diagrama, Olá números indicam pontos principais de rede.</span><span class="sxs-lookup"><span data-stu-id="4e128-116">In hello preceding diagram, hello numbers indicate key network points.</span></span> <span data-ttu-id="4e128-117">pontos de saudação à rede são referenciados geralmente este artigo por seu número associado.</span><span class="sxs-lookup"><span data-stu-id="4e128-117">hello network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="4e128-118">Dependendo da conectividade de rota expressa Olá modelo (colocalização do Exchange de nuvem, ponto a ponto Ethernet Conexão ou para qualquer (IPVPN)) Olá rede pontos 3 e 4 podem ser comutadores (dispositivos de camada 2).</span><span class="sxs-lookup"><span data-stu-id="4e128-118">Depending on hello ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) hello network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="4e128-119">pontos de chave de rede Olá ilustrados são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4e128-119">hello key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="4e128-120">Dispositivo de computação de cliente (por exemplo, um servidor ou PC)</span><span class="sxs-lookup"><span data-stu-id="4e128-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="4e128-121">CEs: roteadores de borda do cliente</span><span class="sxs-lookup"><span data-stu-id="4e128-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="4e128-122">PEs (voltados para CE): roteadores/comutadores de borda do provedor que estão voltados para os roteadores de borda do cliente.</span><span class="sxs-lookup"><span data-stu-id="4e128-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="4e128-123">Chamado tooas PE CEs neste documento.</span><span class="sxs-lookup"><span data-stu-id="4e128-123">Referred tooas PE-CEs in this document.</span></span>
4.  <span data-ttu-id="4e128-124">PEs (voltados para MSEE): roteadores/comutadores de borda do provedor que estão voltados para MSEEs.</span><span class="sxs-lookup"><span data-stu-id="4e128-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="4e128-125">Chamado tooas PE MSEEs neste documento.</span><span class="sxs-lookup"><span data-stu-id="4e128-125">Referred tooas PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="4e128-126">MSEEs: roteadores ExpressRoute do MSEE (Microsoft Enterprise Edge)</span><span class="sxs-lookup"><span data-stu-id="4e128-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="4e128-127">Gateway de Rede Virtual (VNet)</span><span class="sxs-lookup"><span data-stu-id="4e128-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="4e128-128">Computação dispositivo Olá VNet do Azure</span><span class="sxs-lookup"><span data-stu-id="4e128-128">Compute device on hello Azure VNet</span></span>

<span data-ttu-id="4e128-129">Se os modelos de conectividade de posicionamento do Exchange de nuvem ou ponto a ponto Ethernet Conexão hello são usados, o roteador de borda do cliente hello (2) seria estabelecer BGP de emparelhamento com MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="4e128-129">If hello Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, hello customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="4e128-130">Os pontos de rede 3 e 4 ainda existiriam, mas seriam um tanto transparentes como dispositivos de rede de Camada 2.</span><span class="sxs-lookup"><span data-stu-id="4e128-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="4e128-131">Se o modelo de conectividade Olá para qualquer (IPVPN) for usado, Olá PEs (voltado para a MSEE) (4) seria estabelecer BGP de emparelhamento com MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="4e128-131">If hello Any-to-any (IPVPN) connectivity model is used, hello PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="4e128-132">Rotas depois propagará toohello back rede de cliente por meio da rede do provedor de serviços IPVPN de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e128-132">Routes would then propagate back toohello customer network via hello IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="4e128-133">Para alta disponibilidade do ExpressRoute, a Microsoft exige um par redundante de sessões BGP entre MSEEs (5) e PE-MSEEs (4).</span><span class="sxs-lookup"><span data-stu-id="4e128-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="4e128-134">Recomenda-se também mobilizar um par redundante de caminhos de rede entre a rede do cliente e PE-CEs.</span><span class="sxs-lookup"><span data-stu-id="4e128-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="4e128-135">No entanto, no modelo de conexão para qualquer (IPVPN), um único dispositivo CE (2) pode ser conectado tooone ou mais PEs (3).</span><span class="sxs-lookup"><span data-stu-id="4e128-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected tooone or more PEs (3).</span></span>
>
>

<span data-ttu-id="4e128-136">toovalidate um circuito de rota expressa, Olá etapas a seguir são abordados (com o ponto de rede Olá indicado pelo número de saudação associado):</span><span class="sxs-lookup"><span data-stu-id="4e128-136">toovalidate an ExpressRoute circuit, hello following steps are covered (with hello network point indicated by hello associated number):</span></span>
1. [<span data-ttu-id="4e128-137">Validar o estado e o provisionamento do circuito (5)</span><span class="sxs-lookup"><span data-stu-id="4e128-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="4e128-138">Validar que pelo menos um emparelhamento do ExpressRoute está configurado (5)</span><span class="sxs-lookup"><span data-stu-id="4e128-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="4e128-139">Validar ARP entre o provedor de serviços Microsoft e hello (link entre 4 e 5)</span><span class="sxs-lookup"><span data-stu-id="4e128-139">Validate ARP between Microsoft and hello service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="4e128-140">Validar o BGP e rotas Olá MSEE (BGP entre too5 4 e 5 too6 se estiver conectada a uma rede virtual)</span><span class="sxs-lookup"><span data-stu-id="4e128-140">Validate BGP and routes on hello MSEE (BGP between 4 too5, and 5 too6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="4e128-141">Saudação de verificação de estatísticas de tráfego (tráfego que passa pelo 5)</span><span class="sxs-lookup"><span data-stu-id="4e128-141">Check hello Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="4e128-142">Mais validações e verificações serão adicionadas em Olá futuras, visite mensal!</span><span class="sxs-lookup"><span data-stu-id="4e128-142">More validations and checks will be added in hello future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="4e128-143">Validar o estado e o provisionamento do circuito</span><span class="sxs-lookup"><span data-stu-id="4e128-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="4e128-144">Independentemente do modelo de conectividade de saudação, um circuito ExpressRoute tem toobe criado e, portanto, um serviço de chave gerada para o provisionamento do circuito.</span><span class="sxs-lookup"><span data-stu-id="4e128-144">Regardless of hello connectivity model, an ExpressRoute circuit has toobe created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="4e128-145">O provisionamento de um circuito do ExpressRoute estabelece uma conexão de Camada 2 redundante entre PE-MSEEs (4) e MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="4e128-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="4e128-146">Para obter mais informações sobre como toocreate, modificar, configurar e verificar um circuito ExpressRoute, consulte o artigo Olá [criar e modificar um circuito ExpressRoute][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="4e128-146">For more information on how toocreate, modify, provision, and verify an ExpressRoute circuit, see hello article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="4e128-147">Uma chave de serviço identifica exclusivamente um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4e128-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="4e128-148">Essa chave é necessária para a maioria dos comandos do powershell Olá mencionados neste documento.</span><span class="sxs-lookup"><span data-stu-id="4e128-148">This key is required for most of hello powershell commands mentioned in this document.</span></span> <span data-ttu-id="4e128-149">Além disso, se você precisar de assistência da Microsoft ou de um parceiro de rota expressa tootroubleshoot um problema de rota expressa, fornecer serviço Olá tooreadily chave identificar circuito hello.</span><span class="sxs-lookup"><span data-stu-id="4e128-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner tootroubleshoot an ExpressRoute issue, provide hello service key tooreadily identify hello circuit.</span></span>
>
>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="4e128-150">Verificação via Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4e128-150">Verification via hello Azure portal</span></span>
<span data-ttu-id="4e128-151">No portal do Azure de Olá, status de saudação de um circuito de rota expressa pode ser verificado selecionando ![2][2] em Olá menu da barra de lado esquerdo e, em seguida, selecionando Olá circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="4e128-151">In hello Azure portal, hello status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="4e128-152">Selecionando uma rota expressa circuito listado em "Todos os recursos" abre a folha de circuito de rota expressa de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e128-152">Selecting an ExpressRoute circuit listed under "All resources" opens hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="4e128-153">Em Olá ![3][3] seção da folha de Olá Olá essentials é listado como mostrado na seguinte captura de tela de saudação do ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="4e128-153">In hello ![3][3] section of hello blade, hello ExpressRoute essentials are listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="4e128-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="4e128-154">![4][4]</span></span>    

<span data-ttu-id="4e128-155">Em Olá Essentials de rota expressa, *circuito status* indica o status de saudação do circuito Olá Olá lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e128-155">In hello ExpressRoute Essentials, *Circuit status* indicates hello status of hello circuit on hello Microsoft side.</span></span> <span data-ttu-id="4e128-156">*Status do provedor* indica se o circuito de saudação foi *provisionado ou não provisionado* no lado do provedor de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e128-156">*Provider status* indicates if hello circuit has been *Provisioned/Not provisioned* on hello service-provider side.</span></span> 

<span data-ttu-id="4e128-157">Para um toobe de circuito de rota expressa operacional, Olá *circuito status* devem ser *habilitado* e hello *status do provedor* devem ser *provisionado*.</span><span class="sxs-lookup"><span data-stu-id="4e128-157">For an ExpressRoute circuit toobe operational, hello *Circuit status* must be *Enabled* and hello *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="4e128-158">Se hello *circuito status* não é habilitado, entre em contato com [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="4e128-158">If hello *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="4e128-159">Se hello *status do provedor* não é provisionado, entre em contato com seu provedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="4e128-159">If hello *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="4e128-160">Verificação por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e128-160">Verification via PowerShell</span></span>
<span data-ttu-id="4e128-161">toolist todos Olá circuitos de rota expressa em um grupo de recursos, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-161">toolist all hello ExpressRoute circuits in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="4e128-162">Você pode obter o nome do seu grupo de recursos por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e128-162">You can get your resource group name through hello Azure portal.</span></span> <span data-ttu-id="4e128-163">Consulte a subseção anterior Olá deste documento e anote que esse nome de grupo de recursos de saudação está listado na captura de tela de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="4e128-163">See hello previous subsection of this document and note that hello resource group name is listed in hello example screen shot.</span></span>
>
>

<span data-ttu-id="4e128-164">tooselect um circuito de rota expressa específico em um grupo de recursos, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-164">tooselect a particular ExpressRoute circuit in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="4e128-165">Uma resposta de exemplo é:</span><span class="sxs-lookup"><span data-stu-id="4e128-165">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="4e128-166">tooconfirm se um circuito ExpressRoute está funcionando, preste atenção especial toohello campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-166">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="4e128-167">Se hello *CircuitProvisioningState* não é habilitado, entre em contato com [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="4e128-167">If hello *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="4e128-168">Se hello *ServiceProviderProvisioningState* não é provisionado, entre em contato com seu provedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="4e128-168">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="4e128-169">Verificação por meio do PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="4e128-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="4e128-170">toolist todos Olá circuitos de rota expressa em uma assinatura, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-170">toolist all hello ExpressRoute circuits under a subscription, use hello following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="4e128-171">tooselect um circuito de rota expressa específico, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-171">tooselect a particular ExpressRoute circuit, use hello following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="4e128-172">Uma resposta de exemplo é:</span><span class="sxs-lookup"><span data-stu-id="4e128-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="4e128-173">tooconfirm se um circuito ExpressRoute está funcionando, preste atenção especial toohello campos a seguir: ServiceProviderProvisioningState: Status provisionado: habilitada</span><span class="sxs-lookup"><span data-stu-id="4e128-173">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="4e128-174">Se hello *Status* não é habilitado, entre em contato com [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="4e128-174">If hello *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="4e128-175">Se hello *ServiceProviderProvisioningState* não é provisionado, entre em contato com seu provedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="4e128-175">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="4e128-176">Validar Configuração de Emparelhamento</span><span class="sxs-lookup"><span data-stu-id="4e128-176">Validate Peering Configuration</span></span>
<span data-ttu-id="4e128-177">Provedor de serviços de Olá Olá concluído provisionamento do circuito de rota expressa hello, após uma configuração de roteamento pode ser criada pela Olá circuito de rota expressa entre MSEE-PRs (4) e MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="4e128-177">After hello service provider has completed hello provisioning hello ExpressRoute circuit, a routing configuration can be created over hello ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="4e128-178">Cada circuito de rota expressa pode ter um, dois ou três contextos de roteamentos habilitados: emparelhamento particular do Azure (tráfego tooprivate redes virtuais no Azure), emparelhamento público do Azure (tráfego toopublic endereços IP no Azure) e (tráfego tooOffice 365 emparelhamento da Microsoft e Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="4e128-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic tooprivate virtual networks in Azure), Azure public peering (traffic toopublic IP addresses in Azure), and Microsoft peering (traffic tooOffice 365 and Dynamics 365).</span></span> <span data-ttu-id="4e128-179">Para obter mais informações sobre como toocreate e modificar a configuração de roteamento, consulte o artigo Olá [criar e modificar o roteamento para um circuito ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="4e128-179">For more information on how toocreate and modify routing configuration, see hello article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="4e128-180">Verificação via Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4e128-180">Verification via hello Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="4e128-181">Há um bug conhecido no hello portal do Azure no qual os emparelhamentos de rota expressa são *não* mostrado no portal de saudação se configurado pelo provedor de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e128-181">There is a known bug in hello Azure portal wherein ExpressRoute peerings are *NOT* shown in hello portal if configured by hello service provider.</span></span> <span data-ttu-id="4e128-182">Adicionando emparelhamentos de rota expressa por meio do portal de saudação ou o PowerShell *substitui as configurações do provedor de serviço Olá*.</span><span class="sxs-lookup"><span data-stu-id="4e128-182">Adding ExpressRoute peerings via hello portal or PowerShell *overwrites hello service provider settings*.</span></span> <span data-ttu-id="4e128-183">Essa ação quebras Olá roteamento no circuito de rota expressa hello e requer suporte Olá Olá configurações de serviço provedor toorestore hello e restabelecer o roteamento normal.</span><span class="sxs-lookup"><span data-stu-id="4e128-183">This action breaks hello routing on hello ExpressRoute circuit and requires hello support of hello service provider toorestore hello settings and reestablish normal routing.</span></span> <span data-ttu-id="4e128-184">Modificar emparelhamentos de rota expressa Olá apenas se você tiver certeza de que o provedor de serviços hello está fornecendo serviços de camada 2 apenas!</span><span class="sxs-lookup"><span data-stu-id="4e128-184">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="4e128-185">Se fornecida pelo Olá emparelhamentos de provedor e hello serviço estão em branco no portal de saudação camada 3, o PowerShell pode ser usado toosee Olá serviço provedor configurado configurações.</span><span class="sxs-lookup"><span data-stu-id="4e128-185">If layer 3 is provided by hello service provider and hello peerings are blank in hello portal, PowerShell can be used toosee hello service provider configured settings.</span></span>
>
>

<span data-ttu-id="4e128-186">No hello portal do Azure, o status de um circuito de rota expressa pode ser verificado selecionando ![2][2] em Olá menu da barra de lado esquerdo e, em seguida, selecionando Olá circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="4e128-186">In hello Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="4e128-187">Selecionando uma rota expressa circuito listado em "Todos os recursos" abrir folha de circuito de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="4e128-187">Selecting an ExpressRoute circuit listed under "All resources" would open hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="4e128-188">Em Olá ![3][3] seção da folha de Olá Olá essentials é listado como mostrado na seguinte captura de tela de saudação do ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="4e128-188">In hello ![3][3] section of hello blade, hello ExpressRoute essentials would be listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="4e128-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="4e128-189">![5][5]</span></span>

<span data-ttu-id="4e128-190">Em Olá anterior de exemplo, como observado Azure contexto de roteamento de emparelhamento privado é habilitado, enquanto pública do Azure e contextos de roteamento emparelhamento Microsoft não estão habilitados.</span><span class="sxs-lookup"><span data-stu-id="4e128-190">In hello preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="4e128-191">Um contexto de emparelhamento habilitado com êxito também teria sub-redes de primárias e secundárias ponto a ponto (necessária para BGP) Olá listados.</span><span class="sxs-lookup"><span data-stu-id="4e128-191">A successfully enabled peering context would also have hello primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="4e128-192">subredes Olá /30 são usados para endereço IP de interface de saudação do hello MSEEs e MSEEs PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-192">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="4e128-193">Se um emparelhamento não estiver habilitado, verifique se sub-redes primários e secundários Olá atribuídas correspondem configuração Olá MSEEs PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-193">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on PE-MSEEs.</span></span> <span data-ttu-id="4e128-194">Se não, toochange Olá configuração em roteadores MSEE, consulte muito[criar e modificar o roteamento para um circuito de rota expressa][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="4e128-194">If not, toochange hello configuration on MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="4e128-195">Verificação por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e128-195">Verification via PowerShell</span></span>
<span data-ttu-id="4e128-196">tooget hello Azure privado emparelhamento detalhes de configuração, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-196">tooget hello Azure private peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="4e128-197">Uma resposta de exemplo para um emparelhamento privado configurado com êxito é:</span><span class="sxs-lookup"><span data-stu-id="4e128-197">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="4e128-198">Um contexto de emparelhamento habilitado com êxito teria prefixos de endereço primário e secundário Olá listados.</span><span class="sxs-lookup"><span data-stu-id="4e128-198">A successfully enabled peering context would have hello primary and secondary address prefixes listed.</span></span> <span data-ttu-id="4e128-199">subredes Olá /30 são usados para endereço IP de interface de saudação do hello MSEEs e MSEEs PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-199">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="4e128-200">tooget hello Azure público emparelhamento detalhes de configuração, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-200">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="4e128-201">tooget Olá emparelhamento configuração detalhes da Microsoft, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-201">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="4e128-202">Se um emparelhamento não for configurado, haverá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="4e128-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="4e128-203">Uma resposta de exemplo, quando Olá mencionado emparelhamento (público do Azure emparelhamento neste exemplo) não está configurada no circuito de saudação:</span><span class="sxs-lookup"><span data-stu-id="4e128-203">A sample response, when hello stated peering (Azure Public peering in this example) is not configured within hello circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="4e128-204">Se um emparelhamento não estiver habilitado, verifique se Olá primários e secundários sub-redes atribuídas correspondência Olá configuração Olá vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-204">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="4e128-205">Também verifique se hello corrigir *VlanId*, *AzureASN*, e *PeerASN* são usados em MSEEs e se esses valores mapeia toohello usados em Olá vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-205">Also check if hello correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="4e128-206">Se o hash MD5 for escolhido, chave compartilhada Olá deve ser idênticos em par MSEE e MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-206">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="4e128-207">configuração de saudação toochange em roteadores MSEE hello, consulte muito [criar e modificar o roteamento para um circuito ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="4e128-207">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="4e128-208">Verificação por meio do PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="4e128-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="4e128-209">tooget hello Azure privado emparelhamento detalhes de configuração, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-209">tooget hello Azure private peering configuration details, use hello following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="4e128-210">Uma resposta de exemplo para um emparelhamento privado configurado com êxito é:</span><span class="sxs-lookup"><span data-stu-id="4e128-210">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="4e128-211">Habilitado com êxito, de um contexto emparelhamento teria sub-redes de par primário e secundário Olá listados.</span><span class="sxs-lookup"><span data-stu-id="4e128-211">A successfully, enabled peering context would have hello primary and secondary peer subnets listed.</span></span> <span data-ttu-id="4e128-212">subredes Olá /30 são usados para endereço IP de interface de saudação do hello MSEEs e MSEEs PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-212">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="4e128-213">tooget hello Azure público emparelhamento detalhes de configuração, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-213">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="4e128-214">tooget Olá emparelhamento configuração detalhes da Microsoft, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-214">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="4e128-215">Se emparelhamentos de camada 3 foram definidos pelo provedor de serviços de Olá, Olá emparelhamentos de rota expressa por meio do portal de saudação ou o PowerShell de configuração substitui as configurações do provedor de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e128-215">If layer 3 peerings were set by hello service provider, setting hello ExpressRoute peerings via hello portal or PowerShell overwrites hello service provider settings.</span></span> <span data-ttu-id="4e128-216">Redefinir as configurações de emparelhamento Olá provedor no lado do requer suporte Olá Olá do provedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="4e128-216">Resetting hello provider side peering settings requires hello support of hello service provider.</span></span> <span data-ttu-id="4e128-217">Modificar emparelhamentos de rota expressa Olá apenas se você tiver certeza de que o provedor de serviços hello está fornecendo serviços de camada 2 apenas!</span><span class="sxs-lookup"><span data-stu-id="4e128-217">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="4e128-218">Se um emparelhamento não estiver habilitado, verifique se Olá par primário e secundário sub-redes atribuídas correspondência Olá configuração Olá vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-218">If a peering is not enabled, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="4e128-219">Também verifique se hello corrigir *VlanId*, *AzureAsn*, e *PeerAsn* são usados em MSEEs e se esses valores mapeia toohello usados em Olá vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-219">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="4e128-220">configuração de saudação toochange em roteadores MSEE hello, consulte muito [criar e modificar o roteamento para um circuito ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="4e128-220">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a><span data-ttu-id="4e128-221">Validar ARP entre o provedor de serviços Microsoft e hello</span><span class="sxs-lookup"><span data-stu-id="4e128-221">Validate ARP between Microsoft and hello service provider</span></span>
<span data-ttu-id="4e128-222">Esta seção usa comandos do PowerShell (Clássico).</span><span class="sxs-lookup"><span data-stu-id="4e128-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="4e128-223">Se você tiver usando comandos do PowerShell do Azure Resource Manager, verifique se você tem acesso de administrador/coadministrador toohello assinatura por meio de [portal clássico do Azure][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="4e128-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="4e128-224">Para solucionar o problema usando o Gerenciador de recursos do Azure comandos, consulte toohello [tabelas obtendo ARP no modelo de implantação do Gerenciador de recursos de saudação] [ ARP] documento.</span><span class="sxs-lookup"><span data-stu-id="4e128-224">For troubleshooting using Azure Resource Manager commands please refer toohello [Getting ARP tables in hello Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="4e128-225">tooget ARP, Olá portal do Azure e comandos do PowerShell do Azure Resource Manager pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="4e128-225">tooget ARP, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="4e128-226">Se forem encontrados erros com comandos do PowerShell do Azure Resource Manager hello, clássicos comandos do PowerShell devem funcionar como PowerShell clássico comandos também funcionam com circuitos ExpressRoute do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e128-226">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="4e128-227">tooget Olá tabela ARP do roteador MSEE primária Olá para emparelhamento privado do hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-227">tooget hello ARP table from hello primary MSEE router for hello private peering, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="4e128-228">Um exemplo de resposta para comando hello, no cenário de êxito hello:</span><span class="sxs-lookup"><span data-stu-id="4e128-228">An example response for hello command, in hello successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="4e128-229">Da mesma forma, você pode verificar Olá tabela ARP do hello MSEE em Olá *primário*/*secundário* caminho, para *privada* /  *Público*/*Microsoft* emparelhamentos.</span><span class="sxs-lookup"><span data-stu-id="4e128-229">Similarly, you can check hello ARP table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="4e128-230">Olá exemplo a seguir mostra Olá resposta do comando de saudação para um emparelhamento não existe.</span><span class="sxs-lookup"><span data-stu-id="4e128-230">hello following example shows hello response of hello command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="4e128-231">Se não tiver Olá tabela ARP desses endereços IP das interfaces de saudação mapeado tooMAC endereços, Olá revisar informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-231">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
>1. <span data-ttu-id="4e128-232">Se Olá primeiro endereço IP de sub-rede Olá /30 atribuído para Olá link entre Olá PR MSEE e MSEE é usado na interface de saudação do MSEE pr</span><span class="sxs-lookup"><span data-stu-id="4e128-232">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="4e128-233">Azure sempre usa o endereço IP da segunda Olá para MSEEs.</span><span class="sxs-lookup"><span data-stu-id="4e128-233">Azure always uses hello second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="4e128-234">Confirme se Prezado cliente (C-Tag) e marcas de VLAN de serviço (S-Tag) correspondem em par PR MSEE e MSEE.</span><span class="sxs-lookup"><span data-stu-id="4e128-234">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a><span data-ttu-id="4e128-235">Validar o BGP e rotas Olá MSEE</span><span class="sxs-lookup"><span data-stu-id="4e128-235">Validate BGP and routes on hello MSEE</span></span>
<span data-ttu-id="4e128-236">Esta seção usa comandos do PowerShell (Clássico).</span><span class="sxs-lookup"><span data-stu-id="4e128-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="4e128-237">Se você tiver usando comandos do PowerShell do Azure Resource Manager, verifique se você tem acesso de administrador/coadministrador toohello assinatura via [portal clássico do Azure][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="4e128-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="4e128-238">tooget informações sobre o BGP, ambos os Olá portal do Azure e comandos do PowerShell do Azure Resource Manager podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="4e128-238">tooget BGP information, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="4e128-239">Se forem encontrados erros com comandos do PowerShell do Azure Resource Manager hello, clássicos comandos do PowerShell devem funcionar como PowerShell clássico comandos também funcionam com circuitos ExpressRoute do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e128-239">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="4e128-240">tooget Olá a tabela de roteamento (vizinho BGP) resumida de um contexto de roteamento específico, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-240">tooget hello routing table (BGP neighbor) summary for a particular routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="4e128-241">Uma resposta de exemplo é:</span><span class="sxs-lookup"><span data-stu-id="4e128-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="4e128-242">Conforme mostrado na saudação anterior de exemplo, o comando de Olá é útil toodetermine de quanto tempo o contexto de roteamento Olá foi estabelecido.</span><span class="sxs-lookup"><span data-stu-id="4e128-242">As shown in hello preceding example, hello command is useful toodetermine for how long hello routing context has been established.</span></span> <span data-ttu-id="4e128-243">Ele também indica o número de prefixos de rota anunciadas pelo roteador de emparelhamento hello.</span><span class="sxs-lookup"><span data-stu-id="4e128-243">It also indicates number of route prefixes advertised by hello peering router.</span></span>

>[!NOTE]
><span data-ttu-id="4e128-244">Se Olá estado é ativo ou inativo, verifique se Olá par primário e secundário sub-redes atribuídas correspondência Olá configuração Olá vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-244">If hello state is in Active or Idle, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="4e128-245">Também verifique se hello corrigir *VlanId*, *AzureAsn*, e *PeerAsn* são usados em MSEEs e se esses valores mapeia toohello usados em Olá vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-245">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="4e128-246">Se o hash MD5 for escolhido, chave compartilhada Olá deve ser idênticos em par MSEE e MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="4e128-246">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="4e128-247">configuração de saudação toochange em roteadores MSEE hello, consulte muito[criar e modificar o roteamento para um circuito ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="4e128-247">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="4e128-248">Se determinados destinos não estão acessíveis por um emparelhamento particular, consulte a tabela de rota de saudação de saudação MSEEs pertencentes toohello contexto específico de emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="4e128-248">If certain destinations are not reachable over a particular peering, check hello route table of hello MSEEs belonging toohello particular peering context.</span></span> <span data-ttu-id="4e128-249">Se um prefixo correspondente (pode ser NATed IP) está presente na tabela de roteamento hello, verifique se há firewalls/NSG/ACLs no caminho de saudação e permitir o tráfego de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e128-249">If a matching prefix (could be NATed IP) is present in hello routing table, then check if there are firewalls/NSG/ACLs on hello path and if they permit hello traffic.</span></span>
>
>

<span data-ttu-id="4e128-250">tooget Olá tabela completa de roteamento de MSEE em Olá *primário* caminho Olá específico *privada* contexto de roteamento, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-250">tooget hello full routing table from MSEE on hello *Primary* path for hello particular *Private* routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="4e128-251">Um resultado de exemplo com êxito para o comando Olá é:</span><span class="sxs-lookup"><span data-stu-id="4e128-251">An example successful outcome for hello command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="4e128-252">Da mesma forma, você pode verificar a tabela de roteamento de saudação do hello MSEE em hello *primário*/*secundário* caminho, para *privada* / *Pública*/*Microsoft* um contexto de emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="4e128-252">Similarly, you can check hello routing table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="4e128-253">Olá exemplo a seguir mostra Olá resposta do comando de saudação para um emparelhamento não existe:</span><span class="sxs-lookup"><span data-stu-id="4e128-253">hello following example shows hello response of hello command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a><span data-ttu-id="4e128-254">Saudação de verificação de estatísticas de tráfego</span><span class="sxs-lookup"><span data-stu-id="4e128-254">Check hello Traffic Statistics</span></span>
<span data-ttu-id="4e128-255">Olá tooget combinadas estatísticas de tráfego de caminho primário e secundário – bytes e sair – de um contexto de emparelhamento, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-255">tooget hello combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="4e128-256">Um exemplo de saída do comando de saudação é:</span><span class="sxs-lookup"><span data-stu-id="4e128-256">A sample output of hello command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="4e128-257">É um exemplo de saída do comando de saudação para um emparelhamento inexistente:</span><span class="sxs-lookup"><span data-stu-id="4e128-257">A sample output of hello command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="4e128-258">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4e128-258">Next Steps</span></span>
<span data-ttu-id="4e128-259">Para obter mais informações ou Ajuda, consulte Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e128-259">For more information or help, check out hello following links:</span></span>

- <span data-ttu-id="4e128-260">[Suporte da Microsoft][Support]</span><span class="sxs-lookup"><span data-stu-id="4e128-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="4e128-261">[Criar e modificar um circuito do ExpressRoute][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="4e128-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="4e128-262">[Criar e modificar o roteamento de um circuito do ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="4e128-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Conectividade lógica do ExpressRoute"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Ícone Todos os Recursos"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Ícone Visão Geral"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Captura de tela de exemplo do ExpressRoute Essentials"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Captura de tela de exemplo do ExpressRoute Essentials"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






