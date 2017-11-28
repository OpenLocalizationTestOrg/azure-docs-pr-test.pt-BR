---
title: "Introdução à solução de problemas do recurso no Observador de Rede do Azure | Microsoft Docs"
description: "Essa página fornece uma visão geral das capacidades de solução de problemas do recurso do Observador de Rede"
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
ms.openlocfilehash: 0d5091b682d1b25c47b224394bcc2c46366eeb2a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-resource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="3ad25-103">Introdução à solução de problemas do recurso no Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="3ad25-103">Introduction to resource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="3ad25-104">Os Gateways de Rede Virtual fornecem conectividade entre os recursos locais e outras redes virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad25-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="3ad25-105">Para garantir que a comunicação não seja quebrada, é essencial monitorar esses gateways e suas Conexões.</span><span class="sxs-lookup"><span data-stu-id="3ad25-105">Monitoring these gateways and their Connections is critical to ensuring communication is not broken.</span></span> <span data-ttu-id="3ad25-106">O Observador de Rede fornece a capacidade de solucionar problemas das Conexões e dos Gateways de Rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="3ad25-106">Network Watcher provides the capability to troubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="3ad25-107">Ela pode ser chamada pelo Portal, pelo PowerShell, pela CLI ou pela API REST.</span><span class="sxs-lookup"><span data-stu-id="3ad25-107">This can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="3ad25-108">Quando chamado, o Observador de Rede diagnostica a integridade da conexão ou do gateway de rede virtual e retorna os resultados adequados.</span><span class="sxs-lookup"><span data-stu-id="3ad25-108">When called, Network Watcher diagnoses the health of the virtual network gateway or connection and return the appropriate results.</span></span> <span data-ttu-id="3ad25-109">Essa solicitação é uma transação de longa duração e os resultados são retornados quando o diagnóstico for concluído.</span><span class="sxs-lookup"><span data-stu-id="3ad25-109">This request is a long running transaction, the results are returned once the diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="3ad25-111">Resultados</span><span class="sxs-lookup"><span data-stu-id="3ad25-111">Results</span></span>

<span data-ttu-id="3ad25-112">Os resultados preliminares retornados fornecem uma visão geral da integridade do recurso.</span><span class="sxs-lookup"><span data-stu-id="3ad25-112">The preliminary results returned give an overall picture of the health of the resource.</span></span> <span data-ttu-id="3ad25-113">Mais informações podem ser fornecidas sobre os recursos, como mostrado na seção a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ad25-113">Deeper information can be provided for resources as shown in the following section:</span></span>

<span data-ttu-id="3ad25-114">A lista a seguir contém os valores retornados com a API de solução de problemas:</span><span class="sxs-lookup"><span data-stu-id="3ad25-114">The following list is the values returned with the troubleshoot API:</span></span>

* <span data-ttu-id="3ad25-115">**startTime** - esse valor indica a hora que a chamada da API de solução de problemas começou.</span><span class="sxs-lookup"><span data-stu-id="3ad25-115">**startTime** - This value is the time the troubleshoot API call started.</span></span>
* <span data-ttu-id="3ad25-116">**endTime** - esse valor indica a hora que a solução de problemas foi concluída.</span><span class="sxs-lookup"><span data-stu-id="3ad25-116">**endTime** - This value is the time when the troubleshooting ended.</span></span>
* <span data-ttu-id="3ad25-117">**cod** - esse valor não é apresentado como UnHealthy (não íntegro), se houver uma única falha de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="3ad25-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="3ad25-118">**results** - é um conjunto de resultados retornados sobre a Conexão ou o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3ad25-118">**results** - Results is a collection of results returned on the Connection or the virtual network gateway.</span></span>
    * <span data-ttu-id="3ad25-119">**id** - esse valor indica o tipo da falha.</span><span class="sxs-lookup"><span data-stu-id="3ad25-119">**id** - This value is the fault type.</span></span>
    * <span data-ttu-id="3ad25-120">**summary** - esse valor é um resumo da falha.</span><span class="sxs-lookup"><span data-stu-id="3ad25-120">**summary** - This value is a summary of the fault.</span></span>
    * <span data-ttu-id="3ad25-121">**detailed** - esse valor fornece uma descrição detalhada da falha.</span><span class="sxs-lookup"><span data-stu-id="3ad25-121">**detailed** - This value provides a detailed description of the fault.</span></span>
    * <span data-ttu-id="3ad25-122">**recommendedActions** - essa propriedade é um conjunto de ações recomendadas.</span><span class="sxs-lookup"><span data-stu-id="3ad25-122">**recommendedActions** - This property is a collection of recommended actions to take.</span></span>
      * <span data-ttu-id="3ad25-123">**actionText** - esse valor contém o texto que descreve a ação a ser executada.</span><span class="sxs-lookup"><span data-stu-id="3ad25-123">**actionText** - This value contains the text describing what action to take.</span></span>
      * <span data-ttu-id="3ad25-124">**actionUri** - esse valor fornece o URI da documentação sobre como agir.</span><span class="sxs-lookup"><span data-stu-id="3ad25-124">**actionUri** - This value provides the URI to documentation on how to act.</span></span>
      * <span data-ttu-id="3ad25-125">**actionUriText** - esse valor é uma breve descrição do texto de ação.</span><span class="sxs-lookup"><span data-stu-id="3ad25-125">**actionUriText** - This value is a short description of the action text.</span></span>

