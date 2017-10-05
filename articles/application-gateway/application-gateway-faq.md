---
title: Perguntas frequentes sobre o Gateway de Aplicativo do Azure | Microsoft Docs
description: "Esta página fornece respostas às perguntas frequentes sobre o Gateway de Aplicativo do Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 4e6244d92f41e0aa5c8a70db0db2881036984247
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="3f11c-103">Perguntas frequentes sobre o Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="3f11c-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="3f11c-104">Geral</span><span class="sxs-lookup"><span data-stu-id="3f11c-104">General</span></span>

<span data-ttu-id="3f11c-105">**P. O que é o Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="3f11c-106">O Gateway de Aplicativo do Azure é um ADC (Controlador de Entrega de Aplicativos) como um serviço, oferecendo vários recursos de balanceamento de carga de camada 7 para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3f11c-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="3f11c-107">Ele oferece um serviço altamente disponível e escalonável e totalmente gerenciado pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="3f11c-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="3f11c-108">**P. Quais recursos recebem suporte do Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="3f11c-109">O Gateway de Aplicativo oferece suporte ao descarregamento de SSL e SSL de ponta a ponta, Firewall de Aplicativo Web, afinidade de sessão baseada em cookies, roteamento baseado em caminho de url, hospedagem em múltiplos sites e outros.</span><span class="sxs-lookup"><span data-stu-id="3f11c-109">Application Gateway supports SSL offloading and end to end SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="3f11c-110">Para conferir uma lista completa dos recursos com suporte, visite [Introdução ao Gateway de Aplicativo](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="3f11c-110">For a full list of supported features, visit [Introduction to Application Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="3f11c-111">**P. Qual é a diferença entre o Gateway de Aplicativo e o Azure Load Balancer?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-111">**Q. What is the difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="3f11c-112">O Gateway de Aplicativo é um balanceador de carga de camada 7, o que significa que ele funciona com apenas tráfego da Web (HTTP/HTTPS/WebSocket).</span><span class="sxs-lookup"><span data-stu-id="3f11c-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="3f11c-113">Ele oferece suporte a recursos como terminação SSL, a afinidade de sessão baseada em cookie e round robin para tráfego de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="3f11c-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="3f11c-114">Balanceador de carga, equilibra a carga do tráfego na camada 4 (TCP/UDP).</span><span class="sxs-lookup"><span data-stu-id="3f11c-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="3f11c-115">**P. Quais protocolos recebem suporte do Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="3f11c-116">O Gateway de Aplicativo oferece suporte a WebSocket, HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3f11c-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="3f11c-117">**P. Quais recursos têm suporte atualmente como parte do pool de back-end?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="3f11c-118">Pools de back-end podem ser formados por NICs, conjuntos de dimensionamento de máquinas virtuais, IPs públicos, IPs internos, FQDN (nomes de domínio totalmente qualificados) e back-ends multilocatário como Aplicativos Web do Azure .</span><span class="sxs-lookup"><span data-stu-id="3f11c-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="3f11c-119">Membros do pool de back-end do Gateway de Aplicativo não estão vinculados a um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3f11c-119">Application Gateway backend pool members are not tied to an availability set.</span></span> <span data-ttu-id="3f11c-120">Os membros de pools de back-end podem existir entre clusters, data centers ou fora do Azure, desde que tenham conectividade IP.</span><span class="sxs-lookup"><span data-stu-id="3f11c-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="3f11c-121">**P. Em quais regiões o serviço está disponível?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-121">**Q. What regions is the service available in?**</span></span>

