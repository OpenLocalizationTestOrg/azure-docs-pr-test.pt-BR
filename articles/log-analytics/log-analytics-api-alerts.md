---
title: aaaUsing API REST para alertas do OMS Log Analytics
description: "Olá API de REST de alerta da análise de Log permite que você toocreate e gerencie alertas na análise de Log que é parte do Operations Management Suite (OMS).  Este artigo fornece detalhes de saudação API e vários exemplos para executar operações diferentes."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="03310-104">Criar e gerenciar regras de alerta no Log Analytics com a API REST</span><span class="sxs-lookup"><span data-stu-id="03310-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="03310-105">Olá API de REST de alerta da análise de Log permite toocreate e gerenciar alertas no OMS Operations Management Suite ().</span><span class="sxs-lookup"><span data-stu-id="03310-105">hello Log Analytics Alert REST API allows you toocreate and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="03310-106">Este artigo fornece detalhes de saudação API e vários exemplos para executar operações diferentes.</span><span class="sxs-lookup"><span data-stu-id="03310-106">This article provides details of hello API and several examples for performing different operations.</span></span>

<span data-ttu-id="03310-107">Olá API de REST de pesquisa de análise de Log é RESTful e pode ser acessado via Olá API de REST do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="03310-107">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager REST API.</span></span> <span data-ttu-id="03310-108">Neste documento você encontrará exemplos em que o hello API é acessada de uma linha de comando do PowerShell usando [ARMClient](https://github.com/projectkudu/ARMClient), uma ferramenta de linha de comando de software livre que simplifica a invocação Olá API do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="03310-108">In this document you will find examples where hello API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="03310-109">uso de saudação do ARMClient e do PowerShell é uma saudação de tooaccess muitas opções API de pesquisa de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="03310-109">hello use of ARMClient and PowerShell is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="03310-110">Com essas ferramentas, você pode utilizar Olá API RESTful do Gerenciador de recursos do Azure toomake chamadas tooOMS espaços de trabalho e executar comandos de pesquisa dentro deles.</span><span class="sxs-lookup"><span data-stu-id="03310-110">With these tools you can utilize hello RESTful Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="03310-111">Olá API produzirá tooyou de resultados de pesquisa no formato JSON, permitindo que você resultados da pesquisa Olá toouse de diferentes maneiras por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="03310-111">hello API will output search results tooyou in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03310-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="03310-112">Prerequisites</span></span>
<span data-ttu-id="03310-113">Atualmente, os alertas somente podem ser criados com uma pesquisa salva no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="03310-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="03310-114">Você pode consultar toohello [API de REST de pesquisa de Log](log-analytics-log-search-api.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="03310-114">You can refer toohello [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="03310-115">Agendas</span><span class="sxs-lookup"><span data-stu-id="03310-115">Schedules</span></span>
<span data-ttu-id="03310-116">Uma pesquisa salva pode ter um ou mais agendamentos.</span><span class="sxs-lookup"><span data-stu-id="03310-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="03310-117">Olá agenda define quantas vezes hello pesquisa é executada e intervalo de tempo de saudação sobre os critérios de saudação é identificado.</span><span class="sxs-lookup"><span data-stu-id="03310-117">hello schedule defines how often hello search is run and hello time interval over which hello criteria is identified.</span></span>
<span data-ttu-id="03310-118">Agendas têm propriedades de saudação no Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="03310-118">Schedules have hello properties in hello following table.</span></span>

| <span data-ttu-id="03310-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="03310-119">Property</span></span> | <span data-ttu-id="03310-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="03310-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="03310-121">Intervalo</span><span class="sxs-lookup"><span data-stu-id="03310-121">Interval</span></span> |<span data-ttu-id="03310-122">Frequência hello pesquisa é executada.</span><span class="sxs-lookup"><span data-stu-id="03310-122">How often hello search is run.</span></span> <span data-ttu-id="03310-123">Medida em minutos.</span><span class="sxs-lookup"><span data-stu-id="03310-123">Measured in minutes.</span></span> |
| <span data-ttu-id="03310-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="03310-124">QueryTimeSpan</span></span> |<span data-ttu-id="03310-125">intervalo de tempo de saudação em qual Olá critérios é avaliada.</span><span class="sxs-lookup"><span data-stu-id="03310-125">hello time interval over which hello criteria is evaluated.</span></span> <span data-ttu-id="03310-126">Deve ser maior que o intervalo tooor igual.</span><span class="sxs-lookup"><span data-stu-id="03310-126">Must be equal tooor greater than Interval.</span></span> <span data-ttu-id="03310-127">Medida em minutos.</span><span class="sxs-lookup"><span data-stu-id="03310-127">Measured in minutes.</span></span> |
| <span data-ttu-id="03310-128">Versão</span><span class="sxs-lookup"><span data-stu-id="03310-128">Version</span></span> |<span data-ttu-id="03310-129">Olá versão de API que está sendo usada.</span><span class="sxs-lookup"><span data-stu-id="03310-129">hello API version being used.</span></span>  <span data-ttu-id="03310-130">Atualmente, isso deve sempre ser definido too1.</span><span class="sxs-lookup"><span data-stu-id="03310-130">Currently, this should always be set too1.</span></span> |

<span data-ttu-id="03310-131">Por exemplo, considere uma consulta de evento com um Interval (Intervalo) de 15 minutos e Timespan (Período) de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="03310-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="03310-132">Nesse caso, Olá consulta será executada a cada 15 minutos, e um alerta será disparado se critérios Olá continuação tooresolve tootrue em um intervalo de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="03310-132">In this case, hello query would be run every 15 minutes, and an alert would be triggered if hello criteria continued tooresolve tootrue over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="03310-133">Recuperando agendamentos</span><span class="sxs-lookup"><span data-stu-id="03310-133">Retrieving schedules</span></span>
<span data-ttu-id="03310-134">Olá Use obter método tooretrieve todas as agendas de uma pesquisa salva.</span><span class="sxs-lookup"><span data-stu-id="03310-134">Use hello Get method tooretrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="03310-135">Olá Use obter método com um tooretrieve de ID de agenda uma agenda específica de uma pesquisa salva.</span><span class="sxs-lookup"><span data-stu-id="03310-135">Use hello Get method with a schedule ID tooretrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="03310-136">A seguir está um exemplo de resposta para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="03310-136">Following is a sample response for a schedule.</span></span>

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a><span data-ttu-id="03310-137">Criando uma agenda</span><span class="sxs-lookup"><span data-stu-id="03310-137">Creating a schedule</span></span>
<span data-ttu-id="03310-138">Use o método de Put de saudação com uma ID de agenda exclusiva toocreate uma nova agenda.</span><span class="sxs-lookup"><span data-stu-id="03310-138">Use hello Put method with a unique schedule ID toocreate a new schedule.</span></span>  <span data-ttu-id="03310-139">Observe que duas agendas não podem ter Olá a mesma ID mesmo se eles estão associados com diferentes pesquisas salvas.</span><span class="sxs-lookup"><span data-stu-id="03310-139">Note that two schedules cannot have hello same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="03310-140">Quando você cria uma agenda no console do OMS hello, um GUID é criado para ID de agenda hello.</span><span class="sxs-lookup"><span data-stu-id="03310-140">When you create a schedule in hello OMS console, a GUID is created for hello schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="03310-141">nome de saudação para pesquisas salvas todas as agendas e ações criadas com hello API de análise de Log deve ser em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="03310-141">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="03310-142">Editando um agendamento</span><span class="sxs-lookup"><span data-stu-id="03310-142">Editing a schedule</span></span>
<span data-ttu-id="03310-143">Use o método de Put de saudação com uma agenda existente ID para Olá mesmo salvo pesquisar toomodify agendar.</span><span class="sxs-lookup"><span data-stu-id="03310-143">Use hello Put method with an existing schedule ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="03310-144">corpo de saudação da solicitação Olá deve incluir Olá etag da agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-144">hello body of hello request must include hello etag of hello schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="03310-145">Excluindo agendamentos</span><span class="sxs-lookup"><span data-stu-id="03310-145">Deleting schedules</span></span>
<span data-ttu-id="03310-146">Use o método de exclusão de saudação com uma ID de agenda toodelete uma agenda.</span><span class="sxs-lookup"><span data-stu-id="03310-146">Use hello Delete method with a schedule ID toodelete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="03310-147">Ações</span><span class="sxs-lookup"><span data-stu-id="03310-147">Actions</span></span>
<span data-ttu-id="03310-148">Um agendamento pode ter várias ações.</span><span class="sxs-lookup"><span data-stu-id="03310-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="03310-149">Uma ação pode definir um ou mais tooperform de processos, como enviar um email ou iniciar um runbook, ou ele pode definir um limite que determina quando os resultados de saudação de uma pesquisa correspondem a alguns critérios.</span><span class="sxs-lookup"><span data-stu-id="03310-149">An action may define one or more processes tooperform such as sending a mail or starting a runbook, or it may define a threshold that determines when hello results of a search match some criteria.</span></span>  <span data-ttu-id="03310-150">Algumas ações definirá ambos para que os processos de saudação são executados quando Olá limite é atingido.</span><span class="sxs-lookup"><span data-stu-id="03310-150">Some actions will define both so that hello processes are performed when hello threshold is met.</span></span>

<span data-ttu-id="03310-151">Todas as ações têm propriedades de saudação no Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="03310-151">All actions have hello properties in hello following table.</span></span>  <span data-ttu-id="03310-152">Diferentes tipos de alertas têm diferentes propriedades adicionais que são descritas abaixo.</span><span class="sxs-lookup"><span data-stu-id="03310-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="03310-153">Propriedade</span><span class="sxs-lookup"><span data-stu-id="03310-153">Property</span></span> | <span data-ttu-id="03310-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="03310-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="03310-155">Tipo</span><span class="sxs-lookup"><span data-stu-id="03310-155">Type</span></span> |<span data-ttu-id="03310-156">Tipo de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-156">Type of hello action.</span></span>  <span data-ttu-id="03310-157">No momento Olá possíveis valores são alerta e Webhook.</span><span class="sxs-lookup"><span data-stu-id="03310-157">Currently hello possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="03310-158">Nome</span><span class="sxs-lookup"><span data-stu-id="03310-158">Name</span></span> |<span data-ttu-id="03310-159">Nome de exibição de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-159">Display name for hello alert.</span></span> |
| <span data-ttu-id="03310-160">Versão</span><span class="sxs-lookup"><span data-stu-id="03310-160">Version</span></span> |<span data-ttu-id="03310-161">Olá versão de API que está sendo usada.</span><span class="sxs-lookup"><span data-stu-id="03310-161">hello API version being used.</span></span>  <span data-ttu-id="03310-162">Atualmente, isso deve sempre ser definido too1.</span><span class="sxs-lookup"><span data-stu-id="03310-162">Currently, this should always be set too1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="03310-163">Recuperando ações</span><span class="sxs-lookup"><span data-stu-id="03310-163">Retrieving actions</span></span>
<span data-ttu-id="03310-164">Olá Use obter método tooretrieve todas as ações de uma agenda.</span><span class="sxs-lookup"><span data-stu-id="03310-164">Use hello Get method tooretrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="03310-165">Olá Use obter método com hello tooretrieve de ID de ação uma ação específica para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="03310-165">Use hello Get method with hello action ID tooretrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="03310-166">Criar ou editar ações</span><span class="sxs-lookup"><span data-stu-id="03310-166">Creating or editing actions</span></span>
<span data-ttu-id="03310-167">Use o método de Put de saudação com uma ID de ação que é exclusivo toohello agenda toocreate uma nova ação.</span><span class="sxs-lookup"><span data-stu-id="03310-167">Use hello Put method with an action ID that is unique toohello schedule toocreate a new action.</span></span>  <span data-ttu-id="03310-168">Quando você cria uma ação no console do OMS hello, um GUID é para ID de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-168">When you create an action in hello OMS console, a GUID is for hello action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="03310-169">nome de saudação para pesquisas salvas todas as agendas e ações criadas com hello API de análise de Log deve ser em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="03310-169">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="03310-170">Use o método de Put de saudação com uma ação de ID para Olá mesmo salvo pesquisar toomodify agendar.</span><span class="sxs-lookup"><span data-stu-id="03310-170">Use hello Put method with an existing action ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="03310-171">corpo de saudação da solicitação Olá deve incluir Olá etag da agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-171">hello body of hello request must include hello etag of hello schedule.</span></span>

<span data-ttu-id="03310-172">formato da solicitação Olá para criar uma nova ação varia de acordo com o tipo de ação para que esses exemplos são fornecidos nas seções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="03310-172">hello request format for creating a new action varies by action type so these examples are provided in hello sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="03310-173">Excluindo ações</span><span class="sxs-lookup"><span data-stu-id="03310-173">Deleting actions</span></span>
<span data-ttu-id="03310-174">Use o método de exclusão de Olá com hello ação ID toodelete uma ação.</span><span class="sxs-lookup"><span data-stu-id="03310-174">Use hello Delete method with hello action ID toodelete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="03310-175">Ações de Alerta</span><span class="sxs-lookup"><span data-stu-id="03310-175">Alert Actions</span></span>
<span data-ttu-id="03310-176">Um Agendamento deve ter somente uma ação de Alerta.</span><span class="sxs-lookup"><span data-stu-id="03310-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="03310-177">Ações de alerta tem uma ou mais das seções Olá Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="03310-177">Alert actions have one or more of hello sections in hello following table.</span></span>  <span data-ttu-id="03310-178">Elas são descritas em mais detalhes abaixo.</span><span class="sxs-lookup"><span data-stu-id="03310-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="03310-179">Seção</span><span class="sxs-lookup"><span data-stu-id="03310-179">Section</span></span> | <span data-ttu-id="03310-180">Descrição</span><span class="sxs-lookup"><span data-stu-id="03310-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="03310-181">Limite</span><span class="sxs-lookup"><span data-stu-id="03310-181">Threshold</span></span> |<span data-ttu-id="03310-182">Critérios para quando a ação de saudação é executada.</span><span class="sxs-lookup"><span data-stu-id="03310-182">Criteria for when hello action is run.</span></span> |
| <span data-ttu-id="03310-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="03310-183">EmailNotification</span></span> |<span data-ttu-id="03310-184">Envie email de destinatários toomultiple.</span><span class="sxs-lookup"><span data-stu-id="03310-184">Send mail toomultiple recipients.</span></span> |
| <span data-ttu-id="03310-185">Correção</span><span class="sxs-lookup"><span data-stu-id="03310-185">Remediation</span></span> |<span data-ttu-id="03310-186">Iniciar um runbook na automação do Azure tooattempt toocorrect identificado o problema.</span><span class="sxs-lookup"><span data-stu-id="03310-186">Start a runbook in Azure Automation tooattempt toocorrect identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="03310-187">Limites</span><span class="sxs-lookup"><span data-stu-id="03310-187">Thresholds</span></span>
<span data-ttu-id="03310-188">Uma ação de Alerta deve ter somente um limite.</span><span class="sxs-lookup"><span data-stu-id="03310-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="03310-189">Quando os resultados de saudação de uma pesquisa salva correspondem limite de saudação em uma ação associada que a pesquisa, outros processos na ação são executados.</span><span class="sxs-lookup"><span data-stu-id="03310-189">When hello results of a saved search match hello threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="03310-190">Uma ação também pode conter apenas um limite para ser usado com ações de outros tipos que não contêm os limites.</span><span class="sxs-lookup"><span data-stu-id="03310-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="03310-191">Limites têm as propriedades de saudação no Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="03310-191">Thresholds have hello properties in hello following table.</span></span>

| <span data-ttu-id="03310-192">Propriedade</span><span class="sxs-lookup"><span data-stu-id="03310-192">Property</span></span> | <span data-ttu-id="03310-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="03310-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="03310-194">operador</span><span class="sxs-lookup"><span data-stu-id="03310-194">Operator</span></span> |<span data-ttu-id="03310-195">Operador de comparação de limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-195">Operator for hello threshold comparison.</span></span> <br> <span data-ttu-id="03310-196">gt = Maior Que</span><span class="sxs-lookup"><span data-stu-id="03310-196">gt = Greater Than</span></span> <br> <span data-ttu-id="03310-197">lt = Menor Que</span><span class="sxs-lookup"><span data-stu-id="03310-197">lt = Less Than</span></span> |
| <span data-ttu-id="03310-198">Valor</span><span class="sxs-lookup"><span data-stu-id="03310-198">Value</span></span> |<span data-ttu-id="03310-199">Valor de limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-199">Value for hello threshold.</span></span> |

<span data-ttu-id="03310-200">Por exemplo, considere uma consulta de evento com um Interval (Intervalo) de 15 minutos, Timespan (Período) de 30 minutos e Threshold (Limite) maior que 10.</span><span class="sxs-lookup"><span data-stu-id="03310-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="03310-201">Nesse caso, Olá consulta será executada a cada 15 minutos, e um alerta será disparado quando retornado 10 eventos que foram criados em um intervalo de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="03310-201">In this case, hello query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="03310-202">Veja a seguir um exemplo de resposta para uma ação com apenas um limite.</span><span class="sxs-lookup"><span data-stu-id="03310-202">Following is a sample response for an action with only a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

<span data-ttu-id="03310-203">Use o método de Put de saudação com uma ID de ação exclusivo toocreate uma nova ação de limite para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="03310-203">Use hello Put method with a unique action ID toocreate a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="03310-204">Use o método de Put de saudação com um toomodify de ID de ação uma ação de limite existente para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="03310-204">Use hello Put method with an existing action ID toomodify a threshold action for a schedule.</span></span>  <span data-ttu-id="03310-205">corpo de saudação da solicitação de saudação deve incluir Olá etag da ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-205">hello body of hello request must include hello etag of hello action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="03310-206">Notificação por email</span><span class="sxs-lookup"><span data-stu-id="03310-206">Email Notification</span></span>
<span data-ttu-id="03310-207">Notificações por email enviam email tooone ou mais destinatários.</span><span class="sxs-lookup"><span data-stu-id="03310-207">Email Notifications send mail tooone or more recipients.</span></span>  <span data-ttu-id="03310-208">Elas incluem propriedades Olá em Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="03310-208">They include hello properties in hello following table.</span></span>

| <span data-ttu-id="03310-209">Propriedade</span><span class="sxs-lookup"><span data-stu-id="03310-209">Property</span></span> | <span data-ttu-id="03310-210">Descrição</span><span class="sxs-lookup"><span data-stu-id="03310-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="03310-211">Destinatários</span><span class="sxs-lookup"><span data-stu-id="03310-211">Recipients</span></span> |<span data-ttu-id="03310-212">Lista de endereços de email.</span><span class="sxs-lookup"><span data-stu-id="03310-212">List of mail addresses.</span></span> |
| <span data-ttu-id="03310-213">Assunto</span><span class="sxs-lookup"><span data-stu-id="03310-213">Subject</span></span> |<span data-ttu-id="03310-214">assunto Olá mail hello.</span><span class="sxs-lookup"><span data-stu-id="03310-214">hello subject of hello mail.</span></span> |
| <span data-ttu-id="03310-215">Anexo</span><span class="sxs-lookup"><span data-stu-id="03310-215">Attachment</span></span> |<span data-ttu-id="03310-216">Atualmente, não há suporte para nexos, por isso este item sempre terá um valor de "None" (Nenhum).</span><span class="sxs-lookup"><span data-stu-id="03310-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="03310-217">Veja a seguir uma resposta de exemplo para uma ação de notificação por email com um limite.</span><span class="sxs-lookup"><span data-stu-id="03310-217">Following is a sample response for an email notification action with a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="03310-218">Use o método de Put de saudação com uma ID de ação exclusivo toocreate uma nova ação de email para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="03310-218">Use hello Put method with a unique action ID toocreate a new e-mail action for a schedule.</span></span>  <span data-ttu-id="03310-219">Olá exemplo a seguir cria uma notificação por email com um limite para que mensagens de saudação é enviada quando resultados Olá Olá pesquisa salva excederem o limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-219">hello following example creates an email notification with a threshold so hello mail is sent when hello results of hello saved search exceed hello threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="03310-220">Use o método de Put de saudação com um toomodify de ID de ação uma ação de email existente para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="03310-220">Use hello Put method with an existing action ID toomodify an e-mail action for a schedule.</span></span>  <span data-ttu-id="03310-221">corpo de saudação da solicitação de saudação deve incluir Olá etag da ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-221">hello body of hello request must include hello etag of hello action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="03310-222">Ações de correção</span><span class="sxs-lookup"><span data-stu-id="03310-222">Remediation actions</span></span>
<span data-ttu-id="03310-223">Correções de iniciar um runbook na automação do Azure que tentativas de problema de saudação toocorrect identificado pelo alerta hello.</span><span class="sxs-lookup"><span data-stu-id="03310-223">Remediations start a runbook in Azure Automation that attempts toocorrect hello problem identified by hello alert.</span></span>  <span data-ttu-id="03310-224">Você deve criar um webhook de runbook Olá usada em uma ação de correção e especifique Olá URI Olá WebhookUri propriedade.</span><span class="sxs-lookup"><span data-stu-id="03310-224">You must create a webhook for hello runbook used in a remediation action and then specify hello URI in hello WebhookUri property.</span></span>  <span data-ttu-id="03310-225">Quando você cria esta ação usando o console do OMS hello, um webhook novo é criado automaticamente para Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="03310-225">When you create this action using hello OMS console, a new webhook is automatically created for hello runbook.</span></span>

<span data-ttu-id="03310-226">Correções incluem propriedades de saudação em Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="03310-226">Remediations include hello properties in hello following table.</span></span>

| <span data-ttu-id="03310-227">Propriedade</span><span class="sxs-lookup"><span data-stu-id="03310-227">Property</span></span> | <span data-ttu-id="03310-228">Descrição</span><span class="sxs-lookup"><span data-stu-id="03310-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="03310-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="03310-229">RunbookName</span></span> |<span data-ttu-id="03310-230">Nome do runbook hello.</span><span class="sxs-lookup"><span data-stu-id="03310-230">Name of hello runbook.</span></span> <span data-ttu-id="03310-231">Isso deve corresponder a um runbook publicado na conta de automação de saudação configurado no hello solução de automação em seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="03310-231">This must match a published runbook in hello automation account configured in hello Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="03310-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="03310-232">WebhookUri</span></span> |<span data-ttu-id="03310-233">URI da saudação webhook.</span><span class="sxs-lookup"><span data-stu-id="03310-233">URI of hello webhook.</span></span> |
| <span data-ttu-id="03310-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="03310-234">Expiry</span></span> |<span data-ttu-id="03310-235">Olá data de expiração de webhook hello.</span><span class="sxs-lookup"><span data-stu-id="03310-235">hello expiration date and time of hello webhook.</span></span>  <span data-ttu-id="03310-236">Se Olá webhook não tiver uma expiração, isso pode ser qualquer data futura válida.</span><span class="sxs-lookup"><span data-stu-id="03310-236">If hello webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="03310-237">Veja a seguir uma resposta de exemplo para uma ação de correção com um limite.</span><span class="sxs-lookup"><span data-stu-id="03310-237">Following is a sample response for a remediation action with a threshold.</span></span>

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

<span data-ttu-id="03310-238">Use o método de Put de saudação com uma ID de ação exclusivo toocreate uma nova ação de correção para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="03310-238">Use hello Put method with a unique action ID toocreate a new remediation action for a schedule.</span></span>  <span data-ttu-id="03310-239">Hello exemplo a seguir cria uma solução com um limite para que o runbook Olá é iniciada quando resultados Olá Olá pesquisa salva excederem o limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-239">hello following example creates a remediation with a threshold so hello runbook is started when hello results of hello saved search exceed hello threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="03310-240">Use o método de Put de saudação com um toomodify de ID de ação uma ação de correção existente para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="03310-240">Use hello Put method with an existing action ID toomodify a remediation action for a schedule.</span></span>  <span data-ttu-id="03310-241">corpo de saudação da solicitação de saudação deve incluir Olá etag da ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-241">hello body of hello request must include hello etag of hello action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="03310-242">Exemplo</span><span class="sxs-lookup"><span data-stu-id="03310-242">Example</span></span>
<span data-ttu-id="03310-243">A seguir está um exemplo completo de toocreate um novo alerta de email.</span><span class="sxs-lookup"><span data-stu-id="03310-243">Following is a complete example toocreate a new email alert.</span></span>  <span data-ttu-id="03310-244">Ele cria um novo agendamento juntamente com uma ação que contém um limite e um email.</span><span class="sxs-lookup"><span data-stu-id="03310-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="03310-245">Ações de Webhook</span><span class="sxs-lookup"><span data-stu-id="03310-245">Webhook actions</span></span>
<span data-ttu-id="03310-246">Ações de Webhook iniciar um processo chamar uma URL e, opcionalmente, fornecendo um toobe carga enviada.</span><span class="sxs-lookup"><span data-stu-id="03310-246">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span>  <span data-ttu-id="03310-247">Eles são ações tooRemediation semelhantes, exceto que eles se destinam a webhooks que podem chamar outros processos além do runbooks de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="03310-247">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="03310-248">Eles também fornecem a opção adicional de saudação do fornecimento de um processo remoto do toobe entregue toohello de carga.</span><span class="sxs-lookup"><span data-stu-id="03310-248">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="03310-249">Ações de Webhook não têm um limite, mas em vez disso, devem ser adicionadas agenda tooa que tem uma ação com um limite de alerta.</span><span class="sxs-lookup"><span data-stu-id="03310-249">Webhook actions do not have a threshold but instead should be added tooa schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="03310-250">Você pode adicionar várias ações de Webhook todos funcionará quando Olá limite é atingido.</span><span class="sxs-lookup"><span data-stu-id="03310-250">You can add multiple Webhook actions that will all be run when hello threshold is met.</span></span>

<span data-ttu-id="03310-251">Ações de Webhook incluem propriedades Olá no Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="03310-251">Webhook actions include hello properties in hello following table.</span></span>

| <span data-ttu-id="03310-252">Propriedade</span><span class="sxs-lookup"><span data-stu-id="03310-252">Property</span></span> | <span data-ttu-id="03310-253">Descrição</span><span class="sxs-lookup"><span data-stu-id="03310-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="03310-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="03310-254">WebhookUri</span></span> |<span data-ttu-id="03310-255">assunto Olá mail hello.</span><span class="sxs-lookup"><span data-stu-id="03310-255">hello subject of hello mail.</span></span> |
| <span data-ttu-id="03310-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="03310-256">CustomPayload</span></span> |<span data-ttu-id="03310-257">Carga personalizada toobe enviado toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="03310-257">Custom payload toobe sent toohello webhook.</span></span>  <span data-ttu-id="03310-258">formato Olá dependerá de quais webhook hello está esperando.</span><span class="sxs-lookup"><span data-stu-id="03310-258">hello format will depend on what hello webhook is expecting.</span></span> |

<span data-ttu-id="03310-259">Veja a seguir um exemplo de resposta para a ação de webhook e uma ação de alerta associada com um limite.</span><span class="sxs-lookup"><span data-stu-id="03310-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="03310-260">Criar ou editar uma ação de webhook</span><span class="sxs-lookup"><span data-stu-id="03310-260">Create or edit a webhook action</span></span>
<span data-ttu-id="03310-261">Use o método de Put de saudação com uma ID de ação exclusivo toocreate uma nova ação de webhook para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="03310-261">Use hello Put method with a unique action ID toocreate a new webhook action for a schedule.</span></span>  <span data-ttu-id="03310-262">Olá exemplo a seguir cria uma ação de Webhook e uma ação de alerta com um limite para que o webhook Olá será disparada quando resultados Olá Olá pesquisa salva excederem o limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-262">hello following example creates a Webhook action and an Alert action with a threshold so that hello webhook will be triggered when hello results of hello saved search exceed hello threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="03310-263">Use o método de Put de saudação com um toomodify de ID de ação uma ação de webhook existente para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="03310-263">Use hello Put method with an existing action ID toomodify a webhook action for a schedule.</span></span>  <span data-ttu-id="03310-264">corpo de saudação da solicitação de saudação deve incluir Olá etag da ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="03310-264">hello body of hello request must include hello etag of hello action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="03310-265">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03310-265">Next steps</span></span>
* <span data-ttu-id="03310-266">Saudação de uso [pesquisas de log do REST API tooperform](log-analytics-log-search-api.md) na análise de Log.</span><span class="sxs-lookup"><span data-stu-id="03310-266">Use hello [REST API tooperform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

