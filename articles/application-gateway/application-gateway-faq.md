---
title: aaaFrequently perguntado para o Gateway de aplicativo do Azure | Microsoft Docs
description: "Esta página fornece respostas toofrequently perguntas frequentes sobre o Gateway de aplicativo do Azure"
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
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="77ae6-103">Perguntas frequentes sobre o Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="77ae6-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="77ae6-104">Geral</span><span class="sxs-lookup"><span data-stu-id="77ae6-104">General</span></span>

<span data-ttu-id="77ae6-105">**P. O que é o Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="77ae6-106">O Gateway de Aplicativo do Azure é um ADC (Controlador de Entrega de Aplicativos) como um serviço, oferecendo vários recursos de balanceamento de carga de camada 7 para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="77ae6-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="77ae6-107">Ele oferece um serviço altamente disponível e escalonável e totalmente gerenciado pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="77ae6-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="77ae6-108">**P. Quais recursos recebem suporte do Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="77ae6-109">Application Gateway oferece suporte a SSL tooend final e de descarregamento de SSL, Firewall do aplicativo Web, a afinidade de sessão baseada em cookie, url baseadas em caminhos roteamento, várias hospedagem de site e outros.</span><span class="sxs-lookup"><span data-stu-id="77ae6-109">Application Gateway supports SSL offloading and end tooend SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="77ae6-110">Para obter uma lista completa de recursos com suporte, visite [tooApplication Introdução Gateway](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="77ae6-110">For a full list of supported features, visit [Introduction tooApplication Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="77ae6-111">**P. Qual é a diferença Olá entre o balanceador de carga do Azure e o Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-111">**Q. What is hello difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="77ae6-112">O Gateway de Aplicativo é um balanceador de carga de camada 7, o que significa que ele funciona com apenas tráfego da Web (HTTP/HTTPS/WebSocket).</span><span class="sxs-lookup"><span data-stu-id="77ae6-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="77ae6-113">Ele oferece suporte a recursos como terminação SSL, a afinidade de sessão baseada em cookie e round robin para tráfego de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="77ae6-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="77ae6-114">Balanceador de carga, equilibra a carga do tráfego na camada 4 (TCP/UDP).</span><span class="sxs-lookup"><span data-stu-id="77ae6-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="77ae6-115">**P. Quais protocolos recebem suporte do Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="77ae6-116">O Gateway de Aplicativo oferece suporte a WebSocket, HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="77ae6-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="77ae6-117">**P. Quais recursos têm suporte atualmente como parte do pool de back-end?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="77ae6-118">Pools de back-end podem ser formados por NICs, conjuntos de dimensionamento de máquinas virtuais, IPs públicos, IPs internos, FQDN (nomes de domínio totalmente qualificados) e back-ends multilocatário como Aplicativos Web do Azure .</span><span class="sxs-lookup"><span data-stu-id="77ae6-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="77ae6-119">Application Gateway membros do pool de back-end não são ligadas tooan conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="77ae6-119">Application Gateway backend pool members are not tied tooan availability set.</span></span> <span data-ttu-id="77ae6-120">Os membros de pools de back-end podem existir entre clusters, data centers ou fora do Azure, desde que tenham conectividade IP.</span><span class="sxs-lookup"><span data-stu-id="77ae6-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="77ae6-121">**P. Quais regiões Olá serviço está disponível em?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-121">**Q. What regions is hello service available in?**</span></span>

<span data-ttu-id="77ae6-122">O Gateway de Aplicativo está disponível em todas as regiões do Azure global.</span><span class="sxs-lookup"><span data-stu-id="77ae6-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="77ae6-123">Ele também está disponível no [Azure China](https://www.azure.cn/) e no [Azure Governamental](https://azure.microsoft.com/en-us/overview/clouds/government/)</span><span class="sxs-lookup"><span data-stu-id="77ae6-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="77ae6-124">**P. Ele é uma implantação dedicada à minha assinatura ou é compartilhado entre os clientes?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="77ae6-125">O Gateway de Aplicativo é uma implementação dedicada em sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="77ae6-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="77ae6-126">**P. O redirecionamento HTTP-> HTTPS tem suporte?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="77ae6-127">Há suporte para redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="77ae6-127">Redirection is supported.</span></span> <span data-ttu-id="77ae6-128">Visite [visão geral de redirecionamento do Application Gateway](application-gateway-redirect-overview.md) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="77ae6-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn more.</span></span>

<span data-ttu-id="77ae6-129">**P. Em que ordem os ouvintes são processados?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="77ae6-130">Ouvintes são processados na ordem de saudação que são mostradas.</span><span class="sxs-lookup"><span data-stu-id="77ae6-130">Listeners are processed in hello order they are shown.</span></span> <span data-ttu-id="77ae6-131">Por esse motivo, se um ouvinte básico corresponder a uma solicitação de entrada, ele a processará primeiro.</span><span class="sxs-lookup"><span data-stu-id="77ae6-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="77ae6-132">Ouvintes de vários locais devem ser configurados antes que o tráfego de tooensure um ouvinte básico é roteado toohello correto back-end.</span><span class="sxs-lookup"><span data-stu-id="77ae6-132">Multi-site listeners should be configured before a basic listener tooensure traffic is routed toohello correct back-end.</span></span>

<span data-ttu-id="77ae6-133">**P. Onde posso encontrar o IP e o DNS do Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="77ae6-134">Ao usar um endereço IP público como um ponto de extremidade, essas informações podem ser encontradas no recurso de endereço IP público hello, ou na página de visão geral de saudação para Olá Application Gateway no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="77ae6-134">When using a public IP address as an endpoint, this information can be found on hello public IP address resource or on hello Overview page for hello Application Gateway in hello portal.</span></span> <span data-ttu-id="77ae6-135">Para os endereços IP internos, isso pode ser encontrado na página de visão geral de saudação.</span><span class="sxs-lookup"><span data-stu-id="77ae6-135">For internal IP addresses, this can be found on hello Overview page.</span></span>

<span data-ttu-id="77ae6-136">**P. Hello IP ou DNS muda com o tempo de vida de saudação do hello Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-136">**Q. Does hello IP or DNS change over hello lifetime of hello Application Gateway?**</span></span>

<span data-ttu-id="77ae6-137">Olá VIP pode alterar se gateway Olá é interrompido e iniciado pelo cliente hello.</span><span class="sxs-lookup"><span data-stu-id="77ae6-137">hello VIP can change if hello gateway is stopped and started by hello customer.</span></span> <span data-ttu-id="77ae6-138">Olá DNS associado com o Application Gateway não altera ciclo de vida de saudação do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="77ae6-138">hello DNS associated with Application Gateway does not change over hello lifecycle of hello gateway.</span></span> <span data-ttu-id="77ae6-139">Por esse motivo, é recomendável toouse um alias CNAME e aponte-endereço DNS de toohello de saudação Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="77ae6-139">For this reason, it is recommended toouse a CNAME alias and point it toohello DNS address of hello Application Gateway.</span></span>

<span data-ttu-id="77ae6-140">**P. O Gateway de Aplicativo oferece suporte a IP estático?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="77ae6-141">Não, o Gateway de Aplicativo não oferece suporte a endereços IP públicos estáticos, mas oferece suporte a IPs estáticos internos.</span><span class="sxs-lookup"><span data-stu-id="77ae6-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="77ae6-142">**P. Application Gateway dá suporte a vários IPs públicos no gateway Olá?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-142">**Q. Does Application Gateway support multiple public IPs on hello gateway?**</span></span>

<span data-ttu-id="77ae6-143">Há suporte a apenas um endereço IP público em um Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77ae6-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="77ae6-144">**P. O Gateway de Aplicativo oferece suporte a cabeçalhos x-forwarded-for?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="77ae6-145">Sim, Application Gateway insere x-encaminhado-para, proto encaminhados x e cabeçalhos de porta encaminhados x em solicitação Olá encaminhados toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="77ae6-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into hello request forwarded toohello backend.</span></span> <span data-ttu-id="77ae6-146">formato de saudação do cabeçalho x-encaminhado-para é uma lista separada por vírgulas de IP: porta.</span><span class="sxs-lookup"><span data-stu-id="77ae6-146">hello format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="77ae6-147">os valores válidos para proto encaminhados x Olá são http ou https.</span><span class="sxs-lookup"><span data-stu-id="77ae6-147">hello valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="77ae6-148">Porta encaminhados X Especifica a porta de saudação no qual solicitação Olá atingida em Olá Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="77ae6-148">X-forwarded-port specifies hello port at which hello request reached at hello Application Gateway.</span></span>

<span data-ttu-id="77ae6-149">**P. Quanto tempo leva toodeploy um Application Gateway? O meu Gateway de Aplicativo ainda funciona quando está sendo atualizado?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-149">**Q. How long does it take toodeploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="77ae6-150">Novas implantações do Application Gateway podem demorar até too20 tooprovision de minutos.</span><span class="sxs-lookup"><span data-stu-id="77ae6-150">New Application Gateway deployments can take up too20 minutes tooprovision.</span></span> <span data-ttu-id="77ae6-151">Alterações tooinstance tamanho/contagem não precisam de interrupções e gateway Olá permanece ativa durante esse tempo.</span><span class="sxs-lookup"><span data-stu-id="77ae6-151">Changes tooinstance size/count are not disruptive, and hello gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="77ae6-152">Configuração</span><span class="sxs-lookup"><span data-stu-id="77ae6-152">Configuration</span></span>

<span data-ttu-id="77ae6-153">**P. O Gateway de Aplicativo é sempre implantado em uma rede virtual?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="77ae6-154">Sim, o Gateway de Aplicativo é sempre implantado em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="77ae6-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="77ae6-155">Essa sub-rede só pode conter Gateways de Aplicativos.</span><span class="sxs-lookup"><span data-stu-id="77ae6-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="77ae6-156">**P. Application Gateway pode falar tooinstances fora de sua rede virtual?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-156">**Q. Can Application Gateway talk tooinstances outside its virtual network?**</span></span>

<span data-ttu-id="77ae6-157">Gateway de aplicativo pode se comunicar tooinstances fora da rede virtual de saudação que está em como não há conectividade IP.</span><span class="sxs-lookup"><span data-stu-id="77ae6-157">Application Gateway can talk tooinstances outside of hello virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="77ae6-158">Se você estiver planejando toouse IPs internos como membros do pool de back-end, ele requer [emparelhamento VNET](../virtual-network/virtual-network-peering-overview.md) ou [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="77ae6-158">If you plan toouse internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="77ae6-159">**P. Posso implantar tudo na sub-rede do Application Gateway Olá?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-159">**Q. Can I deploy anything else in hello Application Gateway subnet?**</span></span>

<span data-ttu-id="77ae6-160">Não, mas você pode implantar outros application gateways na sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="77ae6-160">No, but you can deploy other application gateways in hello subnet.</span></span>

<span data-ttu-id="77ae6-161">**P. Há suporte para grupos de segurança de rede na sub-rede de Gateway do aplicativo hello?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-161">**Q. Are Network Security Groups supported on hello Application Gateway subnet?**</span></span>

<span data-ttu-id="77ae6-162">Grupos de segurança de rede têm suporte na sub-rede de Gateway do aplicativo hello com hello restrições a seguir:</span><span class="sxs-lookup"><span data-stu-id="77ae6-162">Network Security Groups are supported on hello Application Gateway subnet with hello following restrictions:</span></span>

* <span data-ttu-id="77ae6-163">Exceções devem ser colocadas tráfego de entrada nas portas 65534 65503 para toowork de integridade de back-end corretamente.</span><span class="sxs-lookup"><span data-stu-id="77ae6-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health toowork correctly.</span></span>

* <span data-ttu-id="77ae6-164">A conectividade de internet de saída não pode ser bloqueada.</span><span class="sxs-lookup"><span data-stu-id="77ae6-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="77ae6-165">Tráfego de saudação marca AzureLoadBalancer deve ser permitido.</span><span class="sxs-lookup"><span data-stu-id="77ae6-165">Traffic from hello AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="77ae6-166">**P. Quais são os limites de saudação no Application Gateway? Posso aumentar esses limites?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-166">**Q. What are hello limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="77ae6-167">Visite [limites de Gateway do aplicativo](../azure-subscription-service-limits.md#application-gateway-limits) tooview Olá limites.</span><span class="sxs-lookup"><span data-stu-id="77ae6-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limits.</span></span>

<span data-ttu-id="77ae6-168">**P. Posso usar o Gateway de Aplicativo para tráfego interno e externo ao mesmo tempo?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="77ae6-169">Sim, o Gateway de Aplicativo oferece suporte a um endereço IP interno e um IP externo por Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77ae6-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="77ae6-170">**P. Há suporte para o emparelhamento VNet?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="77ae6-171">Sim, o emparelhamento VNet tem suporte e é útil para o balanceamento de carga de tráfego em outras redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="77ae6-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="77ae6-172">**P. Posso falar servidores locais tooon quando eles estão conectados por túneis de rota expressa ou VPN?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-172">**Q. Can I talk tooon-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="77ae6-173">Sim, contanto que o tráfego seja permitido.</span><span class="sxs-lookup"><span data-stu-id="77ae6-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="77ae6-174">**P. Posso ter um pool de back-end que atende a muitos aplicativos em portas diferentes?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="77ae6-175">Há suporte para arquitetura de microsserviço.</span><span class="sxs-lookup"><span data-stu-id="77ae6-175">Micro service architecture is supported.</span></span> <span data-ttu-id="77ae6-176">Você precisaria de vários tooprobe de configurações de http em portas diferentes.</span><span class="sxs-lookup"><span data-stu-id="77ae6-176">You would need multiple http settings configured tooprobe on different ports.</span></span>

<span data-ttu-id="77ae6-177">**P. Investigações personalizadas têm suporte para curingas/regex nos dados de resposta?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="77ae6-178">As investigações personalizadas não têm suporte para curingas/regex nos dados de resposta.</span><span class="sxs-lookup"><span data-stu-id="77ae6-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="77ae6-179">**P. Como as regras são processadas?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="77ae6-180">Regras são processadas na ordem Olá que estão configurados.</span><span class="sxs-lookup"><span data-stu-id="77ae6-180">Rules are processed in hello order they are configured.</span></span> <span data-ttu-id="77ae6-181">É recomendável que as regras de vários locais são configuradas antes chance de saudação de tooreduce regras básicas que o tráfego é roteada back-end do toohello inadequado como regra básica Olá corresponderia tráfego com base em regra de multissite toohello anterior de porta que está sendo avaliada.</span><span class="sxs-lookup"><span data-stu-id="77ae6-181">It is recommended that multi-site rules are configured before basic rules tooreduce hello chance that traffic is routed toohello inappropriate backend as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="77ae6-182">**P. Como as regras são processadas?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="77ae6-183">Regras são processadas na ordem de saudação que são criados.</span><span class="sxs-lookup"><span data-stu-id="77ae6-183">Rules are processed in hello order they are created.</span></span> <span data-ttu-id="77ae6-184">É recomendável que as regras multissite sejam configuradas antes das regras básicas.</span><span class="sxs-lookup"><span data-stu-id="77ae6-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="77ae6-185">Ao configurar primeiro ouvintes de vários locais, essa configuração reduz a chance de saudação que o tráfego é back-end do toohello roteados inadequados.</span><span class="sxs-lookup"><span data-stu-id="77ae6-185">By configuring multi-site listeners first, this configuration reduces hello chance that traffic is routed toohello inappropriate backend.</span></span> <span data-ttu-id="77ae6-186">Esse problema de roteamento pode ocorrer enquanto a regra básica Olá corresponderia tráfego com base em regra de multissite toohello anterior de porta que está sendo avaliada.</span><span class="sxs-lookup"><span data-stu-id="77ae6-186">This routing issue can occur as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="77ae6-187">**P. O que o campo do Host Olá para testes personalizados significam?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-187">**Q. What does hello Host field for custom probes signify?**</span></span>

<span data-ttu-id="77ae6-188">O campo do host Especifica Olá nome toosend Olá a investigação.</span><span class="sxs-lookup"><span data-stu-id="77ae6-188">Host field specifies hello name toosend hello probe to.</span></span> <span data-ttu-id="77ae6-189">Aplicável somente quando vários sites são configurados no Gateway de Aplicativo; do contrário, use '127.0.0.1'.</span><span class="sxs-lookup"><span data-stu-id="77ae6-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="77ae6-190">Esse valor é diferente do nome de host da VM e está no formato \<protocolo\>://\<host\>:\<porta\>\<caminho\>.</span><span class="sxs-lookup"><span data-stu-id="77ae6-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="77ae6-191">**P. É possível lista branca Application Gateway acesso tooa alguns IPs de origem?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-191">**Q. Can I whitelist Application Gateway access tooa few source IPs?**</span></span>

<span data-ttu-id="77ae6-192">Esse cenário pode ser feito usando os NSGs na sub-rede de Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77ae6-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="77ae6-193">Olá restrições a seguir deve ser colocado na sub-rede Olá Olá listado ordem de prioridade:</span><span class="sxs-lookup"><span data-stu-id="77ae6-193">hello following restrictions should be put on hello subnet in hello listed order of priority:</span></span>

* <span data-ttu-id="77ae6-194">Permitir tráfego de entrada de intervalo de IP/IP de origem.</span><span class="sxs-lookup"><span data-stu-id="77ae6-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="77ae6-195">Permitir solicitações de entrada de todas as fontes tooports 65534 65503 para [comunicação de integridade de back-end](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="77ae6-195">Allow incoming requests from all sources tooports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="77ae6-196">Permitir entradas investigações do balanceador de carga do Azure (marca AzureLoadBalancer) e tráfego de rede virtual (marca VirtualNetwork) em Olá [NSG](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="77ae6-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on hello [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="77ae6-197">Bloquear todo o outro tráfego de entrada com um Negar todas as regras.</span><span class="sxs-lookup"><span data-stu-id="77ae6-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="77ae6-198">Permitir tráfego de saída toohello internet para todos os destinos.</span><span class="sxs-lookup"><span data-stu-id="77ae6-198">Allow outbound traffic toohello internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="77ae6-199">Desempenho</span><span class="sxs-lookup"><span data-stu-id="77ae6-199">Performance</span></span>

<span data-ttu-id="77ae6-200">**P. Como o Gateway de Aplicativo oferece suporte a alta disponibilidade e escalabilidade?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="77ae6-201">O Gateway de Aplicativo dará suporte a cenários de alta disponibilidade quando você tiver duas ou mais instâncias implantadas.</span><span class="sxs-lookup"><span data-stu-id="77ae6-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="77ae6-202">Azure distribui essas instâncias por atualização e falha tooensure domínios que todas as instâncias não falham em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="77ae6-202">Azure distributes these instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="77ae6-203">Application Gateway oferece suporte à escalabilidade adicionando várias instâncias do hello mesma carga de saudação tooshare de gateway.</span><span class="sxs-lookup"><span data-stu-id="77ae6-203">Application Gateway supports scalability by adding multiple instances of hello same gateway tooshare hello load.</span></span>

<span data-ttu-id="77ae6-204">**P. Como posso obter o cenário de recuperação de desastres em data centers com o Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="77ae6-205">Os clientes podem usar o Traffic Manager toodistribute tráfego entre vários Gateways de aplicativo em diferentes data centers.</span><span class="sxs-lookup"><span data-stu-id="77ae6-205">Customers can use Traffic Manager toodistribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="77ae6-206">**P. Há suporte para o dimensionamento automático?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="77ae6-207">Não, mas Application Gateway tem uma métrica de taxa de transferência que pode ser usado tooalert quando um limite for atingido.</span><span class="sxs-lookup"><span data-stu-id="77ae6-207">No, but Application Gateway has a throughput metric that can be used tooalert you when a threshold is reached.</span></span> <span data-ttu-id="77ae6-208">Manualmente adicionando instâncias ou alterando o tamanho não reinicie o gateway de saudação e não afeta o tráfego existente.</span><span class="sxs-lookup"><span data-stu-id="77ae6-208">Manually adding instances or changing size does not restart hello gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="77ae6-209">**P. A escala/redução vertical causa tempo de inatividade?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="77ae6-210">Não há tempo de inatividade, as instâncias são distribuídas entre domínios de atualização e domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="77ae6-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="77ae6-211">**P. Pode alterar o tamanho da instância de médio toolarge sem interrupção?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-211">**Q. Can I change instance size from medium toolarge without disruption?**</span></span>

<span data-ttu-id="77ae6-212">Sim, o Azure distribui instâncias por atualização e falha tooensure domínios que todas as instâncias não falham em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="77ae6-212">Yes, Azure distributes instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="77ae6-213">Aplicativo Gateway oferece suporte ao dimensionamento adicionando várias instâncias do hello mesmo gateway tooshare Olá de carga.</span><span class="sxs-lookup"><span data-stu-id="77ae6-213">Application Gateway supports scaling by adding multiple instances of hello same gateway tooshare hello load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="77ae6-214">Configuração de SSL</span><span class="sxs-lookup"><span data-stu-id="77ae6-214">SSL Configuration</span></span>

<span data-ttu-id="77ae6-215">**P. Quais certificados têm suporte no Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="77ae6-216">Certificados autoassinados, certificados de autoridade de certificação e certificados curinga têm suporte.</span><span class="sxs-lookup"><span data-stu-id="77ae6-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="77ae6-217">Não há suporte para certificados EV.</span><span class="sxs-lookup"><span data-stu-id="77ae6-217">EV certs are not supported.</span></span>

<span data-ttu-id="77ae6-218">**P. Quais são os conjuntos de codificação atual Olá suportados pelo Gateway de aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-218">**Q. What are hello current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="77ae6-219">Olá seguem Olá atual codificação que recebe suportada pelo gateway do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77ae6-219">hello following are hello current cipher suites supported by application gateway.</span></span> <span data-ttu-id="77ae6-220">Visite: [configurar SSL versões de política e conjuntos de codificação no Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn como toocustomize opções de SSL.</span><span class="sxs-lookup"><span data-stu-id="77ae6-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn how toocustomize SSL options.</span></span>

- <span data-ttu-id="77ae6-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="77ae6-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="77ae6-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="77ae6-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="77ae6-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="77ae6-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="77ae6-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="77ae6-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="77ae6-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="77ae6-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="77ae6-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="77ae6-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="77ae6-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="77ae6-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="77ae6-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="77ae6-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="77ae6-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="77ae6-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="77ae6-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="77ae6-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="77ae6-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="77ae6-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="77ae6-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="77ae6-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="77ae6-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="77ae6-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="77ae6-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="77ae6-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="77ae6-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="77ae6-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="77ae6-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="77ae6-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="77ae6-247">**P. Application Gateway também suporta o back-end toohello de tráfego criptografado?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-247">**Q. Does Application Gateway also support re-encryption of traffic toohello backend?**</span></span>

<span data-ttu-id="77ae6-248">Sim, descarregamento SSL do Application Gateway oferece suporte e final tooend SSL, que criptografa novamente back-end toohello de tráfego hello.</span><span class="sxs-lookup"><span data-stu-id="77ae6-248">Yes, Application Gateway supports SSL offload, and end tooend SSL, which re-encrypts hello traffic toohello backend.</span></span>

<span data-ttu-id="77ae6-249">**P. Pode configurar versões de protocolo SSL do SSL política toocontrol?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-249">**Q. Can I configure SSL policy toocontrol SSL Protocol versions?**</span></span>

<span data-ttu-id="77ae6-250">Sim, você pode configurar o Application Gateway toodeny TLS 1.0 por, 1.1 e TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="77ae6-250">Yes, you can configure Application Gateway toodeny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="77ae6-251">SSL 2.0 e 3.0 já estão desabilitados por padrão e não são configuráveis.</span><span class="sxs-lookup"><span data-stu-id="77ae6-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="77ae6-252">**P. Posso configurar conjuntos de codificação e a ordem de política?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="77ae6-253">Sim, há suporte para [configuração de conjuntos de criptografia](application-gateway-ssl-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77ae6-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="77ae6-254">Ao definir uma política personalizada, pelo menos uma das Olá conjuntos de codificação a seguir deve ser habilitada.</span><span class="sxs-lookup"><span data-stu-id="77ae6-254">When defining a custom policy, at least one of hello following cipher suites must be enabled.</span></span> <span data-ttu-id="77ae6-255">Gateway de aplicativo usa o gerenciamento de back-end de toofor SHA256.</span><span class="sxs-lookup"><span data-stu-id="77ae6-255">Application gateway uses SHA256 toofor backend management.</span></span>

* <span data-ttu-id="77ae6-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="77ae6-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="77ae6-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="77ae6-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="77ae6-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="77ae6-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="77ae6-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="77ae6-262">**P. Há suporte para quantos certificados SSL?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="77ae6-263">O SSL too20 certificados têm suporte.</span><span class="sxs-lookup"><span data-stu-id="77ae6-263">Up too20 SSL certificates are supported.</span></span>

<span data-ttu-id="77ae6-264">**P. Quantos certificados de autenticação para nova criptografia de back-end têm suporte?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="77ae6-265">Backup too10 certificados de autenticação são compatíveis com um padrão de 5.</span><span class="sxs-lookup"><span data-stu-id="77ae6-265">Up too10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="77ae6-266">**P. O Gateway de Aplicativo é integrado ao Azure Key Vault de forma nativa?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="77ae6-267">Não, ele não é integrado ao Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="77ae6-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="77ae6-268">Configuração de WAF (Firewall de Aplicativo Web)</span><span class="sxs-lookup"><span data-stu-id="77ae6-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="77ae6-269">**P. Olá SKU WAF oferece todos os recursos de saudação disponíveis com hello SKU padrão?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-269">**Q. Does hello WAF SKU offer all hello features available with hello Standard SKU?**</span></span>

<span data-ttu-id="77ae6-270">Sim, WAF dá suporte a todos os recursos de saudação em Olá SKU padrão.</span><span class="sxs-lookup"><span data-stu-id="77ae6-270">Yes, WAF supports all hello features in hello Standard SKU.</span></span>

<span data-ttu-id="77ae6-271">**P. Qual é versão CRS Olá que Application Gateway oferece suporte?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-271">**Q. What is hello CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="77ae6-272">O Gateway de Aplicativo dá suporte a CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e a CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="77ae6-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="77ae6-273">**P. Como monitorar o WAF?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="77ae6-274">O WAF é monitorado por meio do log de diagnóstico. Encontre mais informações sobre o log de diagnóstico em [Log de diagnósticos e métricas para o Gateway de Aplicativo](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="77ae6-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="77ae6-275">**P. O modo de detecção bloqueia o tráfego?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="77ae6-276">Não, o modo de detecção apenas registra o tráfego em log, o que dispara uma regra WAF.</span><span class="sxs-lookup"><span data-stu-id="77ae6-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="77ae6-277">**P. Como posso personalizar regras WAF?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="77ae6-278">Sim, regras de WAF são personalizáveis, para obter mais informações sobre como toocustomize-los visite [WAF personalizar regras e grupos de regras](application-gateway-customize-waf-rules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="77ae6-278">Yes, WAF rules are customizable, for more information on how toocustomize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="77ae6-279">**P. Quais regras estão disponíveis no momento?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="77ae6-280">WAF atualmente suporta CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), que fornecem segurança de linha de base em relação a maioria das Olá vulnerabilidades de 10 principais identificadas pelo Olá abra Web aplicativo segurança projeto (OWASP) encontrada aqui [OWASP top 10 vulnerabilidades](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="77ae6-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of hello top 10 vulnerabilities identified by hello Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="77ae6-281">Proteção contra injeção de SQL</span><span class="sxs-lookup"><span data-stu-id="77ae6-281">SQL injection protection</span></span>

* <span data-ttu-id="77ae6-282">Proteção contra scripts entre sites</span><span class="sxs-lookup"><span data-stu-id="77ae6-282">Cross site scripting protection</span></span>

* <span data-ttu-id="77ae6-283">Proteção Contra Ataques Comuns da Web, como a injeção de comandos, as solicitações HTTP indesejadas, a divisão de resposta HTTP e o ataque de inclusão de arquivo remoto</span><span class="sxs-lookup"><span data-stu-id="77ae6-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="77ae6-284">Proteção contra violações de protocolo HTTP</span><span class="sxs-lookup"><span data-stu-id="77ae6-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="77ae6-285">Proteção contra anomalias de protocolo HTTP, como ausência de host de agente do usuário e de cabeçalhos de aceitação</span><span class="sxs-lookup"><span data-stu-id="77ae6-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="77ae6-286">Prevenção contra bots, rastreadores e scanners</span><span class="sxs-lookup"><span data-stu-id="77ae6-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="77ae6-287">Detecção de problemas de configuração de aplicativo comuns (ou seja, Apache, IIS etc.)</span><span class="sxs-lookup"><span data-stu-id="77ae6-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="77ae6-288">**P. O WAF também oferece suporte à prevenção de DDoS?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="77ae6-289">Não, o WAF não oferece prevenção de DDoS.</span><span class="sxs-lookup"><span data-stu-id="77ae6-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="77ae6-290">Diagnóstico e registro em log</span><span class="sxs-lookup"><span data-stu-id="77ae6-290">Diagnostics and Logging</span></span>

<span data-ttu-id="77ae6-291">**P. Quais tipos de logs estão disponíveis com o Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="77ae6-292">Há três logs disponíveis para o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77ae6-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="77ae6-293">Para saber mais sobre esses logs e outros recursos de diagnóstico, visite [Integridade de back-end, logs de diagnóstico e métricas para o Gateway de Aplicativo](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="77ae6-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="77ae6-294">**ApplicationGatewayAccessLog** -log de acesso Olá contém cada solicitação enviada toohello Application Gateway front-end.</span><span class="sxs-lookup"><span data-stu-id="77ae6-294">**ApplicationGatewayAccessLog** - hello access log contains each request submitted toohello Application Gateway frontend.</span></span> <span data-ttu-id="77ae6-295">dados de saudação incluem IP do chamador Olá, URL solicitada, latência de resposta, retornam o código, bytes de entrada e saída. O log de acesso é coletado a cada 300 segundos.</span><span class="sxs-lookup"><span data-stu-id="77ae6-295">hello data includes hello caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="77ae6-296">Esse log contém um registro por instância do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77ae6-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="77ae6-297">**ApplicationGatewayPerformanceLog** -log de desempenho Olá captura informações de desempenho de base por instância incluindo solicitação total atendida, a taxa de transferência em bytes, o total de solicitações atendidas, contagem de solicitação com falha, com e sem integridade Contagem de instâncias de back-end.</span><span class="sxs-lookup"><span data-stu-id="77ae6-297">**ApplicationGatewayPerformanceLog** - hello performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="77ae6-298">**ApplicationGatewayFirewallLog** -log de firewall Olá contém solicitações que são registradas por meio do modo de detecção ou prevenção de um gateway de aplicativo que é configurado com o firewall do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="77ae6-298">**ApplicationGatewayFirewallLog** - hello firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="77ae6-299">**P. Como saber se os membros de meu pool de back-end estão íntegros?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="77ae6-300">Você pode usar o cmdlet do PowerShell Olá `Get-AzureRmApplicationGatewayBackendHealth` ou verificar a integridade por meio do portal Olá visitando [diagnóstico de Gateway do aplicativo](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="77ae6-300">You can use hello PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through hello portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="77ae6-301">**P. O que é a política de retenção Olá Olá logs de diagnóstico?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-301">**Q. What is hello retention policy on hello diagnostics logs?**</span></span>

<span data-ttu-id="77ae6-302">Conta de armazenamento do fluxo toohello clientes de logs de diagnóstico e os clientes podem definir a política de retenção de saudação com base em suas preferências.</span><span class="sxs-lookup"><span data-stu-id="77ae6-302">Diagnostic logs flow toohello customers storage account and customers can set hello retention policy based on their preference.</span></span> <span data-ttu-id="77ae6-303">Logs de diagnóstico também podem ser enviados tooan Hub de eventos ou análise de Log.</span><span class="sxs-lookup"><span data-stu-id="77ae6-303">Diagnostic logs can also be sent tooan Event Hub or Log Analytics.</span></span> <span data-ttu-id="77ae6-304">Visite [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="77ae6-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="77ae6-305">**P. Como posso obter logs de auditoria para o Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="77ae6-306">Os logs de auditoria estão disponíveis para o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77ae6-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="77ae6-307">No portal de saudação, clique em **Log de atividades** na folha de menu de saudação de um log de auditoria do Application Gateway tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="77ae6-307">In hello portal, click **Activity Log** in hello menu blade of an Application Gateway tooaccess hello audit log.</span></span> 

<span data-ttu-id="77ae6-308">**P. Posso configurar alertas com o Gateway de Aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="77ae6-309">Sim, o Gateway de Aplicativo oferece suporte a alertas, e os alertas são configurados com base em métricas.</span><span class="sxs-lookup"><span data-stu-id="77ae6-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="77ae6-310">Application Gateway tem uma métrica de "taxa de transferência de", que pode ser tooalert configurado no momento.</span><span class="sxs-lookup"><span data-stu-id="77ae6-310">Application Gateway currently has a metric of "throughput", which can be configured tooalert.</span></span> <span data-ttu-id="77ae6-311">toolearn mais sobre alertas, visite [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="77ae6-311">toolearn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="77ae6-312">**P. A integridade do back-end retorna um status desconhecido, o que pode estar causando esse status?**</span><span class="sxs-lookup"><span data-stu-id="77ae6-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="77ae6-313">motivo mais comum de saudação é back-end toohello de acesso está sendo bloqueado por um NSG ou DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="77ae6-313">hello most common reason is access toohello backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="77ae6-314">Visite [back-end integridade, o log de diagnóstico e métricas para o Application Gateway](application-gateway-diagnostics.md) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="77ae6-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77ae6-315">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77ae6-315">Next Steps</span></span>

<span data-ttu-id="77ae6-316">toolearn mais sobre o Application Gateway visite [tooApplication Introdução Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="77ae6-316">toolearn more about Application Gateway visit [Introduction tooApplication Gateway](application-gateway-introduction.md).</span></span>
