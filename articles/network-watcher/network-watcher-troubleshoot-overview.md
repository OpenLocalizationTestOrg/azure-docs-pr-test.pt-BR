---
title: tooresource aaaIntroduction Solucionando problemas do observador de rede do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral dos recursos de solução de problemas do recurso Olá observador de rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="454ed-103">Introdução tooresource Solucionando problemas do observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="454ed-103">Introduction tooresource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="454ed-104">Os Gateways de Rede Virtual fornecem conectividade entre os recursos locais e outras redes virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="454ed-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="454ed-105">Esses gateways e suas conexões de monitoramento é fundamental tooensuring comunicação não é interrompida.</span><span class="sxs-lookup"><span data-stu-id="454ed-105">Monitoring these gateways and their Connections is critical tooensuring communication is not broken.</span></span> <span data-ttu-id="454ed-106">Observador de rede fornece Olá recurso tootroubleshoot Gateways de rede Virtual e conexões.</span><span class="sxs-lookup"><span data-stu-id="454ed-106">Network Watcher provides hello capability tootroubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="454ed-107">Isso pode ser chamado por meio do portal de saudação, o PowerShell, CLI ou API REST.</span><span class="sxs-lookup"><span data-stu-id="454ed-107">This can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="454ed-108">Quando chamado, o observador de rede diagnostica integridade de saudação do gateway de rede virtual hello ou conexão e resultados de retorno Olá apropriado.</span><span class="sxs-lookup"><span data-stu-id="454ed-108">When called, Network Watcher diagnoses hello health of hello virtual network gateway or connection and return hello appropriate results.</span></span> <span data-ttu-id="454ed-109">Essa solicitação é uma transação de longa execução, resultados de saudação são retornados após a conclusão do diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-109">This request is a long running transaction, hello results are returned once hello diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="454ed-111">Resultados</span><span class="sxs-lookup"><span data-stu-id="454ed-111">Results</span></span>

<span data-ttu-id="454ed-112">resultados de preliminar Olá retornados dão uma visão geral da integridade de saudação do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-112">hello preliminary results returned give an overall picture of hello health of hello resource.</span></span> <span data-ttu-id="454ed-113">Mais informações podem ser fornecidas para recursos, conforme mostrado no hello seção a seguir:</span><span class="sxs-lookup"><span data-stu-id="454ed-113">Deeper information can be provided for resources as shown in hello following section:</span></span>

<span data-ttu-id="454ed-114">Olá lista a seguir é valores hello retornados com hello solucionar problemas de API:</span><span class="sxs-lookup"><span data-stu-id="454ed-114">hello following list is hello values returned with hello troubleshoot API:</span></span>

* <span data-ttu-id="454ed-115">**startTime** -este valor é tempo de saudação Olá solucionar chamada à API iniciada.</span><span class="sxs-lookup"><span data-stu-id="454ed-115">**startTime** - This value is hello time hello troubleshoot API call started.</span></span>
* <span data-ttu-id="454ed-116">**endTime** -esse valor é o tempo de saudação quando a solução de problemas de saudação terminou.</span><span class="sxs-lookup"><span data-stu-id="454ed-116">**endTime** - This value is hello time when hello troubleshooting ended.</span></span>
* <span data-ttu-id="454ed-117">**cod** - esse valor não é apresentado como UnHealthy (não íntegro), se houver uma única falha de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="454ed-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="454ed-118">**resultados** -resultados é um conjunto de resultados retornados no gateway de rede virtual de Conexão ou Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="454ed-118">**results** - Results is a collection of results returned on hello Connection or hello virtual network gateway.</span></span>
    * <span data-ttu-id="454ed-119">**ID** -este valor é o tipo de falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-119">**id** - This value is hello fault type.</span></span>
    * <span data-ttu-id="454ed-120">**Resumo** -esse valor é um resumo das falhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-120">**summary** - This value is a summary of hello fault.</span></span>
    * <span data-ttu-id="454ed-121">**detalhadas** -esse valor fornece uma descrição detalhada da falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-121">**detailed** - This value provides a detailed description of hello fault.</span></span>
    * <span data-ttu-id="454ed-122">**recommendedActions** -essa propriedade é uma coleção de ações recomendadas tootake.</span><span class="sxs-lookup"><span data-stu-id="454ed-122">**recommendedActions** - This property is a collection of recommended actions tootake.</span></span>
      * <span data-ttu-id="454ed-123">**actionText** -esse valor contém o texto de saudação que descreve quais tootake de ação.</span><span class="sxs-lookup"><span data-stu-id="454ed-123">**actionText** - This value contains hello text describing what action tootake.</span></span>
      * <span data-ttu-id="454ed-124">**actionUri** -esse valor fornece Olá URI toodocumentation sobre como tooact.</span><span class="sxs-lookup"><span data-stu-id="454ed-124">**actionUri** - This value provides hello URI toodocumentation on how tooact.</span></span>
      * <span data-ttu-id="454ed-125">**actionUriText** -esse valor é uma breve descrição de texto de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-125">**actionUriText** - This value is a short description of hello action text.</span></span>

