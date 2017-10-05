---
title: "Salvar pesquisas e alertas em soluções OMS | Microsoft Docs"
description: "As soluções no OMS normalmente inclui pesquisas salvas na Log Analytics para analisar os dados coletados pela solução.  Elas podem também definir alertas para notificar o usuário ou executar automaticamente a ação em resposta a um problema crítico.  Este artigo descreve como definir pesquisas e alertas salvos no Log Analytics em um modelo ARM para que eles possam ser incluídos em soluções de gerenciamento."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 21c42a747a08c5386c65d10190baf0054a7adef8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-oms-management-solution-preview"></a><span data-ttu-id="1f5ea-105">Adicionando alertas e pesquisas salvas do Log Analytics à solução de gerenciamento do OMS (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="1f5ea-105">Adding Log Analytics saved searches and alerts to OMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="1f5ea-106">Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="1f5ea-107">Os esquemas descritos a seguir estão sujeitos a alterações.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-107">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="1f5ea-108">As [soluções de gerenciamento no OMS](operations-management-suite-solutions.md) geralmente incluirão [pesquisas salvas](../log-analytics/log-analytics-log-searches.md) no Log Analytics para analisar os dados coletados pela solução.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span></span>  <span data-ttu-id="1f5ea-109">Elas também podem definir [alertas](../log-analytics/log-analytics-alerts.md) para notificar o usuário ou executar automaticamente a ação em resposta a um problema crítico.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span></span>  <span data-ttu-id="1f5ea-110">Este artigo descreve como definir a Log Analytics pesquisas salvas e alertas em um [modelo do Resource Manager](../resource-manager-template-walkthrough.md) para que eles possam ser incluídos em [soluções de gerenciamento de](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="1f5ea-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1f5ea-111">Os exemplos neste artigo usam parâmetros e variáveis que são necessários ou comuns para as soluções de gerenciamento e estão descritos em [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md) (Criando soluções de gerenciamento no OMS (Operations Management Suite))</span><span class="sxs-lookup"><span data-stu-id="1f5ea-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="1f5ea-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1f5ea-112">Prerequisites</span></span>
<span data-ttu-id="1f5ea-113">Este artigo pressupõe que você já esteja familiarizado com o modo para [criar uma solução de gerenciamento](operations-management-suite-solutions-creating.md) e com a estrutura de um [modelo ARM](../resource-group-authoring-templates.md) e de um arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-113">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="1f5ea-114">Espaço de trabalho do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1f5ea-114">Log Analytics Workspace</span></span>
<span data-ttu-id="1f5ea-115">Todos os recursos de Log Analytics estão contidos em um [espaço](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="1f5ea-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="1f5ea-116">Como descrito no [espaço de trabalho OMS e conta de automação](operations-management-suite-solutions.md#oms-workspace-and-automation-account), o espaço de trabalho não está incluído na solução de gerenciamento, mas deve existir antes que a solução seja instalada.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the workspace isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="1f5ea-117">Se ela não estiver disponível, a instalação da solução falhará.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-117">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="1f5ea-118">O nome do espaço de trabalho é no nome de cada recurso de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-118">The name of the workspace is in the name of each Log Analytics resource.</span></span>  <span data-ttu-id="1f5ea-119">Isso é feito na solução com o parâmetro **workspace**, conforme descrito no exemplo a seguir de um recurso savedsearch.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-119">This is done in the solution with the **workspace** parameter as in the following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="1f5ea-120">Pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="1f5ea-120">Saved Searches</span></span>
<span data-ttu-id="1f5ea-121">Incluir [pesquisas salvas](../log-analytics/log-analytics-log-searches.md) em uma solução para permitir aos usuários consultar dados coletados pela solução.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span></span>  <span data-ttu-id="1f5ea-122">Pesquisas salvas aparecerão em **Favoritos** no portal do OMS e **pesquisas salvas** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-122">Saved searches will appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal .</span></span>  <span data-ttu-id="1f5ea-123">Uma pesquisa salva também é necessária para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="1f5ea-124">Os recursos [da pesquisa salva do Log Analytics](../log-analytics/log-analytics-log-searches.md) têm um tipo `Microsoft.OperationalInsights/workspaces/savedSearches` e a seguinte estrutura.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span></span>  <span data-ttu-id="1f5ea-125">Isso inclui variáveis e parâmetros comuns para que você possa copiar e colar este trecho de código em seu arquivo de solução e alterar os nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



<span data-ttu-id="1f5ea-126">Cada uma das propriedades de pesquisas salvas são descritos na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-126">Each of the properties of a saved search are described in the following table.</span></span> 

| <span data-ttu-id="1f5ea-127">Propriedade</span><span class="sxs-lookup"><span data-stu-id="1f5ea-127">Property</span></span> | <span data-ttu-id="1f5ea-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f5ea-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1f5ea-129">categoria</span><span class="sxs-lookup"><span data-stu-id="1f5ea-129">category</span></span> | <span data-ttu-id="1f5ea-130">A categoria para a pesquisa salva.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-130">The category for the saved search.</span></span>  <span data-ttu-id="1f5ea-131">As pesquisas salvas na mesma solução geralmente compartilham uma única categoria para que eles são agrupados juntos no console.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-131">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span></span> |
| <span data-ttu-id="1f5ea-132">displayname</span><span class="sxs-lookup"><span data-stu-id="1f5ea-132">displayname</span></span> | <span data-ttu-id="1f5ea-133">Nome para exibição para a pesquisa salva no portal.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-133">Name to display for the saved search in the portal.</span></span> |
| <span data-ttu-id="1f5ea-134">query</span><span class="sxs-lookup"><span data-stu-id="1f5ea-134">query</span></span> | <span data-ttu-id="1f5ea-135">Consulta a executar.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-135">Query to run.</span></span> |

> [!NOTE]
> <span data-ttu-id="1f5ea-136">Você talvez precise usar caracteres de escape na consulta, se ele inclui os caracteres que podem ser interpretados como JSON.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-136">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="1f5ea-137">Por exemplo, se sua consulta **OperationName:"Microsoft.Compute/virtualMachines/write tipo: AzureActivity"**, deve ser gravado no arquivo de solução como **OperationName tipo: AzureActivity:\"Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="1f5ea-138">Alertas</span><span class="sxs-lookup"><span data-stu-id="1f5ea-138">Alerts</span></span>
<span data-ttu-id="1f5ea-139">[Alertas de Log Analytics](../log-analytics/log-analytics-alerts.md) são criados por regras de alerta que executar uma pesquisa salva em um intervalo regular.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="1f5ea-140">Se os resultados da consulta correspondência aos critérios especificados, será criado um registro de alerta e uma ou mais ações são executadas.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-140">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="1f5ea-141">Regras de alerta em uma solução de gerenciamento são constituídas por três recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-141">Alert rules in a management solution are made up of the following three different resources.</span></span>

- <span data-ttu-id="1f5ea-142">**Pesquisa salva.**</span><span class="sxs-lookup"><span data-stu-id="1f5ea-142">**Saved search.**</span></span>  <span data-ttu-id="1f5ea-143">Define a pesquisa de log que será executada.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-143">Defines the log search that will be run.</span></span>  <span data-ttu-id="1f5ea-144">Várias regras de alerta podem compartilhar uma única pesquisa salva.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="1f5ea-145">**Agenda.**</span><span class="sxs-lookup"><span data-stu-id="1f5ea-145">**Schedule.**</span></span>  <span data-ttu-id="1f5ea-146">Define a frequência com a pesquisa de log será executada.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-146">Defines how often the log search will be run.</span></span>  <span data-ttu-id="1f5ea-147">Cada regra de alerta terá apenas um agendamento.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="1f5ea-148">**Ação de alerta.**</span><span class="sxs-lookup"><span data-stu-id="1f5ea-148">**Alert action.**</span></span>  <span data-ttu-id="1f5ea-149">Cada regra de alerta terá um recurso de ação com um tipo de **Alerta** que define os detalhes do alerta, como os critérios para quando um registro de alerta será criado e a gravidade do alerta.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-149">Each alert rule will have one action resource with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record will be created and the alert's severity.</span></span>  <span data-ttu-id="1f5ea-150">O recurso de ação, opcionalmente, definir uma resposta de email e o runbook.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-150">The action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="1f5ea-151">**Ação de Webhook (opcional).**</span><span class="sxs-lookup"><span data-stu-id="1f5ea-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="1f5ea-152">Se a regra de alerta chamará um webhook, ele requer um recurso de ação adicional com um tipo de **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-152">If the alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="1f5ea-153">Salvar pesquisa recursos descritos acima.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-153">Saved search resources are described above.</span></span>  <span data-ttu-id="1f5ea-154">Outros recursos são descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-154">The other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="1f5ea-155">Recursos de agendamento</span><span class="sxs-lookup"><span data-stu-id="1f5ea-155">Schedule resource</span></span>

<span data-ttu-id="1f5ea-156">Uma pesquisa salva pode ter uma ou mais agendas com cada agenda que representa uma regra de alerta separada.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="1f5ea-157">A agenda define a frequência com que a pesquisa é executada e o intervalo de tempo em que os dados são recuperados.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-157">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span></span>  <span data-ttu-id="1f5ea-158">Os recursos de agendamento têm um tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` e ter a seguinte estrutura.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span></span> <span data-ttu-id="1f5ea-159">Isso inclui variáveis e parâmetros comuns para que você possa copiar e colar este trecho de código em seu arquivo de solução e alterar os nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



<span data-ttu-id="1f5ea-160">As propriedades de recursos de agendamento são descritas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-160">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="1f5ea-161">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="1f5ea-161">Element name</span></span> | <span data-ttu-id="1f5ea-162">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1f5ea-162">Required</span></span> | <span data-ttu-id="1f5ea-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f5ea-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1f5ea-164">Habilitado</span><span class="sxs-lookup"><span data-stu-id="1f5ea-164">enabled</span></span>       | <span data-ttu-id="1f5ea-165">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-165">Yes</span></span> | <span data-ttu-id="1f5ea-166">Especifica se o alerta está habilitado quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-166">Specifies whether the alert is enabled when it's created.</span></span> |
| <span data-ttu-id="1f5ea-167">intervalo</span><span class="sxs-lookup"><span data-stu-id="1f5ea-167">interval</span></span>      | <span data-ttu-id="1f5ea-168">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-168">Yes</span></span> | <span data-ttu-id="1f5ea-169">A frequência com a consulta é executada em minutos.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-169">How often the query runs in minutes.</span></span> |
| <span data-ttu-id="1f5ea-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="1f5ea-170">queryTimeSpan</span></span> | <span data-ttu-id="1f5ea-171">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-171">Yes</span></span> | <span data-ttu-id="1f5ea-172">Período de tempo em minutos no qual avaliar resultados.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-172">Length of time in minutes over which to evaluate results.</span></span> |

<span data-ttu-id="1f5ea-173">O recurso de agendamento deve depender a pesquisa salva para que ele seja criado antes da agenda.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-173">The schedule resource should depend on the saved search so that it's created before the schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="1f5ea-174">Ações</span><span class="sxs-lookup"><span data-stu-id="1f5ea-174">Actions</span></span>
<span data-ttu-id="1f5ea-175">Há dois tipos de recurso de ação especificado pelo **tipo** propriedade.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-175">There are two types of action resource specified by the **Type** property.</span></span>  <span data-ttu-id="1f5ea-176">Uma agenda requer um **alerta** ação que define os detalhes da regra de alerta e quais ações são executadas quando um alerta é criado.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-176">A schedule requires one **Alert** action which defines the details of the alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="1f5ea-177">Ele também pode incluir uma **Webhook** ação se um webhook deve ser chamado a partir do alerta.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-177">It may also include a **Webhook** action if a webhook should be called from the alert.</span></span>  

<span data-ttu-id="1f5ea-178">Recursos de ação com um tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="1f5ea-179">Ações de alerta</span><span class="sxs-lookup"><span data-stu-id="1f5ea-179">Alert actions</span></span>

<span data-ttu-id="1f5ea-180">Cada agenda terá um **alerta** ação.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="1f5ea-181">Isso define os detalhes do alerta e, opcionalmente, ações de notificação e correção.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-181">This defines the details of the alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="1f5ea-182">Uma notificação envia um email para um ou mais endereços.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-182">A notification sends an email to one or more addresses.</span></span>  <span data-ttu-id="1f5ea-183">Uma correção inicia um runbook na automação do Azure para tentar corrigir o problema detectado.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-183">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span></span>

<span data-ttu-id="1f5ea-184">Ações de alerta tem a seguinte estrutura.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-184">Alert actions have the following structure.</span></span>  <span data-ttu-id="1f5ea-185">Isso inclui variáveis e parâmetros comuns para que você possa copiar e colar este trecho de código em seu arquivo de solução e alterar os nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

<span data-ttu-id="1f5ea-186">As propriedades de Recursos de ação de alerta são descritas nas tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-186">The properties for Alert action resources are described in the following tables.</span></span>

| <span data-ttu-id="1f5ea-187">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="1f5ea-187">Element name</span></span> | <span data-ttu-id="1f5ea-188">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1f5ea-188">Required</span></span> | <span data-ttu-id="1f5ea-189">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f5ea-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1f5ea-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="1f5ea-190">Type</span></span> | <span data-ttu-id="1f5ea-191">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-191">Yes</span></span> | <span data-ttu-id="1f5ea-192">Tipo da ação.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-192">Type of the action.</span></span>  <span data-ttu-id="1f5ea-193">Isso será **alerta** para ações de alerta.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="1f5ea-194">Nome</span><span class="sxs-lookup"><span data-stu-id="1f5ea-194">Name</span></span> | <span data-ttu-id="1f5ea-195">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-195">Yes</span></span> | <span data-ttu-id="1f5ea-196">Nome de exibição para o alerta.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-196">Display name for the alert.</span></span>  <span data-ttu-id="1f5ea-197">Esse é o nome que é exibido no console para a regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-197">This is the name that's displayed in the console for the alert rule.</span></span> |
| <span data-ttu-id="1f5ea-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f5ea-198">Description</span></span> | <span data-ttu-id="1f5ea-199">Não</span><span class="sxs-lookup"><span data-stu-id="1f5ea-199">No</span></span> | <span data-ttu-id="1f5ea-200">Descrição opcional do alerta.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-200">Optional description of the alert.</span></span> |
| <span data-ttu-id="1f5ea-201">Severidade</span><span class="sxs-lookup"><span data-stu-id="1f5ea-201">Severity</span></span> | <span data-ttu-id="1f5ea-202">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-202">Yes</span></span> | <span data-ttu-id="1f5ea-203">Severidade do alerta registro dos seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="1f5ea-203">Severity of the alert record from the following values:</span></span><br><br> <span data-ttu-id="1f5ea-204">**Crítico**</span><span class="sxs-lookup"><span data-stu-id="1f5ea-204">**Critical**</span></span><br><span data-ttu-id="1f5ea-205">**Aviso**</span><span class="sxs-lookup"><span data-stu-id="1f5ea-205">**Warning**</span></span><br><span data-ttu-id="1f5ea-206">**Informativo**</span><span class="sxs-lookup"><span data-stu-id="1f5ea-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="1f5ea-207">Limite</span><span class="sxs-lookup"><span data-stu-id="1f5ea-207">Threshold</span></span>
<span data-ttu-id="1f5ea-208">Esta seção é necessária.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-208">This section is required.</span></span>  <span data-ttu-id="1f5ea-209">Define as propriedades para o limite de alerta.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-209">It defines the properties for the alert threshold.</span></span>

| <span data-ttu-id="1f5ea-210">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="1f5ea-210">Element name</span></span> | <span data-ttu-id="1f5ea-211">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1f5ea-211">Required</span></span> | <span data-ttu-id="1f5ea-212">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f5ea-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1f5ea-213">Operador</span><span class="sxs-lookup"><span data-stu-id="1f5ea-213">Operator</span></span> | <span data-ttu-id="1f5ea-214">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-214">Yes</span></span> | <span data-ttu-id="1f5ea-215">O operador para a comparação dos seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="1f5ea-215">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="1f5ea-216">**gt = maior que<br>lt = menor que**</span><span class="sxs-lookup"><span data-stu-id="1f5ea-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="1f5ea-217">Valor</span><span class="sxs-lookup"><span data-stu-id="1f5ea-217">Value</span></span> | <span data-ttu-id="1f5ea-218">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-218">Yes</span></span> | <span data-ttu-id="1f5ea-219">O valor para comparar os resultados.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-219">The value to compare the results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="1f5ea-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="1f5ea-220">MetricsTrigger</span></span>
<span data-ttu-id="1f5ea-221">Esta seção é opcional.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-221">This section is optional.</span></span>  <span data-ttu-id="1f5ea-222">Inclua-o para um alerta de métrica de medição.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="1f5ea-223">Alertas de métrica de medição estão atualmente em visualização pública.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="1f5ea-224">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="1f5ea-224">Element name</span></span> | <span data-ttu-id="1f5ea-225">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1f5ea-225">Required</span></span> | <span data-ttu-id="1f5ea-226">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f5ea-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1f5ea-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="1f5ea-227">TriggerCondition</span></span> | <span data-ttu-id="1f5ea-228">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-228">Yes</span></span> | <span data-ttu-id="1f5ea-229">Especifica se o limite do número total de violações ou falhas consecutivas dos seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="1f5ea-229">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span></span><br><br><span data-ttu-id="1f5ea-230">**Total<br>consecutivas**</span><span class="sxs-lookup"><span data-stu-id="1f5ea-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="1f5ea-231">Operador</span><span class="sxs-lookup"><span data-stu-id="1f5ea-231">Operator</span></span> | <span data-ttu-id="1f5ea-232">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-232">Yes</span></span> | <span data-ttu-id="1f5ea-233">O operador para a comparação dos seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="1f5ea-233">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="1f5ea-234">**gt = maior que<br>lt = menor que**</span><span class="sxs-lookup"><span data-stu-id="1f5ea-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="1f5ea-235">Valor</span><span class="sxs-lookup"><span data-stu-id="1f5ea-235">Value</span></span> | <span data-ttu-id="1f5ea-236">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-236">Yes</span></span> | <span data-ttu-id="1f5ea-237">Número de vezes que os critérios devem ser atendidos para disparar o alerta.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-237">Number of the times the criteria must be met to trigger the alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="1f5ea-238">Limitação</span><span class="sxs-lookup"><span data-stu-id="1f5ea-238">Throttling</span></span>
<span data-ttu-id="1f5ea-239">Esta seção é opcional.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-239">This section is optional.</span></span>  <span data-ttu-id="1f5ea-240">Inclua esta seção se você desejar Suprimir alertas da mesma regra por algum tempo depois que um alerta é criado.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-240">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="1f5ea-241">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="1f5ea-241">Element name</span></span> | <span data-ttu-id="1f5ea-242">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1f5ea-242">Required</span></span> | <span data-ttu-id="1f5ea-243">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f5ea-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1f5ea-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="1f5ea-244">DurationInMinutes</span></span> | <span data-ttu-id="1f5ea-245">Sim, se a limitação elemento incluído</span><span class="sxs-lookup"><span data-stu-id="1f5ea-245">Yes if Throttling element included</span></span> | <span data-ttu-id="1f5ea-246">Número de minutos para suprimir alertas depois da mesma regra de alerta será criado.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-246">Number of minutes to suppress alerts after one from the same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="1f5ea-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="1f5ea-247">EmailNotification</span></span>
 <span data-ttu-id="1f5ea-248">Esta seção é opcional incluí-lo se desejar que o alerta para enviar mensagens a um ou mais destinatários.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-248">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span></span>

| <span data-ttu-id="1f5ea-249">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="1f5ea-249">Element name</span></span> | <span data-ttu-id="1f5ea-250">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1f5ea-250">Required</span></span> | <span data-ttu-id="1f5ea-251">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f5ea-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1f5ea-252">Destinatários</span><span class="sxs-lookup"><span data-stu-id="1f5ea-252">Recipients</span></span> | <span data-ttu-id="1f5ea-253">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-253">Yes</span></span> | <span data-ttu-id="1f5ea-254">Lista delimitada por vírgulas de endereços de email para enviar notificações quando um alerta é criado, como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-254">Comma delimited list of email addresses to send notification when an alert is created such as in the following example.</span></span><br><br><span data-ttu-id="1f5ea-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="1f5ea-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="1f5ea-256">Subject</span><span class="sxs-lookup"><span data-stu-id="1f5ea-256">Subject</span></span> | <span data-ttu-id="1f5ea-257">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-257">Yes</span></span> | <span data-ttu-id="1f5ea-258">Linha de assunto do email.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-258">Subject line of the mail.</span></span> |
| <span data-ttu-id="1f5ea-259">Anexo</span><span class="sxs-lookup"><span data-stu-id="1f5ea-259">Attachment</span></span> | <span data-ttu-id="1f5ea-260">Não</span><span class="sxs-lookup"><span data-stu-id="1f5ea-260">No</span></span> | <span data-ttu-id="1f5ea-261">Anexos não são atualmente suportados.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="1f5ea-262">Se este elemento for incluído, ele deve ser **nenhum**.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="1f5ea-263">Correção</span><span class="sxs-lookup"><span data-stu-id="1f5ea-263">Remediation</span></span>
<span data-ttu-id="1f5ea-264">Esta seção é opcional incluí-lo se você quiser que um runbook para iniciar em resposta ao alerta.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-264">This section is optional  Include it if you want a runbook to start in response to the alert.</span></span> |

| <span data-ttu-id="1f5ea-265">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="1f5ea-265">Element name</span></span> | <span data-ttu-id="1f5ea-266">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1f5ea-266">Required</span></span> | <span data-ttu-id="1f5ea-267">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f5ea-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1f5ea-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="1f5ea-268">RunbookName</span></span> | <span data-ttu-id="1f5ea-269">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-269">Yes</span></span> | <span data-ttu-id="1f5ea-270">Nome do runbook para iniciar.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-270">Name of the runbook to start.</span></span> |
| <span data-ttu-id="1f5ea-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="1f5ea-271">WebhookUri</span></span> | <span data-ttu-id="1f5ea-272">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-272">Yes</span></span> | <span data-ttu-id="1f5ea-273">URI do webhook para o runbook.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-273">Uri of the webhook for the runbook.</span></span> |
| <span data-ttu-id="1f5ea-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="1f5ea-274">Expiry</span></span> | <span data-ttu-id="1f5ea-275">Não</span><span class="sxs-lookup"><span data-stu-id="1f5ea-275">No</span></span> | <span data-ttu-id="1f5ea-276">Data e hora em que a correção expira.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-276">Date and time that the remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="1f5ea-277">Ações de Webhook</span><span class="sxs-lookup"><span data-stu-id="1f5ea-277">Webhook actions</span></span>

<span data-ttu-id="1f5ea-278">Ações de Webhook iniciam um processo chamando uma URL e, opcionalmente, fornecendo uma carga a ser enviada.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-278">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span> <span data-ttu-id="1f5ea-279">Elas são semelhantes às ações de Correção, exceto que se destinam a webhooks que podem invocar outros processos além de runbooks da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-279">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="1f5ea-280">Eles também oferecem a opção adicional de fornecer uma carga a ser enviada para o processo remoto.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-280">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="1f5ea-281">Se o alerta for chamar um webhook, ele precisará de um recurso de ação com um tipo de **Webhook**, além do recurso de ação **Alerta**.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span></span>  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

<span data-ttu-id="1f5ea-282">As propriedades de recursos de ação do Webhook são descritas nas tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-282">The properties for Webhook action resources are described in the following tables.</span></span>

| <span data-ttu-id="1f5ea-283">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="1f5ea-283">Element name</span></span> | <span data-ttu-id="1f5ea-284">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1f5ea-284">Required</span></span> | <span data-ttu-id="1f5ea-285">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f5ea-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="1f5ea-286">type</span><span class="sxs-lookup"><span data-stu-id="1f5ea-286">type</span></span> | <span data-ttu-id="1f5ea-287">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-287">Yes</span></span> | <span data-ttu-id="1f5ea-288">Tipo da ação.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-288">Type of the action.</span></span>  <span data-ttu-id="1f5ea-289">Isso será **Webhook** para ações de webhook.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="1f5ea-290">name</span><span class="sxs-lookup"><span data-stu-id="1f5ea-290">name</span></span> | <span data-ttu-id="1f5ea-291">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-291">Yes</span></span> | <span data-ttu-id="1f5ea-292">Nome de exibição para a ação.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-292">Display name for the action.</span></span>  <span data-ttu-id="1f5ea-293">Isso não é exibido no console.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-293">This is not displayed in the console.</span></span> |
| <span data-ttu-id="1f5ea-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="1f5ea-294">wehookUri</span></span> | <span data-ttu-id="1f5ea-295">Sim</span><span class="sxs-lookup"><span data-stu-id="1f5ea-295">Yes</span></span> | <span data-ttu-id="1f5ea-296">URI para o webhook.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-296">Uri for the webhook.</span></span> |
| <span data-ttu-id="1f5ea-297">customPayload</span><span class="sxs-lookup"><span data-stu-id="1f5ea-297">customPayload</span></span> | <span data-ttu-id="1f5ea-298">Não</span><span class="sxs-lookup"><span data-stu-id="1f5ea-298">No</span></span> | <span data-ttu-id="1f5ea-299">Carga personalizada a ser enviada para o webhook.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-299">Custom payload to be sent to the webhook.</span></span> <span data-ttu-id="1f5ea-300">O formato dependerá do que o webhook está esperando.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-300">The format will depend on what the webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="1f5ea-301">Amostra</span><span class="sxs-lookup"><span data-stu-id="1f5ea-301">Sample</span></span>

<span data-ttu-id="1f5ea-302">A seguir está um exemplo de uma solução que inclua que inclui os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="1f5ea-302">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="1f5ea-303">Pesquisa salva</span><span class="sxs-lookup"><span data-stu-id="1f5ea-303">Saved search</span></span>
- <span data-ttu-id="1f5ea-304">Agenda</span><span class="sxs-lookup"><span data-stu-id="1f5ea-304">Schedule</span></span>
- <span data-ttu-id="1f5ea-305">Ação de alerta</span><span class="sxs-lookup"><span data-stu-id="1f5ea-305">Alert action</span></span>
- <span data-ttu-id="1f5ea-306">Ações de webhook</span><span class="sxs-lookup"><span data-stu-id="1f5ea-306">Webhook action</span></span>

<span data-ttu-id="1f5ea-307">O exemplo usa [parâmetros de solução padrão](operations-management-suite-solutions-solution-file.md#parameters) variáveis que normalmente seriam usados em uma solução em vez de embutir valores nas definições de recurso.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-307">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for the email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


<span data-ttu-id="1f5ea-308">O arquivo de parâmetro a seguir fornece valores de amostras para esta solução.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-308">The following parameter file provides samples values for this solution.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="1f5ea-309">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f5ea-309">Next steps</span></span>
* <span data-ttu-id="1f5ea-310">[Adicionar exibições](operations-management-suite-solutions-resources-views.md) à sua solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-310">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="1f5ea-311">[Adicionar runbooks de automação e outros recursos](operations-management-suite-solutions-resources-automation.md) à sua solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1f5ea-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>

