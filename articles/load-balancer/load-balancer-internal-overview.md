---
title: "Visão geral de Balanceador de carga de aaaInternal | Microsoft Docs"
description: "Visão geral do balanceador de carga interno e seus recursos. Como um balanceador de carga funciona para pontos de extremidade interno do Azure e possíveis cenários tooconfigure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="917af-103">Visão geral do balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="917af-103">Internal load balancer overview</span></span>

<span data-ttu-id="917af-104">Ao contrário de saudação Internet oposta balanceador de carga balanceador de carga interno (ILB) do hello direciona tooresources somente do tráfego dentro de serviço de nuvem hello ou usando VPN tooaccess Olá infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="917af-104">Unlike hello Internet facing load balancer, hello internal load balancer (ILB) directs traffic only tooresources inside hello cloud service or using VPN tooaccess hello Azure infrastructure.</span></span> <span data-ttu-id="917af-105">infraestrutura de saudação restringe acesso toohello com balanceamento de carga endereços IP virtual (VIPs) de um serviço de nuvem ou uma rede Virtual para que eles nunca será o ponto de extremidade do tooan diretamente expostos à Internet.</span><span class="sxs-lookup"><span data-stu-id="917af-105">hello infrastructure restricts access toohello load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed tooan Internet endpoint.</span></span> <span data-ttu-id="917af-106">Isso permite interno de linha de negócios (LOB) toorun de aplicativos no Azure e ser acessado de dentro da nuvem de saudação ou dos recursos locais.</span><span class="sxs-lookup"><span data-stu-id="917af-106">This enables internal line of business (LOB) applications toorun in Azure and be accessed from within hello cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="917af-107">Por que talvez seja necessário balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="917af-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="917af-108">O ILB (Balanceamento de Carga Interno) do Azure fornece balanceamento de carga entre máquinas virtuais que residem em um serviço de nuvem ou em uma rede virtual com escopo regional.</span><span class="sxs-lookup"><span data-stu-id="917af-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="917af-109">Para obter informações sobre o uso de saudação e a configuração de redes virtuais com um escopo regional, consulte [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) em Olá blog do Azure.</span><span class="sxs-lookup"><span data-stu-id="917af-109">For information about hello use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure blog.</span></span> <span data-ttu-id="917af-110">Redes virtuais existentes configuradas para um grupo de afinidade não podem usar o ILB.</span><span class="sxs-lookup"><span data-stu-id="917af-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="917af-111">O ILB permite Olá seguintes tipos de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="917af-111">ILB enables hello following types of load balancing:</span></span>

* <span data-ttu-id="917af-112">Dentro de um serviço de nuvem de máquinas virtuais tooa conjunto de máquinas virtuais que residem dentro de saudação mesmo serviço de nuvem (consulte a Figura 1).</span><span class="sxs-lookup"><span data-stu-id="917af-112">Within a cloud service, from virtual machines tooa set of virtual machines that reside within hello same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="917af-113">Em uma rede virtual, de máquinas virtuais no conjunto de tooa Olá rede virtual de máquinas virtuais que residem dentro de saudação mesmo serviço de nuvem do hello virtual de rede (consulte a Figura 2).</span><span class="sxs-lookup"><span data-stu-id="917af-113">Within a virtual network, from virtual machines in hello virtual network tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 2).</span></span>
* <span data-ttu-id="917af-114">Para uma rede virtual entre locais, de conjunto de tooa de computadores no local de máquinas virtuais que residem dentro de saudação mesmo serviço de nuvem do hello virtual de rede (consulte a Figura 3).</span><span class="sxs-lookup"><span data-stu-id="917af-114">For a cross-premises virtual network, from on-premises computers tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 3).</span></span>
* <span data-ttu-id="917af-115">Aplicativos voltados para Internet, multicamados no qual as camadas de back-end de saudação não estão conectados à Internet mas exigem balanceamento de carga para tráfego de camada do hello voltado para a Internet.</span><span class="sxs-lookup"><span data-stu-id="917af-115">Internet-facing, multi-tier applications in which hello back-end tiers are not Internet-facing but require load balancing for traffic from hello Internet-facing tier.</span></span>
* <span data-ttu-id="917af-116">Balanceamento de carga para aplicativos LOB (linha de negócios) hospedados no Azure sem exigir hardware ou software do balanceador de carga adicional.</span><span class="sxs-lookup"><span data-stu-id="917af-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="917af-117">Incluindo servidores locais no conjunto de saudação de computadores cujo tráfego tem a carga balanceada.</span><span class="sxs-lookup"><span data-stu-id="917af-117">Including on-premises servers in hello set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="917af-118">Aplicativos para a Internet de diversas camadas</span><span class="sxs-lookup"><span data-stu-id="917af-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="917af-119">camada da web de saudação tem pontos de extremidade com acesso à Internet para clientes de Internet e é parte de um conjunto com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="917af-119">hello web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="917af-120">o balanceador de carga Olá distribui o tráfego dos clientes da web para TCP porta 443 (HTTPS) toohello servidores web.</span><span class="sxs-lookup"><span data-stu-id="917af-120">hello load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) toohello web servers.</span></span>

<span data-ttu-id="917af-121">servidores de banco de dados de saudação estejam por trás de um ponto de extremidade ILB que usam servidores de web Olá para armazenamento.</span><span class="sxs-lookup"><span data-stu-id="917af-121">hello database servers are behind an ILB endpoint which hello web servers use for storage.</span></span> <span data-ttu-id="917af-122">Essa carga de serviço do banco de dados com balanceamento de ponto de extremidade, o tráfego tem a carga balanceada entre servidores de banco de dados Olá Olá ILB conjunto.</span><span class="sxs-lookup"><span data-stu-id="917af-122">This database service load balanced endpoint, which traffic is load balanced across hello database servers in hello ILB set.</span></span>

