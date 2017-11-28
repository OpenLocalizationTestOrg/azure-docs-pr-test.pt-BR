---
title: Usando a API REST de Alerta do Log Analytics no OMS
description: "A API REST de Alerta do Log Analytics permite criar e gerenciar alertas no Log Analytics, que faz parte do OMS (Operations Management Suite).  Este artigo fornece detalhes da API e vários exemplos para executar operações diferentes."
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
ms.openlocfilehash: 5ce72ffef4394bf3bbe39fa420c4fcaa965ae35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="cdf7b-104">Criar e gerenciar regras de alerta no Log Analytics com a API REST</span><span class="sxs-lookup"><span data-stu-id="cdf7b-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="cdf7b-105">A API de REST do Log Analytics permite criar e gerenciar alertas no OMS (Operations Management Suite).</span><span class="sxs-lookup"><span data-stu-id="cdf7b-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="cdf7b-106">Este artigo fornece detalhes da API e vários exemplos para executar operações diferentes.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-106">This article provides details of the API and several examples for performing different operations.</span></span>

<span data-ttu-id="cdf7b-107">A API REST de Pesquisa do Log Analytics é RESTful e pode ser acessada por meio da API REST do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span></span> <span data-ttu-id="cdf7b-108">Neste documento, você encontrará exemplos em que a API é acessada por meio de uma linha de comando do PowerShell usando o [ARMClient](https://github.com/projectkudu/ARMClient), uma ferramenta de linha de comando de software livre que simplifica a invocação da API do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-108">In this document you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="cdf7b-109">O uso do ARMClient e do PowerShell é uma das muitas opções para acessar a API de Pesquisa do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="cdf7b-110">Com essas ferramentas, você pode utilizar a API RESTful do Azure Resource Manager para fazer chamadas aos espaços de trabalho do OMS e executar comandos de pesquisa dentro deles.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-110">With these tools you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="cdf7b-111">A API produzirá resultados da pesquisa para você no formato JSON, permitindo que você use os resultados da pesquisa de diferentes maneiras por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdf7b-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cdf7b-112">Prerequisites</span></span>
<span data-ttu-id="cdf7b-113">Atualmente, os alertas somente podem ser criados com uma pesquisa salva no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="cdf7b-114">Você pode consultar a [API REST da Pesquisa de Log](log-analytics-log-search-api.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="cdf7b-115">Agendas</span><span class="sxs-lookup"><span data-stu-id="cdf7b-115">Schedules</span></span>
<span data-ttu-id="cdf7b-116">Uma pesquisa salva pode ter um ou mais agendamentos.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="cdf7b-117">O agendamento define a frequência com que a pesquisa é executada e o intervalo de tempo em que os critérios são identificados.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span></span>
<span data-ttu-id="cdf7b-118">Os agendamentos têm as propriedades indicadas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-118">Schedules have the properties in the following table.</span></span>

| <span data-ttu-id="cdf7b-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cdf7b-119">Property</span></span> | <span data-ttu-id="cdf7b-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="cdf7b-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cdf7b-121">Intervalo</span><span class="sxs-lookup"><span data-stu-id="cdf7b-121">Interval</span></span> |<span data-ttu-id="cdf7b-122">A frequência com que a pesquisa é executada.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-122">How often the search is run.</span></span> <span data-ttu-id="cdf7b-123">Medida em minutos.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-123">Measured in minutes.</span></span> |
| <span data-ttu-id="cdf7b-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="cdf7b-124">QueryTimeSpan</span></span> |<span data-ttu-id="cdf7b-125">O intervalo durante o qual os critérios são avaliados.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-125">The time interval over which the criteria is evaluated.</span></span> <span data-ttu-id="cdf7b-126">Deve ser igual ou maior que Interval.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-126">Must be equal to or greater than Interval.</span></span> <span data-ttu-id="cdf7b-127">Medida em minutos.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-127">Measured in minutes.</span></span> |
| <span data-ttu-id="cdf7b-128">Versão</span><span class="sxs-lookup"><span data-stu-id="cdf7b-128">Version</span></span> |<span data-ttu-id="cdf7b-129">A versão da API que está sendo usada.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-129">The API version being used.</span></span>  <span data-ttu-id="cdf7b-130">Atualmente, isso sempre deve ser definido como 1.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-130">Currently, this should always be set to 1.</span></span> |

<span data-ttu-id="cdf7b-131">Por exemplo, considere uma consulta de evento com um Interval (Intervalo) de 15 minutos e Timespan (Período) de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="cdf7b-132">Nesse caso, a consulta deverá ser executada a cada 15 minutos e um alerta deverá ser disparado se os critérios continuarem a ser resolvidos como verdadeiro por um período de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="cdf7b-133">Recuperando agendamentos</span><span class="sxs-lookup"><span data-stu-id="cdf7b-133">Retrieving schedules</span></span>
<span data-ttu-id="cdf7b-134">Use o método Get para recuperar todos os agendamentos de uma pesquisa salva.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-134">Use the Get method to retrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="cdf7b-135">Use o método Get com uma ID de agendamento para recuperar um agendamento específico para uma pesquisa salva.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="cdf7b-136">A seguir está um exemplo de resposta para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-136">Following is a sample response for a schedule.</span></span>

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

### <a name="creating-a-schedule"></a><span data-ttu-id="cdf7b-137">Criando uma agenda</span><span class="sxs-lookup"><span data-stu-id="cdf7b-137">Creating a schedule</span></span>
<span data-ttu-id="cdf7b-138">Use o método Put com uma ID de agendamento única para criar um novo agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-138">Use the Put method with a unique schedule ID to create a new schedule.</span></span>  <span data-ttu-id="cdf7b-139">Observe que dois agendamento não podem ter a mesma ID, mesmo se estiverem associados a diferentes pesquisas salvas.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="cdf7b-140">Ao criar um agendamento no console do OMS, uma GUID é criado para a ID de agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="cdf7b-141">O nome para todas as pesquisas, agendas e ações salvas criadas com a API do Log Analytics deve estar em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-141">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="cdf7b-142">Editando um agendamento</span><span class="sxs-lookup"><span data-stu-id="cdf7b-142">Editing a schedule</span></span>
<span data-ttu-id="cdf7b-143">Use o método Put com uma ID de agendamento existente para a mesma pesquisa salva para modificar esse agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-143">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="cdf7b-144">O corpo da solicitação deve incluir a Etag do agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-144">The body of the request must include the etag of the schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="cdf7b-145">Excluindo agendamentos</span><span class="sxs-lookup"><span data-stu-id="cdf7b-145">Deleting schedules</span></span>
<span data-ttu-id="cdf7b-146">Use o método Delete com uma ID de agendamento para excluir um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-146">Use the Delete method with a schedule ID to delete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="cdf7b-147">Ações</span><span class="sxs-lookup"><span data-stu-id="cdf7b-147">Actions</span></span>
<span data-ttu-id="cdf7b-148">Um agendamento pode ter várias ações.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="cdf7b-149">Uma ação pode definir um ou mais processos a serem executados, como enviar um email ou iniciar um runbook, ou então ela pode definir um limite que determina quando os resultados de uma pesquisa correspondem a certos critérios.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-149">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span></span>  <span data-ttu-id="cdf7b-150">Algumas ações definirão ambos para que os processos sejam executados quando o limite for atingido.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-150">Some actions will define both so that the processes are performed when the threshold is met.</span></span>

<span data-ttu-id="cdf7b-151">Todas as ações têm as propriedades indicadas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-151">All actions have the properties in the following table.</span></span>  <span data-ttu-id="cdf7b-152">Diferentes tipos de alertas têm diferentes propriedades adicionais que são descritas abaixo.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="cdf7b-153">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cdf7b-153">Property</span></span> | <span data-ttu-id="cdf7b-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="cdf7b-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cdf7b-155">Tipo</span><span class="sxs-lookup"><span data-stu-id="cdf7b-155">Type</span></span> |<span data-ttu-id="cdf7b-156">Tipo da ação.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-156">Type of the action.</span></span>  <span data-ttu-id="cdf7b-157">Atualmente, os valores possíveis são Alerta e Webhook.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-157">Currently the possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="cdf7b-158">Nome</span><span class="sxs-lookup"><span data-stu-id="cdf7b-158">Name</span></span> |<span data-ttu-id="cdf7b-159">Nome de exibição para o alerta.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-159">Display name for the alert.</span></span> |
| <span data-ttu-id="cdf7b-160">Versão</span><span class="sxs-lookup"><span data-stu-id="cdf7b-160">Version</span></span> |<span data-ttu-id="cdf7b-161">A versão da API que está sendo usada.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-161">The API version being used.</span></span>  <span data-ttu-id="cdf7b-162">Atualmente, isso sempre deve ser definido como 1.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-162">Currently, this should always be set to 1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="cdf7b-163">Recuperando ações</span><span class="sxs-lookup"><span data-stu-id="cdf7b-163">Retrieving actions</span></span>
<span data-ttu-id="cdf7b-164">Use o método Get para recuperar todas as ações de um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-164">Use the Get method to retrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="cdf7b-165">Use o método Get com a ID de ação para recuperar uma ação específica de um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-165">Use the Get method with the action ID to retrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="cdf7b-166">Criar ou editar ações</span><span class="sxs-lookup"><span data-stu-id="cdf7b-166">Creating or editing actions</span></span>
<span data-ttu-id="cdf7b-167">Use o método Put com uma ID de ação que seja exclusiva para o agendamento para criar uma nova ação.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-167">Use the Put method with an action ID that is unique to the schedule to create a new action.</span></span>  <span data-ttu-id="cdf7b-168">Quando você cria uma ação no console do OMS, um GUID é fornecido para a ID de ação.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-168">When you create an action in the OMS console, a GUID is for the action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="cdf7b-169">O nome para todas as pesquisas, agendas e ações salvas criadas com a API do Log Analytics deve estar em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-169">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="cdf7b-170">Use o método Put com uma ID de ação existente para a mesma pesquisa salva para modificar esse agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-170">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="cdf7b-171">O corpo da solicitação deve incluir a Etag do agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-171">The body of the request must include the etag of the schedule.</span></span>

<span data-ttu-id="cdf7b-172">O formato da solicitação para criar uma nova ação varia conforme o tipo de ação, veja os exemplos fornecidos nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-172">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="cdf7b-173">Excluindo ações</span><span class="sxs-lookup"><span data-stu-id="cdf7b-173">Deleting actions</span></span>
<span data-ttu-id="cdf7b-174">Use o método Delete com a ID de ação para excluir uma ação.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-174">Use the Delete method with the action ID to delete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="cdf7b-175">Ações de Alerta</span><span class="sxs-lookup"><span data-stu-id="cdf7b-175">Alert Actions</span></span>
<span data-ttu-id="cdf7b-176">Um Agendamento deve ter somente uma ação de Alerta.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="cdf7b-177">Ações de alerta têm uma ou mais das seções na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-177">Alert actions have one or more of the sections in the following table.</span></span>  <span data-ttu-id="cdf7b-178">Elas são descritas em mais detalhes abaixo.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="cdf7b-179">Seção</span><span class="sxs-lookup"><span data-stu-id="cdf7b-179">Section</span></span> | <span data-ttu-id="cdf7b-180">Descrição</span><span class="sxs-lookup"><span data-stu-id="cdf7b-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cdf7b-181">Limite</span><span class="sxs-lookup"><span data-stu-id="cdf7b-181">Threshold</span></span> |<span data-ttu-id="cdf7b-182">Critérios para quando a ação for executada.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-182">Criteria for when the action is run.</span></span> |
| <span data-ttu-id="cdf7b-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="cdf7b-183">EmailNotification</span></span> |<span data-ttu-id="cdf7b-184">Envie email para vários destinatários.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-184">Send mail to multiple recipients.</span></span> |
| <span data-ttu-id="cdf7b-185">Correção</span><span class="sxs-lookup"><span data-stu-id="cdf7b-185">Remediation</span></span> |<span data-ttu-id="cdf7b-186">Inicie um runbook na Automação do Azure para tentar corrigir o problema identificado.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-186">Start a runbook in Azure Automation to attempt to correct identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="cdf7b-187">Limites</span><span class="sxs-lookup"><span data-stu-id="cdf7b-187">Thresholds</span></span>
<span data-ttu-id="cdf7b-188">Uma ação de Alerta deve ter somente um limite.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="cdf7b-189">Quando os resultados de pesquisas salvas coincidem com o limite de uma ação associada à pesquisa, outros processos nesta ação são executados.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-189">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="cdf7b-190">Uma ação também pode conter apenas um limite para ser usado com ações de outros tipos que não contêm os limites.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="cdf7b-191">Os limites têm as propriedades indicadas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-191">Thresholds have the properties in the following table.</span></span>

| <span data-ttu-id="cdf7b-192">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cdf7b-192">Property</span></span> | <span data-ttu-id="cdf7b-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="cdf7b-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cdf7b-194">Operador</span><span class="sxs-lookup"><span data-stu-id="cdf7b-194">Operator</span></span> |<span data-ttu-id="cdf7b-195">Operador de comparação de limite.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-195">Operator for the threshold comparison.</span></span> <br> <span data-ttu-id="cdf7b-196">gt = Maior Que</span><span class="sxs-lookup"><span data-stu-id="cdf7b-196">gt = Greater Than</span></span> <br> <span data-ttu-id="cdf7b-197">lt = Menor Que</span><span class="sxs-lookup"><span data-stu-id="cdf7b-197">lt = Less Than</span></span> |
| <span data-ttu-id="cdf7b-198">Valor</span><span class="sxs-lookup"><span data-stu-id="cdf7b-198">Value</span></span> |<span data-ttu-id="cdf7b-199">Valor para o limite.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-199">Value for the threshold.</span></span> |

<span data-ttu-id="cdf7b-200">Por exemplo, considere uma consulta de evento com um Interval (Intervalo) de 15 minutos, Timespan (Período) de 30 minutos e Threshold (Limite) maior que 10.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="cdf7b-201">Nesse caso, a consulta deverá ser executada a cada 15 minutos e um alerta deverá ser disparado se ela retornar 10 eventos criados dentro de um período de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-201">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="cdf7b-202">Veja a seguir um exemplo de resposta para uma ação com apenas um limite.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-202">Following is a sample response for an action with only a threshold.</span></span>  

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

<span data-ttu-id="cdf7b-203">Use o método Put com uma ID de ação única para criar uma nova ação de limite para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-203">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="cdf7b-204">Use o método Put com uma ID de ação existente para criar uma nova ação de limite para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-204">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span></span>  <span data-ttu-id="cdf7b-205">O corpo da solicitação deve incluir a Etag da ação.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-205">The body of the request must include the etag of the action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="cdf7b-206">Notificação por email</span><span class="sxs-lookup"><span data-stu-id="cdf7b-206">Email Notification</span></span>
<span data-ttu-id="cdf7b-207">Notificações por Email enviam email para um ou mais destinatários.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-207">Email Notifications send mail to one or more recipients.</span></span>  <span data-ttu-id="cdf7b-208">Elas incluem as propriedades indicadas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-208">They include the properties in the following table.</span></span>

| <span data-ttu-id="cdf7b-209">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cdf7b-209">Property</span></span> | <span data-ttu-id="cdf7b-210">Descrição</span><span class="sxs-lookup"><span data-stu-id="cdf7b-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cdf7b-211">Destinatários</span><span class="sxs-lookup"><span data-stu-id="cdf7b-211">Recipients</span></span> |<span data-ttu-id="cdf7b-212">Lista de endereços de email.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-212">List of mail addresses.</span></span> |
| <span data-ttu-id="cdf7b-213">Assunto</span><span class="sxs-lookup"><span data-stu-id="cdf7b-213">Subject</span></span> |<span data-ttu-id="cdf7b-214">O assunto do email.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-214">The subject of the mail.</span></span> |
| <span data-ttu-id="cdf7b-215">Anexo</span><span class="sxs-lookup"><span data-stu-id="cdf7b-215">Attachment</span></span> |<span data-ttu-id="cdf7b-216">Atualmente, não há suporte para nexos, por isso este item sempre terá um valor de "None" (Nenhum).</span><span class="sxs-lookup"><span data-stu-id="cdf7b-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="cdf7b-217">Veja a seguir uma resposta de exemplo para uma ação de notificação por email com um limite.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-217">Following is a sample response for an email notification action with a threshold.</span></span>  

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
            "Subject": "This is the subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="cdf7b-218">Use o método Put com uma ID de ação única para criar uma nova ação de email para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-218">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span></span>  <span data-ttu-id="cdf7b-219">O exemplo a seguir cria uma notificação por email com um limite para que o email seja enviado quando os resultados da pesquisa salvos excederem o limite.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-219">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="cdf7b-220">Use o método Put com uma ID de ação existente para modificar uma ação de email para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-220">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span></span>  <span data-ttu-id="cdf7b-221">O corpo da solicitação deve incluir a Etag da ação.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-221">The body of the request must include the etag of the action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="cdf7b-222">Ações de correção</span><span class="sxs-lookup"><span data-stu-id="cdf7b-222">Remediation actions</span></span>
<span data-ttu-id="cdf7b-223">As correções iniciam um runbook na Automação do Azure que tenta corrigir o problema identificado pelo alerta.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-223">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span></span>  <span data-ttu-id="cdf7b-224">Você deve criar um webhook para o runbook usado em uma ação de correção e especificar o URI na propriedade WebhookUri.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-224">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span></span>  <span data-ttu-id="cdf7b-225">Quando você cria essa ação usando o console do OMS, um novo webhook é criado automaticamente para o runbook.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-225">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span></span>

<span data-ttu-id="cdf7b-226">As correções incluem as propriedades indicadas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-226">Remediations include the properties in the following table.</span></span>

| <span data-ttu-id="cdf7b-227">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cdf7b-227">Property</span></span> | <span data-ttu-id="cdf7b-228">Descrição</span><span class="sxs-lookup"><span data-stu-id="cdf7b-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cdf7b-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="cdf7b-229">RunbookName</span></span> |<span data-ttu-id="cdf7b-230">Nome do runbook.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-230">Name of the runbook.</span></span> <span data-ttu-id="cdf7b-231">Isso deve corresponder a um runbook publicado na conta de automação configurada na Solução de Automação no seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-231">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="cdf7b-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="cdf7b-232">WebhookUri</span></span> |<span data-ttu-id="cdf7b-233">O URI do webhook.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-233">URI of the webhook.</span></span> |
| <span data-ttu-id="cdf7b-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="cdf7b-234">Expiry</span></span> |<span data-ttu-id="cdf7b-235">A data e hora de expiração do webhook.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-235">The expiration date and time of the webhook.</span></span>  <span data-ttu-id="cdf7b-236">Caso o webhook não expire, esta pode ser qualquer data futura válida.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-236">If the webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="cdf7b-237">Veja a seguir uma resposta de exemplo para uma ação de correção com um limite.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-237">Following is a sample response for a remediation action with a threshold.</span></span>

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

<span data-ttu-id="cdf7b-238">Use o método Put com uma ID de ação única para criar uma nova ação de correção para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-238">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span></span>  <span data-ttu-id="cdf7b-239">O exemplo a seguir cria uma correção com um limite para que o runbook seja iniciado quando os resultados da pesquisa salvos excederem o limite.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-239">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="cdf7b-240">Use o método Put com uma ID de ação existente para modificar uma ação de correção para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-240">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span></span>  <span data-ttu-id="cdf7b-241">O corpo da solicitação deve incluir a Etag da ação.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-241">The body of the request must include the etag of the action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="cdf7b-242">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cdf7b-242">Example</span></span>
<span data-ttu-id="cdf7b-243">Veja a seguir um exemplo completo para criar um novo alerta de email.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-243">Following is a complete example to create a new email alert.</span></span>  <span data-ttu-id="cdf7b-244">Ele cria um novo agendamento juntamente com uma ação que contém um limite e um email.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="cdf7b-245">Ações de Webhook</span><span class="sxs-lookup"><span data-stu-id="cdf7b-245">Webhook actions</span></span>
<span data-ttu-id="cdf7b-246">Ações de Webhook iniciam um processo chamando uma URL e, opcionalmente, fornecendo uma carga a ser enviada.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-246">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span>  <span data-ttu-id="cdf7b-247">Elas são semelhantes às ações de Correção, exceto que se destinam a webhooks que podem invocar outros processos além de runbooks da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-247">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="cdf7b-248">Eles também oferecem a opção adicional de fornecer uma carga a ser enviada para o processo remoto.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-248">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="cdf7b-249">Ações de Webhook não têm um limite, devendo ser adicionadas a um agendamento que tem uma ação de Alerta com um limite.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-249">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="cdf7b-250">Você pode adicionar várias ações de Webhook que serão executadas quando o limite for atingido.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-250">You can add multiple Webhook actions that will all be run when the threshold is met.</span></span>

<span data-ttu-id="cdf7b-251">Ações de webhook incluem as propriedades indicadas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-251">Webhook actions include the properties in the following table.</span></span>

| <span data-ttu-id="cdf7b-252">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cdf7b-252">Property</span></span> | <span data-ttu-id="cdf7b-253">Descrição</span><span class="sxs-lookup"><span data-stu-id="cdf7b-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cdf7b-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="cdf7b-254">WebhookUri</span></span> |<span data-ttu-id="cdf7b-255">O assunto do email.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-255">The subject of the mail.</span></span> |
| <span data-ttu-id="cdf7b-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="cdf7b-256">CustomPayload</span></span> |<span data-ttu-id="cdf7b-257">Carga personalizada a ser enviada para o webhook.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-257">Custom payload to be sent to the webhook.</span></span>  <span data-ttu-id="cdf7b-258">O formato dependerá do que o webhook está esperando.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-258">The format will depend on what the webhook is expecting.</span></span> |

<span data-ttu-id="cdf7b-259">Veja a seguir um exemplo de resposta para a ação de webhook e uma ação de alerta associada com um limite.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

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

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="cdf7b-260">Criar ou editar uma ação de webhook</span><span class="sxs-lookup"><span data-stu-id="cdf7b-260">Create or edit a webhook action</span></span>
<span data-ttu-id="cdf7b-261">Use o método Put com uma ID de ação única para criar uma nova ação de webhook para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-261">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span></span>  <span data-ttu-id="cdf7b-262">O exemplo a seguir cria uma ação de Webhook e uma ação de alerta com um limite para que o webhook seja acionado quando os resultados da pesquisa salvos excederem o limite.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-262">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="cdf7b-263">Use o método Put com uma ID de ação existente para modificar uma ação de webhook para um agendamento.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-263">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span></span>  <span data-ttu-id="cdf7b-264">O corpo da solicitação deve incluir a Etag da ação.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-264">The body of the request must include the etag of the action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="cdf7b-265">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cdf7b-265">Next steps</span></span>
* <span data-ttu-id="cdf7b-266">Use a [API REST para executar pesquisas de log](log-analytics-log-search-api.md) no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="cdf7b-266">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