<span data-ttu-id="3ad25-126">As tabelas a seguir mostram os diversos tipos de falha (id em resultados da lista anterior) que estão disponíveis e se a falha cria logs.</span><span class="sxs-lookup"><span data-stu-id="3ad25-126">The following tables show the different fault types (id under results from the preceding list) that are available and if the fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="3ad25-127">Gateway</span><span class="sxs-lookup"><span data-stu-id="3ad25-127">Gateway</span></span>

| <span data-ttu-id="3ad25-128">Tipo de Falha</span><span class="sxs-lookup"><span data-stu-id="3ad25-128">Fault Type</span></span> | <span data-ttu-id="3ad25-129">Motivo</span><span class="sxs-lookup"><span data-stu-id="3ad25-129">Reason</span></span> | <span data-ttu-id="3ad25-130">Registro</span><span class="sxs-lookup"><span data-stu-id="3ad25-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="3ad25-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="3ad25-131">NoFault</span></span> | <span data-ttu-id="3ad25-132">Quando nenhum erro é detectado.</span><span class="sxs-lookup"><span data-stu-id="3ad25-132">When no error is detected.</span></span> |<span data-ttu-id="3ad25-133">Sim</span><span class="sxs-lookup"><span data-stu-id="3ad25-133">Yes</span></span>|
| <span data-ttu-id="3ad25-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="3ad25-134">GatewayNotFound</span></span> | <span data-ttu-id="3ad25-135">Não é possível localizar o Gateway ou o Gateway não está provisionado.</span><span class="sxs-lookup"><span data-stu-id="3ad25-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="3ad25-136">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-136">No</span></span>|
| <span data-ttu-id="3ad25-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="3ad25-137">PlannedMaintenance</span></span> |  <span data-ttu-id="3ad25-138">A instância do gateway está em manutenção.</span><span class="sxs-lookup"><span data-stu-id="3ad25-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="3ad25-139">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-139">No</span></span>|
| <span data-ttu-id="3ad25-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="3ad25-140">UserDrivenUpdate</span></span> | <span data-ttu-id="3ad25-141">Uma atualização de um usuário está em andamento.</span><span class="sxs-lookup"><span data-stu-id="3ad25-141">When a user update is in progress.</span></span> <span data-ttu-id="3ad25-142">Isso pode ser uma operação de redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="3ad25-142">This could be a resize operation.</span></span> | <span data-ttu-id="3ad25-143">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-143">No</span></span> |
| <span data-ttu-id="3ad25-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="3ad25-144">VipUnResponsive</span></span> | <span data-ttu-id="3ad25-145">Não é possível acessar a instância primária do Gateway.</span><span class="sxs-lookup"><span data-stu-id="3ad25-145">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="3ad25-146">Isso acontece quando a investigação de integridade falha.</span><span class="sxs-lookup"><span data-stu-id="3ad25-146">This happens when the health probe fails.</span></span> | <span data-ttu-id="3ad25-147">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-147">No</span></span> |
| <span data-ttu-id="3ad25-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="3ad25-148">PlatformInActive</span></span> | <span data-ttu-id="3ad25-149">Há um problema com a plataforma.</span><span class="sxs-lookup"><span data-stu-id="3ad25-149">There is an issue with the platform.</span></span> | <span data-ttu-id="3ad25-150">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-150">No</span></span>|
| <span data-ttu-id="3ad25-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="3ad25-151">ServiceNotRunning</span></span> | <span data-ttu-id="3ad25-152">O serviço subjacente não está em execução.</span><span class="sxs-lookup"><span data-stu-id="3ad25-152">The underlying service is not running.</span></span> | <span data-ttu-id="3ad25-153">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-153">No</span></span>|
| <span data-ttu-id="3ad25-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="3ad25-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="3ad25-155">Não existe Conexões no gateway.</span><span class="sxs-lookup"><span data-stu-id="3ad25-155">No Connections exists on the gateway.</span></span> <span data-ttu-id="3ad25-156">Isso é apenas um aviso.</span><span class="sxs-lookup"><span data-stu-id="3ad25-156">This is only a warning.</span></span>| <span data-ttu-id="3ad25-157">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-157">No</span></span>|
| <span data-ttu-id="3ad25-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="3ad25-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="3ad25-159">As conexões não estão conectadas.</span><span class="sxs-lookup"><span data-stu-id="3ad25-159">Connections are not connected.</span></span> <span data-ttu-id="3ad25-160">Isso é apenas um aviso.</span><span class="sxs-lookup"><span data-stu-id="3ad25-160">This is only a warning.</span></span>| <span data-ttu-id="3ad25-161">Sim</span><span class="sxs-lookup"><span data-stu-id="3ad25-161">Yes</span></span>|
| <span data-ttu-id="3ad25-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="3ad25-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="3ad25-163">O uso de CPU do Gateway atual é > 95%.</span><span class="sxs-lookup"><span data-stu-id="3ad25-163">The current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="3ad25-164">Sim</span><span class="sxs-lookup"><span data-stu-id="3ad25-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="3ad25-165">Conexão</span><span class="sxs-lookup"><span data-stu-id="3ad25-165">Connection</span></span>

