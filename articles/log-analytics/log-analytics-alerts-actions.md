---
title: "tooalerts aaaResponses na análise de Log do OMS | Microsoft Docs"
description: "Alertas de análise de Log identificar informações importantes no seu repositório do OMS e podem proativamente notificá-lo de problemas ou invocar ações tooattempt toocorrect-los.  Este artigo descreve como toocreate uma regra de alerta e ações diferentes de saudação de detalhes que podem executar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a><span data-ttu-id="79c94-104">Adicione regras de tooalert de ações na análise de Log</span><span class="sxs-lookup"><span data-stu-id="79c94-104">Add actions tooalert rules in Log Analytics</span></span>
<span data-ttu-id="79c94-105">Quando um [alerta é criado na análise de Log](log-analytics-alerts.md), você tem a opção de saudação do [configurar regra de alerta Olá](log-analytics-alerts.md) tooperform uma ou mais ações.</span><span class="sxs-lookup"><span data-stu-id="79c94-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have hello option of [configuring hello alert rule](log-analytics-alerts.md) tooperform one or more actions.</span></span>  <span data-ttu-id="79c94-106">Este artigo descreve ações diferentes de saudação que estão disponíveis e os detalhes sobre como configurar cada tipo.</span><span class="sxs-lookup"><span data-stu-id="79c94-106">This article describes hello different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="79c94-107">Ação</span><span class="sxs-lookup"><span data-stu-id="79c94-107">Action</span></span> | <span data-ttu-id="79c94-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="79c94-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="79c94-109">Email</span><span class="sxs-lookup"><span data-stu-id="79c94-109">Email</span></span>](#email-actions) | <span data-ttu-id="79c94-110">Envie um email com detalhes de saudação do tooone alerta hello ou mais destinatários.</span><span class="sxs-lookup"><span data-stu-id="79c94-110">Send an e-mail with hello details of hello alert tooone or more recipients.</span></span> |
| [<span data-ttu-id="79c94-111">Webhook</span><span class="sxs-lookup"><span data-stu-id="79c94-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="79c94-112">Invoque um processo externo por meio de uma única solicitação HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="79c94-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="79c94-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="79c94-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="79c94-114">Inicie um runbook na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="79c94-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="79c94-115">Ações de email</span><span class="sxs-lookup"><span data-stu-id="79c94-115">Email actions</span></span>
<span data-ttu-id="79c94-116">Ações de email enviar um email com detalhes de saudação do tooone alerta hello ou mais destinatários.</span><span class="sxs-lookup"><span data-stu-id="79c94-116">Email actions send an e-mail with hello details of hello alert tooone or more recipients.</span></span>  <span data-ttu-id="79c94-117">Você pode especificar o assunto de saudação do email hello, mas seu conteúdo é um formato padrão criado pela análise de Log.</span><span class="sxs-lookup"><span data-stu-id="79c94-117">You can specify hello subject of hello mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="79c94-118">Ele inclui informações de resumo, como nome de saudação do alerta de saudação em toodetails de adição de registros tooten retornado pela pesquisa de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-118">It includes summary information such as hello name of hello alert in addition toodetails of up tooten records returned by hello log search.</span></span>  <span data-ttu-id="79c94-119">Ele também inclui uma pesquisa de log de tooa link na análise de Log que retornará todo o conjunto de registros de saudação da consulta.</span><span class="sxs-lookup"><span data-stu-id="79c94-119">It also includes a link tooa log search in Log Analytics that will return hello entire set of records from that query.</span></span>   <span data-ttu-id="79c94-120">Olá remetente do email Olá é *equipe do Microsoft Operations Management Suite &lt; noreply@oms.microsoft.com &gt;* .</span><span class="sxs-lookup"><span data-stu-id="79c94-120">hello sender of hello mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="79c94-121">Ações de email exigem propriedades Olá Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="79c94-121">Email actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="79c94-122">Propriedade</span><span class="sxs-lookup"><span data-stu-id="79c94-122">Property</span></span> | <span data-ttu-id="79c94-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="79c94-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="79c94-124">Assunto</span><span class="sxs-lookup"><span data-stu-id="79c94-124">Subject</span></span> |<span data-ttu-id="79c94-125">Assunto no email de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-125">Subject in hello email.</span></span>  <span data-ttu-id="79c94-126">Não é possível modificar o corpo de saudação de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-126">You cannot modify hello body of hello mail.</span></span> |
| <span data-ttu-id="79c94-127">Destinatários</span><span class="sxs-lookup"><span data-stu-id="79c94-127">Recipients</span></span> |<span data-ttu-id="79c94-128">Endereços de todos os destinatários de email.</span><span class="sxs-lookup"><span data-stu-id="79c94-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="79c94-129">Se você especificar mais de um endereço e endereços de saudação separada com um ponto e vírgula (;).</span><span class="sxs-lookup"><span data-stu-id="79c94-129">If you specify more than one address, then separate hello addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="79c94-130">Ações de Webhook</span><span class="sxs-lookup"><span data-stu-id="79c94-130">Webhook actions</span></span>

<span data-ttu-id="79c94-131">Ações de Webhook permitem tooinvoke um processo externo por meio de uma única solicitação HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="79c94-131">Webhook actions allow you tooinvoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="79c94-132">o serviço de Hello está sendo chamado deve suporte webhooks e determinar como ele usará qualquer carga recebe.</span><span class="sxs-lookup"><span data-stu-id="79c94-132">hello service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="79c94-133">Você poderia chamar uma API REST que não dão suporte especificamente às webhooks como solicitação hello está em um formato que Olá que API compreende.</span><span class="sxs-lookup"><span data-stu-id="79c94-133">You could also call a REST API that doesn't specifically support webhooks as long as hello request is in a format that hello API understands.</span></span>  <span data-ttu-id="79c94-134">Exemplos de como usar um webhook no alerta de tooan resposta estão enviando uma mensagem no [Slack](http://slack.com) ou criar um incidente no [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="79c94-134">Examples of using a webhook in response tooan alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="79c94-135">Instruções completas para a criação de uma regra de alerta com um atraso de toocall de webhook está disponível em [Webhooks em alertas de análise de Log](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="79c94-135">A complete walkthrough of creating an alert rule with a webhook toocall Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="79c94-136">Ações de Webhook exigem propriedades Olá Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="79c94-136">Webhook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="79c94-137">Propriedade</span><span class="sxs-lookup"><span data-stu-id="79c94-137">Property</span></span> | <span data-ttu-id="79c94-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="79c94-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="79c94-139">URL de Webhook</span><span class="sxs-lookup"><span data-stu-id="79c94-139">Webhook URL</span></span> |<span data-ttu-id="79c94-140">URL de saudação do webhook hello.</span><span class="sxs-lookup"><span data-stu-id="79c94-140">hello URL of hello webhook.</span></span> |
| <span data-ttu-id="79c94-141">Carga JSON personalizada</span><span class="sxs-lookup"><span data-stu-id="79c94-141">Custom JSON payload</span></span> |<span data-ttu-id="79c94-142">Carga personalizada toosend com hello webhook.</span><span class="sxs-lookup"><span data-stu-id="79c94-142">Custom payload toosend with hello webhook.</span></span>  <span data-ttu-id="79c94-143">Confira os detalhes abaixo.</span><span class="sxs-lookup"><span data-stu-id="79c94-143">See below for details.</span></span> |


<span data-ttu-id="79c94-144">Webhooks incluir uma URL e uma carga formatada em JSON Olá dados enviados serviço externo toohello.</span><span class="sxs-lookup"><span data-stu-id="79c94-144">Webhooks include a URL and a payload formatted in JSON that is hello data sent toohello external service.</span></span>  <span data-ttu-id="79c94-145">Por padrão, a carga de saudação incluirá valores hello no Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="79c94-145">By default, hello payload will include hello values in hello following table.</span></span>  <span data-ttu-id="79c94-146">Você pode escolher tooreplace essa carga com um personalizado de sua preferência.</span><span class="sxs-lookup"><span data-stu-id="79c94-146">You can choose tooreplace this payload with a custom one of your own.</span></span>  <span data-ttu-id="79c94-147">Nesse caso você pode usar variáveis de saudação na tabela de saudação para cada Olá parâmetros tooinclude seu valor em sua carga personalizada.</span><span class="sxs-lookup"><span data-stu-id="79c94-147">In that case you can use hello variables in hello table for each of hello parameters tooinclude their value in your custom payload.</span></span>

| <span data-ttu-id="79c94-148">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="79c94-148">Parameter</span></span> | <span data-ttu-id="79c94-149">Variável</span><span class="sxs-lookup"><span data-stu-id="79c94-149">Variable</span></span> | <span data-ttu-id="79c94-150">Descrição</span><span class="sxs-lookup"><span data-stu-id="79c94-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="79c94-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="79c94-151">AlertRuleName</span></span> |<span data-ttu-id="79c94-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="79c94-152">#alertrulename</span></span> |<span data-ttu-id="79c94-153">Nome da regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-153">Name of hello alert rule.</span></span> |
| <span data-ttu-id="79c94-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="79c94-154">AlertThresholdOperator</span></span> |<span data-ttu-id="79c94-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="79c94-155">#thresholdoperator</span></span> |<span data-ttu-id="79c94-156">Operador de limite para a regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-156">Threshold operator for hello alert rule.</span></span>  <span data-ttu-id="79c94-157">*Greater than (Maior que)* ou *Less than (Menor que)*.</span><span class="sxs-lookup"><span data-stu-id="79c94-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="79c94-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="79c94-158">AlertThresholdValue</span></span> |<span data-ttu-id="79c94-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="79c94-159">#thresholdvalue</span></span> |<span data-ttu-id="79c94-160">Valor de limite para a regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-160">Threshold value for hello alert rule.</span></span> |
| <span data-ttu-id="79c94-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="79c94-161">LinkToSearchResults</span></span> |<span data-ttu-id="79c94-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="79c94-162">#linktosearchresults</span></span> |<span data-ttu-id="79c94-163">Vincule a pesquisa de log de análise de tooLog que retorna registros de saudação da consulta de saudação que criou o alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-163">Link tooLog Analytics log search that returns hello records from hello query that created hello alert.</span></span> |
| <span data-ttu-id="79c94-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="79c94-164">ResultCount</span></span> |<span data-ttu-id="79c94-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="79c94-165">#searchresultcount</span></span> |<span data-ttu-id="79c94-166">Número de registros nos resultados da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="79c94-166">Number of records in hello search results.</span></span> |
| <span data-ttu-id="79c94-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="79c94-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="79c94-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="79c94-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="79c94-169">Hora de término para a consulta Olá no formato UTC.</span><span class="sxs-lookup"><span data-stu-id="79c94-169">End time for hello query in UTC format.</span></span> |
| <span data-ttu-id="79c94-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="79c94-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="79c94-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="79c94-171">#searchinterval</span></span> |<span data-ttu-id="79c94-172">Janela de tempo para a regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-172">Time window for hello alert rule.</span></span> |
| <span data-ttu-id="79c94-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="79c94-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="79c94-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="79c94-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="79c94-175">Hora de consulta de saudação de início no formato UTC.</span><span class="sxs-lookup"><span data-stu-id="79c94-175">Start time for hello query in UTC format.</span></span> |
| <span data-ttu-id="79c94-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="79c94-176">SearchQuery</span></span> |<span data-ttu-id="79c94-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="79c94-177">#searchquery</span></span> |<span data-ttu-id="79c94-178">Consulta de pesquisa de log usada pela regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-178">Log search query used by hello alert rule.</span></span> |
| <span data-ttu-id="79c94-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="79c94-179">SearchResults</span></span> |<span data-ttu-id="79c94-180">Veja abaixo</span><span class="sxs-lookup"><span data-stu-id="79c94-180">See below</span></span> |<span data-ttu-id="79c94-181">Registros retornados pela consulta Olá no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="79c94-181">Records returned by hello query in JSON format.</span></span>  <span data-ttu-id="79c94-182">Limitado toohello registros primeiros 5.000.</span><span class="sxs-lookup"><span data-stu-id="79c94-182">Limited toohello first 5,000 records.</span></span> |
| <span data-ttu-id="79c94-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="79c94-183">WorkspaceID</span></span> |<span data-ttu-id="79c94-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="79c94-184">#workspaceid</span></span> |<span data-ttu-id="79c94-185">ID do seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="79c94-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="79c94-186">Por exemplo, você pode especificar Olá carga personalizada que inclui um único parâmetro de chamada a seguir *texto*.</span><span class="sxs-lookup"><span data-stu-id="79c94-186">For example, you might specify hello following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="79c94-187">serviço de saudação que chama esse webhook seria esperando esse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="79c94-187">hello service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="79c94-188">Essa carga de exemplo resolveria toosomething como Olá a seguir quando enviadas toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="79c94-188">This example payload would resolve toosomething like hello following when sent toohello webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="79c94-189">tooinclude resultados da pesquisa em uma carga personalizada, adicione Olá linha a seguir como uma propriedade de nível superior na carga de json hello.</span><span class="sxs-lookup"><span data-stu-id="79c94-189">tooinclude search results in a custom payload, add hello following line as a top level property in hello json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="79c94-190">Por exemplo, toocreate uma carga personalizada que inclui apenas o nome do alerta hello e resultados da pesquisa hello, você pode usar Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="79c94-190">For example, toocreate a custom payload that includes just hello alert name and hello search results, you could use hello following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="79c94-191">Você pode percorrer um exemplo completo de como criar uma regra de alerta com um webhook toostart um serviço externo no [criar uma ação de alerta do webhook na análise de logs do OMS toosend mensagem tooSlack](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="79c94-191">You can walk through a complete example of creating an alert rule with a webhook toostart an external service at [Create an alert webhook action in OMS Log Analytics toosend message tooSlack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="79c94-192">Ações de runbook</span><span class="sxs-lookup"><span data-stu-id="79c94-192">Runbook actions</span></span>
<span data-ttu-id="79c94-193">Ações de runbook iniciam um runbook na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="79c94-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="79c94-194">Em ordem toouse esse tipo de ação, você deve ter Olá [solução de automação](log-analytics-add-solutions.md) instalado e configurado em seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="79c94-194">In order toouse this type of action, you must have hello [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="79c94-195">Você pode selecionar Olá runbooks na conta de automação de saudação que você configurou no hello solução de automação.</span><span class="sxs-lookup"><span data-stu-id="79c94-195">You can select from hello runbooks in hello automation account that you configured in hello Automation solution.</span></span>

<span data-ttu-id="79c94-196">Ações de runbook exigem propriedades Olá Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="79c94-196">Runbook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="79c94-197">Propriedade</span><span class="sxs-lookup"><span data-stu-id="79c94-197">Property</span></span> | <span data-ttu-id="79c94-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="79c94-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="79c94-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="79c94-199">Runbook</span></span> | <span data-ttu-id="79c94-200">Runbook que você deseja toostart quando um alerta é criado.</span><span class="sxs-lookup"><span data-stu-id="79c94-200">Runbook that you want toostart when an alert is created.</span></span> |
| <span data-ttu-id="79c94-201">Executar em</span><span class="sxs-lookup"><span data-stu-id="79c94-201">Run on</span></span> | <span data-ttu-id="79c94-202">Especifique **Azure** toorun Olá runbook na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="79c94-202">Specify **Azure** toorun hello runbook in hello cloud.</span></span>  <span data-ttu-id="79c94-203">Especifique **Hybrid worker** toorun Olá runbook em um agente com [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) instalado.</span><span class="sxs-lookup"><span data-stu-id="79c94-203">Specify **Hybrid worker** toorun hello runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="79c94-204">Iniciar o runbook ações Olá runbook usando um [webhook](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="79c94-204">Runbook actions start hello runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="79c94-205">Quando você criar regra de alerta hello, ele criará automaticamente um webhook novo runbook Olá com nome hello **correção de alerta do OMS** seguido por um GUID.</span><span class="sxs-lookup"><span data-stu-id="79c94-205">When you create hello alert rule, it will automatically create a new webhook for hello runbook with hello name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="79c94-206">Diretamente você não pode preencher quaisquer parâmetros de runbook hello, mas Olá [$WebhookData parâmetro](../automation/automation-webhooks.md) incluirá Olá detalhes do alerta hello, incluindo Olá resultados da pesquisa de log de saudação que o criou.</span><span class="sxs-lookup"><span data-stu-id="79c94-206">You cannot directly populate any parameters of hello runbook, but hello [$WebhookData parameter](../automation/automation-webhooks.md) will include hello details of hello alert, including hello results of hello log search that created it.</span></span>  <span data-ttu-id="79c94-207">Olá runbook precisará toodefine **$WebhookData** como um parâmetro para que ele tooaccess Olá propriedades do alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-207">hello runbook will need toodefine **$WebhookData** as a parameter for it tooaccess hello properties of hello alert.</span></span>  <span data-ttu-id="79c94-208">Olá dados de alerta estão disponíveis no formato json em uma única propriedade chamado **SearchResults** em Olá **RequestBody** propriedade **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="79c94-208">hello alert data is available in json format in a single property called **SearchResults** in hello **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="79c94-209">Isso será necessário com propriedades Olá Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="79c94-209">This will have with hello properties in hello following table.</span></span>

| <span data-ttu-id="79c94-210">Nó</span><span class="sxs-lookup"><span data-stu-id="79c94-210">Node</span></span> | <span data-ttu-id="79c94-211">Descrição</span><span class="sxs-lookup"><span data-stu-id="79c94-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="79c94-212">ID</span><span class="sxs-lookup"><span data-stu-id="79c94-212">id</span></span> |<span data-ttu-id="79c94-213">Caminho e o GUID da pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-213">Path and GUID of hello search.</span></span> |
| <span data-ttu-id="79c94-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="79c94-214">__metadata</span></span> |<span data-ttu-id="79c94-215">Informações sobre Olá alerta incluindo Olá número de registros e status Olá dos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="79c94-215">Information about hello alert including hello number of records and status of hello search results.</span></span> |
| <span data-ttu-id="79c94-216">valor</span><span class="sxs-lookup"><span data-stu-id="79c94-216">value</span></span> |<span data-ttu-id="79c94-217">Entrada separada para cada registro nos resultados da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="79c94-217">Separate entry for each record in hello search results.</span></span>  <span data-ttu-id="79c94-218">detalhes de saudação de entrada hello corresponderá propriedades hello e valores de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="79c94-218">hello details of hello entry will match hello properties and values of hello record.</span></span> |

<span data-ttu-id="79c94-219">Por exemplo, hello runbook a seguir seria extrair Olá registros retornados pela pesquisa de log hello e atribuir propriedades diferentes com base no tipo de saudação de cada registro.</span><span class="sxs-lookup"><span data-stu-id="79c94-219">For example, hello following runbook would extract hello records returned by hello log search  and assign different properties based on hello type of each record.</span></span>  <span data-ttu-id="79c94-220">Observe que esse runbook Olá inicia convertendo **RequestBody** do json para que ele pode ser editado como um objeto no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79c94-220">Note that hello runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a><span data-ttu-id="79c94-221">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79c94-221">Next steps</span></span>
- <span data-ttu-id="79c94-222">Conclua um passo a passo para [configurar um webhook](log-analytics-alerts-webhooks.md) com uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="79c94-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="79c94-223">Saiba como toowrite [runbooks na automação do Azure](https://azure.microsoft.com/documentation/services/automation) tooremediate problemas identificados por alertas.</span><span class="sxs-lookup"><span data-stu-id="79c94-223">Learn how toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problems identified by alerts.</span></span>
