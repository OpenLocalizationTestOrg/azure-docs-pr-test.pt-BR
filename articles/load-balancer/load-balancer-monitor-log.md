---
title: "aaaMonitor operações, eventos e contadores de Balanceador de carga | Microsoft Docs"
description: Saiba como tooenable eventos de alerta e teste o log de status de integridade para o balanceador de carga do Azure
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
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="bb05e-103">Análise de log para Balanceador de Carga do Azure</span><span class="sxs-lookup"><span data-stu-id="bb05e-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="bb05e-104">Você pode usar diferentes tipos de logs no Azure toomanage e solucionar problemas de balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="bb05e-104">You can use different types of logs in Azure toomanage and troubleshoot load balancers.</span></span> <span data-ttu-id="bb05e-105">Alguns desses logs podem ser acessado por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="bb05e-105">Some of these logs can be accessed through hello portal.</span></span> <span data-ttu-id="bb05e-106">Todos os logs podem ser extraídos de um armazenamento de blobs do Azure e exibidos em diferentes ferramentas, como o Excel e o PowerBI.</span><span class="sxs-lookup"><span data-stu-id="bb05e-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="bb05e-107">Você pode aprender mais sobre Olá diferentes tipos de logs de lista de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="bb05e-107">You can learn more about hello different types of logs from hello list below.</span></span>