| <span data-ttu-id="3ad25-166">Tipo de Falha</span><span class="sxs-lookup"><span data-stu-id="3ad25-166">Fault Type</span></span> | <span data-ttu-id="3ad25-167">Motivo</span><span class="sxs-lookup"><span data-stu-id="3ad25-167">Reason</span></span> | <span data-ttu-id="3ad25-168">Registro</span><span class="sxs-lookup"><span data-stu-id="3ad25-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="3ad25-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="3ad25-169">NoFault</span></span> | <span data-ttu-id="3ad25-170">Quando nenhum erro é detectado.</span><span class="sxs-lookup"><span data-stu-id="3ad25-170">When no error is detected.</span></span> |<span data-ttu-id="3ad25-171">Sim</span><span class="sxs-lookup"><span data-stu-id="3ad25-171">Yes</span></span>|
| <span data-ttu-id="3ad25-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="3ad25-172">GatewayNotFound</span></span> | <span data-ttu-id="3ad25-173">Não é possível localizar o Gateway ou o Gateway não está provisionado.</span><span class="sxs-lookup"><span data-stu-id="3ad25-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="3ad25-174">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-174">No</span></span>|
| <span data-ttu-id="3ad25-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="3ad25-175">PlannedMaintenance</span></span> | <span data-ttu-id="3ad25-176">A instância do gateway está em manutenção.</span><span class="sxs-lookup"><span data-stu-id="3ad25-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="3ad25-177">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-177">No</span></span>|
| <span data-ttu-id="3ad25-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="3ad25-178">UserDrivenUpdate</span></span> | <span data-ttu-id="3ad25-179">Uma atualização de um usuário está em andamento.</span><span class="sxs-lookup"><span data-stu-id="3ad25-179">When a user update is in progress.</span></span> <span data-ttu-id="3ad25-180">Isso pode ser uma operação de redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="3ad25-180">This could be a resize operation.</span></span>  | <span data-ttu-id="3ad25-181">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-181">No</span></span> |
| <span data-ttu-id="3ad25-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="3ad25-182">VipUnResponsive</span></span> | <span data-ttu-id="3ad25-183">Não é possível acessar a instância primária do Gateway.</span><span class="sxs-lookup"><span data-stu-id="3ad25-183">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="3ad25-184">Isso acontece quando a investigação de integridade falha.</span><span class="sxs-lookup"><span data-stu-id="3ad25-184">It happens when the health probe fails.</span></span> | <span data-ttu-id="3ad25-185">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-185">No</span></span> |
| <span data-ttu-id="3ad25-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="3ad25-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="3ad25-187">A configuração da Conexão está ausente.</span><span class="sxs-lookup"><span data-stu-id="3ad25-187">Connection configuration is missing.</span></span> | <span data-ttu-id="3ad25-188">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-188">No</span></span> |
| <span data-ttu-id="3ad25-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="3ad25-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="3ad25-190">A Conexão está marcado como "desconectada".</span><span class="sxs-lookup"><span data-stu-id="3ad25-190">The Connection is marked "disconnected".</span></span> |<span data-ttu-id="3ad25-191">Não</span><span class="sxs-lookup"><span data-stu-id="3ad25-191">No</span></span>|
| <span data-ttu-id="3ad25-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="3ad25-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="3ad25-193">O serviço subjacente não tem a Conexão configurada.</span><span class="sxs-lookup"><span data-stu-id="3ad25-193">The underlying service does not have the Connection configured.</span></span> | <span data-ttu-id="3ad25-194">Sim</span><span class="sxs-lookup"><span data-stu-id="3ad25-194">Yes</span></span> |
| <span data-ttu-id="3ad25-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="3ad25-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="3ad25-196">O serviço subjacente está marcado como em espera.</span><span class="sxs-lookup"><span data-stu-id="3ad25-196">The underlying service is marked as standby.</span></span>| <span data-ttu-id="3ad25-197">Sim</span><span class="sxs-lookup"><span data-stu-id="3ad25-197">Yes</span></span>|
| <span data-ttu-id="3ad25-198">Autenticação</span><span class="sxs-lookup"><span data-stu-id="3ad25-198">Authentication</span></span> | <span data-ttu-id="3ad25-199">Incompatibilidade de chave pré-compartilhada.</span><span class="sxs-lookup"><span data-stu-id="3ad25-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="3ad25-200">Sim</span><span class="sxs-lookup"><span data-stu-id="3ad25-200">Yes</span></span>|
| <span data-ttu-id="3ad25-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="3ad25-201">PeerReachability</span></span> | <span data-ttu-id="3ad25-202">O gateway correspondente não está acessível.</span><span class="sxs-lookup"><span data-stu-id="3ad25-202">The peer gateway is not reachable.</span></span> | <span data-ttu-id="3ad25-203">Sim</span><span class="sxs-lookup"><span data-stu-id="3ad25-203">Yes</span></span>|
| <span data-ttu-id="3ad25-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="3ad25-204">IkePolicyMismatch</span></span> | <span data-ttu-id="3ad25-205">O gateway de mesmo nível tem diretivas IKE que não são suportadas pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad25-205">The peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="3ad25-206">Sim</span><span class="sxs-lookup"><span data-stu-id="3ad25-206">Yes</span></span>|
| <span data-ttu-id="3ad25-207">Erro WfpParse</span><span class="sxs-lookup"><span data-stu-id="3ad25-207">WfpParse Error</span></span> | <span data-ttu-id="3ad25-208">Ocorreu um erro ao analisar o log WFP.</span><span class="sxs-lookup"><span data-stu-id="3ad25-208">An error occurred parsing the WFP log.</span></span> |<span data-ttu-id="3ad25-209">Sim</span><span class="sxs-lookup"><span data-stu-id="3ad25-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="3ad25-210">Tipos de gateway com suporte</span><span class="sxs-lookup"><span data-stu-id="3ad25-210">Supported Gateway types</span></span>

