---
title: "aaaSaved pesquisas e alertas em soluções do OMS | Microsoft Docs"
description: "Soluções do OMS normalmente incluirá as pesquisas salvas em dados de tooanalyze de análise de Log coletados pela solução de saudação.  Eles podem também definir usuário de saudação toonotify alertas ou entram em ação automaticamente em um problema crítico de tooa de resposta.  Este artigo descreve como toodefine análise de Log salvos pesquisas e alertas em um modelo do ARM para que possam ser incluídos em soluções de gerenciamento."
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
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a><span data-ttu-id="ea978-105">Adição de análise de Log salvo tooOMS pesquisas e alertas de solução de gerenciamento (visualização)</span><span class="sxs-lookup"><span data-stu-id="ea978-105">Adding Log Analytics saved searches and alerts tooOMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="ea978-106">Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="ea978-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="ea978-107">Qualquer esquema descrita abaixo é toochange de assunto.</span><span class="sxs-lookup"><span data-stu-id="ea978-107">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="ea978-108">[Soluções de gerenciamento do OMS](operations-management-suite-solutions.md) geralmente inclui [pesquisas salvas](../log-analytics/log-analytics-log-searches.md) nos dados de tooanalyze de análise de Log coletados pela solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooanalyze data collected by hello solution.</span></span>  <span data-ttu-id="ea978-109">Eles também podem definir [alertas](../log-analytics/log-analytics-alerts.md) toonotify Olá usuário ou entram em ação automaticamente em um problema crítico de tooa de resposta.</span><span class="sxs-lookup"><span data-stu-id="ea978-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) toonotify hello user or automatically take action in response tooa critical issue.</span></span>  <span data-ttu-id="ea978-110">Este artigo descreve como toodefine análise de Log salvos pesquisas e alertas em um [modelo de gerenciamento de recursos](../resource-manager-template-walkthrough.md) para que eles podem ser incluídos em [soluções de gerenciamento de](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="ea978-110">This article describes how toodefine Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ea978-111">Olá exemplos neste artigo usam parâmetros e variáveis que são ambos soluções toomanagement necessárias ou comuns e descritos na [criando soluções de gerenciamento no OMS Operations Management Suite ()](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="ea978-111">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="ea978-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ea978-112">Prerequisites</span></span>
<span data-ttu-id="ea978-113">Este artigo pressupõe que você já está familiarizado com como muito[criar uma solução de gerenciamento](operations-management-suite-solutions-creating.md) e a estrutura de saudação de um [modelo do ARM](../resource-group-authoring-templates.md) e o arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="ea978-113">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="ea978-114">Espaço de trabalho do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ea978-114">Log Analytics Workspace</span></span>
<span data-ttu-id="ea978-115">Todos os recursos de Log Analytics estão contidos em um [espaço](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="ea978-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="ea978-116">Conforme descrito em [OMS espaço de trabalho e a conta de automação](operations-management-suite-solutions.md#oms-workspace-and-automation-account) espaço de trabalho de saudação não está incluído na solução de gerenciamento de hello, mas deve existir antes de saudação solução estiver instalada.</span><span class="sxs-lookup"><span data-stu-id="ea978-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello workspace isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="ea978-117">Se não estiver disponível, Olá solução instalação falhará.</span><span class="sxs-lookup"><span data-stu-id="ea978-117">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="ea978-118">nome de saudação do espaço de trabalho de saudação está em nome de saudação de cada recurso de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="ea978-118">hello name of hello workspace is in hello name of each Log Analytics resource.</span></span>  <span data-ttu-id="ea978-119">Isso é feito na solução de saudação com hello **espaço de trabalho** parâmetro como Olá seguinte exemplo de um recurso de savedsearch.</span><span class="sxs-lookup"><span data-stu-id="ea978-119">This is done in hello solution with hello **workspace** parameter as in hello following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="ea978-120">Pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="ea978-120">Saved Searches</span></span>
<span data-ttu-id="ea978-121">Incluir [pesquisas salvas](../log-analytics/log-analytics-log-searches.md) em um solução tooallow usuários tooquery dados coletados pela sua solução.</span><span class="sxs-lookup"><span data-stu-id="ea978-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution tooallow users tooquery data collected by your solution.</span></span>  <span data-ttu-id="ea978-122">Pesquisas salvas serão exibidas sob o **Favoritos** no portal do OMS hello e **pesquisas salvas** em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea978-122">Saved searches will appear under **Favorites** in hello OMS portal and **Saved Searches** in hello Azure portal .</span></span>  <span data-ttu-id="ea978-123">Uma pesquisa salva também é necessária para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="ea978-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="ea978-124">[Pesquisa de análise de log salva](../log-analytics/log-analytics-log-searches.md) recursos têm um tipo de `Microsoft.OperationalInsights/workspaces/savedSearches` e ter Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="ea978-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have hello following structure.</span></span>  <span data-ttu-id="ea978-125">Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="ea978-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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



<span data-ttu-id="ea978-126">Cada uma das propriedades de saudação de pesquisas salvas são descritos na Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="ea978-126">Each of hello properties of a saved search are described in hello following table.</span></span> 

| <span data-ttu-id="ea978-127">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ea978-127">Property</span></span> | <span data-ttu-id="ea978-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="ea978-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ea978-129">categoria</span><span class="sxs-lookup"><span data-stu-id="ea978-129">category</span></span> | <span data-ttu-id="ea978-130">categoria de saudação de pesquisa salva hello.</span><span class="sxs-lookup"><span data-stu-id="ea978-130">hello category for hello saved search.</span></span>  <span data-ttu-id="ea978-131">Qualquer pesquisas salvas em Olá mesma solução geralmente compartilharão uma única categoria para que eles são agrupados juntos no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-131">Any saved searches in hello same solution will often share a single category so they are grouped together in hello console.</span></span> |
| <span data-ttu-id="ea978-132">displayname</span><span class="sxs-lookup"><span data-stu-id="ea978-132">displayname</span></span> | <span data-ttu-id="ea978-133">Nome toodisplay para Olá pesquisa salva no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-133">Name toodisplay for hello saved search in hello portal.</span></span> |
| <span data-ttu-id="ea978-134">query</span><span class="sxs-lookup"><span data-stu-id="ea978-134">query</span></span> | <span data-ttu-id="ea978-135">Toorun de consulta.</span><span class="sxs-lookup"><span data-stu-id="ea978-135">Query toorun.</span></span> |

> [!NOTE]
> <span data-ttu-id="ea978-136">Talvez seja necessário toouse caracteres de escape na consulta Olá se ele inclui os caracteres que podem ser interpretados como JSON.</span><span class="sxs-lookup"><span data-stu-id="ea978-136">You may need toouse escape characters in hello query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="ea978-137">Por exemplo, se a consulta foi **OperationName:"Microsoft.Compute/virtualMachines/write tipo: AzureActivity"**, ele deve ser gravado no arquivo de solução hello como **OperationName tipo: AzureActivity:\" Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="ea978-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in hello solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="ea978-138">Alertas</span><span class="sxs-lookup"><span data-stu-id="ea978-138">Alerts</span></span>
<span data-ttu-id="ea978-139">[Alertas de Log Analytics](../log-analytics/log-analytics-alerts.md) são criados por regras de alerta que executar uma pesquisa salva em um intervalo regular.</span><span class="sxs-lookup"><span data-stu-id="ea978-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="ea978-140">Se os resultados de saudação de consulta Olá correspondam aos critérios especificados, será criado um registro de alerta e um ou mais ações são executadas.</span><span class="sxs-lookup"><span data-stu-id="ea978-140">If hello results of hello query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="ea978-141">Regras de alerta em uma solução de gerenciamento são compostas de saudação três diferentes recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ea978-141">Alert rules in a management solution are made up of hello following three different resources.</span></span>

- <span data-ttu-id="ea978-142">**Pesquisa salva.**</span><span class="sxs-lookup"><span data-stu-id="ea978-142">**Saved search.**</span></span>  <span data-ttu-id="ea978-143">Define a pesquisa de log de saudação que será executada.</span><span class="sxs-lookup"><span data-stu-id="ea978-143">Defines hello log search that will be run.</span></span>  <span data-ttu-id="ea978-144">Várias regras de alerta podem compartilhar uma única pesquisa salva.</span><span class="sxs-lookup"><span data-stu-id="ea978-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="ea978-145">**Agenda.**</span><span class="sxs-lookup"><span data-stu-id="ea978-145">**Schedule.**</span></span>  <span data-ttu-id="ea978-146">Define a frequência hello pesquisa de log será executada.</span><span class="sxs-lookup"><span data-stu-id="ea978-146">Defines how often hello log search will be run.</span></span>  <span data-ttu-id="ea978-147">Cada regra de alerta terá apenas um agendamento.</span><span class="sxs-lookup"><span data-stu-id="ea978-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="ea978-148">**Ação de alerta.**</span><span class="sxs-lookup"><span data-stu-id="ea978-148">**Alert action.**</span></span>  <span data-ttu-id="ea978-149">Cada regra de alerta terá um recurso de ação com um tipo de **alerta** que define os detalhes de saudação do alerta hello como critérios hello quando um registro de alerta será criado e Olá a severidade do alerta.</span><span class="sxs-lookup"><span data-stu-id="ea978-149">Each alert rule will have one action resource with a type of **Alert** that defines hello details of hello alert such as hello criteria for when an alert record will be created and hello alert's severity.</span></span>  <span data-ttu-id="ea978-150">o recurso de ação Olá opcionalmente definirá uma resposta de email e o runbook.</span><span class="sxs-lookup"><span data-stu-id="ea978-150">hello action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="ea978-151">**Ação de Webhook (opcional).**</span><span class="sxs-lookup"><span data-stu-id="ea978-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="ea978-152">Se a regra de alerta Olá chamará um webhook, então requer um recurso de uma ação adicional com um tipo de **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="ea978-152">If hello alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="ea978-153">Salvar pesquisa recursos descritos acima.</span><span class="sxs-lookup"><span data-stu-id="ea978-153">Saved search resources are described above.</span></span>  <span data-ttu-id="ea978-154">Olá outros recursos são descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="ea978-154">hello other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="ea978-155">Recursos de agendamento</span><span class="sxs-lookup"><span data-stu-id="ea978-155">Schedule resource</span></span>

<span data-ttu-id="ea978-156">Uma pesquisa salva pode ter uma ou mais agendas com cada agenda que representa uma regra de alerta separada.</span><span class="sxs-lookup"><span data-stu-id="ea978-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="ea978-157">Hello agendamento define quantas vezes hello pesquisa é executada e Olá intervalo de tempo pela qual Olá dados são recuperados.</span><span class="sxs-lookup"><span data-stu-id="ea978-157">hello schedule defines how often hello search is run and hello time interval over which hello data is retrieved.</span></span>  <span data-ttu-id="ea978-158">Recursos de agendamento tem um tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` e ter Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="ea978-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have hello following structure.</span></span> <span data-ttu-id="ea978-159">Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="ea978-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


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



<span data-ttu-id="ea978-160">Propriedades de saudação para recursos de agendamento são descritas Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="ea978-160">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="ea978-161">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="ea978-161">Element name</span></span> | <span data-ttu-id="ea978-162">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ea978-162">Required</span></span> | <span data-ttu-id="ea978-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="ea978-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ea978-164">Habilitado</span><span class="sxs-lookup"><span data-stu-id="ea978-164">enabled</span></span>       | <span data-ttu-id="ea978-165">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-165">Yes</span></span> | <span data-ttu-id="ea978-166">Especifica se o alerta de saudação é habilitado quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="ea978-166">Specifies whether hello alert is enabled when it's created.</span></span> |
| <span data-ttu-id="ea978-167">intervalo</span><span class="sxs-lookup"><span data-stu-id="ea978-167">interval</span></span>      | <span data-ttu-id="ea978-168">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-168">Yes</span></span> | <span data-ttu-id="ea978-169">Frequência hello consulta é executada em minutos.</span><span class="sxs-lookup"><span data-stu-id="ea978-169">How often hello query runs in minutes.</span></span> |
| <span data-ttu-id="ea978-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="ea978-170">queryTimeSpan</span></span> | <span data-ttu-id="ea978-171">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-171">Yes</span></span> | <span data-ttu-id="ea978-172">Período de tempo em minutos nos quais resultados tooevaluate.</span><span class="sxs-lookup"><span data-stu-id="ea978-172">Length of time in minutes over which tooevaluate results.</span></span> |

<span data-ttu-id="ea978-173">Olá agenda recurso depende de saudação pesquisa salva para que ele seja criado antes de agendamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-173">hello schedule resource should depend on hello saved search so that it's created before hello schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="ea978-174">Ações</span><span class="sxs-lookup"><span data-stu-id="ea978-174">Actions</span></span>
<span data-ttu-id="ea978-175">Há dois tipos de recurso de ação especificado pela Olá **tipo** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ea978-175">There are two types of action resource specified by hello **Type** property.</span></span>  <span data-ttu-id="ea978-176">Uma agenda requer um **alerta** ação que define os detalhes de saudação de regra de alerta hello e quais ações são executadas quando um alerta é criado.</span><span class="sxs-lookup"><span data-stu-id="ea978-176">A schedule requires one **Alert** action which defines hello details of hello alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="ea978-177">Ele também pode incluir um **Webhook** ação se um webhook deve ser chamado de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-177">It may also include a **Webhook** action if a webhook should be called from hello alert.</span></span>  

<span data-ttu-id="ea978-178">Recursos de ação com um tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="ea978-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="ea978-179">Ações de alerta</span><span class="sxs-lookup"><span data-stu-id="ea978-179">Alert actions</span></span>

<span data-ttu-id="ea978-180">Cada agenda terá um **alerta** ação.</span><span class="sxs-lookup"><span data-stu-id="ea978-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="ea978-181">Isso define os detalhes de saudação do alerta hello e, opcionalmente, as ações de notificação e correção.</span><span class="sxs-lookup"><span data-stu-id="ea978-181">This defines hello details of hello alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="ea978-182">Uma notificação envia um email tooone ou mais endereços.</span><span class="sxs-lookup"><span data-stu-id="ea978-182">A notification sends an email tooone or more addresses.</span></span>  <span data-ttu-id="ea978-183">Uma correção inicia um runbook na edição do Azure Automation tooattempt tooremediate Olá detectado.</span><span class="sxs-lookup"><span data-stu-id="ea978-183">A remediation starts a runbook in Azure Automation tooattempt tooremediate hello detected issue.</span></span>

<span data-ttu-id="ea978-184">Ações de alerta tem Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="ea978-184">Alert actions have hello following structure.</span></span>  <span data-ttu-id="ea978-185">Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="ea978-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 



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

<span data-ttu-id="ea978-186">Propriedades de saudação para recursos de ação de alerta são descritas Olá tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="ea978-186">hello properties for Alert action resources are described in hello following tables.</span></span>

| <span data-ttu-id="ea978-187">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="ea978-187">Element name</span></span> | <span data-ttu-id="ea978-188">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ea978-188">Required</span></span> | <span data-ttu-id="ea978-189">Descrição</span><span class="sxs-lookup"><span data-stu-id="ea978-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ea978-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="ea978-190">Type</span></span> | <span data-ttu-id="ea978-191">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-191">Yes</span></span> | <span data-ttu-id="ea978-192">Tipo de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-192">Type of hello action.</span></span>  <span data-ttu-id="ea978-193">Isso será **alerta** para ações de alerta.</span><span class="sxs-lookup"><span data-stu-id="ea978-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="ea978-194">Nome</span><span class="sxs-lookup"><span data-stu-id="ea978-194">Name</span></span> | <span data-ttu-id="ea978-195">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-195">Yes</span></span> | <span data-ttu-id="ea978-196">Nome de exibição de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-196">Display name for hello alert.</span></span>  <span data-ttu-id="ea978-197">Este é o nome de saudação que é exibido no console de saudação de regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-197">This is hello name that's displayed in hello console for hello alert rule.</span></span> |
| <span data-ttu-id="ea978-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="ea978-198">Description</span></span> | <span data-ttu-id="ea978-199">Não</span><span class="sxs-lookup"><span data-stu-id="ea978-199">No</span></span> | <span data-ttu-id="ea978-200">Descrição opcional do alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-200">Optional description of hello alert.</span></span> |
| <span data-ttu-id="ea978-201">Severity</span><span class="sxs-lookup"><span data-stu-id="ea978-201">Severity</span></span> | <span data-ttu-id="ea978-202">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-202">Yes</span></span> | <span data-ttu-id="ea978-203">Severidade do alerta registro Olá Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="ea978-203">Severity of hello alert record from hello following values:</span></span><br><br> <span data-ttu-id="ea978-204">**Crítico**</span><span class="sxs-lookup"><span data-stu-id="ea978-204">**Critical**</span></span><br><span data-ttu-id="ea978-205">**Aviso**</span><span class="sxs-lookup"><span data-stu-id="ea978-205">**Warning**</span></span><br><span data-ttu-id="ea978-206">**Informativo**</span><span class="sxs-lookup"><span data-stu-id="ea978-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="ea978-207">Limite</span><span class="sxs-lookup"><span data-stu-id="ea978-207">Threshold</span></span>
<span data-ttu-id="ea978-208">Esta seção é necessária.</span><span class="sxs-lookup"><span data-stu-id="ea978-208">This section is required.</span></span>  <span data-ttu-id="ea978-209">Ele define as propriedades de saudação para limite de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-209">It defines hello properties for hello alert threshold.</span></span>

| <span data-ttu-id="ea978-210">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="ea978-210">Element name</span></span> | <span data-ttu-id="ea978-211">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ea978-211">Required</span></span> | <span data-ttu-id="ea978-212">Descrição</span><span class="sxs-lookup"><span data-stu-id="ea978-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ea978-213">Operador</span><span class="sxs-lookup"><span data-stu-id="ea978-213">Operator</span></span> | <span data-ttu-id="ea978-214">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-214">Yes</span></span> | <span data-ttu-id="ea978-215">Operador de comparação de saudação do hello valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="ea978-215">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="ea978-216">**gt = maior que<br>lt = menor que**</span><span class="sxs-lookup"><span data-stu-id="ea978-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="ea978-217">Valor</span><span class="sxs-lookup"><span data-stu-id="ea978-217">Value</span></span> | <span data-ttu-id="ea978-218">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-218">Yes</span></span> | <span data-ttu-id="ea978-219">resultados de saudação do Hello valor toocompare.</span><span class="sxs-lookup"><span data-stu-id="ea978-219">hello value toocompare hello results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="ea978-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="ea978-220">MetricsTrigger</span></span>
<span data-ttu-id="ea978-221">Esta seção é opcional.</span><span class="sxs-lookup"><span data-stu-id="ea978-221">This section is optional.</span></span>  <span data-ttu-id="ea978-222">Inclua-o para um alerta de métrica de medição.</span><span class="sxs-lookup"><span data-stu-id="ea978-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="ea978-223">Alertas de métrica de medição estão atualmente em visualização pública.</span><span class="sxs-lookup"><span data-stu-id="ea978-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="ea978-224">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="ea978-224">Element name</span></span> | <span data-ttu-id="ea978-225">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ea978-225">Required</span></span> | <span data-ttu-id="ea978-226">Descrição</span><span class="sxs-lookup"><span data-stu-id="ea978-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ea978-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="ea978-227">TriggerCondition</span></span> | <span data-ttu-id="ea978-228">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-228">Yes</span></span> | <span data-ttu-id="ea978-229">Especifica se o limite de saudação para o número total de violações ou falhas consecutivas da saudação valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="ea978-229">Specifies whether hello threshold is for total number of breaches or consecutive breaches from hello following values:</span></span><br><br><span data-ttu-id="ea978-230">**Total<br>consecutivas**</span><span class="sxs-lookup"><span data-stu-id="ea978-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="ea978-231">Operador</span><span class="sxs-lookup"><span data-stu-id="ea978-231">Operator</span></span> | <span data-ttu-id="ea978-232">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-232">Yes</span></span> | <span data-ttu-id="ea978-233">Operador de comparação de saudação do hello valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="ea978-233">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="ea978-234">**gt = maior que<br>lt = menor que**</span><span class="sxs-lookup"><span data-stu-id="ea978-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="ea978-235">Valor</span><span class="sxs-lookup"><span data-stu-id="ea978-235">Value</span></span> | <span data-ttu-id="ea978-236">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-236">Yes</span></span> | <span data-ttu-id="ea978-237">Número de saudação vezes Olá critérios deve ser atendido tootrigger alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-237">Number of hello times hello criteria must be met tootrigger hello alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="ea978-238">Limitação</span><span class="sxs-lookup"><span data-stu-id="ea978-238">Throttling</span></span>
<span data-ttu-id="ea978-239">Esta seção é opcional.</span><span class="sxs-lookup"><span data-stu-id="ea978-239">This section is optional.</span></span>  <span data-ttu-id="ea978-240">Inclua esta seção se deseja receber alertas toosuppress de saudação mesma regra por algum tempo depois que um alerta é criado.</span><span class="sxs-lookup"><span data-stu-id="ea978-240">Include this section if you want toosuppress alerts from hello same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="ea978-241">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="ea978-241">Element name</span></span> | <span data-ttu-id="ea978-242">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ea978-242">Required</span></span> | <span data-ttu-id="ea978-243">Descrição</span><span class="sxs-lookup"><span data-stu-id="ea978-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ea978-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="ea978-244">DurationInMinutes</span></span> | <span data-ttu-id="ea978-245">Sim, se a limitação elemento incluído</span><span class="sxs-lookup"><span data-stu-id="ea978-245">Yes if Throttling element included</span></span> | <span data-ttu-id="ea978-246">Número de alertas de toosuppress minutos depois que um de saudação mesma regra de alerta é criada.</span><span class="sxs-lookup"><span data-stu-id="ea978-246">Number of minutes toosuppress alerts after one from hello same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="ea978-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="ea978-247">EmailNotification</span></span>
 <span data-ttu-id="ea978-248">Esta seção é opcional incluir se desejar Olá tooone de email de alerta toosend ou mais destinatários.</span><span class="sxs-lookup"><span data-stu-id="ea978-248">This section is optional  Include it if you want hello alert toosend mail tooone or more recipients.</span></span>

| <span data-ttu-id="ea978-249">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="ea978-249">Element name</span></span> | <span data-ttu-id="ea978-250">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ea978-250">Required</span></span> | <span data-ttu-id="ea978-251">Descrição</span><span class="sxs-lookup"><span data-stu-id="ea978-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ea978-252">Destinatários</span><span class="sxs-lookup"><span data-stu-id="ea978-252">Recipients</span></span> | <span data-ttu-id="ea978-253">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-253">Yes</span></span> | <span data-ttu-id="ea978-254">Lista delimitada por vírgulas de email endereços toosend notificação quando um alerta é criado, como no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-254">Comma delimited list of email addresses toosend notification when an alert is created such as in hello following example.</span></span><br><br><span data-ttu-id="ea978-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="ea978-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="ea978-256">Subject</span><span class="sxs-lookup"><span data-stu-id="ea978-256">Subject</span></span> | <span data-ttu-id="ea978-257">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-257">Yes</span></span> | <span data-ttu-id="ea978-258">Linha de assunto de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-258">Subject line of hello mail.</span></span> |
| <span data-ttu-id="ea978-259">Anexo</span><span class="sxs-lookup"><span data-stu-id="ea978-259">Attachment</span></span> | <span data-ttu-id="ea978-260">Não</span><span class="sxs-lookup"><span data-stu-id="ea978-260">No</span></span> | <span data-ttu-id="ea978-261">Anexos não são atualmente suportados.</span><span class="sxs-lookup"><span data-stu-id="ea978-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="ea978-262">Se este elemento for incluído, ele deve ser **nenhum**.</span><span class="sxs-lookup"><span data-stu-id="ea978-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="ea978-263">Correção</span><span class="sxs-lookup"><span data-stu-id="ea978-263">Remediation</span></span>
<span data-ttu-id="ea978-264">Esta seção é opcional incluí-lo se você quiser toostart um runbook no alerta de toohello de resposta.</span><span class="sxs-lookup"><span data-stu-id="ea978-264">This section is optional  Include it if you want a runbook toostart in response toohello alert.</span></span> |

| <span data-ttu-id="ea978-265">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="ea978-265">Element name</span></span> | <span data-ttu-id="ea978-266">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ea978-266">Required</span></span> | <span data-ttu-id="ea978-267">Descrição</span><span class="sxs-lookup"><span data-stu-id="ea978-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ea978-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="ea978-268">RunbookName</span></span> | <span data-ttu-id="ea978-269">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-269">Yes</span></span> | <span data-ttu-id="ea978-270">Nome da saudação runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="ea978-270">Name of hello runbook toostart.</span></span> |
| <span data-ttu-id="ea978-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="ea978-271">WebhookUri</span></span> | <span data-ttu-id="ea978-272">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-272">Yes</span></span> | <span data-ttu-id="ea978-273">URI do webhook Olá Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="ea978-273">Uri of hello webhook for hello runbook.</span></span> |
| <span data-ttu-id="ea978-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="ea978-274">Expiry</span></span> | <span data-ttu-id="ea978-275">Não</span><span class="sxs-lookup"><span data-stu-id="ea978-275">No</span></span> | <span data-ttu-id="ea978-276">Data e hora em que Olá correção expira.</span><span class="sxs-lookup"><span data-stu-id="ea978-276">Date and time that hello remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="ea978-277">Ações de Webhook</span><span class="sxs-lookup"><span data-stu-id="ea978-277">Webhook actions</span></span>

<span data-ttu-id="ea978-278">Ações de Webhook iniciar um processo chamar uma URL e, opcionalmente, fornecendo um toobe carga enviada.</span><span class="sxs-lookup"><span data-stu-id="ea978-278">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span> <span data-ttu-id="ea978-279">Eles são ações tooRemediation semelhantes, exceto que eles se destinam a webhooks que podem chamar outros processos além do runbooks de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea978-279">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="ea978-280">Eles também fornecem a opção adicional de saudação do fornecimento de um processo remoto do toobe entregue toohello de carga.</span><span class="sxs-lookup"><span data-stu-id="ea978-280">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="ea978-281">Se o alerta chamará um webhook, será necessário um recurso de ação com um tipo de **Webhook** na adição toohello **alerta** recurso de ação.</span><span class="sxs-lookup"><span data-stu-id="ea978-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition toohello **Alert** action resource.</span></span>  

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

<span data-ttu-id="ea978-282">Propriedades de saudação para recursos de ação de Webhook são descritas Olá tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="ea978-282">hello properties for Webhook action resources are described in hello following tables.</span></span>

| <span data-ttu-id="ea978-283">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="ea978-283">Element name</span></span> | <span data-ttu-id="ea978-284">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ea978-284">Required</span></span> | <span data-ttu-id="ea978-285">Descrição</span><span class="sxs-lookup"><span data-stu-id="ea978-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ea978-286">type</span><span class="sxs-lookup"><span data-stu-id="ea978-286">type</span></span> | <span data-ttu-id="ea978-287">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-287">Yes</span></span> | <span data-ttu-id="ea978-288">Tipo de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-288">Type of hello action.</span></span>  <span data-ttu-id="ea978-289">Isso será **Webhook** para ações de webhook.</span><span class="sxs-lookup"><span data-stu-id="ea978-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="ea978-290">name</span><span class="sxs-lookup"><span data-stu-id="ea978-290">name</span></span> | <span data-ttu-id="ea978-291">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-291">Yes</span></span> | <span data-ttu-id="ea978-292">Nome de exibição para a ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-292">Display name for hello action.</span></span>  <span data-ttu-id="ea978-293">Isso não é exibido no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-293">This is not displayed in hello console.</span></span> |
| <span data-ttu-id="ea978-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="ea978-294">wehookUri</span></span> | <span data-ttu-id="ea978-295">Sim</span><span class="sxs-lookup"><span data-stu-id="ea978-295">Yes</span></span> | <span data-ttu-id="ea978-296">URI do webhook hello.</span><span class="sxs-lookup"><span data-stu-id="ea978-296">Uri for hello webhook.</span></span> |
| <span data-ttu-id="ea978-297">customPayload</span><span class="sxs-lookup"><span data-stu-id="ea978-297">customPayload</span></span> | <span data-ttu-id="ea978-298">Não</span><span class="sxs-lookup"><span data-stu-id="ea978-298">No</span></span> | <span data-ttu-id="ea978-299">Carga personalizada toobe enviado toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="ea978-299">Custom payload toobe sent toohello webhook.</span></span> <span data-ttu-id="ea978-300">formato Olá dependerá de quais webhook hello está esperando.</span><span class="sxs-lookup"><span data-stu-id="ea978-300">hello format will depend on what hello webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="ea978-301">Amostra</span><span class="sxs-lookup"><span data-stu-id="ea978-301">Sample</span></span>

<span data-ttu-id="ea978-302">A seguir está um exemplo de uma solução que incluem que inclui Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ea978-302">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="ea978-303">Pesquisa salva</span><span class="sxs-lookup"><span data-stu-id="ea978-303">Saved search</span></span>
- <span data-ttu-id="ea978-304">Agenda</span><span class="sxs-lookup"><span data-stu-id="ea978-304">Schedule</span></span>
- <span data-ttu-id="ea978-305">Ação de alerta</span><span class="sxs-lookup"><span data-stu-id="ea978-305">Alert action</span></span>
- <span data-ttu-id="ea978-306">Ações de webhook</span><span class="sxs-lookup"><span data-stu-id="ea978-306">Webhook action</span></span>

<span data-ttu-id="ea978-307">Olá exemplo usa [parâmetros de solução padrão](operations-management-suite-solutions-solution-file.md#parameters) variáveis que normalmente seriam usados em uma solução como oposição toohardcoding valores nas definições de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea978-307">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>

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
              "Description": "List of recipients for hello email alert separated by semicolon"
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


<span data-ttu-id="ea978-308">Olá, arquivo de parâmetro a seguir fornece valores de exemplos para esta solução.</span><span class="sxs-lookup"><span data-stu-id="ea978-308">hello following parameter file provides samples values for this solution.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="ea978-309">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea978-309">Next steps</span></span>
* <span data-ttu-id="ea978-310">[Adicionar modos de exibição](operations-management-suite-solutions-resources-views.md) tooyour solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="ea978-310">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="ea978-311">[Adicionar runbooks de automação e outros recursos](operations-management-suite-solutions-resources-automation.md) tooyour solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="ea978-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>

