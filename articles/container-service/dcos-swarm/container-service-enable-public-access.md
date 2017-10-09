---
title: "o aplicativo de contêiner do aaaEnable access tooAzure DC/sistema operacional | Microsoft Docs"
description: "Como público tooenable acessar contêineres tooDC/sistema operacional no serviço de contêiner do Azure."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a><span data-ttu-id="6fac4-104">Habilitar o aplicativo de serviço de contêiner do Azure tooan acesso público</span><span class="sxs-lookup"><span data-stu-id="6fac4-104">Enable public access tooan Azure Container Service application</span></span>
<span data-ttu-id="6fac4-105">Qualquer contêiner de DC/OS em Olá ACS [pool de agente pública](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) é exposto automaticamente toohello internet.</span><span class="sxs-lookup"><span data-stu-id="6fac4-105">Any DC/OS container in hello ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed toohello internet.</span></span> <span data-ttu-id="6fac4-106">Por padrão, as portas **80**, **443**, **8080** estão abertas e qualquer contêiner (público) que esteja ouvindo nessas portas estará acessível.</span><span class="sxs-lookup"><span data-stu-id="6fac4-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="6fac4-107">Este artigo mostra como tooopen mais portas para seus aplicativos no serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="6fac4-107">This article shows you how tooopen more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="6fac4-108">Abrir uma porta (portal)</span><span class="sxs-lookup"><span data-stu-id="6fac4-108">Open a port (portal)</span></span>
<span data-ttu-id="6fac4-109">Primeiro, precisamos de porta de saudação tooopen que desejamos.</span><span class="sxs-lookup"><span data-stu-id="6fac4-109">First, we need tooopen hello port we want.</span></span>

