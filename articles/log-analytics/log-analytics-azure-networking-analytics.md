---
title: "aaaAzure solução de análise de rede na análise de Log | Microsoft Docs"
description: "Você pode usar o hello solução de análise de rede do Azure nos logs de Gateway de aplicativo do Azure e logs de grupo de segurança de rede do Azure de tooreview análise de Log."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="93a6e-103">Soluções de monitoramento de rede do Azure no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="93a6e-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="93a6e-104">Análise de log oferece Olá soluções para monitorar suas redes a seguir:</span><span class="sxs-lookup"><span data-stu-id="93a6e-104">Log Analytics offers hello following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="93a6e-105">Monitor de Desempenho de Rede (NPM) para</span><span class="sxs-lookup"><span data-stu-id="93a6e-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="93a6e-106">Olá monitorar a integridade da rede</span><span class="sxs-lookup"><span data-stu-id="93a6e-106">Monitor hello health of your network</span></span>
* <span data-ttu-id="93a6e-107">Tooreview de análise de Gateway do aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-107">Azure Application Gateway analytics tooreview</span></span>
 * <span data-ttu-id="93a6e-108">Logs do Gateway de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="93a6e-109">Métricas do Gateway de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="93a6e-110">Tooreview de análise do grupo de segurança de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-110">Azure Network Security Group analytics tooreview</span></span>
 * <span data-ttu-id="93a6e-111">Logs do Grupo de Segurança de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="93a6e-112">Monitor de Desempenho de Rede (NPM)</span><span class="sxs-lookup"><span data-stu-id="93a6e-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="93a6e-113">Olá [Monitor de desempenho de rede](log-analytics-network-performance-monitor.md) solução de gerenciamento é uma solução, que monitora a integridade de saudação, a disponibilidade e a acessibilidade de redes de monitoramento de rede.</span><span class="sxs-lookup"><span data-stu-id="93a6e-113">hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors hello health, availability and reachability of networks.</span></span>  <span data-ttu-id="93a6e-114">É usado toomonitor conectividade entre:</span><span class="sxs-lookup"><span data-stu-id="93a6e-114">It is used toomonitor connectivity between:</span></span>

* <span data-ttu-id="93a6e-115">Nuvem pública e local</span><span class="sxs-lookup"><span data-stu-id="93a6e-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="93a6e-116">Data centers e locais de usuário (filiais)</span><span class="sxs-lookup"><span data-stu-id="93a6e-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="93a6e-117">Sub-redes hospedando várias camadas de um aplicativo de várias camadas.</span><span class="sxs-lookup"><span data-stu-id="93a6e-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="93a6e-118">Para obter mais informações, confira [Monitor de Desempenho de Rede](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="93a6e-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="93a6e-119">Análise do Gateway de Aplicativo e do Grupo de Segurança de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="93a6e-120">soluções de saudação toouse:</span><span class="sxs-lookup"><span data-stu-id="93a6e-120">toouse hello solutions:</span></span>
1. <span data-ttu-id="93a6e-121">Adicionar tooLog de solução de gerenciamento Olá Analytics, e</span><span class="sxs-lookup"><span data-stu-id="93a6e-121">Add hello management solution tooLog Analytics, and</span></span>
2. <span data-ttu-id="93a6e-122">Habilite o diagnóstico toodirect Olá diagnóstico tooa análise de Log espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="93a6e-122">Enable diagnostics toodirect hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="93a6e-123">Não é necessário toowrite Olá logs tooAzure o armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="93a6e-123">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

