---
title: "Visão geral do balanceador de carga interno | Microsoft Docs"
description: "Visão geral do balanceador de carga interno e seus recursos. Como um balanceador de carga funciona no Azure e possíveis cenários para configurar pontos de extremidade internos"
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
ms.openlocfilehash: d324aaf8ec2c8766d5cf11452158d14c19cba4d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="5dfe3-103">Visão geral do balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="5dfe3-103">Internal load balancer overview</span></span>

<span data-ttu-id="5dfe3-104">Ao contrário do balanceador de carga voltado para a Internet, o ILB (Balanceador de Carga Interno) direciona o tráfego somente para os recursos dentro do serviço de nuvem ou usa VPN para acessar a infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-104">Unlike the Internet facing load balancer, the internal load balancer (ILB) directs traffic only to resources inside the cloud service or using VPN to access the Azure infrastructure.</span></span> <span data-ttu-id="5dfe3-105">A infraestrutura restringe o acesso aos VIPs (endereços IP virtuais) de balanceamento de carga de um Serviço de nuvem ou uma Rede virtual, de modo que nunca será exposta diretamente a um ponto de extremidade da Internet.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-105">The infrastructure restricts access to the load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed to an Internet endpoint.</span></span> <span data-ttu-id="5dfe3-106">Isso permite que aplicativos LOB (linha de negócios) internos sejam executados no Azure e acessados na nuvem ou nos recursos locais.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-106">This enables internal line of business (LOB) applications to run in Azure and be accessed from within the cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="5dfe3-107">Por que talvez seja necessário balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="5dfe3-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="5dfe3-108">O ILB (Balanceamento de Carga Interno) do Azure fornece balanceamento de carga entre máquinas virtuais que residem em um serviço de nuvem ou em uma rede virtual com escopo regional.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="5dfe3-109">Para obter informações sobre o uso e a configuração de redes virtuais com escopo regional, consulte [Redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) no blog do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-109">For information about the use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in the Azure blog.</span></span> <span data-ttu-id="5dfe3-110">Redes virtuais existentes configuradas para um grupo de afinidade não podem usar o ILB.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="5dfe3-111">O ILB habilita os seguintes tipos de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="5dfe3-111">ILB enables the following types of load balancing:</span></span>

* <span data-ttu-id="5dfe3-112">Dentro de um serviço de nuvem, de máquinas virtuais a um conjunto de máquinas virtuais que residem no mesmo serviço de nuvem (veja a Figura 1).</span><span class="sxs-lookup"><span data-stu-id="5dfe3-112">Within a cloud service, from virtual machines to a set of virtual machines that reside within the same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="5dfe3-113">Em uma rede virtual, de máquinas virtuais na rede virtual a um conjunto de máquinas virtuais que residem no mesmo serviço de nuvem da rede virtual (veja a Figura 2).</span><span class="sxs-lookup"><span data-stu-id="5dfe3-113">Within a virtual network, from virtual machines in the virtual network to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 2).</span></span>
* <span data-ttu-id="5dfe3-114">Para uma rede virtual entre instalações, de computadores locais a um conjunto de máquinas virtuais que residem no mesmo serviço de nuvem da rede virtual (veja a Figura 3).</span><span class="sxs-lookup"><span data-stu-id="5dfe3-114">For a cross-premises virtual network, from on-premises computers to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 3).</span></span>
* <span data-ttu-id="5dfe3-115">Aplicativos para a Internet de diversas camadas, cujas camadas de back-end não são para a Internet, mas exigem balanceamento de carga para tráfego da camada para a Internet.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-115">Internet-facing, multi-tier applications in which the back-end tiers are not Internet-facing but require load balancing for traffic from the Internet-facing tier.</span></span>
* <span data-ttu-id="5dfe3-116">Balanceamento de carga para aplicativos LOB (linha de negócios) hospedados no Azure sem exigir hardware ou software do balanceador de carga adicional.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="5dfe3-117">Incluindo servidores locais, no conjunto de computadores, cujo tráfego é de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-117">Including on-premises servers in the set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="5dfe3-118">Aplicativos para a Internet de diversas camadas</span><span class="sxs-lookup"><span data-stu-id="5dfe3-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="5dfe3-119">A camada Web tem pontos de extremidade para a Internet para clientes de Internet e faz parte de um conjunto de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-119">The web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="5dfe3-120">O balanceador de carga distribui o tráfego de entrada de clientes Web para a porta TCP 443 (HTTPS) até os servidores Web.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-120">The load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) to the web servers.</span></span>

<span data-ttu-id="5dfe3-121">Os servidores de banco de dados estão protegidos por um ponto de extremidade ILB que os servidores Web usam para armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-121">The database servers are behind an ILB endpoint which the web servers use for storage.</span></span> <span data-ttu-id="5dfe3-122">Esse ponto de extremidade de balanceamento de carga do serviço de banco de dados, cujo tráfego é de carga balanceada entre servidores de banco de dados do conjunto ILB.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-122">This database service load balanced endpoint, which traffic is load balanced across the database servers in the ILB set.</span></span>