<span data-ttu-id="3ad25-211">A lista a seguir mostra quais gateways e conexões têm suporte com a solução de problemas do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="3ad25-211">The following list shows the support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="3ad25-212">**Tipos de gateway**</span><span class="sxs-lookup"><span data-stu-id="3ad25-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="3ad25-213">VPN</span><span class="sxs-lookup"><span data-stu-id="3ad25-213">VPN</span></span>      | <span data-ttu-id="3ad25-214">Suportado</span><span class="sxs-lookup"><span data-stu-id="3ad25-214">Supported</span></span>        |
|<span data-ttu-id="3ad25-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3ad25-215">ExpressRoute</span></span> | <span data-ttu-id="3ad25-216">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="3ad25-216">Not Supported</span></span> |
|<span data-ttu-id="3ad25-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="3ad25-217">Hypernet</span></span> | <span data-ttu-id="3ad25-218">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="3ad25-218">Not Supported</span></span>|
|<span data-ttu-id="3ad25-219">**Tipos de VPN**</span><span class="sxs-lookup"><span data-stu-id="3ad25-219">**VPN types**</span></span> | |
|<span data-ttu-id="3ad25-220">Baseada em Rota</span><span class="sxs-lookup"><span data-stu-id="3ad25-220">Route Based</span></span> | <span data-ttu-id="3ad25-221">Suportado</span><span class="sxs-lookup"><span data-stu-id="3ad25-221">Supported</span></span>|
|<span data-ttu-id="3ad25-222">Baseada em Políticas</span><span class="sxs-lookup"><span data-stu-id="3ad25-222">Policy Based</span></span> | <span data-ttu-id="3ad25-223">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="3ad25-223">Not Supported</span></span>|
|<span data-ttu-id="3ad25-224">**Tipos de conexão**</span><span class="sxs-lookup"><span data-stu-id="3ad25-224">**Connection types**</span></span>||
|<span data-ttu-id="3ad25-225">IPsec</span><span class="sxs-lookup"><span data-stu-id="3ad25-225">IPSec</span></span>| <span data-ttu-id="3ad25-226">Suportado</span><span class="sxs-lookup"><span data-stu-id="3ad25-226">Supported</span></span>|
|<span data-ttu-id="3ad25-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="3ad25-227">VNet2Vnet</span></span>| <span data-ttu-id="3ad25-228">Suportado</span><span class="sxs-lookup"><span data-stu-id="3ad25-228">Supported</span></span>|
|<span data-ttu-id="3ad25-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3ad25-229">ExpressRoute</span></span>| <span data-ttu-id="3ad25-230">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="3ad25-230">Not Supported</span></span>|
|<span data-ttu-id="3ad25-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="3ad25-231">Hypernet</span></span>| <span data-ttu-id="3ad25-232">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="3ad25-232">Not Supported</span></span>|
|<span data-ttu-id="3ad25-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="3ad25-233">VPNClient</span></span>| <span data-ttu-id="3ad25-234">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="3ad25-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="3ad25-235">Arquivos de log</span><span class="sxs-lookup"><span data-stu-id="3ad25-235">Log files</span></span>