<span data-ttu-id="917af-123">Olá imagem mostra a seguir Olá aplicativo multicamadas da Internet em Olá mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="917af-123">hello following image shows hello Internet facing multi-tier application within hello same cloud service.</span></span>

![Serviço de nuvem único de balanceamento de carga interno](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="917af-125">Figura 1 – Aplicativo para a Internet de várias camadas</span><span class="sxs-lookup"><span data-stu-id="917af-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="917af-126">Outro uso possíveis para um aplicativo de várias camado é quando Olá ILB implantado tooa serviço de nuvem diferente de Olá um serviço Olá consumidor para Olá ILB.</span><span class="sxs-lookup"><span data-stu-id="917af-126">Another possible use for a multi-tier application is when hello ILB deployed tooa different cloud service than hello one consuming hello service for hello ILB.</span></span>

<span data-ttu-id="917af-127">Nuvem serviços usando Olá mesma rede virtual será necessário acessam o ponto de extremidade do toohello ILB.</span><span class="sxs-lookup"><span data-stu-id="917af-127">Cloud services using hello same virtual network will have access toohello ILB endpoint.</span></span> <span data-ttu-id="917af-128">Olá seguindo a imagem mostra servidores web front-end estão em um serviço de nuvem diferente de saudação de banco de dados back-end e usando Olá pontos de extremidade ILB Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="917af-128">hello following image shows front-end web servers are in a different cloud service from hello database back-end and using hello ILB endpoint within hello same virtual network.</span></span>

![Balanceamento de carga interno entre serviços de nuvem](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="917af-130">Figura 2 – Servidores front-end em um serviço de nuvem diferente</span><span class="sxs-lookup"><span data-stu-id="917af-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="917af-131">Aplicativos de linha de negócios intranet</span><span class="sxs-lookup"><span data-stu-id="917af-131">Intranet line of business applications</span></span>

<span data-ttu-id="917af-132">Tráfego de clientes na rede local de saudação obter com balanceamento de carga em conjunto de saudação de servidores LOB usando a rede de tooAzure de conexão VPN.</span><span class="sxs-lookup"><span data-stu-id="917af-132">Traffic from clients on hello on-premises network get load-balanced across hello set of LOB servers using VPN connection tooAzure network.</span></span>

<span data-ttu-id="917af-133">máquina de cliente Olá terá acesso tooan endereço IP do serviço de VPN do Azure usando VPN de ponto toosite.</span><span class="sxs-lookup"><span data-stu-id="917af-133">hello client machine will have access tooan IP address from Azure VPN service using point toosite VPN.</span></span> <span data-ttu-id="917af-134">Ele permite Olá use Olá aplicativo LOB hospedado por trás do ponto de extremidade do hello ILB.</span><span class="sxs-lookup"><span data-stu-id="917af-134">It allows hello use hello LOB application hosted behind hello ILB endpoint.</span></span>

![Usando VPN de ponto toosite de balanceamento de carga interno](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="917af-136">Figura 3: aplicativos LOB hospedados por trás de ponto de extremidade Olá LB</span><span class="sxs-lookup"><span data-stu-id="917af-136">Figure 3 - LOB applications hosted behind hello LB endpoint</span></span>

<span data-ttu-id="917af-137">Outro cenário para Olá LOB é toohave uma toosite VPN toohello rede virtual site onde o ponto de extremidade do hello ILB está configurado.</span><span class="sxs-lookup"><span data-stu-id="917af-137">Another scenario for hello LOB is toohave a site toosite VPN toohello virtual network where hello ILB endpoint is configured.</span></span> <span data-ttu-id="917af-138">Isso permite que o local rede tráfego roteado de toobe toohello ILB ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="917af-138">This allows on-premises network traffic toobe routed toohello ILB endpoint.</span></span>

![Usando o site toosite VPN de balanceamento de carga interno](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="917af-140">Figura 4 - o tráfego de rede local roteada toohello ILB ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="917af-140">Figure 4 - On-premises network traffic routed toohello ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="917af-141">Limitações</span><span class="sxs-lookup"><span data-stu-id="917af-141">Limitations</span></span>

<span data-ttu-id="917af-142">As configurações do Balanceador de Carga Interno não dão suporte a SNAT.</span><span class="sxs-lookup"><span data-stu-id="917af-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="917af-143">Olá o contexto deste documento, SNAT refere-se tooport com origem NAT.</span><span class="sxs-lookup"><span data-stu-id="917af-143">In hello context of this document, SNAT refers tooport masquerading source  network address translation.</span></span>  <span data-ttu-id="917af-144">Isso se aplica a tooscenarios onde uma VM em um pool de Balanceador de carga precisa de endereço IP de front-end do tooreach Olá respectivos interno balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="917af-144">This applies tooscenarios where a VM in a load balancer pool needs tooreach hello respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="917af-145">Não há suporte para cenário no balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="917af-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="917af-146">Falhas de Conexão ocorrerá quando o fluxo de saudação é com balanceamento de carga toohello VM originado fluxo Olá.</span><span class="sxs-lookup"><span data-stu-id="917af-146">Connection failures will occur when hello flow is load balanced toohello VM which originated hello flow.</span></span> <span data-ttu-id="917af-147">Você deve usar um balanceador de carga de estilo de proxy para esses cenários.</span><span class="sxs-lookup"><span data-stu-id="917af-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="917af-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="917af-148">Next Steps</span></span>

[<span data-ttu-id="917af-149">Suporte do Azure Resource Manager para o Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="917af-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="917af-150">Introdução à configuração de um balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="917af-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="917af-151">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="917af-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="917af-152">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="917af-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="917af-153">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="917af-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