<span data-ttu-id="454ed-126">Olá seguintes tabelas Mostrar Olá falha diferentes tipos (id em resultados de saudação anterior lista) que estão disponíveis e se a falha de saudação cria logs.</span><span class="sxs-lookup"><span data-stu-id="454ed-126">hello following tables show hello different fault types (id under results from hello preceding list) that are available and if hello fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="454ed-127">Gateway</span><span class="sxs-lookup"><span data-stu-id="454ed-127">Gateway</span></span>

| <span data-ttu-id="454ed-128">Tipo de Falha</span><span class="sxs-lookup"><span data-stu-id="454ed-128">Fault Type</span></span> | <span data-ttu-id="454ed-129">Motivo</span><span class="sxs-lookup"><span data-stu-id="454ed-129">Reason</span></span> | <span data-ttu-id="454ed-130">Registro</span><span class="sxs-lookup"><span data-stu-id="454ed-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="454ed-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="454ed-131">NoFault</span></span> | <span data-ttu-id="454ed-132">Quando nenhum erro é detectado.</span><span class="sxs-lookup"><span data-stu-id="454ed-132">When no error is detected.</span></span> |<span data-ttu-id="454ed-133">Sim</span><span class="sxs-lookup"><span data-stu-id="454ed-133">Yes</span></span>|
| <span data-ttu-id="454ed-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="454ed-134">GatewayNotFound</span></span> | <span data-ttu-id="454ed-135">Não é possível localizar o Gateway ou o Gateway não está provisionado.</span><span class="sxs-lookup"><span data-stu-id="454ed-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="454ed-136">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-136">No</span></span>|
| <span data-ttu-id="454ed-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="454ed-137">PlannedMaintenance</span></span> |  <span data-ttu-id="454ed-138">A instância do gateway está em manutenção.</span><span class="sxs-lookup"><span data-stu-id="454ed-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="454ed-139">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-139">No</span></span>|
| <span data-ttu-id="454ed-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="454ed-140">UserDrivenUpdate</span></span> | <span data-ttu-id="454ed-141">Uma atualização de um usuário está em andamento.</span><span class="sxs-lookup"><span data-stu-id="454ed-141">When a user update is in progress.</span></span> <span data-ttu-id="454ed-142">Isso pode ser uma operação de redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="454ed-142">This could be a resize operation.</span></span> | <span data-ttu-id="454ed-143">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-143">No</span></span> |
| <span data-ttu-id="454ed-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="454ed-144">VipUnResponsive</span></span> | <span data-ttu-id="454ed-145">É possível acessar a instância primária de saudação do hello Gateway.</span><span class="sxs-lookup"><span data-stu-id="454ed-145">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="454ed-146">Isso acontece quando ocorre falha na investigação de integridade de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-146">This happens when hello health probe fails.</span></span> | <span data-ttu-id="454ed-147">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-147">No</span></span> |
| <span data-ttu-id="454ed-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="454ed-148">PlatformInActive</span></span> | <span data-ttu-id="454ed-149">Há um problema com a plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-149">There is an issue with hello platform.</span></span> | <span data-ttu-id="454ed-150">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-150">No</span></span>|
| <span data-ttu-id="454ed-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="454ed-151">ServiceNotRunning</span></span> | <span data-ttu-id="454ed-152">serviço subjacente Olá não está em execução.</span><span class="sxs-lookup"><span data-stu-id="454ed-152">hello underlying service is not running.</span></span> | <span data-ttu-id="454ed-153">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-153">No</span></span>|
| <span data-ttu-id="454ed-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="454ed-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="454ed-155">Nenhuma conexão existe no gateway hello.</span><span class="sxs-lookup"><span data-stu-id="454ed-155">No Connections exists on hello gateway.</span></span> <span data-ttu-id="454ed-156">Isso é apenas um aviso.</span><span class="sxs-lookup"><span data-stu-id="454ed-156">This is only a warning.</span></span>| <span data-ttu-id="454ed-157">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-157">No</span></span>|
| <span data-ttu-id="454ed-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="454ed-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="454ed-159">As conexões não estão conectadas.</span><span class="sxs-lookup"><span data-stu-id="454ed-159">Connections are not connected.</span></span> <span data-ttu-id="454ed-160">Isso é apenas um aviso.</span><span class="sxs-lookup"><span data-stu-id="454ed-160">This is only a warning.</span></span>| <span data-ttu-id="454ed-161">Sim</span><span class="sxs-lookup"><span data-stu-id="454ed-161">Yes</span></span>|
| <span data-ttu-id="454ed-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="454ed-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="454ed-163">uso de CPU do Gateway atual Olá é > 95%.</span><span class="sxs-lookup"><span data-stu-id="454ed-163">hello current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="454ed-164">Sim</span><span class="sxs-lookup"><span data-stu-id="454ed-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="454ed-165">Conexão</span><span class="sxs-lookup"><span data-stu-id="454ed-165">Connection</span></span>