<span data-ttu-id="93a6e-124">Você pode habilitar o diagnóstico e solução de saudação correspondente para um ou ambos os grupos de segurança de rede e Gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93a6e-124">You can enable diagnostics and hello corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="93a6e-125">Se você não habilitar o log de diagnóstico para um tipo de recurso específico, mas instala solução hello, folhas de painel Olá para esse recurso estão em branco e exibem uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="93a6e-125">If you do not enable diagnostic logging for a particular resource type, but install hello solution, hello dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="93a6e-126">Em janeiro de 2017, Olá suporte para a forma de envio de logs do tooLog Application Gateways e os grupos de segurança de rede, que análise alterada.</span><span class="sxs-lookup"><span data-stu-id="93a6e-126">In January 2017, hello supported way of sending logs from Application Gateways and Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="93a6e-127">Se você vir Olá **análise de rede do Azure (preterido)** solução, consulte muito[migrando de solução de análise de rede antiga Olá](#migrating-from-the-old-networking-analytics-solution) para obter as etapas que você precisa toofollow.</span><span class="sxs-lookup"><span data-stu-id="93a6e-127">If you see hello **Azure Networking Analytics (deprecated)** solution, refer too[migrating from hello old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need toofollow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="93a6e-128">Examinar os detalhes da coleção de dados de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="93a6e-129">análise de Gateway de aplicativo do Azure Hello e soluções de gerenciamento de análise de grupo de segurança de rede Olá coletam logs de diagnóstico diretamente no Azure Application Gateways e os grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="93a6e-129">hello Azure Application Gateway analytics and hello Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="93a6e-130">Não é necessário toowrite Olá logs tooAzure armazenamento de Blob e nenhum agente é necessária para a coleta de dados.</span><span class="sxs-lookup"><span data-stu-id="93a6e-130">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="93a6e-131">Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para análise de Gateway de aplicativo do Azure e análises de grupo de segurança de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="93a6e-131">hello following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and hello Network Security Group analytics.</span></span>