<span data-ttu-id="5dfe3-123">A imagem a seguir mostra o aplicativo para a Internet de várias camadas no mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-123">The following image shows the Internet facing multi-tier application within the same cloud service.</span></span>

![Serviço de nuvem único de balanceamento de carga interno](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="5dfe3-125">Figura 1 – Aplicativo para a Internet de várias camadas</span><span class="sxs-lookup"><span data-stu-id="5dfe3-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="5dfe3-126">Outro uso possível para um aplicativo com diversas camadas é quando o ILB é implantado em um serviço de nuvem diferente daquele que consome o serviço para o ILB.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-126">Another possible use for a multi-tier application is when the ILB deployed to a different cloud service than the one consuming the service for the ILB.</span></span>

<span data-ttu-id="5dfe3-127">Serviços de nuvem que usam a mesma rede virtual terão acesso ao ponto de extremidade ILB.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-127">Cloud services using the same virtual network will have access to the ILB endpoint.</span></span> <span data-ttu-id="5dfe3-128">A imagem mostra que os servidores Web front-end estão em um serviço de nuvem diferente do back-end do banco de dados e estão usando o ponto de extremidade ILB dentro da mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-128">The following image shows front-end web servers are in a different cloud service from the database back-end and using the ILB endpoint within the same virtual network.</span></span>

![Balanceamento de carga interno entre serviços de nuvem](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="5dfe3-130">Figura 2 – Servidores front-end em um serviço de nuvem diferente</span><span class="sxs-lookup"><span data-stu-id="5dfe3-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="5dfe3-131">Aplicativos de linha de negócios intranet</span><span class="sxs-lookup"><span data-stu-id="5dfe3-131">Intranet line of business applications</span></span>

<span data-ttu-id="5dfe3-132">Tráfego de clientes em redes locais tem balanceamento de carga em um conjunto de servidores LOB que usam conexão VPN com a rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-132">Traffic from clients on the on-premises network get load-balanced across the set of LOB servers using VPN connection to Azure network.</span></span>

<span data-ttu-id="5dfe3-133">O computador cliente terá acesso a um endereço IP do serviço de VPN do Azure que usa a VPN de ponto a site.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-133">The client machine will have access to an IP address from Azure VPN service using point to site VPN.</span></span> <span data-ttu-id="5dfe3-134">Permite o uso do aplicativo LOB hospedado atrás do ponto de extremidade ILB.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-134">It allows the use the LOB application hosted behind the ILB endpoint.</span></span>

![Balanceamento de carga interno usando VPN ponto a site](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="5dfe3-136">Figura 3 – Aplicativos LOB hospedados atrás do ponto de extremidade LB</span><span class="sxs-lookup"><span data-stu-id="5dfe3-136">Figure 3 - LOB applications hosted behind the LB endpoint</span></span>

<span data-ttu-id="5dfe3-137">Outro cenário para LOB é ter uma VPN site a site para a rede virtual na qual o ponto de extremidade ILB foi configurado.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-137">Another scenario for the LOB is to have a site to site VPN to the virtual network where the ILB endpoint is configured.</span></span> <span data-ttu-id="5dfe3-138">Isso permite que o tráfego de rede local seja roteado para o ponto de extremidade ILB.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-138">This allows on-premises network traffic to be routed to the ILB endpoint.</span></span>

![Balanceamento de carga interno usando VPN site a site](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="5dfe3-140">Figura 4 – Tráfego de rede local roteado para o ponto de extremidade ILB</span><span class="sxs-lookup"><span data-stu-id="5dfe3-140">Figure 4 - On-premises network traffic routed to the ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="5dfe3-141">Limitações</span><span class="sxs-lookup"><span data-stu-id="5dfe3-141">Limitations</span></span>

<span data-ttu-id="5dfe3-142">As configurações do Balanceador de Carga Interno não dão suporte a SNAT.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="5dfe3-143">No contexto deste documento, SNAT refere-se à conversão de endereços de rede de origem simulada de porta.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-143">In the context of this document, SNAT refers to port masquerading source  network address translation.</span></span>  <span data-ttu-id="5dfe3-144">Isso se aplica a cenários em que a VM em um pool de balanceador de carga precisa alcançar o endereço IP de front-end do respectivo balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-144">This applies to scenarios where a VM in a load balancer pool needs to reach the respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="5dfe3-145">Não há suporte para cenário no balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="5dfe3-146">Falhas de conexão ocorrerão quando a carga do fluxo for balanceada para a VM que originou o fluxo.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-146">Connection failures will occur when the flow is load balanced to the VM which originated the flow.</span></span> <span data-ttu-id="5dfe3-147">Você deve usar um balanceador de carga de estilo de proxy para esses cenários.</span><span class="sxs-lookup"><span data-stu-id="5dfe3-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dfe3-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5dfe3-148">Next Steps</span></span>

[<span data-ttu-id="5dfe3-149">Suporte do Azure Resource Manager para o Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5dfe3-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="5dfe3-150">Introdução à configuração de um balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="5dfe3-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="5dfe3-151">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="5dfe3-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="5dfe3-152">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="5dfe3-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="5dfe3-153">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="5dfe3-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