| <span data-ttu-id="454ed-166">Tipo de Falha</span><span class="sxs-lookup"><span data-stu-id="454ed-166">Fault Type</span></span> | <span data-ttu-id="454ed-167">Motivo</span><span class="sxs-lookup"><span data-stu-id="454ed-167">Reason</span></span> | <span data-ttu-id="454ed-168">Registro</span><span class="sxs-lookup"><span data-stu-id="454ed-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="454ed-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="454ed-169">NoFault</span></span> | <span data-ttu-id="454ed-170">Quando nenhum erro é detectado.</span><span class="sxs-lookup"><span data-stu-id="454ed-170">When no error is detected.</span></span> |<span data-ttu-id="454ed-171">Sim</span><span class="sxs-lookup"><span data-stu-id="454ed-171">Yes</span></span>|
| <span data-ttu-id="454ed-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="454ed-172">GatewayNotFound</span></span> | <span data-ttu-id="454ed-173">Não é possível localizar o Gateway ou o Gateway não está provisionado.</span><span class="sxs-lookup"><span data-stu-id="454ed-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="454ed-174">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-174">No</span></span>|
| <span data-ttu-id="454ed-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="454ed-175">PlannedMaintenance</span></span> | <span data-ttu-id="454ed-176">A instância do gateway está em manutenção.</span><span class="sxs-lookup"><span data-stu-id="454ed-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="454ed-177">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-177">No</span></span>|
| <span data-ttu-id="454ed-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="454ed-178">UserDrivenUpdate</span></span> | <span data-ttu-id="454ed-179">Uma atualização de um usuário está em andamento.</span><span class="sxs-lookup"><span data-stu-id="454ed-179">When a user update is in progress.</span></span> <span data-ttu-id="454ed-180">Isso pode ser uma operação de redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="454ed-180">This could be a resize operation.</span></span>  | <span data-ttu-id="454ed-181">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-181">No</span></span> |
| <span data-ttu-id="454ed-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="454ed-182">VipUnResponsive</span></span> | <span data-ttu-id="454ed-183">É possível acessar a instância primária de saudação do hello Gateway.</span><span class="sxs-lookup"><span data-stu-id="454ed-183">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="454ed-184">Isso acontece quando ocorre falha na investigação de integridade de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-184">It happens when hello health probe fails.</span></span> | <span data-ttu-id="454ed-185">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-185">No</span></span> |
| <span data-ttu-id="454ed-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="454ed-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="454ed-187">A configuração da Conexão está ausente.</span><span class="sxs-lookup"><span data-stu-id="454ed-187">Connection configuration is missing.</span></span> | <span data-ttu-id="454ed-188">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-188">No</span></span> |
| <span data-ttu-id="454ed-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="454ed-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="454ed-190">Olá Conexão está marcado como "desconectada".</span><span class="sxs-lookup"><span data-stu-id="454ed-190">hello Connection is marked "disconnected".</span></span> |<span data-ttu-id="454ed-191">Não</span><span class="sxs-lookup"><span data-stu-id="454ed-191">No</span></span>|
| <span data-ttu-id="454ed-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="454ed-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="454ed-193">serviço subjacente Olá não tem Olá que Conexão configurada.</span><span class="sxs-lookup"><span data-stu-id="454ed-193">hello underlying service does not have hello Connection configured.</span></span> | <span data-ttu-id="454ed-194">Sim</span><span class="sxs-lookup"><span data-stu-id="454ed-194">Yes</span></span> |
| <span data-ttu-id="454ed-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="454ed-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="454ed-196">Olá serviço subjacente é marcado como em espera.</span><span class="sxs-lookup"><span data-stu-id="454ed-196">hello underlying service is marked as standby.</span></span>| <span data-ttu-id="454ed-197">Sim</span><span class="sxs-lookup"><span data-stu-id="454ed-197">Yes</span></span>|
| <span data-ttu-id="454ed-198">Autenticação</span><span class="sxs-lookup"><span data-stu-id="454ed-198">Authentication</span></span> | <span data-ttu-id="454ed-199">Incompatibilidade de chave pré-compartilhada.</span><span class="sxs-lookup"><span data-stu-id="454ed-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="454ed-200">Sim</span><span class="sxs-lookup"><span data-stu-id="454ed-200">Yes</span></span>|
| <span data-ttu-id="454ed-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="454ed-201">PeerReachability</span></span> | <span data-ttu-id="454ed-202">gateway do Hello correspondente não está acessível.</span><span class="sxs-lookup"><span data-stu-id="454ed-202">hello peer gateway is not reachable.</span></span> | <span data-ttu-id="454ed-203">Sim</span><span class="sxs-lookup"><span data-stu-id="454ed-203">Yes</span></span>|
| <span data-ttu-id="454ed-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="454ed-204">IkePolicyMismatch</span></span> | <span data-ttu-id="454ed-205">gateway de par de saudação tem políticas de IKE que não são suportadas pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="454ed-205">hello peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="454ed-206">Sim</span><span class="sxs-lookup"><span data-stu-id="454ed-206">Yes</span></span>|
| <span data-ttu-id="454ed-207">Erro WfpParse</span><span class="sxs-lookup"><span data-stu-id="454ed-207">WfpParse Error</span></span> | <span data-ttu-id="454ed-208">Erro ao analisar logs WFP hello.</span><span class="sxs-lookup"><span data-stu-id="454ed-208">An error occurred parsing hello WFP log.</span></span> |<span data-ttu-id="454ed-209">Sim</span><span class="sxs-lookup"><span data-stu-id="454ed-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="454ed-210">Tipos de gateway com suporte</span><span class="sxs-lookup"><span data-stu-id="454ed-210">Supported Gateway types</span></span>