| <span data-ttu-id="93a6e-132">Plataforma</span><span class="sxs-lookup"><span data-stu-id="93a6e-132">Platform</span></span> | <span data-ttu-id="93a6e-133">Agente direto</span><span class="sxs-lookup"><span data-stu-id="93a6e-133">Direct agent</span></span> | <span data-ttu-id="93a6e-134">Agente do Systems Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="93a6e-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="93a6e-135">As tabelas</span><span class="sxs-lookup"><span data-stu-id="93a6e-135">Azure</span></span> | <span data-ttu-id="93a6e-136">Operations Manager necessário?</span><span class="sxs-lookup"><span data-stu-id="93a6e-136">Operations Manager required?</span></span> | <span data-ttu-id="93a6e-137">Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="93a6e-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="93a6e-138">Frequência de coleta</span><span class="sxs-lookup"><span data-stu-id="93a6e-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="93a6e-139">As tabelas</span><span class="sxs-lookup"><span data-stu-id="93a6e-139">Azure</span></span> |  |  |<span data-ttu-id="93a6e-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="93a6e-140">&#8226;</span></span> |  |  |<span data-ttu-id="93a6e-141">quando conectado</span><span class="sxs-lookup"><span data-stu-id="93a6e-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="93a6e-142">Solução de análise de Gateway de Aplicativo do Azure no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="93a6e-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Símbolo da Análise do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="93a6e-144">Olá logs a seguir têm suporte para Gateways de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="93a6e-144">hello following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="93a6e-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="93a6e-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="93a6e-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="93a6e-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="93a6e-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="93a6e-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="93a6e-148">Olá métricas a seguir têm suporte para Gateways de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="93a6e-148">hello following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="93a6e-149">Taxa de transferência de 5 minutos</span><span class="sxs-lookup"><span data-stu-id="93a6e-149">5 minute throughput</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="93a6e-150">Instalar e configurar a solução de saudação</span><span class="sxs-lookup"><span data-stu-id="93a6e-150">Install and configure hello solution</span></span>
<span data-ttu-id="93a6e-151">Use Olá tooinstall instruções a seguir e configure a solução de análise do hello Azure Application Gateway:</span><span class="sxs-lookup"><span data-stu-id="93a6e-151">Use hello following instructions tooinstall and configure hello Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="93a6e-152">Habilitar a solução de análise de Gateway de aplicativo do Azure de saudação do [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="93a6e-152">Enable hello Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="93a6e-153">Habilite o log de diagnóstico para Olá [Application Gateways](../application-gateway/application-gateway-diagnostics.md) toomonitor desejado.</span><span class="sxs-lookup"><span data-stu-id="93a6e-153">Enable diagnostics logging for hello [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want toomonitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a><span data-ttu-id="93a6e-154">Habilitar o diagnóstico de Gateway de aplicativo do Azure no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="93a6e-154">Enable Azure Application Gateway diagnostics in hello portal</span></span>

1. <span data-ttu-id="93a6e-155">No portal do Azure de Olá, navegar toomonitor de recurso do Application Gateway toohello</span><span class="sxs-lookup"><span data-stu-id="93a6e-155">In hello Azure portal, navigate toohello Application Gateway resource toomonitor</span></span>
2. <span data-ttu-id="93a6e-156">Selecione *logs de diagnóstico* tooopen Olá página a seguir</span><span class="sxs-lookup"><span data-stu-id="93a6e-156">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![imagem do recurso do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="93a6e-158">Clique em *Ativar diagnóstico* tooopen Olá página a seguir</span><span class="sxs-lookup"><span data-stu-id="93a6e-158">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![imagem do recurso do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="93a6e-160">tooturn em diagnóstico, clique em *na* em *Status*</span><span class="sxs-lookup"><span data-stu-id="93a6e-160">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="93a6e-161">Clique em Olá caixa de seleção *enviar tooLog análise*</span><span class="sxs-lookup"><span data-stu-id="93a6e-161">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="93a6e-162">Selecione um espaço de trabalho existente do Log Analytics ou crie um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="93a6e-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="93a6e-163">Clique em caixa de seleção de saudação em **Log** para cada Olá toocollect de tipos de log</span><span class="sxs-lookup"><span data-stu-id="93a6e-163">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="93a6e-164">Clique em *salvar* tooenable log de saudação do diagnóstico tooLog análise</span><span class="sxs-lookup"><span data-stu-id="93a6e-164">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="93a6e-165">Habilitar o diagnóstico de rede do Azure usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="93a6e-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="93a6e-166">saudação de script do PowerShell a seguir fornece um exemplo de como tooenable log de diagnóstico para os gateways de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="93a6e-166">hello following PowerShell script provides an example of how tooenable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="93a6e-167">Usar a análise do Gateway de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-167">Use Azure Application Gateway analytics</span></span>
![imagem do bloco Análise do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="93a6e-169">Depois de clicar em Olá **analytics do Azure Application Gateway** lado a lado em Olá visão geral, você pode exibir resumos dos seus logs e, em seguida, fazer uma busca de toodetails para Olá categorias a seguir:</span><span class="sxs-lookup"><span data-stu-id="93a6e-169">After you click hello **Azure Application Gateway analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="93a6e-170">Logs de acesso do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="93a6e-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="93a6e-171">Erros de cliente e servidor nos logs de acesso do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="93a6e-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="93a6e-172">Solicitações por hora para cada Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="93a6e-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="93a6e-173">Solicitações com falha por hora para cada Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="93a6e-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="93a6e-174">Erros por agente do usuário para Gateways de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="93a6e-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="93a6e-175">Desempenho do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="93a6e-175">Application Gateway performance</span></span>
  * <span data-ttu-id="93a6e-176">Integridade do host para o Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="93a6e-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="93a6e-177">Percentil 95 e máximo para solicitações com falha do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="93a6e-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![imagem do painel Análise do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![imagem do painel Análise do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="93a6e-180">Em Olá **analytics do Azure Application Gateway** painel, examine as informações de resumo de saudação em uma das folhas de saudação e, em seguida, clique em uma tooview informações detalhadas sobre a página de pesquisa de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="93a6e-180">On hello **Azure Application Gateway analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="93a6e-181">Em qualquer uma das páginas de pesquisa de log hello, você pode exibir os resultados por tempo, resultados detalhados e o histórico de pesquisa de log.</span><span class="sxs-lookup"><span data-stu-id="93a6e-181">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="93a6e-182">Você também pode filtrar pelos resultados de saudação toonarrow facetas.</span><span class="sxs-lookup"><span data-stu-id="93a6e-182">You can also filter by facets toonarrow hello results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="93a6e-183">Solução de análise de Grupo de Segurança de Rede do Azure no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="93a6e-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Símbolo da Análise do Grupo de Segurança de Rede do Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="93a6e-185">Olá logs a seguir têm suporte para grupos de segurança de rede:</span><span class="sxs-lookup"><span data-stu-id="93a6e-185">hello following logs are supported for network security groups:</span></span>

* <span data-ttu-id="93a6e-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="93a6e-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="93a6e-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="93a6e-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="93a6e-188">Instalar e configurar a solução de saudação</span><span class="sxs-lookup"><span data-stu-id="93a6e-188">Install and configure hello solution</span></span>
<span data-ttu-id="93a6e-189">Use Olá tooinstall instruções a seguir e configurar a solução de análise de rede do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="93a6e-189">Use hello following instructions tooinstall and configure hello Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="93a6e-190">Habilitar a solução de análise de grupo de segurança de rede do Azure de saudação do [do Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="93a6e-190">Enable hello Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="93a6e-191">Habilite o log de diagnóstico para Olá [grupo de segurança de rede](../virtual-network/virtual-network-nsg-manage-log.md) recursos que você deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="93a6e-191">Enable diagnostics logging for hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want toomonitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a><span data-ttu-id="93a6e-192">Habilitar o diagnóstico de grupo de segurança de rede do Azure no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="93a6e-192">Enable Azure network security group diagnostics in hello portal</span></span>

1. <span data-ttu-id="93a6e-193">No portal do Azure de Olá, navegar toohello toomonitor de recurso de grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="93a6e-193">In hello Azure portal, navigate toohello Network Security Group resource toomonitor</span></span>
2. <span data-ttu-id="93a6e-194">Selecione *logs de diagnóstico* tooopen Olá página a seguir</span><span class="sxs-lookup"><span data-stu-id="93a6e-194">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![imagem do recurso de Grupo de Segurança de Rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="93a6e-196">Clique em *Ativar diagnóstico* tooopen Olá página a seguir</span><span class="sxs-lookup"><span data-stu-id="93a6e-196">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![imagem do recurso de Grupo de Segurança de Rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="93a6e-198">tooturn em diagnóstico, clique em *na* em *Status*</span><span class="sxs-lookup"><span data-stu-id="93a6e-198">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="93a6e-199">Clique em Olá caixa de seleção *enviar tooLog análise*</span><span class="sxs-lookup"><span data-stu-id="93a6e-199">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="93a6e-200">Selecione um espaço de trabalho existente do Log Analytics ou crie um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="93a6e-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="93a6e-201">Clique em caixa de seleção de saudação em **Log** para cada Olá toocollect de tipos de log</span><span class="sxs-lookup"><span data-stu-id="93a6e-201">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="93a6e-202">Clique em *salvar* tooenable log de saudação do diagnóstico tooLog análise</span><span class="sxs-lookup"><span data-stu-id="93a6e-202">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="93a6e-203">Habilitar o diagnóstico de rede do Azure usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="93a6e-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="93a6e-204">saudação de script do PowerShell a seguir fornece um exemplo de como tooenable log de diagnóstico para os grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="93a6e-204">hello following PowerShell script provides an example of how tooenable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="93a6e-205">Usar a análise de Grupo de Segurança de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="93a6e-206">Depois de clicar em Olá **análise do grupo de segurança de rede do Azure** lado a lado em Olá visão geral, você pode exibir resumos dos seus logs e, em seguida, fazer uma busca de toodetails para Olá categorias a seguir:</span><span class="sxs-lookup"><span data-stu-id="93a6e-206">After you click hello **Azure Network Security Group analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="93a6e-207">Fluxos bloqueados no grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="93a6e-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="93a6e-208">Regras do grupo de segurança de rede com fluxos bloqueados</span><span class="sxs-lookup"><span data-stu-id="93a6e-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="93a6e-209">Endereços MAC com fluxos bloqueados</span><span class="sxs-lookup"><span data-stu-id="93a6e-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="93a6e-210">Fluxos permitidos no grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="93a6e-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="93a6e-211">Regras com fluxos permitidos do grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="93a6e-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="93a6e-212">Endereços MAC com fluxos permitidos</span><span class="sxs-lookup"><span data-stu-id="93a6e-212">MAC addresses with allowed flows</span></span>

![imagem do painel Análise do Grupo de Segurança de Rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![imagem do painel Análise do Grupo de Segurança de Rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="93a6e-215">Em Olá **análise do grupo de segurança de rede do Azure** painel, examine as informações de resumo de saudação em uma das folhas de saudação e, em seguida, clique em uma tooview informações detalhadas sobre a página de pesquisa de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="93a6e-215">On hello **Azure Network Security Group analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="93a6e-216">Em qualquer uma das páginas de pesquisa de log hello, você pode exibir os resultados por tempo, resultados detalhados e o histórico de pesquisa de log.</span><span class="sxs-lookup"><span data-stu-id="93a6e-216">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="93a6e-217">Você também pode filtrar pelos resultados de saudação toonarrow facetas.</span><span class="sxs-lookup"><span data-stu-id="93a6e-217">You can also filter by facets toonarrow hello results.</span></span>

## <a name="migrating-from-hello-old-networking-analytics-solution"></a><span data-ttu-id="93a6e-218">Migrando de solução de análise de rede antiga Olá</span><span class="sxs-lookup"><span data-stu-id="93a6e-218">Migrating from hello old Networking Analytics solution</span></span>
<span data-ttu-id="93a6e-219">Em janeiro de 2017, Olá suporte para a forma de envio de logs do Azure Application Gateways e grupos de segurança de rede do Azure tooLog alterada de análise.</span><span class="sxs-lookup"><span data-stu-id="93a6e-219">In January 2017, hello supported way of sending logs from Azure Application Gateways and Azure Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="93a6e-220">Essas alterações fornecem Olá vantagens a seguir:</span><span class="sxs-lookup"><span data-stu-id="93a6e-220">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="93a6e-221">Os logs são gravados diretamente tooLog análise sem Olá necessário toouse uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="93a6e-221">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="93a6e-222">Menor latência de tempo de saudação quando os logs são gerados toothem disponíveis na análise de Log</span><span class="sxs-lookup"><span data-stu-id="93a6e-222">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="93a6e-223">Menos etapas de configuração</span><span class="sxs-lookup"><span data-stu-id="93a6e-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="93a6e-224">Um formato comum para todos os tipos de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="93a6e-225">Olá toouse atualizado soluções:</span><span class="sxs-lookup"><span data-stu-id="93a6e-225">toouse hello updated solutions:</span></span>

1. [<span data-ttu-id="93a6e-226">Configurar o diagnóstico toobe enviado diretamente tooLog análise de Gateways de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-226">Configure diagnostics toobe sent directly tooLog Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="93a6e-227">Configurar o diagnóstico toobe enviado diretamente tooLog análise de grupos de segurança de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="93a6e-227">Configure diagnostics toobe sent directly tooLog Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="93a6e-228">Habilitar Olá *análises de Gateway do aplicativo do Azure* e hello *análise de grupo de segurança de rede do Azure* solução usando Olá processo descrito em [soluções adicionar análise de Log Olá Galeria de soluções](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="93a6e-228">Enable hello *Azure Application Gateway Analytics* and hello *Azure Network Security Group Analytics* solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="93a6e-229">Atualizar todos os painéis, as consultas salvas ou alertas toouse Olá novo tipo de dados</span><span class="sxs-lookup"><span data-stu-id="93a6e-229">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="93a6e-230">O tipo é tooAzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="93a6e-230">Type is tooAzureDiagnostics.</span></span> <span data-ttu-id="93a6e-231">Você pode usar os logs de sistema de rede do hello ResourceType toofilter tooAzure.</span><span class="sxs-lookup"><span data-stu-id="93a6e-231">You can use hello ResourceType toofilter tooAzure networking logs.</span></span>

    | <span data-ttu-id="93a6e-232">Em vez de:</span><span class="sxs-lookup"><span data-stu-id="93a6e-232">Instead of:</span></span> | <span data-ttu-id="93a6e-233">Use:</span><span class="sxs-lookup"><span data-stu-id="93a6e-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="93a6e-234">Para qualquer campo que tenha um sufixo de \_s, \_d, ou \_g em nome do hello, alteração Olá primeiro caractere toolower caso</span><span class="sxs-lookup"><span data-stu-id="93a6e-234">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
   + <span data-ttu-id="93a6e-235">Para qualquer campo que tenha um sufixo de \_o nome, dados de saudação é dividido em campos individuais com base nos nomes de campo Olá aninhado.</span><span class="sxs-lookup"><span data-stu-id="93a6e-235">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span>
4. <span data-ttu-id="93a6e-236">Remover Olá *análise de rede do Azure (preterido)* solução.</span><span class="sxs-lookup"><span data-stu-id="93a6e-236">Remove hello *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="93a6e-237">Se você estiver usando o PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="93a6e-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="93a6e-238">Os dados coletados antes de alterar Olá não estiver visível na nova solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="93a6e-238">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="93a6e-239">Você pode continuar tooquery para esse dados usando Olá tipo antigo e nomes de campo.</span><span class="sxs-lookup"><span data-stu-id="93a6e-239">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="93a6e-240">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="93a6e-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="93a6e-241">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="93a6e-241">Next steps</span></span>
* <span data-ttu-id="93a6e-242">Use [pesquisas de Log na análise de Log](log-analytics-log-searches.md) tooview obter dados de diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="93a6e-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure diagnostics data.</span></span>
