---
title: "Monitorar operações, eventos e contadores para o Balanceador de Carga | Microsoft Docs"
description: "Saiba como habilitar o registro em log de eventos de alerta e do status da integridade de investigação para o Balanceador de Carga do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 638ecd5e02889bd8cb6e7429dfcec335feaac4a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="ac046-103">Análise de log para Balanceador de Carga do Azure</span><span class="sxs-lookup"><span data-stu-id="ac046-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="ac046-104">Você pode usar diferentes tipos de log no Azure para gerenciar e solucionar problemas de balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="ac046-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span></span> <span data-ttu-id="ac046-105">Alguns desses logs podem ser acessados por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="ac046-105">Some of these logs can be accessed through the portal.</span></span> <span data-ttu-id="ac046-106">Todos os logs podem ser extraídos de um armazenamento de blobs do Azure e exibidos em diferentes ferramentas, como o Excel e o PowerBI.</span><span class="sxs-lookup"><span data-stu-id="ac046-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="ac046-107">Você pode saber mais sobre os diferentes tipos de logs na lista abaixo.</span><span class="sxs-lookup"><span data-stu-id="ac046-107">You can learn more about the different types of logs from the list below.</span></span>

* <span data-ttu-id="ac046-108">**Logs de auditoria:** é possível usar os [Logs de Auditoria do Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conhecidos como Logs Operacionais) para exibir todas as operações que estão sendo enviadas à(s) sua(s) assinatura(s) do Azure, bem como seu status.</span><span class="sxs-lookup"><span data-stu-id="ac046-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span></span> <span data-ttu-id="ac046-109">Os logs de auditoria são habilitados por padrão e podem ser exibidos no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac046-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="ac046-110">**Logs de eventos de alerta:** Você pode usar esse log para ver quais alertas foram gerados para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="ac046-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span></span> <span data-ttu-id="ac046-111">O status do balanceador de carga é coletado a cada cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="ac046-111">The status for the load balancer is collected every five minutes.</span></span> <span data-ttu-id="ac046-112">Esse log será gravado somente se um evento de alerta do balanceador de carga for gerado.</span><span class="sxs-lookup"><span data-stu-id="ac046-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="ac046-113">**Logs de investigação de integridade:** Você pode usar esse log para exibir os problemas detectados pelo seu teste de integridade, como o número de instâncias no pool de back-end que não estão recebendo solicitações do balanceador de carga devido a falhas de investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="ac046-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span></span> <span data-ttu-id="ac046-114">Esse log é gravado quando há uma alteração no status de investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="ac046-114">This log is written to when there is a change in the health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac046-115">Atualmente, a análise de log funciona somente para balanceadores de carga voltados para a Internet.</span><span class="sxs-lookup"><span data-stu-id="ac046-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="ac046-116">Os logs estão disponíveis apenas para os recursos implantados no modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="ac046-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="ac046-117">Você não pode usar logs para recursos do modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="ac046-117">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="ac046-118">Para saber mais sobre esses modelos de implantação, consulte [Understanding Resource Manager deployment and classic deployment (Noções básicas sobre a implantação do Resource Manager e a implantação clássica)](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ac046-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="ac046-119">Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="ac046-119">Enable logging</span></span>

<span data-ttu-id="ac046-120">O log de auditoria é habilitado automaticamente para todos os recursos do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="ac046-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="ac046-121">Você precisa habilitar o registro em log da investigação de integridade e de eventos para começar a coletar os dados disponíveis por meio desses logs.</span><span class="sxs-lookup"><span data-stu-id="ac046-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="ac046-122">Use as etapas a seguir para habilitar o registro em log.</span><span class="sxs-lookup"><span data-stu-id="ac046-122">Use the following steps to enable logging.</span></span>