<span data-ttu-id="454ed-211">Olá lista a seguir mostra suporte Olá mostra quais gateways e conexões são compatíveis com a solução de problemas do observador de rede.</span><span class="sxs-lookup"><span data-stu-id="454ed-211">hello following list shows hello support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="454ed-212">**Tipos de gateway**</span><span class="sxs-lookup"><span data-stu-id="454ed-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="454ed-213">VPN</span><span class="sxs-lookup"><span data-stu-id="454ed-213">VPN</span></span>      | <span data-ttu-id="454ed-214">Suportado</span><span class="sxs-lookup"><span data-stu-id="454ed-214">Supported</span></span>        |
|<span data-ttu-id="454ed-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="454ed-215">ExpressRoute</span></span> | <span data-ttu-id="454ed-216">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="454ed-216">Not Supported</span></span> |
|<span data-ttu-id="454ed-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="454ed-217">Hypernet</span></span> | <span data-ttu-id="454ed-218">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="454ed-218">Not Supported</span></span>|
|<span data-ttu-id="454ed-219">**Tipos de VPN**</span><span class="sxs-lookup"><span data-stu-id="454ed-219">**VPN types**</span></span> | |
|<span data-ttu-id="454ed-220">Baseada em Rota</span><span class="sxs-lookup"><span data-stu-id="454ed-220">Route Based</span></span> | <span data-ttu-id="454ed-221">Suportado</span><span class="sxs-lookup"><span data-stu-id="454ed-221">Supported</span></span>|
|<span data-ttu-id="454ed-222">Baseada em Políticas</span><span class="sxs-lookup"><span data-stu-id="454ed-222">Policy Based</span></span> | <span data-ttu-id="454ed-223">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="454ed-223">Not Supported</span></span>|
|<span data-ttu-id="454ed-224">**Tipos de conexão**</span><span class="sxs-lookup"><span data-stu-id="454ed-224">**Connection types**</span></span>||
|<span data-ttu-id="454ed-225">IPsec</span><span class="sxs-lookup"><span data-stu-id="454ed-225">IPSec</span></span>| <span data-ttu-id="454ed-226">Suportado</span><span class="sxs-lookup"><span data-stu-id="454ed-226">Supported</span></span>|
|<span data-ttu-id="454ed-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="454ed-227">VNet2Vnet</span></span>| <span data-ttu-id="454ed-228">Suportado</span><span class="sxs-lookup"><span data-stu-id="454ed-228">Supported</span></span>|
|<span data-ttu-id="454ed-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="454ed-229">ExpressRoute</span></span>| <span data-ttu-id="454ed-230">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="454ed-230">Not Supported</span></span>|
|<span data-ttu-id="454ed-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="454ed-231">Hypernet</span></span>| <span data-ttu-id="454ed-232">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="454ed-232">Not Supported</span></span>|
|<span data-ttu-id="454ed-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="454ed-233">VPNClient</span></span>| <span data-ttu-id="454ed-234">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="454ed-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="454ed-235">Arquivos de log</span><span class="sxs-lookup"><span data-stu-id="454ed-235">Log files</span></span>