<span data-ttu-id="3f11c-122">O Gateway de Aplicativo está disponível em todas as regiões do Azure global.</span><span class="sxs-lookup"><span data-stu-id="3f11c-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="3f11c-123">Ele também está disponível no [Azure China](https://www.azure.cn/) e no [Azure Governamental](https://azure.microsoft.com/en-us/overview/clouds/government/)</span><span class="sxs-lookup"><span data-stu-id="3f11c-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="3f11c-124">**P. Ele é uma implantação dedicada à minha assinatura ou é compartilhado entre os clientes?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="3f11c-125">O Gateway de Aplicativo é uma implementação dedicada em sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3f11c-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="3f11c-126">**P. O redirecionamento HTTP-> HTTPS tem suporte?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="3f11c-127">Há suporte para redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="3f11c-127">Redirection is supported.</span></span> <span data-ttu-id="3f11c-128">Visite [Visão geral do redirecionamento do Gateway de Aplicativo](application-gateway-redirect-overview.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="3f11c-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) to learn more.</span></span>

<span data-ttu-id="3f11c-129">**P. Em que ordem os ouvintes são processados?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="3f11c-130">Os ouvintes são processados na ordem em que eles são mostrados.</span><span class="sxs-lookup"><span data-stu-id="3f11c-130">Listeners are processed in the order they are shown.</span></span> <span data-ttu-id="3f11c-131">Por esse motivo, se um ouvinte básico corresponder a uma solicitação de entrada, ele a processará primeiro.</span><span class="sxs-lookup"><span data-stu-id="3f11c-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="3f11c-132">Ouvintes multissite devem ser configurados antes de um ouvinte básico para assegurar que o tráfego seja roteado para o back-end correto.</span><span class="sxs-lookup"><span data-stu-id="3f11c-132">Multi-site listeners should be configured before a basic listener to ensure traffic is routed to the correct back-end.</span></span>

<span data-ttu-id="3f11c-133">**P. Onde posso encontrar o IP e o DNS do Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="3f11c-134">Ao usar um endereço IP público como um ponto de extremidade, essas informações podem ser encontradas no recurso do endereço IP público ou na página Visão geral do Gateway de Aplicativo no portal.</span><span class="sxs-lookup"><span data-stu-id="3f11c-134">When using a public IP address as an endpoint, this information can be found on the public IP address resource or on the Overview page for the Application Gateway in the portal.</span></span> <span data-ttu-id="3f11c-135">Para endereços IP internos, isso pode ser encontrado na página Visão geral.</span><span class="sxs-lookup"><span data-stu-id="3f11c-135">For internal IP addresses, this can be found on the Overview page.</span></span>

<span data-ttu-id="3f11c-136">**P. O IP ou DNS muda durante o tempo de vida do Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-136">**Q. Does the IP or DNS change over the lifetime of the Application Gateway?**</span></span>

<span data-ttu-id="3f11c-137">O VIP pode mudar se o gateway for interrompido e iniciado pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="3f11c-137">The VIP can change if the gateway is stopped and started by the customer.</span></span> <span data-ttu-id="3f11c-138">O DNS associado ao Gateway de Aplicativo não muda durante o ciclo de vida do gateway.</span><span class="sxs-lookup"><span data-stu-id="3f11c-138">The DNS associated with Application Gateway does not change over the lifecycle of the gateway.</span></span> <span data-ttu-id="3f11c-139">Por esse motivo, recomendamos o uso um alias do CNAME e apontá-lo para o endereço DNS do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-139">For this reason, it is recommended to use a CNAME alias and point it to the DNS address of the Application Gateway.</span></span>

<span data-ttu-id="3f11c-140">**P. O Gateway de Aplicativo oferece suporte a IP estático?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="3f11c-141">Não, o Gateway de Aplicativo não oferece suporte a endereços IP públicos estáticos, mas oferece suporte a IPs estáticos internos.</span><span class="sxs-lookup"><span data-stu-id="3f11c-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="3f11c-142">**P. O Gateway de Aplicativo oferece suporte a vários IPs públicos no gateway?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-142">**Q. Does Application Gateway support multiple public IPs on the gateway?**</span></span>

<span data-ttu-id="3f11c-143">Há suporte a apenas um endereço IP público em um Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="3f11c-144">**P. O Gateway de Aplicativo oferece suporte a cabeçalhos x-forwarded-for?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="3f11c-145">Sim, o Gateway de Aplicativo insere cabeçalhos x-forwarded-for, x-forwarded-proto e x-forwarded-port na solicitação encaminhada ao back-end.</span><span class="sxs-lookup"><span data-stu-id="3f11c-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into the request forwarded to the backend.</span></span> <span data-ttu-id="3f11c-146">O formato do cabeçalho x-forwarded-for é uma lista separada por vírgulas de IP:Porta.</span><span class="sxs-lookup"><span data-stu-id="3f11c-146">The format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="3f11c-147">Os valores válidos para x-forwarded-proto são http ou https.</span><span class="sxs-lookup"><span data-stu-id="3f11c-147">The valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="3f11c-148">X-forwarded-port especifica a porta na qual a solicitação alcançou o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-148">X-forwarded-port specifies the port at which the request reached at the Application Gateway.</span></span>

<span data-ttu-id="3f11c-149">**P. Quanto tempo demora para implantar um Gateway de Aplicativo? O meu Gateway de Aplicativo ainda funciona quando está sendo atualizado?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-149">**Q. How long does it take to deploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="3f11c-150">Novas implantações do Gateway de Aplicativo podem levar até 20 minutos para provisionar.</span><span class="sxs-lookup"><span data-stu-id="3f11c-150">New Application Gateway deployments can take up to 20 minutes to provision.</span></span> <span data-ttu-id="3f11c-151">Alterações de tamanho/contagem de instâncias não são interrompidas, e o gateway permanece ativo durante esse tempo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-151">Changes to instance size/count are not disruptive, and the gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="3f11c-152">Configuração</span><span class="sxs-lookup"><span data-stu-id="3f11c-152">Configuration</span></span>

<span data-ttu-id="3f11c-153">**P. O Gateway de Aplicativo é sempre implantado em uma rede virtual?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="3f11c-154">Sim, o Gateway de Aplicativo é sempre implantado em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3f11c-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="3f11c-155">Essa sub-rede só pode conter Gateways de Aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3f11c-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="3f11c-156">**P. O Gateway de Aplicativo pode se comunicar com instâncias fora de sua rede virtual?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-156">**Q. Can Application Gateway talk to instances outside its virtual network?**</span></span>

<span data-ttu-id="3f11c-157">O Gateway de Aplicativo pode se comunicar com instâncias fora da rede virtual na qual ele está localizado contanto que haja conectividade de IP.</span><span class="sxs-lookup"><span data-stu-id="3f11c-157">Application Gateway can talk to instances outside of the virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="3f11c-158">Se você planeja usar IPs internos como membros de pool de back-end, será necessário usar o [Emparelhamento VNET](../virtual-network/virtual-network-peering-overview.md) ou o [Gateway de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="3f11c-158">If you plan to use internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="3f11c-159">**P. Posso implantar qualquer coisa na sub-rede do Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-159">**Q. Can I deploy anything else in the Application Gateway subnet?**</span></span>

<span data-ttu-id="3f11c-160">Não, mas você pode implantar outros gateways de aplicativo na sub-rede.</span><span class="sxs-lookup"><span data-stu-id="3f11c-160">No, but you can deploy other application gateways in the subnet.</span></span>

<span data-ttu-id="3f11c-161">**P. Há suporte para Grupos de segurança de rede na sub-rede do Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-161">**Q. Are Network Security Groups supported on the Application Gateway subnet?**</span></span>

<span data-ttu-id="3f11c-162">Há suporte para Grupos de segurança de rede na sub-rede do Gateway de Aplicativo com as seguintes restrições:</span><span class="sxs-lookup"><span data-stu-id="3f11c-162">Network Security Groups are supported on the Application Gateway subnet with the following restrictions:</span></span>

* <span data-ttu-id="3f11c-163">Exceções devem ser colocadas para tráfego de entrada nas portas 65503-65534 para integridade de back-end para funcionar corretamente.</span><span class="sxs-lookup"><span data-stu-id="3f11c-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health to work correctly.</span></span>

* <span data-ttu-id="3f11c-164">A conectividade de internet de saída não pode ser bloqueada.</span><span class="sxs-lookup"><span data-stu-id="3f11c-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="3f11c-165">Tráfego de marca AzureLoadBalancer deve ser permitido.</span><span class="sxs-lookup"><span data-stu-id="3f11c-165">Traffic from the AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="3f11c-166">**P. Quais são os limites no Gateway de Aplicativo? Posso aumentar esses limites?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-166">**Q. What are the limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="3f11c-167">Visite [Limites do Gateway de Aplicativo](../azure-subscription-service-limits.md#application-gateway-limits) para exibir os limites.</span><span class="sxs-lookup"><span data-stu-id="3f11c-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) to view the limits.</span></span>

<span data-ttu-id="3f11c-168">**P. Posso usar o Gateway de Aplicativo para tráfego interno e externo ao mesmo tempo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="3f11c-169">Sim, o Gateway de Aplicativo oferece suporte a um endereço IP interno e um IP externo por Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="3f11c-170">**P. Há suporte para o emparelhamento VNet?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="3f11c-171">Sim, o emparelhamento VNet tem suporte e é útil para o balanceamento de carga de tráfego em outras redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="3f11c-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="3f11c-172">**P. Posso falar com servidores locais quando eles estiverem conectados por túneis de VPN ou ExpressRoute?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-172">**Q. Can I talk to on-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="3f11c-173">Sim, contanto que o tráfego seja permitido.</span><span class="sxs-lookup"><span data-stu-id="3f11c-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="3f11c-174">**P. Posso ter um pool de back-end que atende a muitos aplicativos em portas diferentes?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="3f11c-175">Há suporte para arquitetura de microsserviço.</span><span class="sxs-lookup"><span data-stu-id="3f11c-175">Micro service architecture is supported.</span></span> <span data-ttu-id="3f11c-176">Você precisaria de várias configurações http definidas para investigação em portas diferentes.</span><span class="sxs-lookup"><span data-stu-id="3f11c-176">You would need multiple http settings configured to probe on different ports.</span></span>

<span data-ttu-id="3f11c-177">**P. Investigações personalizadas têm suporte para curingas/regex nos dados de resposta?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="3f11c-178">As investigações personalizadas não têm suporte para curingas/regex nos dados de resposta.</span><span class="sxs-lookup"><span data-stu-id="3f11c-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="3f11c-179">**P. Como as regras são processadas?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="3f11c-180">As regras são processadas na ordem em que elas são configuradas.</span><span class="sxs-lookup"><span data-stu-id="3f11c-180">Rules are processed in the order they are configured.</span></span> <span data-ttu-id="3f11c-181">É recomendável que as regras multissites sejam configuradas antes de regras básicas para reduzir a chance de que o tráfego seja roteado para o back-end inadequado, já que a regra básica corresponderia o tráfego com base na porta antes da regra multissite que está sendo avaliada.</span><span class="sxs-lookup"><span data-stu-id="3f11c-181">It is recommended that multi-site rules are configured before basic rules to reduce the chance that traffic is routed to the inappropriate backend as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="3f11c-182">**P. Como as regras são processadas?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="3f11c-183">As regras são processadas na ordem em que são criadas.</span><span class="sxs-lookup"><span data-stu-id="3f11c-183">Rules are processed in the order they are created.</span></span> <span data-ttu-id="3f11c-184">É recomendável que as regras multissite sejam configuradas antes das regras básicas.</span><span class="sxs-lookup"><span data-stu-id="3f11c-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="3f11c-185">Ao configurar primeiro os ouvintes multissite, essa configuração reduz a chance de o tráfego ser roteado para o back-end inadequado.</span><span class="sxs-lookup"><span data-stu-id="3f11c-185">By configuring multi-site listeners first, this configuration reduces the chance that traffic is routed to the inappropriate backend.</span></span> <span data-ttu-id="3f11c-186">Esse problema de roteamento pode ocorrer, pois a regra básica corresponderia ao tráfego com base na porta antes da regra multissite ser avaliada.</span><span class="sxs-lookup"><span data-stu-id="3f11c-186">This routing issue can occur as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="3f11c-187">**P. O que significa o campo Host para investigações personalizadas?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-187">**Q. What does the Host field for custom probes signify?**</span></span>

<span data-ttu-id="3f11c-188">O campo Host especifica o nome ao qual enviar a investigação.</span><span class="sxs-lookup"><span data-stu-id="3f11c-188">Host field specifies the name to send the probe to.</span></span> <span data-ttu-id="3f11c-189">Aplicável somente quando vários sites são configurados no Gateway de Aplicativo; do contrário, use '127.0.0.1'.</span><span class="sxs-lookup"><span data-stu-id="3f11c-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="3f11c-190">Esse valor é diferente do nome de host da VM e está no formato \<protocolo\>://\<host\>:\<porta\>\<caminho\>.</span><span class="sxs-lookup"><span data-stu-id="3f11c-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="3f11c-191">**P. É possível lista permissões de acesso do Gateway de Aplicativo para alguns IPs de origem?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-191">**Q. Can I whitelist Application Gateway access to a few source IPs?**</span></span>

<span data-ttu-id="3f11c-192">Esse cenário pode ser feito usando os NSGs na sub-rede de Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="3f11c-193">As seguintes restrições devem ser colocadas na sub-rede na ordem listada de prioridade:</span><span class="sxs-lookup"><span data-stu-id="3f11c-193">The following restrictions should be put on the subnet in the listed order of priority:</span></span>

* <span data-ttu-id="3f11c-194">Permitir tráfego de entrada de intervalo de IP/IP de origem.</span><span class="sxs-lookup"><span data-stu-id="3f11c-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="3f11c-195">Permitir solicitações de entrada de todas as fontes para portas 65534 65503 para [comunicação de integridade de back-end](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="3f11c-195">Allow incoming requests from all sources to ports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="3f11c-196">Permitir entradas investigações do Azure Load Balancer (marca AzureLoadBalancer) e tráfego de rede virtual entrada (marca VirtualNetwork) no [NSG](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="3f11c-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on the [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="3f11c-197">Bloquear todo o outro tráfego de entrada com um Negar todas as regras.</span><span class="sxs-lookup"><span data-stu-id="3f11c-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="3f11c-198">Permitir tráfego de saída para a internet para todos os destinos.</span><span class="sxs-lookup"><span data-stu-id="3f11c-198">Allow outbound traffic to the internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="3f11c-199">Desempenho</span><span class="sxs-lookup"><span data-stu-id="3f11c-199">Performance</span></span>

<span data-ttu-id="3f11c-200">**P. Como o Gateway de Aplicativo oferece suporte a alta disponibilidade e escalabilidade?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="3f11c-201">O Gateway de Aplicativo dará suporte a cenários de alta disponibilidade quando você tiver duas ou mais instâncias implantadas.</span><span class="sxs-lookup"><span data-stu-id="3f11c-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="3f11c-202">O Azure distribui essas instâncias entre domínios de atualização e de falha para garantir que todas as instâncias não falham ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-202">Azure distributes these instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="3f11c-203">O Gateway de Aplicativo dá suporte à escalabilidade adicionando várias instâncias do mesmo gateway para compartilhar a carga.</span><span class="sxs-lookup"><span data-stu-id="3f11c-203">Application Gateway supports scalability by adding multiple instances of the same gateway to share the load.</span></span>

<span data-ttu-id="3f11c-204">**P. Como posso obter o cenário de recuperação de desastres em data centers com o Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="3f11c-205">Os clientes podem usar o Gerenciador de Tráfego para distribuir o tráfego entre vários Gateways de Aplicativo em data centers diferentes.</span><span class="sxs-lookup"><span data-stu-id="3f11c-205">Customers can use Traffic Manager to distribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="3f11c-206">**P. Há suporte para o dimensionamento automático?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="3f11c-207">Não, mas o Gateway de Aplicativo tem uma métrica de taxa de transferência que pode ser usada para enviar um alerta quando um limite for atingido.</span><span class="sxs-lookup"><span data-stu-id="3f11c-207">No, but Application Gateway has a throughput metric that can be used to alert you when a threshold is reached.</span></span> <span data-ttu-id="3f11c-208">A adição manual de instâncias ou alteração do tamanho não reinicia o gateway e não afeta o tráfego existente.</span><span class="sxs-lookup"><span data-stu-id="3f11c-208">Manually adding instances or changing size does not restart the gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="3f11c-209">**P. A escala/redução vertical causa tempo de inatividade?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="3f11c-210">Não há tempo de inatividade, as instâncias são distribuídas entre domínios de atualização e domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="3f11c-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="3f11c-211">**P. Posso alterar o tamanho da instância de média para grande sem interrupções?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-211">**Q. Can I change instance size from medium to large without disruption?**</span></span>

<span data-ttu-id="3f11c-212">Sim, o Azure distribui essas instâncias entre domínios de atualização e de falha para garantir que todas as instâncias não falham ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-212">Yes, Azure distributes instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="3f11c-213">O Gateway de Aplicativo dá suporte à escalabilidade adicionando várias instâncias do mesmo gateway para compartilhar a carga.</span><span class="sxs-lookup"><span data-stu-id="3f11c-213">Application Gateway supports scaling by adding multiple instances of the same gateway to share the load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="3f11c-214">Configuração de SSL</span><span class="sxs-lookup"><span data-stu-id="3f11c-214">SSL Configuration</span></span>

<span data-ttu-id="3f11c-215">**P. Quais certificados têm suporte no Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="3f11c-216">Certificados autoassinados, certificados de autoridade de certificação e certificados curinga têm suporte.</span><span class="sxs-lookup"><span data-stu-id="3f11c-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="3f11c-217">Não há suporte para certificados EV.</span><span class="sxs-lookup"><span data-stu-id="3f11c-217">EV certs are not supported.</span></span>

<span data-ttu-id="3f11c-218">**P. Quais são os conjuntos de criptografia atuais com suporte do Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-218">**Q. What are the current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="3f11c-219">A seguir, os conjuntos de criptografia atuais que têm suporte do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-219">The following are the current cipher suites supported by application gateway.</span></span> <span data-ttu-id="3f11c-220">Visite: [configurar SSL versões de política e conjuntos de codificação no Gateway de Aplicativo](application-gateway-configure-ssl-policy-powershell.md) para aprender a personalizar opções de SSL.</span><span class="sxs-lookup"><span data-stu-id="3f11c-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn how to customize SSL options.</span></span>

- <span data-ttu-id="3f11c-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="3f11c-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="3f11c-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="3f11c-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="3f11c-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="3f11c-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="3f11c-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="3f11c-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="3f11c-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="3f11c-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="3f11c-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="3f11c-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="3f11c-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="3f11c-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="3f11c-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="3f11c-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="3f11c-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="3f11c-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="3f11c-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="3f11c-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="3f11c-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="3f11c-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="3f11c-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="3f11c-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="3f11c-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="3f11c-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="3f11c-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="3f11c-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="3f11c-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="3f11c-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="3f11c-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3f11c-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="3f11c-247">**P. O Gateway de Aplicativo também oferece suporte à nova criptografia de tráfego para o back-end?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-247">**Q. Does Application Gateway also support re-encryption of traffic to the backend?**</span></span>

<span data-ttu-id="3f11c-248">Sim, o Gateway de Aplicativo oferece suporte ao descarregamento SSL, SSL de ponta a ponta, que criptografa novamente o tráfego para o back-end.</span><span class="sxs-lookup"><span data-stu-id="3f11c-248">Yes, Application Gateway supports SSL offload, and end to end SSL, which re-encrypts the traffic to the backend.</span></span>

<span data-ttu-id="3f11c-249">**P. Posso configurar a política de SSL para controlar as versões de protocolo SSL?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-249">**Q. Can I configure SSL policy to control SSL Protocol versions?**</span></span>

<span data-ttu-id="3f11c-250">Sim, você pode configurar o Gateway de Aplicativo para negar TLS1.0, TLS1.1 e TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="3f11c-250">Yes, you can configure Application Gateway to deny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="3f11c-251">SSL 2.0 e 3.0 já estão desabilitados por padrão e não são configuráveis.</span><span class="sxs-lookup"><span data-stu-id="3f11c-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="3f11c-252">**P. Posso configurar conjuntos de codificação e a ordem de política?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="3f11c-253">Sim, há suporte para [configuração de conjuntos de criptografia](application-gateway-ssl-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3f11c-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="3f11c-254">Ao definir uma política personalizada, pelo menos um dos seguintes pacotes de codificação deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="3f11c-254">When defining a custom policy, at least one of the following cipher suites must be enabled.</span></span> <span data-ttu-id="3f11c-255">O Gateway de Aplicativo usa SHA256 para gerenciamento de back-end.</span><span class="sxs-lookup"><span data-stu-id="3f11c-255">Application gateway uses SHA256 to for backend management.</span></span>

* <span data-ttu-id="3f11c-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="3f11c-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="3f11c-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="3f11c-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="3f11c-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="3f11c-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3f11c-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="3f11c-262">**P. Há suporte para quantos certificados SSL?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="3f11c-263">Há suporte para até 20 certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="3f11c-263">Up to 20 SSL certificates are supported.</span></span>

<span data-ttu-id="3f11c-264">**P. Quantos certificados de autenticação para nova criptografia de back-end têm suporte?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="3f11c-265">Há suporte para até 10 certificados de autenticação, com um padrão de cinco.</span><span class="sxs-lookup"><span data-stu-id="3f11c-265">Up to 10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="3f11c-266">**P. O Gateway de Aplicativo é integrado ao Azure Key Vault de forma nativa?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="3f11c-267">Não, ele não é integrado ao Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3f11c-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="3f11c-268">Configuração de WAF (Firewall de Aplicativo Web)</span><span class="sxs-lookup"><span data-stu-id="3f11c-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="3f11c-269">**P. O SKU WAF oferece todos os recursos disponíveis com o SKU Standard?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-269">**Q. Does the WAF SKU offer all the features available with the Standard SKU?**</span></span>

<span data-ttu-id="3f11c-270">Sim, o WAF oferece suporte a todos os recursos no SKU Standard.</span><span class="sxs-lookup"><span data-stu-id="3f11c-270">Yes, WAF supports all the features in the Standard SKU.</span></span>

<span data-ttu-id="3f11c-271">**P. Qual é a versão do CRS com suporte do Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-271">**Q. What is the CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="3f11c-272">O Gateway de Aplicativo dá suporte a CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e a CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="3f11c-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="3f11c-273">**P. Como monitorar o WAF?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="3f11c-274">O WAF é monitorado por meio do log de diagnóstico. Encontre mais informações sobre o log de diagnóstico em [Log de diagnósticos e métricas para o Gateway de Aplicativo](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="3f11c-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="3f11c-275">**P. O modo de detecção bloqueia o tráfego?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="3f11c-276">Não, o modo de detecção apenas registra o tráfego em log, o que dispara uma regra WAF.</span><span class="sxs-lookup"><span data-stu-id="3f11c-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="3f11c-277">**P. Como posso personalizar regras WAF?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="3f11c-278">Sim, as regras WAF são personalizáveis, para saber mais sobre como personalizá-las visita [Personalizar grupos de regras e regras WAF](application-gateway-customize-waf-rules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3f11c-278">Yes, WAF rules are customizable, for more information on how to customize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="3f11c-279">**P. Quais regras estão disponíveis no momento?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="3f11c-280">No momento, o WAF oferece suporte a CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), que fornece segurança de linha de base contra a maioria das dez principais vulnerabilidades identificadas pelo OWASP (Open Web Application Security Project) encontradas aqui [Dez principais vulnerabilidades do OWASP](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="3f11c-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of the top 10 vulnerabilities identified by the Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="3f11c-281">Proteção contra injeção de SQL</span><span class="sxs-lookup"><span data-stu-id="3f11c-281">SQL injection protection</span></span>

* <span data-ttu-id="3f11c-282">Proteção contra scripts entre sites</span><span class="sxs-lookup"><span data-stu-id="3f11c-282">Cross site scripting protection</span></span>

* <span data-ttu-id="3f11c-283">Proteção Contra Ataques Comuns da Web, como a injeção de comandos, as solicitações HTTP indesejadas, a divisão de resposta HTTP e o ataque de inclusão de arquivo remoto</span><span class="sxs-lookup"><span data-stu-id="3f11c-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="3f11c-284">Proteção contra violações de protocolo HTTP</span><span class="sxs-lookup"><span data-stu-id="3f11c-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="3f11c-285">Proteção contra anomalias de protocolo HTTP, como ausência de host de agente do usuário e de cabeçalhos de aceitação</span><span class="sxs-lookup"><span data-stu-id="3f11c-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="3f11c-286">Prevenção contra bots, rastreadores e scanners</span><span class="sxs-lookup"><span data-stu-id="3f11c-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="3f11c-287">Detecção de problemas de configuração de aplicativo comuns (ou seja, Apache, IIS etc.)</span><span class="sxs-lookup"><span data-stu-id="3f11c-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="3f11c-288">**P. O WAF também oferece suporte à prevenção de DDoS?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="3f11c-289">Não, o WAF não oferece prevenção de DDoS.</span><span class="sxs-lookup"><span data-stu-id="3f11c-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="3f11c-290">Diagnóstico e registro em log</span><span class="sxs-lookup"><span data-stu-id="3f11c-290">Diagnostics and Logging</span></span>

<span data-ttu-id="3f11c-291">**P. Quais tipos de logs estão disponíveis com o Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="3f11c-292">Há três logs disponíveis para o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="3f11c-293">Para saber mais sobre esses logs e outros recursos de diagnóstico, visite [Integridade de back-end, logs de diagnóstico e métricas para o Gateway de Aplicativo](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="3f11c-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="3f11c-294">**ApplicationGatewayAccessLog** - O log de acesso contém cada solicitação enviada ao front-end do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-294">**ApplicationGatewayAccessLog** - The access log contains each request submitted to the Application Gateway frontend.</span></span> <span data-ttu-id="3f11c-295">Os dados incluem o IP do chamador, a URL solicitada, latência da resposta, o código de retorno, bytes de entrada e saída. O log de acesso é coletado a cada 300 segundos.</span><span class="sxs-lookup"><span data-stu-id="3f11c-295">The data includes the caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="3f11c-296">Esse log contém um registro por instância do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="3f11c-297">**ApplicationGatewayPerformanceLog** - O log de desempenho captura informações sobre o desempenho por instância, incluindo a solicitação total atendida, a taxa de transferência em bytes, o total de solicitações atendidas, a contagem de solicitações com falha, a contagem de instâncias de back-end íntegras ou não.</span><span class="sxs-lookup"><span data-stu-id="3f11c-297">**ApplicationGatewayPerformanceLog** - The performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="3f11c-298">**ApplicationGatewayFirewallLog** - O log de firewall contém solicitações registradas por meio do modo de detecção ou prevenção de um gateway de aplicativo configurado com o firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3f11c-298">**ApplicationGatewayFirewallLog** - The firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="3f11c-299">**P. Como saber se os membros de meu pool de back-end estão íntegros?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="3f11c-300">Use o cmdlet do PowerShell `Get-AzureRmApplicationGatewayBackendHealth` ou verifique a integridade por meio do portal visitando [Diagnóstico do Gateway de Aplicativo](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="3f11c-300">You can use the PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through the portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="3f11c-301">**P. Qual é a política de retenção nos logs de diagnóstico?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-301">**Q. What is the retention policy on the diagnostics logs?**</span></span>

<span data-ttu-id="3f11c-302">Os logs de diagnóstico fluem para a conta de armazenamento de clientes, e os clientes podem definir a política de retenção com base em suas preferências.</span><span class="sxs-lookup"><span data-stu-id="3f11c-302">Diagnostic logs flow to the customers storage account and customers can set the retention policy based on their preference.</span></span> <span data-ttu-id="3f11c-303">Os logs de diagnóstico também podem ser enviados a um Hub de Eventos ou ao Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3f11c-303">Diagnostic logs can also be sent to an Event Hub or Log Analytics.</span></span> <span data-ttu-id="3f11c-304">Visite [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="3f11c-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="3f11c-305">**P. Como posso obter logs de auditoria para o Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="3f11c-306">Os logs de auditoria estão disponíveis para o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f11c-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="3f11c-307">No portal, clique em **Log de Atividades** na folha do menu de um Gateway de Aplicativo para acessar o log de auditoria.</span><span class="sxs-lookup"><span data-stu-id="3f11c-307">In the portal, click **Activity Log** in the menu blade of an Application Gateway to access the audit log.</span></span> 

<span data-ttu-id="3f11c-308">**P. Posso configurar alertas com o Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="3f11c-309">Sim, o Gateway de Aplicativo oferece suporte a alertas, e os alertas são configurados com base em métricas.</span><span class="sxs-lookup"><span data-stu-id="3f11c-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="3f11c-310">No momento, o Gateway de Aplicativo tem uma métrica de "taxa de transferência", que pode ser configurada para o alerta.</span><span class="sxs-lookup"><span data-stu-id="3f11c-310">Application Gateway currently has a metric of "throughput", which can be configured to alert.</span></span> <span data-ttu-id="3f11c-311">Para saber mais sobre alertas, visite [Receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3f11c-311">To learn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="3f11c-312">**P. A integridade do back-end retorna um status desconhecido, o que pode estar causando esse status?**</span><span class="sxs-lookup"><span data-stu-id="3f11c-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="3f11c-313">O motivo mais comum é o bloqueio ao acesso do back-end por um NSG ou DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="3f11c-313">The most common reason is access to the backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="3f11c-314">Visite [Integridade do back-end, registro em log e métricas de diagnóstico do Gateway de Aplicativo](application-gateway-diagnostics.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="3f11c-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f11c-315">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f11c-315">Next Steps</span></span>

<span data-ttu-id="3f11c-316">Para saber mais sobre o Gateway de Aplicativo, visite [Introdução ao Gateway de Aplicativo](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3f11c-316">To learn more about Application Gateway visit [Introduction to Application Gateway](application-gateway-introduction.md).</span></span>
