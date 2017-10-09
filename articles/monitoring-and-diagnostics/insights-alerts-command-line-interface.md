---
title: "alertas de aaaCreate para serviços do Azure - CLI plataforma cruzada | Microsoft Docs"
description: "Disparar emails, notificações, URLs de sites de chamada (webhooks) ou automação quando Olá que especificar condições."
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
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="3af89-103">Criar alertas de métricas no Azure Monitor para Serviços do Azure – CLI de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="3af89-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3af89-104">Portal</span><span class="sxs-lookup"><span data-stu-id="3af89-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="3af89-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3af89-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="3af89-106">CLI</span><span class="sxs-lookup"><span data-stu-id="3af89-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="3af89-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3af89-107">Overview</span></span>
<span data-ttu-id="3af89-108">Este artigo mostra como tooset alertas de métrica do Azure usando Olá multiplataforma Interface de linha de comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="3af89-108">This article shows you how tooset up Azure metric alerts using hello cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="3af89-109">Monitor do Azure é Olá novo nome para o que era chamado de "Azure Insights" até 25 de setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="3af89-109">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="3af89-110">No entanto, Olá namespaces e, portanto, comandos de saudação abaixo ainda contêm insights"Olá".</span><span class="sxs-lookup"><span data-stu-id="3af89-110">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
>
>

<span data-ttu-id="3af89-111">Você pode receber um alerta com base em métricas de monitoramento ou em eventos nos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af89-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="3af89-112">**Valores da métrica** - Olá gatilhos de alerta quando o valor de saudação de uma métrica especificada cruza um limite que você atribui em qualquer direção.</span><span class="sxs-lookup"><span data-stu-id="3af89-112">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="3af89-113">Ou seja, ela aciona ambos quando Olá primeiro condição e, em seguida, posteriormente quando que condição é não está sendo atendida.</span><span class="sxs-lookup"><span data-stu-id="3af89-113">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="3af89-114">**Eventos do log de atividades** – um alerta pode disparar em *cada* evento ou somente quando determinados eventos ocorrem.</span><span class="sxs-lookup"><span data-stu-id="3af89-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="3af89-115">mais sobre alertas de log de atividade de toolearn [clique aqui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="3af89-115">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="3af89-116">Você pode configurar uma saudação de métrica toodo alerta após quando ele dispara:</span><span class="sxs-lookup"><span data-stu-id="3af89-116">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="3af89-117">enviar o administrador do serviço de toohello de notificações de email e coadministradores</span><span class="sxs-lookup"><span data-stu-id="3af89-117">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="3af89-118">Envie email tooadditional emails que você especificar.</span><span class="sxs-lookup"><span data-stu-id="3af89-118">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="3af89-119">chamar um webhook</span><span class="sxs-lookup"><span data-stu-id="3af89-119">call a webhook</span></span>
* <span data-ttu-id="3af89-120">Iniciar a execução de um runbook do Azure (apenas de saudação portal do Azure no momento)</span><span class="sxs-lookup"><span data-stu-id="3af89-120">start execution of an Azure runbook (only from hello Azure portal at this time)</span></span>