1. <span data-ttu-id="6fac4-110">Faça logon no portal de toohello.</span><span class="sxs-lookup"><span data-stu-id="6fac4-110">Log in toohello portal.</span></span>
2. <span data-ttu-id="6fac4-111">Grupo de recursos de saudação localizar implantado Olá serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="6fac4-111">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="6fac4-112">Selecione o balanceador de carga do agente de saudação (que é chamado semelhante muito**agente XXXX-XXXX lb**).</span><span class="sxs-lookup"><span data-stu-id="6fac4-112">Select hello agent load balancer (which is named similar too**XXXX-agent-lb-XXXX**).</span></span>
   
    ![Balanceador de carga do serviço de contêiner do Azure](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="6fac4-114">Clique em **Investigações** e então em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6fac4-114">Click **Probes** and then **Add**.</span></span>
   
    ![Investigações do balanceador de carga do serviço de contêiner do Azure](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="6fac4-116">Preencha o formulário de investigação de saudação e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="6fac4-116">Fill out hello probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="6fac4-117">Campo</span><span class="sxs-lookup"><span data-stu-id="6fac4-117">Field</span></span> | <span data-ttu-id="6fac4-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="6fac4-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="6fac4-119">Nome</span><span class="sxs-lookup"><span data-stu-id="6fac4-119">Name</span></span> |<span data-ttu-id="6fac4-120">Um nome descritivo da investigação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fac4-120">A descriptive name of hello probe.</span></span> |
   | <span data-ttu-id="6fac4-121">Porta</span><span class="sxs-lookup"><span data-stu-id="6fac4-121">Port</span></span> |<span data-ttu-id="6fac4-122">porta Olá Olá tootest de contêiner.</span><span class="sxs-lookup"><span data-stu-id="6fac4-122">hello port of hello container tootest.</span></span> |
   | <span data-ttu-id="6fac4-123">Caminho</span><span class="sxs-lookup"><span data-stu-id="6fac4-123">Path</span></span> |<span data-ttu-id="6fac4-124">(Quando estiver no modo de HTTP) Olá tooprobe de caminho relativo do site.</span><span class="sxs-lookup"><span data-stu-id="6fac4-124">(When in HTTP mode) hello relative website path tooprobe.</span></span> <span data-ttu-id="6fac4-125">Não há suporte para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6fac4-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="6fac4-126">Intervalo</span><span class="sxs-lookup"><span data-stu-id="6fac4-126">Interval</span></span> |<span data-ttu-id="6fac4-127">quantidade de saudação de tempo entre a investigação tentativas, em segundos.</span><span class="sxs-lookup"><span data-stu-id="6fac4-127">hello amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="6fac4-128">Limite não íntegro</span><span class="sxs-lookup"><span data-stu-id="6fac4-128">Unhealthy threshold</span></span> |<span data-ttu-id="6fac4-129">Número de investigação consecutivas tentativas antes de considerar o contêiner de saudação não íntegro.</span><span class="sxs-lookup"><span data-stu-id="6fac4-129">Number of consecutive probe attempts before considering hello container unhealthy.</span></span> |
6. <span data-ttu-id="6fac4-130">Volta na propriedades Olá Olá agente do balanceador de carga, clique em **regras de balanceamento de carga** e **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6fac4-130">Back at hello properties of hello agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Regras do balanceador de carga do serviço de contêiner do Azure](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="6fac4-132">Preencha o formulário de Balanceador de carga hello e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="6fac4-132">Fill out hello load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="6fac4-133">Campo</span><span class="sxs-lookup"><span data-stu-id="6fac4-133">Field</span></span> | <span data-ttu-id="6fac4-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="6fac4-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="6fac4-135">Nome</span><span class="sxs-lookup"><span data-stu-id="6fac4-135">Name</span></span> |<span data-ttu-id="6fac4-136">Um nome descritivo saudação do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6fac4-136">A descriptive name of hello load balancer.</span></span> |
   | <span data-ttu-id="6fac4-137">Porta</span><span class="sxs-lookup"><span data-stu-id="6fac4-137">Port</span></span> |<span data-ttu-id="6fac4-138">porta de entrada de saudação pública.</span><span class="sxs-lookup"><span data-stu-id="6fac4-138">hello public incoming port.</span></span> |
   | <span data-ttu-id="6fac4-139">Porta de back-end</span><span class="sxs-lookup"><span data-stu-id="6fac4-139">Backend port</span></span> |<span data-ttu-id="6fac4-140">porta de público interno Olá Olá contêiner tooroute do tráfego de para.</span><span class="sxs-lookup"><span data-stu-id="6fac4-140">hello internal-public port of hello container tooroute traffic to.</span></span> |
   | <span data-ttu-id="6fac4-141">Pool de back-end</span><span class="sxs-lookup"><span data-stu-id="6fac4-141">Backend pool</span></span> |<span data-ttu-id="6fac4-142">contêineres de saudação do pool será o destino de saudação para este balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6fac4-142">hello containers in this pool will be hello target for this load balancer.</span></span> |
   | <span data-ttu-id="6fac4-143">Investigação</span><span class="sxs-lookup"><span data-stu-id="6fac4-143">Probe</span></span> |<span data-ttu-id="6fac4-144">Olá toodetermine investigação usada se um destino em Olá **pool de back-end** está íntegro.</span><span class="sxs-lookup"><span data-stu-id="6fac4-144">hello probe used toodetermine if a target in hello **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="6fac4-145">Persistência de sessão</span><span class="sxs-lookup"><span data-stu-id="6fac4-145">Session persistence</span></span> |<span data-ttu-id="6fac4-146">Determina como o tráfego de um cliente deve ser tratado durante Olá Olá sessão de.</span><span class="sxs-lookup"><span data-stu-id="6fac4-146">Determines how traffic from a client should be handled for hello duration of hello session.</span></span><br><br><span data-ttu-id="6fac4-147">**Nenhum**: solicitações sucessivas do mesmo cliente pode ser tratado por qualquer contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fac4-147">**None**: Successive requests from hello same client can be handled by any container.</span></span><br><span data-ttu-id="6fac4-148">**Cliente IP**: Olá de solicitações sucessivas do hello mesmo IP do cliente são manipuladas pelo mesmo contêiner.</span><span class="sxs-lookup"><span data-stu-id="6fac4-148">**Client IP**: Successive requests from hello same client IP are handled by hello same container.</span></span><br><span data-ttu-id="6fac4-149">**Cliente IP e protocolo**: Olá de solicitações sucessivas do hello a mesma combinação de IP e protocolo de cliente são manipuladas pelo mesmo contêiner.</span><span class="sxs-lookup"><span data-stu-id="6fac4-149">**Client IP and protocol**: Successive requests from hello same client IP and protocol combination are handled by hello same container.</span></span> |
   | <span data-ttu-id="6fac4-150">Tempo limite de ociosidade</span><span class="sxs-lookup"><span data-stu-id="6fac4-150">Idle timeout</span></span> |<span data-ttu-id="6fac4-151">(Somente TCP) Em minutos, Olá tookeep tempo abrir um cliente TCP/HTTP sem depender de *keep-alive* mensagens.</span><span class="sxs-lookup"><span data-stu-id="6fac4-151">(TCP only) In minutes, hello time tookeep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="6fac4-152">Adicionar uma regra de segurança (portal)</span><span class="sxs-lookup"><span data-stu-id="6fac4-152">Add a security rule (portal)</span></span>
<span data-ttu-id="6fac4-153">Em seguida, precisamos tooadd uma regra de segurança que roteia o tráfego de nosso porta aberta por meio de firewall de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fac4-153">Next, we need tooadd a security rule that routes traffic from our opened port through hello firewall.</span></span>

1. <span data-ttu-id="6fac4-154">Faça logon no portal de toohello.</span><span class="sxs-lookup"><span data-stu-id="6fac4-154">Log in toohello portal.</span></span>
2. <span data-ttu-id="6fac4-155">Grupo de recursos de saudação localizar implantado Olá serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="6fac4-155">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="6fac4-156">Selecione Olá **pública** grupo de segurança de rede do agente (que é chamado semelhante muito**XXXX-agente-público-nsg-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="6fac4-156">Select hello **public** agent network security group (which is named similar too**XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Grupo de segurança de rede do serviço de contêiner do Azure](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="6fac4-158">Selecione **Regras de segurança de entrada** e **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6fac4-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Regras do grupo de segurança de rede do serviço de contêiner do Azure](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="6fac4-160">Insira a porta pública Olá tooallow de regra de firewall e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="6fac4-160">Fill out hello firewall rule tooallow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="6fac4-161">Campo</span><span class="sxs-lookup"><span data-stu-id="6fac4-161">Field</span></span> | <span data-ttu-id="6fac4-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="6fac4-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="6fac4-163">Nome</span><span class="sxs-lookup"><span data-stu-id="6fac4-163">Name</span></span> |<span data-ttu-id="6fac4-164">Um nome descritivo Olá de regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="6fac4-164">A descriptive name of hello firewall rule.</span></span> |
   | <span data-ttu-id="6fac4-165">Prioridade</span><span class="sxs-lookup"><span data-stu-id="6fac4-165">Priority</span></span> |<span data-ttu-id="6fac4-166">Classificação de prioridade para a regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fac4-166">Priority rank for hello rule.</span></span> <span data-ttu-id="6fac4-167">Olá inferior Olá número Olá Olá prioridade.</span><span class="sxs-lookup"><span data-stu-id="6fac4-167">hello lower hello number hello higher hello priority.</span></span> |
   | <span data-ttu-id="6fac4-168">Fonte</span><span class="sxs-lookup"><span data-stu-id="6fac4-168">Source</span></span> |<span data-ttu-id="6fac4-169">Restringir Olá entrada IP endereço intervalo toobe permitido ou negado por essa regra.</span><span class="sxs-lookup"><span data-stu-id="6fac4-169">Restrict hello incoming IP address range toobe allowed or denied by this rule.</span></span> <span data-ttu-id="6fac4-170">Use **qualquer** toonot especificam uma restrição.</span><span class="sxs-lookup"><span data-stu-id="6fac4-170">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="6fac4-171">O Barramento de</span><span class="sxs-lookup"><span data-stu-id="6fac4-171">Service</span></span> |<span data-ttu-id="6fac4-172">Selecione um conjunto de serviços predefinidos para os quais foi definida essa regra de segurança.</span><span class="sxs-lookup"><span data-stu-id="6fac4-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="6fac4-173">Caso contrário, use **personalizado** toocreate seus próprios.</span><span class="sxs-lookup"><span data-stu-id="6fac4-173">Otherwise use **Custom** toocreate your own.</span></span> |
   | <span data-ttu-id="6fac4-174">Protocolo</span><span class="sxs-lookup"><span data-stu-id="6fac4-174">Protocol</span></span> |<span data-ttu-id="6fac4-175">Restrinja o tráfego baseado em **TCP** ou **UDP**.</span><span class="sxs-lookup"><span data-stu-id="6fac4-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="6fac4-176">Use **qualquer** toonot especificam uma restrição.</span><span class="sxs-lookup"><span data-stu-id="6fac4-176">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="6fac4-177">Intervalo de portas</span><span class="sxs-lookup"><span data-stu-id="6fac4-177">Port range</span></span> |<span data-ttu-id="6fac4-178">Quando **Service** é **personalizado**, especifica o intervalo de saudação de portas que essa regra afeta.</span><span class="sxs-lookup"><span data-stu-id="6fac4-178">When **Service** is **Custom**, specifies hello range of ports that this rule affects.</span></span> <span data-ttu-id="6fac4-179">Você pode usar uma única porta, como **80** ou um intervalo, como **1024–1500**.</span><span class="sxs-lookup"><span data-stu-id="6fac4-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="6fac4-180">Ação</span><span class="sxs-lookup"><span data-stu-id="6fac4-180">Action</span></span> |<span data-ttu-id="6fac4-181">Permitir ou negar o tráfego que atenda aos critérios de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fac4-181">Allow or deny traffic that meets hello criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6fac4-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6fac4-182">Next steps</span></span>
<span data-ttu-id="6fac4-183">Saiba mais sobre a diferença de saudação entre [públicos e privados agentes de DC/OS](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="6fac4-183">Learn about hello difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="6fac4-184">Leia mais informações sobre [como gerenciar seus contêineres de DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="6fac4-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