* <span data-ttu-id="bb05e-108">**Logs de auditoria:** você pode usar [os Logs de auditoria do Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conhecido como Logs operacionais) tooview todas as operações que estão sendo enviado tooyour assinaturas do Azure e seu status.</span><span class="sxs-lookup"><span data-stu-id="bb05e-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) tooview all operations being submitted tooyour Azure subscription(s), and their status.</span></span> <span data-ttu-id="bb05e-109">Logs de auditoria são habilitados por padrão e podem ser exibidos no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb05e-109">Audit logs are enabled by default, and can be viewed in hello Azure portal.</span></span>
* <span data-ttu-id="bb05e-110">**Logs de eventos de alerta:** você pode usar este rasied de alertas do log tooview pelo Balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb05e-110">**Alert event logs:** You can use this log tooview alerts rasied by hello load balancer.</span></span> <span data-ttu-id="bb05e-111">status de Olá Olá balanceador de carga são coletados a cada cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="bb05e-111">hello status for hello load balancer is collected every five minutes.</span></span> <span data-ttu-id="bb05e-112">Esse log será gravado somente se um evento de alerta do balanceador de carga for gerado.</span><span class="sxs-lookup"><span data-stu-id="bb05e-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="bb05e-113">**Logs de investigação de integridade:** você pode usar esse problemas de tooview log detectado pelo seu teste de integridade, como o número de saudação de instâncias de seu pool de back-end que não estejam recebendo solicitações do balanceador de carga Olá devido a falhas de investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="bb05e-113">**Health probe logs:** You can use this log tooview problems detected by your health probe, such as hello number of instances in your backend-pool that are not receiving requests from hello load balancer because of health probe failures.</span></span> <span data-ttu-id="bb05e-114">Esse log é gravado toowhen há uma alteração no status de investigação de integridade de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb05e-114">This log is written toowhen there is a change in hello health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb05e-115">Atualmente, a análise de log funciona somente para balanceadores de carga voltados para a Internet.</span><span class="sxs-lookup"><span data-stu-id="bb05e-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="bb05e-116">Logs só estão disponíveis para os recursos implantados no modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb05e-116">Logs are only available for resources deployed in hello Resource Manager deployment model.</span></span> <span data-ttu-id="bb05e-117">Você não pode usar os logs para recursos no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="bb05e-117">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="bb05e-118">Para obter mais informações sobre modelos de implantação hello, consulte [Noções básicas sobre o Gerenciador de recursos de implantação e implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bb05e-118">For more information about hello deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="bb05e-119">Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="bb05e-119">Enable logging</span></span>

<span data-ttu-id="bb05e-120">O log de auditoria é habilitado automaticamente para todos os recursos do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="bb05e-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="bb05e-121">Você precisará tooenable eventos e integridade investigação log toostart coletando dados de saudação disponíveis por meio desses logs.</span><span class="sxs-lookup"><span data-stu-id="bb05e-121">You need tooenable event and health probe logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="bb05e-122">Use Olá log de tooenable as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="bb05e-122">Use hello following steps tooenable logging.</span></span>

<span data-ttu-id="bb05e-123">Entrar toohello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bb05e-123">Sign-in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="bb05e-124">Se você ainda não tiver um balanceador de carga, [crie um](load-balancer-get-started-internet-arm-ps.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="bb05e-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="bb05e-125">No portal de saudação, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="bb05e-125">In hello portal, click **Browse**.</span></span>
2. <span data-ttu-id="bb05e-126">Selecione **Balanceadores de carga**.</span><span class="sxs-lookup"><span data-stu-id="bb05e-126">Select **Load Balancers**.</span></span>

    ![portal - balanceador de carga](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="bb05e-128">Selecione um balanceador de carga existente >> **Todas as Configurações**.</span><span class="sxs-lookup"><span data-stu-id="bb05e-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="bb05e-129">Olá direita da caixa de diálogo de saudação em nome de Olá Olá do balanceador de carga, role muito**monitoramento**, clique em **diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="bb05e-129">On hello right side of hello dialog under hello name of hello load balancer, scroll too**Monitoring**, click **Diagnostics**.</span></span>

    ![portal - configurações do balanceador de carga](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="bb05e-131">Em Olá **diagnóstico** painel, em **Status**, selecione **em**.</span><span class="sxs-lookup"><span data-stu-id="bb05e-131">In hello **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="bb05e-132">Clique em **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="bb05e-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="bb05e-133">Em **LOGS**, selecione uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="bb05e-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="bb05e-134">Use Olá controle deslizante toodetermine quantos dias a partir da data de evento será armazenada nos logs de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb05e-134">Use hello slider toodetermine how many days worth of event data will be stored in hello event logs.</span></span> 
8. <span data-ttu-id="bb05e-135">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bb05e-135">Click **Save**.</span></span>

    ![Portal – Logs de diagnóstico](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="bb05e-137">Os logs de auditoria não exigem uma conta de armazenamento separada.</span><span class="sxs-lookup"><span data-stu-id="bb05e-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="bb05e-138">Olá uso de armazenamento para integridade e eventos de log de teste incorrerão em encargos de serviço.</span><span class="sxs-lookup"><span data-stu-id="bb05e-138">hello use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="bb05e-139">Log de auditoria</span><span class="sxs-lookup"><span data-stu-id="bb05e-139">Audit log</span></span>

<span data-ttu-id="bb05e-140">log de auditoria de saudação é gerado por padrão.</span><span class="sxs-lookup"><span data-stu-id="bb05e-140">hello audit log is generated by default.</span></span> <span data-ttu-id="bb05e-141">Olá logs são preservados por 90 dias no armazenamento de Logs de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb05e-141">hello logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="bb05e-142">Saiba mais sobre esses logs lendo Olá [exibir eventos e logs de auditoria](../monitoring-and-diagnostics/insights-debugging-with-events.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="bb05e-142">Learn more about these logs by reading hello [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="bb05e-143">Log de eventos de alerta</span><span class="sxs-lookup"><span data-stu-id="bb05e-143">Alert event log</span></span>

<span data-ttu-id="bb05e-144">Esse log só será gerado se você o tiver habilitado para cada balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="bb05e-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="bb05e-145">eventos de saudação são registrados no formato JSON e armazenados na conta de armazenamento Olá especificado quando você habilitou o log de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb05e-145">hello events are logged in JSON format and stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="bb05e-146">a seguir Olá é um exemplo de um evento.</span><span class="sxs-lookup"><span data-stu-id="bb05e-146">hello following is an example of an event.</span></span>

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

<span data-ttu-id="bb05e-147">Olá JSON de saída mostra Olá *eventname* propriedade que descreve a razão Olá Olá balanceador de carga criado um alerta.</span><span class="sxs-lookup"><span data-stu-id="bb05e-147">hello JSON output shows hello *eventname* property which will describe hello reason for hello load balancer created an alert.</span></span> <span data-ttu-id="bb05e-148">Nesse caso, o alerta Olá gerado venceu esgotamento de porta de tooTCP causado por origem que limita IP NAT (SNAT).</span><span class="sxs-lookup"><span data-stu-id="bb05e-148">In this case, hello alert generated was due tooTCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="bb05e-149">Log de investigação de integridade</span><span class="sxs-lookup"><span data-stu-id="bb05e-149">Health probe log</span></span>

<span data-ttu-id="bb05e-150">Esse log só será gerado se você o tiver habilitado para cada balanceador de carga, conforme detalhado acima.</span><span class="sxs-lookup"><span data-stu-id="bb05e-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="bb05e-151">Olá dados são armazenados na conta de armazenamento Olá especificado quando você habilitou o log de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb05e-151">hello data is stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="bb05e-152">Um contêiner denominado 'insights-logs-loadbalancerprobehealthstatus' é criado e Olá dados a seguir é registrada:</span><span class="sxs-lookup"><span data-stu-id="bb05e-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and hello following data is logged:</span></span>

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

<span data-ttu-id="bb05e-153">a saída JSON Olá mostra no hello propriedades campo Olá informações básicas sobre status de integridade de investigação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb05e-153">hello JSON output shows in hello properties field hello basic information for hello probe health status.</span></span> <span data-ttu-id="bb05e-154">Olá *dipDownCount* propriedade mostra o número total de saudação de instâncias Olá back-end que não estejam recebendo o tráfego de rede devido a respostas de investigação de toofailed.</span><span class="sxs-lookup"><span data-stu-id="bb05e-154">hello *dipDownCount* property shows hello total number of instances on hello back-end which are not receiving network traffic due toofailed probe responses.</span></span>

## <a name="view-and-analyze-hello-audit-log"></a><span data-ttu-id="bb05e-155">Exibir e analisar o log de auditoria de saudação</span><span class="sxs-lookup"><span data-stu-id="bb05e-155">View and analyze hello audit log</span></span>

<span data-ttu-id="bb05e-156">Você pode exibir e analisar dados de log de auditoria usando qualquer um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="bb05e-156">You can view and analyze audit log data using any of hello following methods:</span></span>

* <span data-ttu-id="bb05e-157">**Ferramentas do Azure:** recuperar informações de logs de auditoria Olá por meio do PowerShell do Azure, hello Azure Interface de linha de comando (CLI), Olá API REST do Azure, ou Olá portal de visualização do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb05e-157">**Azure tools:** Retrieve information from hello audit logs through Azure PowerShell, hello Azure Command Line Interface (CLI), hello Azure REST API, or hello Azure preview portal.</span></span> <span data-ttu-id="bb05e-158">Instruções passo a passo para cada método são detalhadas no hello [operações com o Gerenciador de recursos de auditoria](../azure-resource-manager/resource-group-audit.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="bb05e-158">Step-by-step instructions for each method are detailed in hello [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="bb05e-159">**Power BI:** se você ainda não tiver uma conta do [Power BI](https://powerbi.microsoft.com/pricing), será possível experimentar gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="bb05e-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="bb05e-160">Usando Olá [conteúdo de Logs de auditoria do Azure pack para o Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), você pode analisar seus dados com painéis pré-configurados, ou você pode personalizar exibições toosuit seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="bb05e-160">Using hello [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views toosuit your requirements.</span></span>

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a><span data-ttu-id="bb05e-161">Exibir e analisar a investigação de integridade hello e log de eventos</span><span class="sxs-lookup"><span data-stu-id="bb05e-161">View and analyze hello health probe and event log</span></span>

<span data-ttu-id="bb05e-162">Você precisa de armazenamento de tooyour tooconnect de conta e recuperar entradas de log Olá JSON para logs de investigação de integridade e eventos.</span><span class="sxs-lookup"><span data-stu-id="bb05e-162">You need tooconnect tooyour storage account and retrieve hello JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="bb05e-163">Depois de baixar os arquivos JSON hello, você pode convertê-los tooCSV e view no Excel, Power BI ou qualquer outra ferramenta de visualização de dados.</span><span class="sxs-lookup"><span data-stu-id="bb05e-163">Once you download hello JSON files, you can convert them tooCSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="bb05e-164">Se você estiver familiarizado com os conceitos básicos de alterar valores de constantes e variáveis em c# e o Visual Studio, você pode usar o hello [ferramentas de conversor de log](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponíveis no GitHub.</span><span class="sxs-lookup"><span data-stu-id="bb05e-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb05e-165">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bb05e-165">Additional resources</span></span>

* <span data-ttu-id="bb05e-166">[Visualizar os logs de auditoria do Azure com o Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .</span><span class="sxs-lookup"><span data-stu-id="bb05e-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="bb05e-167">[Exibir e analisar logs de auditoria do Azure no Power BI e muito mais](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .</span><span class="sxs-lookup"><span data-stu-id="bb05e-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb05e-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb05e-168">Next steps</span></span>

[<span data-ttu-id="bb05e-169">Entender as investigações do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="bb05e-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
