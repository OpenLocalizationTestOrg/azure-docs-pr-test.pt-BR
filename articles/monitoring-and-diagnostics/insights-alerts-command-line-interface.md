---
title: "Criar alertas para os serviços do Azure - CLI entre plataformas | Microsoft Docs"
description: "Disparar emails, notificações, chame URLs de sites (webhooks) ou automação quando as condições especificadas forem atendidas."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: 92246a8da73a244a1c9a924bed55711d71a20fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="4883f-103">Criar alertas de métricas no Azure Monitor para Serviços do Azure – CLI de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="4883f-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4883f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="4883f-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="4883f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4883f-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="4883f-106">CLI</span><span class="sxs-lookup"><span data-stu-id="4883f-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="4883f-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4883f-107">Overview</span></span>
<span data-ttu-id="4883f-108">Este artigo mostra como configurar alertas do Azure usando a CLI (Interface de linha de comando) de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="4883f-108">This article shows you how to set up Azure metric alerts using the cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="4883f-109">O Azure Monitor é o novo nome do que era chamado "Azure Insights" até 25 de setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="4883f-109">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="4883f-110">No entanto, os namespaces e, portanto, os comandos a seguir ainda contêm os “insights”.</span><span class="sxs-lookup"><span data-stu-id="4883f-110">However, the namespaces and thus the commands below still contain the "insights".</span></span>
>
>