<span data-ttu-id="3af89-121">Você pode configurar e obter informações sobre regras de alerta de métrica usando</span><span class="sxs-lookup"><span data-stu-id="3af89-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="3af89-122">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3af89-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="3af89-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3af89-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="3af89-124">CLI (Interface de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="3af89-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="3af89-125">API REST do Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="3af89-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="3af89-126">Você pode sempre receber ajuda para os comandos digitando um comando e colocando - a Ajuda no final de saudação.</span><span class="sxs-lookup"><span data-stu-id="3af89-126">You can always receive help for commands by typing a command and putting -help at hello end.</span></span> <span data-ttu-id="3af89-127">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af89-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a><span data-ttu-id="3af89-128">Criar regras de alerta usando Olá CLI</span><span class="sxs-lookup"><span data-stu-id="3af89-128">Create alert rules using hello CLI</span></span>
1. <span data-ttu-id="3af89-129">Execute Olá pré-requisitos e tooAzure de logon.</span><span class="sxs-lookup"><span data-stu-id="3af89-129">Perform hello Prerequisites and login tooAzure.</span></span> <span data-ttu-id="3af89-130">Consulte [Exemplos de CLI do Azure Monitor](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3af89-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="3af89-131">Em resumo, Olá CLI de instalar e executar esses comandos.</span><span class="sxs-lookup"><span data-stu-id="3af89-131">In short, install hello CLI and run these commands.</span></span> <span data-ttu-id="3af89-132">Eles se conectado, mostrar quais assinatura que você está usando e prepará-lo toorun comandos de Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af89-132">They get you logged in, show what subscription you are using, and prepare you toorun Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="3af89-133">as regras existentes em um grupo de recursos, toolist usar Olá formulário a seguir **insights do azure lista de regras de alertas** *[Opções] &lt;resourceGroup&gt;*</span><span class="sxs-lookup"><span data-stu-id="3af89-133">toolist existing rules on a resource group, use hello following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="3af89-134">toocreate uma regra, você precisa toohave várias partes importantes de informações pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="3af89-134">toocreate a rule, you need toohave several important pieces of information first.</span></span>
  * <span data-ttu-id="3af89-135">Olá **ID de recurso** para os recursos de saudação deseja tooset um alerta para</span><span class="sxs-lookup"><span data-stu-id="3af89-135">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="3af89-136">Olá **definições de métrica** disponíveis para esse recurso</span><span class="sxs-lookup"><span data-stu-id="3af89-136">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="3af89-137">Olá unidirecional tooget ID de recurso é toouse Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af89-137">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="3af89-138">Supondo que o recurso de saudação já foi criada, selecione-o no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="3af89-138">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="3af89-139">Na folha da próxima hello, selecione *propriedades* em Olá *configurações* seção.</span><span class="sxs-lookup"><span data-stu-id="3af89-139">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="3af89-140">Olá *ID de recurso* é um campo na folha de saudação Avançar.</span><span class="sxs-lookup"><span data-stu-id="3af89-140">hello *RESOURCE ID* is a field in hello next blade.</span></span> <span data-ttu-id="3af89-141">Outra maneira é Olá toouse [Gerenciador de recursos do Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3af89-141">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="3af89-142">Um exemplo de ID de recurso para um aplicativo Web é</span><span class="sxs-lookup"><span data-stu-id="3af89-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="3af89-143">tooget uma lista de métricas disponíveis hello e as unidades para as métricas para exemplo de recursos anterior hello, use Olá CLI comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3af89-143">tooget a list of hello available metrics and units for those metrics for hello previous resource example, use hello following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="3af89-144">*PT1M* é a granularidade de saudação de medida disponíveis da saudação (intervalos de 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="3af89-144">*PT1M* is hello granularity of hello available measurement (1-minute intervals).</span></span> <span data-ttu-id="3af89-145">O uso de diferentes granularidades oferece opções diferentes de métrica.</span><span class="sxs-lookup"><span data-stu-id="3af89-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="3af89-146">toocreate uma regra de alerta com base em métrica, use um comando de saudação formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="3af89-146">toocreate a metric-based alert rule, use a command of hello following form:</span></span>

    <span data-ttu-id="3af89-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="3af89-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="3af89-148">Olá exemplo configura um alerta a seguir em um recurso de site da web.</span><span class="sxs-lookup"><span data-stu-id="3af89-148">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="3af89-149">Olá alerta gatilhos sempre que ele recebe consistentemente qualquer tráfego de 5 minutos e, novamente, quando ele recebe nenhum tráfego de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="3af89-149">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="3af89-150">toocreate webhook ou enviar email quando um alerta de métrica é acionado, primeiro crie email hello e/ou webhooks.</span><span class="sxs-lookup"><span data-stu-id="3af89-150">toocreate webhook or send email when a metric alert fires, first create hello email and/or webhooks.</span></span> <span data-ttu-id="3af89-151">Criar a regra de saudação imediatamente posteriormente.</span><span class="sxs-lookup"><span data-stu-id="3af89-151">Then create hello rule immediately afterwards.</span></span> <span data-ttu-id="3af89-152">Você não pode associar webhook ou emails com já criou regras usando Olá CLI.</span><span class="sxs-lookup"><span data-stu-id="3af89-152">You cannot associate webhook or emails with already created rules using hello CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="3af89-153">Você pode verificar se os alertas foram criados corretamente examinando uma regra individual.</span><span class="sxs-lookup"><span data-stu-id="3af89-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="3af89-154">regras de toodelete, use um comando do formulário de saudação:</span><span class="sxs-lookup"><span data-stu-id="3af89-154">toodelete rules, use a command of hello form:</span></span>

    <span data-ttu-id="3af89-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="3af89-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="3af89-156">Esses comandos excluem regras Olá criadas anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="3af89-156">These commands delete hello rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="3af89-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3af89-157">Next steps</span></span>
* <span data-ttu-id="3af89-158">[Obter uma visão geral do monitoramento do Azure](monitoring-overview.md) incluindo Olá tipos de informações você pode coletar e monitorar.</span><span class="sxs-lookup"><span data-stu-id="3af89-158">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="3af89-159">Saiba mais sobre como [configurar webhooks em alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="3af89-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="3af89-160">Saiba mais sobre [Configurar alertas em eventos de Log de Atividades](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="3af89-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="3af89-161">Saiba mais sobre [Runbooks da Automação do Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="3af89-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="3af89-162">Obter um [visão geral de coleta de logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detalhadas métricas de alta frequência em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="3af89-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="3af89-163">Obter um [visão geral da coleção de métricas](insights-how-to-customize-monitoring.md) toomake-se de que o serviço está disponível e respondendo.</span><span class="sxs-lookup"><span data-stu-id="3af89-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