<span data-ttu-id="ac046-123">Entre no [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac046-123">Sign-in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="ac046-124">Se você ainda não tiver um balanceador de carga, [crie um](load-balancer-get-started-internet-arm-ps.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="ac046-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="ac046-125">No portal, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="ac046-125">In the portal, click **Browse**.</span></span>
2. <span data-ttu-id="ac046-126">Selecione **Balanceadores de carga**.</span><span class="sxs-lookup"><span data-stu-id="ac046-126">Select **Load Balancers**.</span></span>

    ![portal - balanceador de carga](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="ac046-128">Selecione um balanceador de carga existente >> **Todas as Configurações**.</span><span class="sxs-lookup"><span data-stu-id="ac046-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="ac046-129">No lado direito da caixa de diálogo com o nome do balanceador de carga, role até **Monitoramento**, clique em **Diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="ac046-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span></span>

    ![portal - configurações do balanceador de carga](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="ac046-131">No painel **Diagnóstico**, em **Status**, selecione **Ativar**.</span><span class="sxs-lookup"><span data-stu-id="ac046-131">In the **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="ac046-132">Clique em **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="ac046-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="ac046-133">Em **LOGS**, selecione uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="ac046-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="ac046-134">Use o controle deslizante para determinar por quantos dias os dados do evento serão mantidos nos logs de eventos.</span><span class="sxs-lookup"><span data-stu-id="ac046-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span></span> 
8. <span data-ttu-id="ac046-135">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ac046-135">Click **Save**.</span></span>

    ![Portal – Logs de diagnóstico](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="ac046-137">Os logs de auditoria não exigem uma conta de armazenamento separada.</span><span class="sxs-lookup"><span data-stu-id="ac046-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="ac046-138">O uso do armazenamento para registro em log de eventos e da investigação de integridade incorrerá em cobranças de serviço.</span><span class="sxs-lookup"><span data-stu-id="ac046-138">The use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="ac046-139">Log de auditoria</span><span class="sxs-lookup"><span data-stu-id="ac046-139">Audit log</span></span>

<span data-ttu-id="ac046-140">O log de auditoria é gerado por padrão.</span><span class="sxs-lookup"><span data-stu-id="ac046-140">The audit log is generated by default.</span></span> <span data-ttu-id="ac046-141">Os logs são preservados por 90 dias no repositório de Logs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac046-141">The logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="ac046-142">Saiba mais sobre esses logs lendo o artigo [Exibir logs de eventos e de auditoria](../monitoring-and-diagnostics/insights-debugging-with-events.md) .</span><span class="sxs-lookup"><span data-stu-id="ac046-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="ac046-143">Log de eventos de alerta</span><span class="sxs-lookup"><span data-stu-id="ac046-143">Alert event log</span></span>

<span data-ttu-id="ac046-144">Esse log só será gerado se você o tiver habilitado para cada balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="ac046-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="ac046-145">Os dados são registrados no formato JSON e armazenados na conta de armazenamento especificada quando você habilitou o registro em log.</span><span class="sxs-lookup"><span data-stu-id="ac046-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="ac046-146">Segue um exemplo de um evento.</span><span class="sxs-lookup"><span data-stu-id="ac046-146">The following is an example of an event.</span></span>

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

<span data-ttu-id="ac046-147">A saída JSON mostra a propriedade *eventname* , que descreverá o motivo para o balanceador de carga ter criado um alerta.</span><span class="sxs-lookup"><span data-stu-id="ac046-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span></span> <span data-ttu-id="ac046-148">Nesse caso, o alerta gerado foi devido à exaustão da porta TCP causada pelos limites de NAT do IP de origem (SNAT).</span><span class="sxs-lookup"><span data-stu-id="ac046-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="ac046-149">Log de investigação de integridade</span><span class="sxs-lookup"><span data-stu-id="ac046-149">Health probe log</span></span>

<span data-ttu-id="ac046-150">Esse log só será gerado se você o tiver habilitado para cada balanceador de carga, conforme detalhado acima.</span><span class="sxs-lookup"><span data-stu-id="ac046-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="ac046-151">Os dados são armazenados na conta de armazenamento especificada quando você habilitou o registro em log.</span><span class="sxs-lookup"><span data-stu-id="ac046-151">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="ac046-152">Um contêiner denominado 'insights-logs-loadbalancerprobehealthstatus' é criado e os seguintes dados são registrados:</span><span class="sxs-lookup"><span data-stu-id="ac046-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span></span>

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

<span data-ttu-id="ac046-153">A saída JSON mostra no campo de propriedades as informações básicas do status da integridade da investigação.</span><span class="sxs-lookup"><span data-stu-id="ac046-153">The JSON output shows in the properties field the basic information for the probe health status.</span></span> <span data-ttu-id="ac046-154">A propriedade *dipDownCount* mostra o número total de instâncias no back-end que não estão recebendo tráfego de rede devido à falha nas respostas de investigação.</span><span class="sxs-lookup"><span data-stu-id="ac046-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span></span>

## <a name="view-and-analyze-the-audit-log"></a><span data-ttu-id="ac046-155">Exibir e analisar o log de auditoria</span><span class="sxs-lookup"><span data-stu-id="ac046-155">View and analyze the audit log</span></span>

<span data-ttu-id="ac046-156">Você pode exibir e analisar dados do log de auditoria usando qualquer um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="ac046-156">You can view and analyze audit log data using any of the following methods:</span></span>

* <span data-ttu-id="ac046-157">**Ferramentas do azure:** recupere informações dos logs de auditoria por meio do Azure PowerShell, a CLI (Interface de Linha de Comando) do Azure, a API REST do Azure ou o portal de visualização do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac046-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span> <span data-ttu-id="ac046-158">Instruções passo a passo para cada método são detalhadas no artigo [Operações de auditoria com o Gerenciador de Recursos](../azure-resource-manager/resource-group-audit.md) .</span><span class="sxs-lookup"><span data-stu-id="ac046-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="ac046-159">**Power BI:** se você ainda não tiver uma conta do [Power BI](https://powerbi.microsoft.com/pricing), será possível experimentar gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="ac046-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="ac046-160">Usando o [Pacote de conteúdo dos Logs de Auditoria do Azure para Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), é possível analisar seus dados com painéis pré-configurados que ou é possível personalizar as exibições para elas se adequarem aos seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="ac046-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span></span>

## <a name="view-and-analyze-the-health-probe-and-event-log"></a><span data-ttu-id="ac046-161">Exibir e analisar o log de eventos de investigação de integridade</span><span class="sxs-lookup"><span data-stu-id="ac046-161">View and analyze the health probe and event log</span></span>

<span data-ttu-id="ac046-162">Você precisa se conectar à sua conta de armazenamento e recuperar as entradas de log JSON para logs de eventos e investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="ac046-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="ac046-163">Depois de baixar os arquivos JSON, você pode convertê-los em CSV e exibi-lo no Excel, no PowerBI ou em qualquer outra ferramenta de visualização de dados.</span><span class="sxs-lookup"><span data-stu-id="ac046-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="ac046-164">Se estiver familiarizado com o Visual Studio e os conceitos básicos de alteração de valores de constantes e variáveis em C#, você poderá usar as [ferramentas de conversor de log](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponíveis no GitHub.</span><span class="sxs-lookup"><span data-stu-id="ac046-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac046-165">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ac046-165">Additional resources</span></span>

* <span data-ttu-id="ac046-166">[Visualizar os logs de auditoria do Azure com o Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ac046-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="ac046-167">[Exibir e analisar logs de auditoria do Azure no Power BI e muito mais](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .</span><span class="sxs-lookup"><span data-stu-id="ac046-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac046-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac046-168">Next steps</span></span>

[<span data-ttu-id="ac046-169">Entender as investigações do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="ac046-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