<span data-ttu-id="454ed-236">arquivos de log de solução de problemas do Hello recursos são armazenados em uma conta de armazenamento após a conclusão da solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="454ed-236">hello resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="454ed-237">Olá imagem a seguir mostra conteúdo de exemplo hello de uma chamada que resultou em erro.</span><span class="sxs-lookup"><span data-stu-id="454ed-237">hello following image shows hello example contents of a call that resulted in an error.</span></span>

![arquivo zip][1]

> [!NOTE]
> <span data-ttu-id="454ed-239">Em alguns casos, somente um subconjunto dos arquivos de log de saudação é gravado toostorage.</span><span class="sxs-lookup"><span data-stu-id="454ed-239">In some cases, only a subset of hello logs files is written toostorage.</span></span>

<span data-ttu-id="454ed-240">Para obter instruções sobre como baixar os arquivos de contas de armazenamento do azure, consulte muito[Introdução ao armazenamento de BLOBs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="454ed-240">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="454ed-241">Outra ferramenta que pode ser usada é o Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="454ed-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="454ed-242">Para obter mais informações sobre o Gerenciador de armazenamento podem ser encontradas aqui em Olá link a seguir: [Gerenciador de armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="454ed-242">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="454ed-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="454ed-243">ConnectionStats.txt</span></span>

<span data-ttu-id="454ed-244">Olá **ConnectionStats.txt** arquivo contém estatísticas gerais de saudação Conexão, incluindo bytes de entrada e saída, o status de Conexão e saudação de tempo de saudação Conexão foi estabelecida.</span><span class="sxs-lookup"><span data-stu-id="454ed-244">hello **ConnectionStats.txt** file contains overall stats of hello Connection, including ingress and egress bytes, Connection status, and hello time hello Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="454ed-245">Se Olá toohello de chamada de API de solução de problemas retorna íntegro, a única coisa que Olá retornada no arquivo zip de saudação é um **ConnectionStats.txt** arquivo.</span><span class="sxs-lookup"><span data-stu-id="454ed-245">If hello call toohello troubleshooting API returns healthy, hello only thing returned in hello zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="454ed-246">conteúdo deste arquivo Hello é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="454ed-246">hello contents of this file are similar toohello following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="454ed-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="454ed-247">CPUStats.txt</span></span>

<span data-ttu-id="454ed-248">Olá **CPUStats.txt** arquivo contém o uso da CPU e memória disponível no momento de saudação do teste.</span><span class="sxs-lookup"><span data-stu-id="454ed-248">hello **CPUStats.txt** file contains CPU usage and memory available at hello time of testing.</span></span>  <span data-ttu-id="454ed-249">conteúdo deste arquivo Hello é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="454ed-249">hello contents of this file is similar toohello following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="454ed-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="454ed-250">IKEErrors.txt</span></span>

<span data-ttu-id="454ed-251">Olá **IKEErrors.txt** arquivo contendo quaisquer erros de IKE que foram encontrados durante o monitoramento.</span><span class="sxs-lookup"><span data-stu-id="454ed-251">hello **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="454ed-252">Olá, exemplo a seguir mostra Olá conteúdo de um arquivo de IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="454ed-252">hello following example shows hello contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="454ed-253">Os erros podem ser diferentes dependendo do problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-253">Your errors may be different depending on hello issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="454ed-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="454ed-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="454ed-255">Olá **Scrubbed wfpdiag.txt** arquivo de log contém o log de wfp hello.</span><span class="sxs-lookup"><span data-stu-id="454ed-255">hello **Scrubbed-wfpdiag.txt** log file contains hello wfp log.</span></span> <span data-ttu-id="454ed-256">Esse log contém o registro de descarte do pacote e de falhas de IKE/AuthIP.</span><span class="sxs-lookup"><span data-stu-id="454ed-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="454ed-257">Olá exemplo a seguir mostra conteúdo de saudação do arquivo de Scrubbed wfpdiag.txt de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-257">hello following example shows hello contents of hello Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="454ed-258">Neste exemplo, a chave compartilhada de saudação de uma Conexão não estava correto como pode ser visto na linha de 3ª Olá da parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-258">In this example, hello shared key of a Connection was not correct as can be seen from hello 3rd line from hello bottom.</span></span> <span data-ttu-id="454ed-259">saudação de exemplo a seguir é apenas um trecho de todo o log hello, como log Olá pode ser demorado, dependendo do problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="454ed-259">hello following example is just a snippet of hello entire log, as hello log can be lengthy depending on hello issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="454ed-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="454ed-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="454ed-261">Olá **wfpdiag.txt.sum** arquivo é um log mostrando buffers hello e eventos processados.</span><span class="sxs-lookup"><span data-stu-id="454ed-261">hello **wfpdiag.txt.sum** file is a log showing hello buffers and events processed.</span></span>

<span data-ttu-id="454ed-262">Olá, exemplo a seguir é Olá conteúdo de um arquivo de wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="454ed-262">hello following example is hello contents of a wfpdiag.txt.sum file.</span></span>
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a><span data-ttu-id="454ed-263">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="454ed-263">Next steps</span></span>

<span data-ttu-id="454ed-264">Saiba como Gateways de VPN toodiagnose e conexões por meio de Olá portal visitando [solução de problemas do Gateway - portal do Azure](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="454ed-264">Learn how toodiagnose VPN Gateways and Connections through hello portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