<span data-ttu-id="3ad25-236">Os arquivos de log para solução de problemas de recursos são armazenados em uma conta de armazenamento após a conclusão da solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="3ad25-236">The resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="3ad25-237">A imagem a seguir mostra o conteúdo de exemplo de uma chamada que resultou em um erro.</span><span class="sxs-lookup"><span data-stu-id="3ad25-237">The following image shows the example contents of a call that resulted in an error.</span></span>

![arquivo zip][1]

> [!NOTE]
> <span data-ttu-id="3ad25-239">Em alguns casos, somente um subconjunto dos arquivos de log é gravado no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3ad25-239">In some cases, only a subset of the logs files is written to storage.</span></span>

<span data-ttu-id="3ad25-240">Para obter instruções sobre como baixar os arquivos de contas de armazenamento do Azure, consulte [Introdução ao armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="3ad25-240">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="3ad25-241">Outra ferramenta que pode ser usada é o Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3ad25-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="3ad25-242">Para obter mais informações sobre o Gerenciador de armazenamento, acesse o link: [Gerenciador de armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="3ad25-242">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="3ad25-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="3ad25-243">ConnectionStats.txt</span></span>

<span data-ttu-id="3ad25-244">O arquivo **ConnectionStats.txt** contém estatísticas gerais da Conexão, incluindo bytes de entrada e saída, status da Conexão e a hora que a Conexão foi estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3ad25-244">The **ConnectionStats.txt** file contains overall stats of the Connection, including ingress and egress bytes, Connection status, and the time the Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="3ad25-245">Se a chamada para a API de solução de problemas retornar como íntegra, o único item retornado no arquivo zip será um arquivo **ConnectionStats.txt**.</span><span class="sxs-lookup"><span data-stu-id="3ad25-245">If the call to the troubleshooting API returns healthy, the only thing returned in the zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="3ad25-246">O conteúdo desse arquivo é semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ad25-246">The contents of this file are similar to the following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="3ad25-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="3ad25-247">CPUStats.txt</span></span>

<span data-ttu-id="3ad25-248">O arquivo **CPUStats.txt** contém o uso da CPU e memória disponível no momento do teste.</span><span class="sxs-lookup"><span data-stu-id="3ad25-248">The **CPUStats.txt** file contains CPU usage and memory available at the time of testing.</span></span>  <span data-ttu-id="3ad25-249">O conteúdo desse arquivo é semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ad25-249">The contents of this file is similar to the following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="3ad25-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="3ad25-250">IKEErrors.txt</span></span>

<span data-ttu-id="3ad25-251">O arquivo **IKEErrors.txt** contém erros de IKE que foram encontrados durante o monitoramento.</span><span class="sxs-lookup"><span data-stu-id="3ad25-251">The **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="3ad25-252">O exemplo a seguir mostra o conteúdo de um arquivo de IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="3ad25-252">The following example shows the contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="3ad25-253">Os erros podem ser diferentes dependendo do problema.</span><span class="sxs-lookup"><span data-stu-id="3ad25-253">Your errors may be different depending on the issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="3ad25-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="3ad25-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="3ad25-255">O arquivo de log **Scrubbed-wfpdiag.txt** contém o log wfp.</span><span class="sxs-lookup"><span data-stu-id="3ad25-255">The **Scrubbed-wfpdiag.txt** log file contains the wfp log.</span></span> <span data-ttu-id="3ad25-256">Esse log contém o registro de descarte do pacote e de falhas de IKE/AuthIP.</span><span class="sxs-lookup"><span data-stu-id="3ad25-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="3ad25-257">O exemplo a seguir mostra o conteúdo de um arquivo Scrubbed-wfpdiag.txt.</span><span class="sxs-lookup"><span data-stu-id="3ad25-257">The following example shows the contents of the Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="3ad25-258">Neste exemplo, a chave compartilhada de uma Conexão não está correta, como pode ser visto na 3ª linha da parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3ad25-258">In this example, the shared key of a Connection was not correct as can be seen from the 3rd line from the bottom.</span></span> <span data-ttu-id="3ad25-259">O exemplo a seguir é apenas um trecho do log inteiro, já que, dependendo do problema, o log pode ser demorado.</span><span class="sxs-lookup"><span data-stu-id="3ad25-259">The following example is just a snippet of the entire log, as the log can be lengthy depending on the issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from the high priority thread pool list
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

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="3ad25-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="3ad25-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="3ad25-261">O arquivo **wfpdiag.txt.sum** é um log que exibe buffers e eventos processados.</span><span class="sxs-lookup"><span data-stu-id="3ad25-261">The **wfpdiag.txt.sum** file is a log showing the buffers and events processed.</span></span>

<span data-ttu-id="3ad25-262">O exemplo a seguir é o conteúdo de um arquivo wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="3ad25-262">The following example is the contents of a wfpdiag.txt.sum file.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="3ad25-263">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3ad25-263">Next steps</span></span>

<span data-ttu-id="3ad25-264">Saiba como diagnosticar Gateways de VPN e Conexões por meio do Portal visitando [Solução de Problemas de Gateway – Portal do Azure](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3ad25-264">Learn how to diagnose VPN Gateways and Connections through the portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
