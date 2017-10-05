---
title: "Criar alertas para os serviços do Azure – PowerShell | Microsoft Docs"
description: "Disparar emails, notificações, chame URLs de sites (webhooks) ou automação quando as condições especificadas forem atendidas."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 50127242cdf156771d0610e58cf2fc41281adae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="9daae-103">Criar alertas de métrica no Azure Monitor para serviços do Azure – PowerShell</span><span class="sxs-lookup"><span data-stu-id="9daae-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9daae-104">Portal</span><span class="sxs-lookup"><span data-stu-id="9daae-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="9daae-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9daae-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="9daae-106">CLI</span><span class="sxs-lookup"><span data-stu-id="9daae-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="9daae-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9daae-107">Overview</span></span>
<span data-ttu-id="9daae-108">Este artigo mostra como configurar alertas de métrica do Azure usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9daae-108">This article shows you how to set up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="9daae-109">Você pode receber um alerta com base em métricas de monitoramento ou em eventos nos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="9daae-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="9daae-110">**Valores da métrica** - o alerta dispara quando o valor de uma métrica especificada ultrapassa um limite que você atribui em qualquer direção.</span><span class="sxs-lookup"><span data-stu-id="9daae-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="9daae-111">Ou seja, ele dispara quando a condição é atendida pela primeira vez e posteriormente, quando essa condição não está sendo mais atendida.</span><span class="sxs-lookup"><span data-stu-id="9daae-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="9daae-112">**Eventos do log de atividades** – um alerta pode disparar em *cada* evento ou somente quando determinados eventos ocorrem.</span><span class="sxs-lookup"><span data-stu-id="9daae-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="9daae-113">Para saber mais sobre alertas de log de atividades, [clique aqui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="9daae-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="9daae-114">Você pode configurar um alerta de métrica para fazer o seguinte quando ele dispara:</span><span class="sxs-lookup"><span data-stu-id="9daae-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="9daae-115">enviar um email para o administrador de serviços e os coadministradores</span><span class="sxs-lookup"><span data-stu-id="9daae-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="9daae-116">enviar email para outros emails que você especificar.</span><span class="sxs-lookup"><span data-stu-id="9daae-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="9daae-117">chamar um webhook</span><span class="sxs-lookup"><span data-stu-id="9daae-117">call a webhook</span></span>
* <span data-ttu-id="9daae-118">iniciar a execução de um runbook do Azure (apenas no Portal do Azure)</span><span class="sxs-lookup"><span data-stu-id="9daae-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="9daae-119">Você pode configurar e obter informações sobre o uso de regras de alerta</span><span class="sxs-lookup"><span data-stu-id="9daae-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="9daae-120">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9daae-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="9daae-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9daae-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="9daae-122">CLI (Interface de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="9daae-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="9daae-123">API REST do Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="9daae-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="9daae-124">Para saber mais, digite ```Get-Help``` e depois o comando do PowerShell sobre o qual você deseja obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="9daae-124">For additional information, you can always type ```Get-Help``` and then the PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="9daae-125">Criar regras de alerta no PowerShell</span><span class="sxs-lookup"><span data-stu-id="9daae-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="9daae-126">Fazer logon no Azure.</span><span class="sxs-lookup"><span data-stu-id="9daae-126">Log in to Azure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="9daae-127">Obter uma lista das inscrições disponíveis.</span><span class="sxs-lookup"><span data-stu-id="9daae-127">Get a list of the subscriptions you have available.</span></span> <span data-ttu-id="9daae-128">Verifique se você está trabalhando com a assinatura correta.</span><span class="sxs-lookup"><span data-stu-id="9daae-128">Verify that you are working with the right subscription.</span></span> <span data-ttu-id="9daae-129">Se não estiver, defina a correta usando a saída de `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="9daae-129">If not, set it to the right one using the output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="9daae-130">Para listar as regras existentes em um grupo de recursos, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="9daae-130">To list existing rules on a resource group, use the following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="9daae-131">Para criar uma regra, primeiro precisa ter várias informações importantes.</span><span class="sxs-lookup"><span data-stu-id="9daae-131">To create a rule, you need to have several important pieces of information first.</span></span>

  * <span data-ttu-id="9daae-132">A **ID de recurso** para o recurso que deve ter um alerta</span><span class="sxs-lookup"><span data-stu-id="9daae-132">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="9daae-133">As **definições de métricas** disponíveis para esse recurso</span><span class="sxs-lookup"><span data-stu-id="9daae-133">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="9daae-134">Uma maneira de obter a ID de recurso é usar o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9daae-134">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="9daae-135">Supondo que o recurso já foi criado, selecione-o no portal.</span><span class="sxs-lookup"><span data-stu-id="9daae-135">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="9daae-136">Na próxima folha, selecione *Propriedades* na seção *Configurações*.</span><span class="sxs-lookup"><span data-stu-id="9daae-136">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="9daae-137">A **ID DE RECURSO** é um campo na folha seguinte.</span><span class="sxs-lookup"><span data-stu-id="9daae-137">**RESOURCE ID** is a field in the next blade.</span></span> <span data-ttu-id="9daae-138">Outra maneira é usar o [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9daae-138">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="9daae-139">Um exemplo de ID de Recurso para um aplicativo Web é</span><span class="sxs-lookup"><span data-stu-id="9daae-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="9daae-140">Você pode usar `Get-AzureRmMetricDefinition` para exibir a lista de todas as definições de métrica para um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="9daae-140">You can use `Get-AzureRmMetricDefinition` to view the list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="9daae-141">O exemplo a seguir gera uma tabela com o nome de métrica e a unidade dessa métrica.</span><span class="sxs-lookup"><span data-stu-id="9daae-141">The following example generates a table with the metric Name and the Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="9daae-142">Uma lista completa das opções disponíveis para Get-AzureRmMetricDefinition está disponível executando Get-MetricDefinitions.</span><span class="sxs-lookup"><span data-stu-id="9daae-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="9daae-143">O exemplo a seguir configura um alerta em um recurso de site da Web.</span><span class="sxs-lookup"><span data-stu-id="9daae-143">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="9daae-144">O alerta dispara sempre que ele recebe tráfego por cinco minutos de forma consistente e novamente quando ele não recebe tráfego por cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="9daae-144">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="9daae-145">Para criar o webhook ou enviar email quando um alerta é disparado, primeiro crie o email e/ou os webhooks.</span><span class="sxs-lookup"><span data-stu-id="9daae-145">To create webhook or send email when an alert triggers, first create the email and/or webhooks.</span></span> <span data-ttu-id="9daae-146">Em seguida, crie imediatamente a regra com a marca -Actions,e conforme mostra o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9daae-146">Then immediately create the rule afterwards with the -Actions tag and as shown in the following example.</span></span> <span data-ttu-id="9daae-147">Você não pode associar o webhook ou emails a regras já criadas usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9daae-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="9daae-148">Verificar se os alertas foram criados corretamente examinando regras individuais.</span><span class="sxs-lookup"><span data-stu-id="9daae-148">To verify that your alerts have been created properly by looking at the individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="9daae-149">Excluir seus alertas.</span><span class="sxs-lookup"><span data-stu-id="9daae-149">Delete your alerts.</span></span> <span data-ttu-id="9daae-150">Esses comandos excluem as regras criadas anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9daae-150">These commands delete the rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="9daae-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9daae-151">Next steps</span></span>
* <span data-ttu-id="9daae-152">[Obter uma visão geral do monitoramento do Azure](monitoring-overview.md) , incluindo os tipos de informações que você pode coletar e monitorar.</span><span class="sxs-lookup"><span data-stu-id="9daae-152">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="9daae-153">Saiba mais sobre como [configurar webhooks em alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="9daae-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="9daae-154">Saiba mais sobre [Configurar alertas em eventos de Log de Atividades](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="9daae-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="9daae-155">Saiba mais sobre [Runbooks da Automação do Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="9daae-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="9daae-156">Tenha uma [visão geral da coleta de logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md) para coletar métricas detalhadas de alta frequência em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="9daae-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="9daae-157">Tenha uma [visão geral da coleção de métricas](insights-how-to-customize-monitoring.md) para verificar se o serviço está disponível e responsivo.</span><span class="sxs-lookup"><span data-stu-id="9daae-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