<span data-ttu-id="4883f-111">Você pode receber um alerta com base em métricas de monitoramento ou em eventos nos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="4883f-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="4883f-112">**Valores da métrica** - o alerta dispara quando o valor de uma métrica especificada ultrapassa um limite que você atribui em qualquer direção.</span><span class="sxs-lookup"><span data-stu-id="4883f-112">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="4883f-113">Ou seja, ele dispara quando a condição é atendida pela primeira vez e posteriormente, quando essa condição não está sendo mais atendida.</span><span class="sxs-lookup"><span data-stu-id="4883f-113">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="4883f-114">**Eventos do log de atividades** – um alerta pode disparar em *cada* evento ou somente quando determinados eventos ocorrem.</span><span class="sxs-lookup"><span data-stu-id="4883f-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="4883f-115">Para saber mais sobre alertas de log de atividades, [clique aqui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="4883f-115">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="4883f-116">Você pode configurar um alerta de métrica para fazer o seguinte quando ele dispara:</span><span class="sxs-lookup"><span data-stu-id="4883f-116">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="4883f-117">enviar um email para o administrador de serviços e os coadministradores</span><span class="sxs-lookup"><span data-stu-id="4883f-117">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="4883f-118">enviar email para outros emails que você especificar.</span><span class="sxs-lookup"><span data-stu-id="4883f-118">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="4883f-119">chamar um webhook</span><span class="sxs-lookup"><span data-stu-id="4883f-119">call a webhook</span></span>
* <span data-ttu-id="4883f-120">iniciar a execução de um runbook do Azure (apenas no portal do Azure no momento)</span><span class="sxs-lookup"><span data-stu-id="4883f-120">start execution of an Azure runbook (only from the Azure portal at this time)</span></span>

<span data-ttu-id="4883f-121">Você pode configurar e obter informações sobre regras de alerta de métrica usando</span><span class="sxs-lookup"><span data-stu-id="4883f-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="4883f-122">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4883f-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="4883f-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4883f-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="4883f-124">CLI (Interface de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="4883f-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="4883f-125">API REST do Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="4883f-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="4883f-126">Você sempre pode receber ajuda sobre os comandos digitando um comando e colocando -help no final.</span><span class="sxs-lookup"><span data-stu-id="4883f-126">You can always receive help for commands by typing a command and putting -help at the end.</span></span> <span data-ttu-id="4883f-127">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4883f-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-the-cli"></a><span data-ttu-id="4883f-128">Criar regras de alerta usando a CLI</span><span class="sxs-lookup"><span data-stu-id="4883f-128">Create alert rules using the CLI</span></span>
1. <span data-ttu-id="4883f-129">Conclua os pré-requisitos e entre no Azure.</span><span class="sxs-lookup"><span data-stu-id="4883f-129">Perform the Prerequisites and login to Azure.</span></span> <span data-ttu-id="4883f-130">Consulte [Exemplos de CLI do Azure Monitor](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4883f-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="4883f-131">Em resumo, instale a CLI e execute os comandos.</span><span class="sxs-lookup"><span data-stu-id="4883f-131">In short, install the CLI and run these commands.</span></span> <span data-ttu-id="4883f-132">Eles conectam você, mostram qual assinatura está usando e preparam para executar comandos do Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="4883f-132">They get you logged in, show what subscription you are using, and prepare you to run Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="4883f-133">Para listar as regras existentes em um grupo de recursos, use o seguinte formato **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span><span class="sxs-lookup"><span data-stu-id="4883f-133">To list existing rules on a resource group, use the following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="4883f-134">Para criar uma regra, primeiro precisa ter várias informações importantes.</span><span class="sxs-lookup"><span data-stu-id="4883f-134">To create a rule, you need to have several important pieces of information first.</span></span>
  * <span data-ttu-id="4883f-135">A **ID de recurso** para o recurso que deve ter um alerta</span><span class="sxs-lookup"><span data-stu-id="4883f-135">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="4883f-136">As **definições de métricas** disponíveis para esse recurso</span><span class="sxs-lookup"><span data-stu-id="4883f-136">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="4883f-137">Uma maneira de obter a ID de recurso é usar o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4883f-137">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="4883f-138">Supondo que o recurso já foi criado, selecione-o no portal.</span><span class="sxs-lookup"><span data-stu-id="4883f-138">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="4883f-139">Na próxima folha, selecione *Propriedades* na seção *Configurações*.</span><span class="sxs-lookup"><span data-stu-id="4883f-139">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="4883f-140">A *ID DE RECURSO* é um campo na folha seguinte.</span><span class="sxs-lookup"><span data-stu-id="4883f-140">The *RESOURCE ID* is a field in the next blade.</span></span> <span data-ttu-id="4883f-141">Outra maneira é usar o [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4883f-141">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="4883f-142">Um exemplo de ID de recurso para um aplicativo Web é</span><span class="sxs-lookup"><span data-stu-id="4883f-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="4883f-143">Para obter uma lista de unidades e métricas disponíveis para essas métricas para o exemplo de recurso anterior, use o seguinte comando CLI:</span><span class="sxs-lookup"><span data-stu-id="4883f-143">To get a list of the available metrics and units for those metrics for the previous resource example, use the following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="4883f-144">*PT1M* é a granularidade da medição disponível (intervalos de 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="4883f-144">*PT1M* is the granularity of the available measurement (1-minute intervals).</span></span> <span data-ttu-id="4883f-145">O uso de diferentes granularidades oferece opções diferentes de métrica.</span><span class="sxs-lookup"><span data-stu-id="4883f-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="4883f-146">Para criar uma regra de alerta com base em métrica, use um comando da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4883f-146">To create a metric-based alert rule, use a command of the following form:</span></span>

    <span data-ttu-id="4883f-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="4883f-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="4883f-148">O exemplo a seguir configura um alerta em um recurso de site da Web.</span><span class="sxs-lookup"><span data-stu-id="4883f-148">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="4883f-149">O alerta dispara sempre que ele recebe tráfego por cinco minutos de forma consistente e novamente quando ele não recebe tráfego por cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="4883f-149">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="4883f-150">Para criar o webhook ou enviar email quando um alerta de métrica é disparado, primeiro crie o email e/ou os webhooks.</span><span class="sxs-lookup"><span data-stu-id="4883f-150">To create webhook or send email when a metric alert fires, first create the email and/or webhooks.</span></span> <span data-ttu-id="4883f-151">Crie a regra imediatamente a seguir.</span><span class="sxs-lookup"><span data-stu-id="4883f-151">Then create the rule immediately afterwards.</span></span> <span data-ttu-id="4883f-152">Você não pode associar webhook ou emails a regras já criadas usando a CLI.</span><span class="sxs-lookup"><span data-stu-id="4883f-152">You cannot associate webhook or emails with already created rules using the CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="4883f-153">Você pode verificar se os alertas foram criados corretamente examinando uma regra individual.</span><span class="sxs-lookup"><span data-stu-id="4883f-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="4883f-154">Para excluir regras, use um comando com esta forma:</span><span class="sxs-lookup"><span data-stu-id="4883f-154">To delete rules, use a command of the form:</span></span>

    <span data-ttu-id="4883f-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="4883f-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="4883f-156">Esses comandos excluem as regras criadas anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="4883f-156">These commands delete the rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="4883f-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4883f-157">Next steps</span></span>
* <span data-ttu-id="4883f-158">[Obter uma visão geral do monitoramento do Azure](monitoring-overview.md) , incluindo os tipos de informações que você pode coletar e monitorar.</span><span class="sxs-lookup"><span data-stu-id="4883f-158">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="4883f-159">Saiba mais sobre como [configurar webhooks em alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4883f-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="4883f-160">Saiba mais sobre [Configurar alertas em eventos de Log de Atividades](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4883f-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="4883f-161">Saiba mais sobre [Runbooks da Automação do Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="4883f-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="4883f-162">Tenha uma [visão geral da coleta de logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md) para coletar métricas detalhadas de alta frequência em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="4883f-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="4883f-163">Tenha uma [visão geral da coleção de métricas](insights-how-to-customize-monitoring.md) para verificar se o serviço está disponível e responsivo.</span><span class="sxs-lookup"><span data-stu-id="4883f-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
