---
title: "alertas de aaaCreate para serviços do Azure - PowerShell | Microsoft Docs"
description: "Disparar emails, notificações, URLs de sites de chamada (webhooks) ou automação quando Olá que especificar condições."
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
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="b534d-103">Criar alertas de métrica no Azure Monitor para serviços do Azure – PowerShell</span><span class="sxs-lookup"><span data-stu-id="b534d-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b534d-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b534d-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="b534d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b534d-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="b534d-106">CLI</span><span class="sxs-lookup"><span data-stu-id="b534d-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="b534d-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b534d-107">Overview</span></span>
<span data-ttu-id="b534d-108">Este artigo mostra como tooset a métrica do Azure alertas usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b534d-108">This article shows you how tooset up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="b534d-109">Você pode receber um alerta com base em métricas de monitoramento ou em eventos nos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="b534d-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="b534d-110">**Valores da métrica** - Olá gatilhos de alerta quando o valor de saudação de uma métrica especificada cruza um limite que você atribui em qualquer direção.</span><span class="sxs-lookup"><span data-stu-id="b534d-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="b534d-111">Ou seja, ela aciona ambos quando Olá primeiro condição e, em seguida, posteriormente quando que condição é não está sendo atendida.</span><span class="sxs-lookup"><span data-stu-id="b534d-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="b534d-112">**Eventos do log de atividades** – um alerta pode disparar em *cada* evento ou somente quando determinados eventos ocorrem.</span><span class="sxs-lookup"><span data-stu-id="b534d-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="b534d-113">mais sobre alertas de log de atividade de toolearn [clique aqui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="b534d-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="b534d-114">Você pode configurar uma saudação de métrica toodo alerta após quando ele dispara:</span><span class="sxs-lookup"><span data-stu-id="b534d-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="b534d-115">enviar o administrador do serviço de toohello de notificações de email e coadministradores</span><span class="sxs-lookup"><span data-stu-id="b534d-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="b534d-116">Envie email tooadditional emails que você especificar.</span><span class="sxs-lookup"><span data-stu-id="b534d-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="b534d-117">chamar um webhook</span><span class="sxs-lookup"><span data-stu-id="b534d-117">call a webhook</span></span>
* <span data-ttu-id="b534d-118">Iniciar a execução de um runbook do Azure (apenas de saudação portal do Azure)</span><span class="sxs-lookup"><span data-stu-id="b534d-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="b534d-119">Você pode configurar e obter informações sobre o uso de regras de alerta</span><span class="sxs-lookup"><span data-stu-id="b534d-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="b534d-120">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b534d-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="b534d-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b534d-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="b534d-122">CLI (Interface de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="b534d-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="b534d-123">API REST do Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="b534d-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="b534d-124">Para obter informações adicionais, você pode digitar sempre ```Get-Help``` e, em seguida, Olá comando do PowerShell que você deseja obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="b534d-124">For additional information, you can always type ```Get-Help``` and then hello PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="b534d-125">Criar regras de alerta no PowerShell</span><span class="sxs-lookup"><span data-stu-id="b534d-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="b534d-126">Faça logon em tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b534d-126">Log in tooAzure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="b534d-127">Obter uma lista de assinaturas de saudação que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="b534d-127">Get a list of hello subscriptions you have available.</span></span> <span data-ttu-id="b534d-128">Verifique se que você está trabalhando com assinatura de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="b534d-128">Verify that you are working with hello right subscription.</span></span> <span data-ttu-id="b534d-129">Se não, defina-o à direita de toohello um usando a saída de saudação do `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="b534d-129">If not, set it toohello right one using hello output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="b534d-130">as regras existentes em um grupo de recursos, toolist use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b534d-130">toolist existing rules on a resource group, use hello following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="b534d-131">toocreate uma regra, você precisa toohave várias partes importantes de informações pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="b534d-131">toocreate a rule, you need toohave several important pieces of information first.</span></span>

  * <span data-ttu-id="b534d-132">Olá **ID de recurso** para os recursos de saudação deseja tooset um alerta para</span><span class="sxs-lookup"><span data-stu-id="b534d-132">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="b534d-133">Olá **definições de métrica** disponíveis para esse recurso</span><span class="sxs-lookup"><span data-stu-id="b534d-133">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="b534d-134">Olá unidirecional tooget ID de recurso é toouse Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b534d-134">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="b534d-135">Supondo que o recurso de saudação já foi criada, selecione-o no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="b534d-135">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="b534d-136">Na folha da próxima hello, selecione *propriedades* em Olá *configurações* seção.</span><span class="sxs-lookup"><span data-stu-id="b534d-136">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="b534d-137">**ID do recurso** é um campo na folha de saudação Avançar.</span><span class="sxs-lookup"><span data-stu-id="b534d-137">**RESOURCE ID** is a field in hello next blade.</span></span> <span data-ttu-id="b534d-138">Outra maneira é Olá toouse [Gerenciador de recursos do Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b534d-138">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="b534d-139">Um exemplo de ID de Recurso para um aplicativo Web é</span><span class="sxs-lookup"><span data-stu-id="b534d-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="b534d-140">Você pode usar `Get-AzureRmMetricDefinition` tooview lista de saudação de todas as definições de métrica para um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="b534d-140">You can use `Get-AzureRmMetricDefinition` tooview hello list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="b534d-141">Olá exemplo a seguir gera uma tabela com o nome de métrica de saudação e hello unidade para métrica.</span><span class="sxs-lookup"><span data-stu-id="b534d-141">hello following example generates a table with hello metric Name and hello Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="b534d-142">Uma lista completa das opções disponíveis para Get-AzureRmMetricDefinition está disponível executando Get-MetricDefinitions.</span><span class="sxs-lookup"><span data-stu-id="b534d-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="b534d-143">Olá exemplo configura um alerta a seguir em um recurso de site da web.</span><span class="sxs-lookup"><span data-stu-id="b534d-143">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="b534d-144">Olá alerta gatilhos sempre que ele recebe consistentemente qualquer tráfego de 5 minutos e, novamente, quando ele recebe nenhum tráfego de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="b534d-144">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="b534d-145">toocreate webhook ou enviar email quando dispara um alerta, primeiro crie email hello e/ou webhooks.</span><span class="sxs-lookup"><span data-stu-id="b534d-145">toocreate webhook or send email when an alert triggers, first create hello email and/or webhooks.</span></span> <span data-ttu-id="b534d-146">Criar regra Olá posteriormente com imediatamente Olá - marca de ações e, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b534d-146">Then immediately create hello rule afterwards with hello -Actions tag and as shown in hello following example.</span></span> <span data-ttu-id="b534d-147">Você não pode associar o webhook ou emails a regras já criadas usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b534d-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="b534d-148">tooverify que os alertas foram criados corretamente examinando regras individuais hello.</span><span class="sxs-lookup"><span data-stu-id="b534d-148">tooverify that your alerts have been created properly by looking at hello individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="b534d-149">Excluir seus alertas.</span><span class="sxs-lookup"><span data-stu-id="b534d-149">Delete your alerts.</span></span> <span data-ttu-id="b534d-150">Esses comandos excluem regras Olá criadas anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b534d-150">These commands delete hello rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="b534d-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b534d-151">Next steps</span></span>
* <span data-ttu-id="b534d-152">[Obter uma visão geral do monitoramento do Azure](monitoring-overview.md) incluindo Olá tipos de informações você pode coletar e monitorar.</span><span class="sxs-lookup"><span data-stu-id="b534d-152">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="b534d-153">Saiba mais sobre como [configurar webhooks em alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="b534d-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="b534d-154">Saiba mais sobre [Configurar alertas em eventos de Log de Atividades](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="b534d-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="b534d-155">Saiba mais sobre [Runbooks da Automação do Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="b534d-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="b534d-156">Obter um [visão geral de coleta de logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detalhadas métricas de alta frequência em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="b534d-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="b534d-157">Obter um [visão geral da coleção de métricas](insights-how-to-customize-monitoring.md) toomake-se de que o serviço está disponível e respondendo.</span><span class="sxs-lookup"><span data-stu-id="b534d-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
