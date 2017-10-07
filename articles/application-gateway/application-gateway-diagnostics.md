---
title: "aaaMonitor acessar logs, logs de desempenho, integridade de back-end e métricas para o Application Gateway | Microsoft Docs"
description: Saiba como tooenable e gerenciar os logs de acesso e logs de desempenho para o Application Gateway
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="b3fad-103">Integridade do back-end, logs de diagnóstico e métricas do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="b3fad-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="b3fad-104">Usando o Gateway de aplicativo do Azure, você pode monitorar os recursos em Olá maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3fad-104">By using Azure Application Gateway, you can monitor resources in hello following ways:</span></span>

* <span data-ttu-id="b3fad-105">[Integridade de back-end](#back-end-health): Application Gateway fornece integridade de saudação de toomonitor Olá recurso de servidores Olá Olá pools de back-end por meio de saudação portal do Azure e do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3fad-105">[Back-end health](#back-end-health): Application Gateway provides hello capability toomonitor hello health of hello servers in hello back-end pools through hello Azure portal and through PowerShell.</span></span> <span data-ttu-id="b3fad-106">Você também pode encontrar integridade Olá dos pools de back-end Olá por meio de logs de diagnóstico de desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-106">You can also find hello health of hello back-end pools through hello performance diagnostic logs.</span></span>

* <span data-ttu-id="b3fad-107">[Logs](#diagnostic-logs): permitem Logs de desempenho, acesso, e outros dados toobe salvo ou consumidos a partir de um recurso para fins de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="b3fad-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data toobe saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="b3fad-108">[Métricas](#metrics): atualmente, o Gateway de Aplicativo tem uma métrica.</span><span class="sxs-lookup"><span data-stu-id="b3fad-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="b3fad-109">Essa métrica mede a taxa de transferência de saudação do gateway de aplicativo hello em bytes por segundo.</span><span class="sxs-lookup"><span data-stu-id="b3fad-109">This metric measures hello throughput of hello application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="b3fad-110">Integridade do back-end</span><span class="sxs-lookup"><span data-stu-id="b3fad-110">Back-end health</span></span>

<span data-ttu-id="b3fad-111">Application Gateway fornece integridade de saudação do hello recurso toomonitor de membros individuais de pools de back-end Olá através do portal hello, PowerShell e Olá interface de linha de comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="b3fad-111">Application Gateway provides hello capability toomonitor hello health of individual members of hello back-end pools through hello portal, PowerShell, and hello command-line interface (CLI).</span></span> <span data-ttu-id="b3fad-112">Você também pode encontrar uma integridade agregada resumo dos pools de back-end por meio de logs de diagnóstico de desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-112">You can also find an aggregated health summary of back-end pools through hello performance diagnostic logs.</span></span> 

<span data-ttu-id="b3fad-113">relatório de integridade de back-end de saudação reflete a saída de hello de instâncias de saudação toohello de investigação de integridade back-end Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="b3fad-113">hello back-end health report reflects hello output of hello Application Gateway health probe toohello back-end instances.</span></span> <span data-ttu-id="b3fad-114">Quando probing for bem-sucedida e Olá volta final pode receber tráfego, ele será considerado íntegro.</span><span class="sxs-lookup"><span data-stu-id="b3fad-114">When probing is successful and hello back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="b3fad-115">Caso contrário, ele é considerado não íntegro.</span><span class="sxs-lookup"><span data-stu-id="b3fad-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3fad-116">Se houver um grupo de segurança de rede (NSG) em uma sub-rede de Gateway do aplicativo, abra a intervalos de porta 65503 65534 na sub-rede de Gateway do aplicativo hello para tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="b3fad-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on hello Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="b3fad-117">Essas portas são necessárias para Olá toowork de API de integridade de back-end.</span><span class="sxs-lookup"><span data-stu-id="b3fad-117">These ports are required for hello back-end health API toowork.</span></span>


### <a name="view-back-end-health-through-hello-portal"></a><span data-ttu-id="b3fad-118">Exibir a integridade de back-end por meio do portal Olá</span><span class="sxs-lookup"><span data-stu-id="b3fad-118">View back-end health through hello portal</span></span>

<span data-ttu-id="b3fad-119">No portal de hello, integridade de back-end é fornecida automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b3fad-119">In hello portal, back-end health is provided automatically.</span></span> <span data-ttu-id="b3fad-120">Em um gateway de aplicativo existente, selecione **Monitoramento** > **Integridade do back-end**.</span><span class="sxs-lookup"><span data-stu-id="b3fad-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="b3fad-121">Cada membro no pool de back-end hello está listado nesta página (se ele é uma NIC, IP ou FQDN).</span><span class="sxs-lookup"><span data-stu-id="b3fad-121">Each member in hello back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="b3fad-122">São mostrados o nome do pool de back-end, a porta, as configurações de HTTP do back-end e o status de integridade.</span><span class="sxs-lookup"><span data-stu-id="b3fad-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="b3fad-123">Os valores válidos para o status de integridade são **Íntegro**, **Não íntegro** e **Desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="b3fad-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="b3fad-124">Se você ver um status de integridade de back-end do **desconhecido**, certifique-se de que esse acesso toohello back-end não está bloqueado por uma regra NSG, uma rota definida pelo usuário (UDR) ou um personalizadas de DNS na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-124">If you see a back-end health status of **Unknown**, ensure that access toohello back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in hello virtual network.</span></span>

![Integridade do back-end][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="b3fad-126">Exibir a integridade do back-end por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fad-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="b3fad-127">Olá, código do PowerShell a seguir mostra como a integridade de back-end tooview usando Olá `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b3fad-127">hello following PowerShell code shows how tooview back-end health by using hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="b3fad-128">Exibir a integridade do back-end por meio da CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="b3fad-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="b3fad-129">Resultados</span><span class="sxs-lookup"><span data-stu-id="b3fad-129">Results</span></span>

<span data-ttu-id="b3fad-130">saudação de trecho de código a seguir mostra um exemplo de resposta de saudação:</span><span class="sxs-lookup"><span data-stu-id="b3fad-130">hello following snippet shows an example of hello response:</span></span>

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <span data-ttu-id="b3fad-131"><a name="diagnostic-logging"></a>Logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="b3fad-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="b3fad-132">Você pode usar diferentes tipos de logs no Azure toomanage e solucionar problemas com gateways de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b3fad-132">You can use different types of logs in Azure toomanage and troubleshoot application gateways.</span></span> <span data-ttu-id="b3fad-133">Você pode acessar alguns desses logs por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-133">You can access some of these logs through hello portal.</span></span> <span data-ttu-id="b3fad-134">Todos os logs podem ser extraídos de um Armazenamento de blobs do Azure e exibidos em diferentes ferramentas, como [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel e Power BI.</span><span class="sxs-lookup"><span data-stu-id="b3fad-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="b3fad-135">Você pode aprender mais sobre Olá diferentes tipos de logs de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3fad-135">You can learn more about hello different types of logs from hello following list:</span></span>

* <span data-ttu-id="b3fad-136">**Log de atividades**: você pode usar [logs de atividades do Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conhecida como logs de auditoria e logs operacionais) tooview todas as operações que são enviadas tooyour assinatura do Azure e seu status.</span><span class="sxs-lookup"><span data-stu-id="b3fad-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) tooview all operations that are submitted tooyour Azure subscription, and their status.</span></span> <span data-ttu-id="b3fad-137">As entradas de log de atividades são coletadas por padrão, e você pode exibi-los no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-137">Activity log entries are collected by default, and you can view them in hello Azure portal.</span></span>
* <span data-ttu-id="b3fad-138">**Log de acesso**: você pode usar padrões de acesso a este log tooview Application Gateway e analisar informações importantes, incluindo chamador Olá IP, URL solicitada, latência de resposta, o código de retorno e bytes de entrada e saída. Um log de acesso é coletado a cada 300 segundos.</span><span class="sxs-lookup"><span data-stu-id="b3fad-138">**Access log**: You can use this log tooview Application Gateway access patterns and analyze important information, including hello caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="b3fad-139">Esse log contém um registro por instância do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b3fad-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="b3fad-140">instância do Application Gateway Olá pode ser identificada pela propriedade de instanceId hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-140">hello Application Gateway instance can be identified by hello instanceId property.</span></span>
* <span data-ttu-id="b3fad-141">**Log de desempenho**: você pode usar este tooview de log como instâncias de Gateway de aplicativos são executados.</span><span class="sxs-lookup"><span data-stu-id="b3fad-141">**Performance log**: You can use this log tooview how Application Gateway instances are performing.</span></span> <span data-ttu-id="b3fad-142">Esse log captura informações de desempenho de cada instância, incluindo o total de solicitações atendidas, a vazão de dados em bytes, o total de solicitações atendidas, a contagem de solicitações com falha e a contagem de instâncias de back-end íntegras ou não íntegras.</span><span class="sxs-lookup"><span data-stu-id="b3fad-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="b3fad-143">Um log de desempenho é coletado a cada 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="b3fad-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="b3fad-144">**Log de firewall**: você pode usar este solicitações Olá tooview de log que são registrados por meio do modo de detecção ou prevenção de um gateway de aplicativo que é configurado com o firewall do aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-144">**Firewall log**: You can use this log tooview hello requests that are logged through either detection or prevention mode of an application gateway that is configured with hello web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="b3fad-145">Logs estão disponíveis apenas para os recursos implantados no modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-145">Logs are available only for resources deployed in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="b3fad-146">Você não pode usar os logs para recursos no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-146">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="b3fad-147">Para melhor compreensão de modelos de saudação dois, consulte Olá [Noções básicas sobre o Gerenciador de recursos de implantação e implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b3fad-147">For a better understanding of hello two models, see hello [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="b3fad-148">Você tem três opções para armazenar os logs:</span><span class="sxs-lookup"><span data-stu-id="b3fad-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="b3fad-149">**Conta de armazenamento**: as contas de armazenamento são mais adequadas para os logs quando eles são armazenados por mais tempo e examinados quando necessário.</span><span class="sxs-lookup"><span data-stu-id="b3fad-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="b3fad-150">**Hubs de eventos**: hubs de eventos são uma ótima opção para a integração com outras informações de segurança e tooget alertas sobre os recursos das ferramentas de gerenciamento de eventos (SEIM).</span><span class="sxs-lookup"><span data-stu-id="b3fad-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools tooget alerts on your resources.</span></span>
* <span data-ttu-id="b3fad-151">**Log Analytics**: o Log Analytics é mais adequado para o monitoramento geral em tempo real do aplicativo ou para a observação de tendências.</span><span class="sxs-lookup"><span data-stu-id="b3fad-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="b3fad-152">Habilitar o log por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fad-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="b3fad-153">O log de atividade é habilitado automaticamente para todos os recursos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3fad-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="b3fad-154">Você deve habilitar o acesso e toostart de log de desempenho coleta dados de saudação disponíveis por meio desses logs.</span><span class="sxs-lookup"><span data-stu-id="b3fad-154">You must enable access and performance logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="b3fad-155">tooenable log Olá use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3fad-155">tooenable logging, use hello following steps:</span></span>

1. <span data-ttu-id="b3fad-156">Observe a ID do recurso da sua conta de armazenamento, onde são armazenados dados de log hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-156">Note your storage account's resource ID, where hello log data is stored.</span></span> <span data-ttu-id="b3fad-157">Esse valor é de formulário Olá: /subscriptions/\<subscriptionId\>/resourceGroups/\<nome do grupo de recursos\>/providers/Microsoft.Storage/storageAccounts/\<denomedecontadearmazenamento\>.</span><span class="sxs-lookup"><span data-stu-id="b3fad-157">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="b3fad-158">Use qualquer conta de armazenamento em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b3fad-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="b3fad-159">Você pode usar essas informações para Olá toofind portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3fad-159">You can use hello Azure portal toofind this information.</span></span>

    ![Portal: ID do recurso da conta de armazenamento](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="b3fad-161">Anote a ID do Recurso do gateway de aplicativo para o qual o log está habilitado.</span><span class="sxs-lookup"><span data-stu-id="b3fad-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="b3fad-162">Esse valor é de formulário Olá: /subscriptions/\<subscriptionId\>/resourceGroups/\<nome do grupo de recursos\>/providers/Microsoft.Network/applicationGateways/\<gateway de aplicativo nome\>.</span><span class="sxs-lookup"><span data-stu-id="b3fad-162">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="b3fad-163">Você pode usar essas informações para toofind portal hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-163">You can use hello portal toofind this information.</span></span>

    ![Portal: ID do recurso do gateway de aplicativo](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="b3fad-165">Habilite o log de diagnóstico usando Olá cmdlet do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3fad-165">Enable diagnostic logging by using hello following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="b3fad-166">Os logs de atividades não exigem uma conta de armazenamento separada.</span><span class="sxs-lookup"><span data-stu-id="b3fad-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="b3fad-167">uso de saudação do armazenamento para o log de desempenho e acesso incorre em encargos de serviço.</span><span class="sxs-lookup"><span data-stu-id="b3fad-167">hello use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-hello-azure-portal"></a><span data-ttu-id="b3fad-168">Habilitar registro em log por meio de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b3fad-168">Enable logging through hello Azure portal</span></span>

1. <span data-ttu-id="b3fad-169">Olá portal do Azure, encontrar seu recurso e clique em **logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="b3fad-169">In hello Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="b3fad-170">Para o Gateway de Aplicativo, três logs estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="b3fad-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="b3fad-171">Log de acesso</span><span class="sxs-lookup"><span data-stu-id="b3fad-171">Access log</span></span>
   * <span data-ttu-id="b3fad-172">Log de desempenho</span><span class="sxs-lookup"><span data-stu-id="b3fad-172">Performance log</span></span>
   * <span data-ttu-id="b3fad-173">Log de firewall</span><span class="sxs-lookup"><span data-stu-id="b3fad-173">Firewall log</span></span>

2. <span data-ttu-id="b3fad-174">toostart a coleta de dados, clique em **Ativar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="b3fad-174">toostart collecting data, click **Turn on diagnostics**.</span></span>

   ![Ativando o diagnóstico][1]

3. <span data-ttu-id="b3fad-176">Olá **as configurações de diagnóstico** folha fornece configurações Olá Olá logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b3fad-176">hello **Diagnostics settings** blade provides hello settings for hello diagnostic logs.</span></span> <span data-ttu-id="b3fad-177">Neste exemplo, a análise de Log armazena Olá logs.</span><span class="sxs-lookup"><span data-stu-id="b3fad-177">In this example, Log Analytics stores hello logs.</span></span> <span data-ttu-id="b3fad-178">Clique em **configurar** em **análise de Log** tooconfigure seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b3fad-178">Click **Configure** under **Log Analytics** tooconfigure your workspace.</span></span> <span data-ttu-id="b3fad-179">Você também pode usar hubs de eventos e um armazenamento conta toosave Olá logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b3fad-179">You can also use event hubs and a storage account toosave hello diagnostic logs.</span></span>

   ![Iniciar o processo de configuração Olá][2]

4. <span data-ttu-id="b3fad-181">Escolha um espaço de trabalho do OMS (Operations Management Suite) existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="b3fad-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="b3fad-182">Este exemplo usa um existente.</span><span class="sxs-lookup"><span data-stu-id="b3fad-182">This example uses an existing one.</span></span>

   ![Opções de espaços de trabalho do OMS][3]

5. <span data-ttu-id="b3fad-184">Confirme as configurações de saudação e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="b3fad-184">Confirm hello settings and click **Save**.</span></span>

   ![Folha Configurações de diagnóstico com seleções][4]

### <a name="activity-log"></a><span data-ttu-id="b3fad-186">Log de atividades</span><span class="sxs-lookup"><span data-stu-id="b3fad-186">Activity log</span></span>

<span data-ttu-id="b3fad-187">Por padrão, o Azure gera o log de atividades hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-187">Azure generates hello activity log by default.</span></span> <span data-ttu-id="b3fad-188">Olá logs são preservados por 90 dias no armazenamento de logs de eventos do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-188">hello logs are preserved for 90 days in hello Azure event logs store.</span></span> <span data-ttu-id="b3fad-189">Saiba mais sobre esses logs lendo Olá [exibir eventos e log de atividades](../monitoring-and-diagnostics/insights-debugging-with-events.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b3fad-189">Learn more about these logs by reading hello [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="b3fad-190">Log de acesso</span><span class="sxs-lookup"><span data-stu-id="b3fad-190">Access log</span></span>

<span data-ttu-id="b3fad-191">log de acesso de saudação é gerado apenas se você tiver habilitado em cada instância de Gateway do aplicativo, conforme detalhado nas etapas anteriores de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-191">hello access log is generated only if you've enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="b3fad-192">Olá dados são armazenados na conta de armazenamento Olá especificado quando você habilitou o log de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-192">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="b3fad-193">Cada acesso do Application Gateway é registrado no formato JSON, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="b3fad-193">Each access of Application Gateway is logged in JSON format, as shown in hello following example:</span></span>


|<span data-ttu-id="b3fad-194">Valor</span><span class="sxs-lookup"><span data-stu-id="b3fad-194">Value</span></span>  |<span data-ttu-id="b3fad-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="b3fad-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="b3fad-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="b3fad-196">instanceId</span></span>     | <span data-ttu-id="b3fad-197">Application Gateway instância solicitação Olá atendidas.</span><span class="sxs-lookup"><span data-stu-id="b3fad-197">Application Gateway instance that served hello request.</span></span>        |
|<span data-ttu-id="b3fad-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="b3fad-198">clientIP</span></span>     | <span data-ttu-id="b3fad-199">IP de origem para a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-199">Originating IP for hello request.</span></span>        |
|<span data-ttu-id="b3fad-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="b3fad-200">clientPort</span></span>     | <span data-ttu-id="b3fad-201">Porta de origem para solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-201">Originating port for hello request.</span></span>       |
|<span data-ttu-id="b3fad-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="b3fad-202">httpMethod</span></span>     | <span data-ttu-id="b3fad-203">Método HTTP usado por solicitação hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-203">HTTP method used by hello request.</span></span>       |
|<span data-ttu-id="b3fad-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="b3fad-204">requestUri</span></span>     | <span data-ttu-id="b3fad-205">URI da solicitação recebida hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-205">URI of hello received request.</span></span>        |
|<span data-ttu-id="b3fad-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="b3fad-206">RequestQuery</span></span>     | <span data-ttu-id="b3fad-207">**Roteada por servidor**: instância de pool de Back-end que recebeu a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-207">**Server-Routed**: Back-end pool instance that was sent hello request.</span></span> </br> <span data-ttu-id="b3fad-208">**X-AzureApplicationGateway-LOG-ID**: ID de correlação usado para solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for hello request.</span></span> <span data-ttu-id="b3fad-209">Ele pode ser usado tootroubleshoot tráfego problemas em servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-209">It can be used tootroubleshoot traffic issues on hello back-end servers.</span></span> </br><span data-ttu-id="b3fad-210">**STATUS do servidor**: código de resposta HTTP recebido do Application Gateway de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from hello back end.</span></span>       |
|<span data-ttu-id="b3fad-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="b3fad-211">UserAgent</span></span>     | <span data-ttu-id="b3fad-212">Agente do usuário do cabeçalho de solicitação HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-212">User agent from hello HTTP request header.</span></span>        |
|<span data-ttu-id="b3fad-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="b3fad-213">httpStatus</span></span>     | <span data-ttu-id="b3fad-214">Código de status HTTP retornado toohello cliente do Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="b3fad-214">HTTP status code returned toohello client from Application Gateway.</span></span>       |
|<span data-ttu-id="b3fad-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="b3fad-215">httpVersion</span></span>     | <span data-ttu-id="b3fad-216">Versão HTTP da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-216">HTTP version of hello request.</span></span>        |
|<span data-ttu-id="b3fad-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="b3fad-217">receivedBytes</span></span>     | <span data-ttu-id="b3fad-218">Tamanho do pacote recebido, em bytes.</span><span class="sxs-lookup"><span data-stu-id="b3fad-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="b3fad-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="b3fad-219">sentBytes</span></span>| <span data-ttu-id="b3fad-220">Tamanho do pacote enviado, em bytes.</span><span class="sxs-lookup"><span data-stu-id="b3fad-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="b3fad-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="b3fad-221">timeTaken</span></span>| <span data-ttu-id="b3fad-222">Período de tempo (em milissegundos) necessário para que um toobe de solicitação processadas e seu toobe resposta enviada.</span><span class="sxs-lookup"><span data-stu-id="b3fad-222">Length of time (in milliseconds) that it takes for a request toobe processed and its response toobe sent.</span></span> <span data-ttu-id="b3fad-223">Isso é calculado como o intervalo de saudação do tempo de saudação quando o Application Gateway recebe o primeiro byte de um tempo de toohello de solicitação HTTP quando resposta Olá envia a conclusão da operação Olá.</span><span class="sxs-lookup"><span data-stu-id="b3fad-223">This is calculated as hello interval from hello time when Application Gateway receives hello first byte of an HTTP request toohello time when hello response send operation finishes.</span></span> <span data-ttu-id="b3fad-224">É importante toonote que Olá campo Time-Taken geralmente inclui o tempo de saudação que viajam pela rede Olá pacotes de solicitação e resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-224">It's important toonote that hello Time-Taken field usually includes hello time that hello request and response packets are traveling over hello network.</span></span> |
|<span data-ttu-id="b3fad-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="b3fad-225">sslEnabled</span></span>| <span data-ttu-id="b3fad-226">Se os pools de back-end de toohello de comunicação usado SSL.</span><span class="sxs-lookup"><span data-stu-id="b3fad-226">Whether communication toohello back-end pools used SSL.</span></span> <span data-ttu-id="b3fad-227">Os valores válidos são ativado e desativado.</span><span class="sxs-lookup"><span data-stu-id="b3fad-227">Valid values are on and off.</span></span>|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a><span data-ttu-id="b3fad-228">Log de desempenho</span><span class="sxs-lookup"><span data-stu-id="b3fad-228">Performance log</span></span>

<span data-ttu-id="b3fad-229">log de desempenho de saudação é gerado apenas se você habilitou em cada instância de Gateway do aplicativo, conforme detalhado nas etapas anteriores de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-229">hello performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="b3fad-230">Olá dados são armazenados na conta de armazenamento Olá especificado quando você habilitou o log de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-230">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="b3fad-231">dados de log de desempenho de saudação são gerados em intervalos de 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="b3fad-231">hello performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="b3fad-232">Olá seguintes dados é registrado:</span><span class="sxs-lookup"><span data-stu-id="b3fad-232">hello following data is logged:</span></span>


|<span data-ttu-id="b3fad-233">Valor</span><span class="sxs-lookup"><span data-stu-id="b3fad-233">Value</span></span>  |<span data-ttu-id="b3fad-234">Descrição</span><span class="sxs-lookup"><span data-stu-id="b3fad-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="b3fad-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="b3fad-235">instanceId</span></span>     |  <span data-ttu-id="b3fad-236">Instância do Gateway de Aplicativo para a qual os dados de desempenho estão sendo gerados.</span><span class="sxs-lookup"><span data-stu-id="b3fad-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="b3fad-237">Para um gateway de aplicativo de várias instâncias, há uma linha por instância.</span><span class="sxs-lookup"><span data-stu-id="b3fad-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="b3fad-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="b3fad-238">healthyHostCount</span></span>     | <span data-ttu-id="b3fad-239">Número de hosts íntegros no pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-239">Number of healthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="b3fad-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="b3fad-240">unHealthyHostCount</span></span>     | <span data-ttu-id="b3fad-241">Número de hosts não íntegro no pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-241">Number of unhealthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="b3fad-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="b3fad-242">requestCount</span></span>     | <span data-ttu-id="b3fad-243">Número de solicitações atendidas.</span><span class="sxs-lookup"><span data-stu-id="b3fad-243">Number of requests served.</span></span>        |
|<span data-ttu-id="b3fad-244">latency</span><span class="sxs-lookup"><span data-stu-id="b3fad-244">latency</span></span> | <span data-ttu-id="b3fad-245">Latência (em milissegundos) de solicitações de saudação instância toohello back-end que atende a solicitações de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-245">Latency (in milliseconds) of requests from hello instance toohello back end that serves hello requests.</span></span> |
|<span data-ttu-id="b3fad-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="b3fad-246">failedRequestCount</span></span>| <span data-ttu-id="b3fad-247">Número de solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="b3fad-247">Number of failed requests.</span></span>|
|<span data-ttu-id="b3fad-248">throughput</span><span class="sxs-lookup"><span data-stu-id="b3fad-248">throughput</span></span>| <span data-ttu-id="b3fad-249">Taxa de transferência média desde o último log hello, medido em bytes por segundo.</span><span class="sxs-lookup"><span data-stu-id="b3fad-249">Average throughput since hello last log, measured in bytes per second.</span></span>|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> <span data-ttu-id="b3fad-250">Latência é calculada de tempo de saudação quando o primeiro byte de solicitação HTTP de Olá Olá é recebida toohello tempo quando o último byte de resposta HTTP de Olá Olá é enviado.</span><span class="sxs-lookup"><span data-stu-id="b3fad-250">Latency is calculated from hello time when hello first byte of hello HTTP request is received toohello time when hello last byte of hello HTTP response is sent.</span></span> <span data-ttu-id="b3fad-251">Sua saudação soma de Olá Application Gateway tempo de processamento mais hello toohello de custo de rede volta terminar, mais tempo Olá Olá back-end leva tooprocess Olá solicitação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-251">It's hello sum of hello Application Gateway processing time plus hello network cost toohello back end, plus hello time that hello back end takes tooprocess hello request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="b3fad-252">Log de firewall</span><span class="sxs-lookup"><span data-stu-id="b3fad-252">Firewall log</span></span>

<span data-ttu-id="b3fad-253">log de firewall de saudação é gerado apenas se você habilitou para cada gateway do aplicativo, conforme detalhado nas etapas anteriores de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-253">hello firewall log is generated only if you have enabled it for each application gateway, as detailed in hello preceding steps.</span></span> <span data-ttu-id="b3fad-254">Esse log também requer que firewall saudação do aplicativo web está configurado em um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b3fad-254">This log also requires that hello web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="b3fad-255">Olá dados são armazenados na conta de armazenamento Olá especificado quando você habilitou o log de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-255">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="b3fad-256">Olá seguintes dados é registrado:</span><span class="sxs-lookup"><span data-stu-id="b3fad-256">hello following data is logged:</span></span>


|<span data-ttu-id="b3fad-257">Valor</span><span class="sxs-lookup"><span data-stu-id="b3fad-257">Value</span></span>  |<span data-ttu-id="b3fad-258">Descrição</span><span class="sxs-lookup"><span data-stu-id="b3fad-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="b3fad-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="b3fad-259">instanceId</span></span>     | <span data-ttu-id="b3fad-260">Instância do Gateway de Aplicativo para a qual os dados de firewall estão sendo gerados.</span><span class="sxs-lookup"><span data-stu-id="b3fad-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="b3fad-261">Para um gateway de aplicativo de várias instâncias, há uma linha por instância.</span><span class="sxs-lookup"><span data-stu-id="b3fad-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="b3fad-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="b3fad-262">clientIp</span></span>     |   <span data-ttu-id="b3fad-263">IP de origem para a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-263">Originating IP for hello request.</span></span>      |
|<span data-ttu-id="b3fad-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="b3fad-264">clientPort</span></span>     |  <span data-ttu-id="b3fad-265">Porta de origem para solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-265">Originating port for hello request.</span></span>       |
|<span data-ttu-id="b3fad-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="b3fad-266">requestUri</span></span>     | <span data-ttu-id="b3fad-267">URL de solicitação recebida hello.</span><span class="sxs-lookup"><span data-stu-id="b3fad-267">URL of hello received request.</span></span>       |
|<span data-ttu-id="b3fad-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="b3fad-268">ruleSetType</span></span>     | <span data-ttu-id="b3fad-269">Tipo de conjunto de regras.</span><span class="sxs-lookup"><span data-stu-id="b3fad-269">Rule set type.</span></span> <span data-ttu-id="b3fad-270">valor disponível da saudação é OWASP.</span><span class="sxs-lookup"><span data-stu-id="b3fad-270">hello available value is OWASP.</span></span>        |
|<span data-ttu-id="b3fad-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="b3fad-271">ruleSetVersion</span></span>     | <span data-ttu-id="b3fad-272">Versão utilizada do conjunto de regras.</span><span class="sxs-lookup"><span data-stu-id="b3fad-272">Rule set version used.</span></span> <span data-ttu-id="b3fad-273">Os valores disponíveis são 2.2.9 e 3.0.</span><span class="sxs-lookup"><span data-stu-id="b3fad-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="b3fad-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="b3fad-274">ruleId</span></span>     | <span data-ttu-id="b3fad-275">ID da regra de saudação acionar o evento.</span><span class="sxs-lookup"><span data-stu-id="b3fad-275">Rule ID of hello triggering event.</span></span>        |
|<span data-ttu-id="b3fad-276">Message</span><span class="sxs-lookup"><span data-stu-id="b3fad-276">message</span></span>     | <span data-ttu-id="b3fad-277">Mensagem amigável para Olá acionar o evento.</span><span class="sxs-lookup"><span data-stu-id="b3fad-277">User-friendly message for hello triggering event.</span></span> <span data-ttu-id="b3fad-278">Mais detalhes são fornecidos na seção de detalhes de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-278">More details are provided in hello details section.</span></span>        |
|<span data-ttu-id="b3fad-279">ação</span><span class="sxs-lookup"><span data-stu-id="b3fad-279">action</span></span>     |  <span data-ttu-id="b3fad-280">Ação executada na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-280">Action taken on hello request.</span></span> <span data-ttu-id="b3fad-281">Os valores disponíveis são Bloqueada e Permitida.</span><span class="sxs-lookup"><span data-stu-id="b3fad-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="b3fad-282">site</span><span class="sxs-lookup"><span data-stu-id="b3fad-282">site</span></span>     | <span data-ttu-id="b3fad-283">Site para o qual Olá log foi gerado.</span><span class="sxs-lookup"><span data-stu-id="b3fad-283">Site for which hello log was generated.</span></span> <span data-ttu-id="b3fad-284">No momento, somente Global é listado porque as regras são globais.</span><span class="sxs-lookup"><span data-stu-id="b3fad-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="b3fad-285">detalhes</span><span class="sxs-lookup"><span data-stu-id="b3fad-285">details</span></span>     | <span data-ttu-id="b3fad-286">Detalhes da saudação acionar o evento.</span><span class="sxs-lookup"><span data-stu-id="b3fad-286">Details of hello triggering event.</span></span>        |
|<span data-ttu-id="b3fad-287">details.message</span><span class="sxs-lookup"><span data-stu-id="b3fad-287">details.message</span></span>     | <span data-ttu-id="b3fad-288">Descrição da regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-288">Description of hello rule.</span></span>        |
|<span data-ttu-id="b3fad-289">details.data</span><span class="sxs-lookup"><span data-stu-id="b3fad-289">details.data</span></span>     | <span data-ttu-id="b3fad-290">Dados específicos encontrados na solicitação regra Olá correspondentes.</span><span class="sxs-lookup"><span data-stu-id="b3fad-290">Specific data found in request that matched hello rule.</span></span>         |
|<span data-ttu-id="b3fad-291">details.file</span><span class="sxs-lookup"><span data-stu-id="b3fad-291">details.file</span></span>     | <span data-ttu-id="b3fad-292">Arquivo de configuração que continha a regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-292">Configuration file that contained hello rule.</span></span>        |
|<span data-ttu-id="b3fad-293">details.line</span><span class="sxs-lookup"><span data-stu-id="b3fad-293">details.line</span></span>     | <span data-ttu-id="b3fad-294">Número de linha no arquivo de configuração de saudação que disparou o evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-294">Line number in hello configuration file that triggered hello event.</span></span>       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a><span data-ttu-id="b3fad-295">Exibir e analisar o log de atividades de saudação</span><span class="sxs-lookup"><span data-stu-id="b3fad-295">View and analyze hello activity log</span></span>

<span data-ttu-id="b3fad-296">Você pode exibir e analisar dados de log de atividade usando qualquer um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="b3fad-296">You can view and analyze activity log data by using any of hello following methods:</span></span>

* <span data-ttu-id="b3fad-297">**Ferramentas do Azure**: recuperar informações do log de atividades de saudação por meio do PowerShell do Azure, Olá CLI do Azure, Olá API REST do Azure, ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3fad-297">**Azure tools**: Retrieve information from hello activity log through Azure PowerShell, hello Azure CLI, hello Azure REST API, or hello Azure portal.</span></span> <span data-ttu-id="b3fad-298">Instruções passo a passo para cada método são detalhadas no hello [operações de atividade com o Gerenciador de recursos](../azure-resource-manager/resource-group-audit.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b3fad-298">Step-by-step instructions for each method are detailed in hello [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="b3fad-299">**Power BI**: se ainda não tiver uma conta do [Power BI](https://powerbi.microsoft.com/pricing), experimente uma gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="b3fad-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="b3fad-300">Usando Olá [conteúdo de Logs de atividades do Azure pack para o Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), você pode analisar seus dados com painéis pré-configurados que você pode usar como está ou personalizar.</span><span class="sxs-lookup"><span data-stu-id="b3fad-300">By using hello [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a><span data-ttu-id="b3fad-301">Exibir e analisar Olá acesso, desempenho e logs de firewall</span><span class="sxs-lookup"><span data-stu-id="b3fad-301">View and analyze hello access, performance, and firewall logs</span></span>

<span data-ttu-id="b3fad-302">Azure [análise de Log](../log-analytics/log-analytics-azure-networking-analytics.md) pode coletar arquivos de log de eventos e contadores Olá de sua conta de armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="b3fad-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect hello counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="b3fad-303">Ele inclui visualizações e tooanalyze de recursos avançados de pesquisa seus logs.</span><span class="sxs-lookup"><span data-stu-id="b3fad-303">It includes visualizations and powerful search capabilities tooanalyze your logs.</span></span>

<span data-ttu-id="b3fad-304">Também pode conectar-se a conta de armazenamento tooyour e recuperar entradas de log Olá JSON para logs de acesso e o desempenho.</span><span class="sxs-lookup"><span data-stu-id="b3fad-304">You can also connect tooyour storage account and retrieve hello JSON log entries for access and performance logs.</span></span> <span data-ttu-id="b3fad-305">Depois de baixar os arquivos JSON hello, você pode convertê-los tooCSV e exibi-los no Excel, Power BI ou qualquer outra ferramenta de visualização de dados.</span><span class="sxs-lookup"><span data-stu-id="b3fad-305">After you download hello JSON files, you can convert them tooCSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="b3fad-306">Se você estiver familiarizado com os conceitos básicos de alterar valores de constantes e variáveis em c# e o Visual Studio, você pode usar o hello [ferramentas de conversor de log](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponíveis no GitHub.</span><span class="sxs-lookup"><span data-stu-id="b3fad-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="b3fad-307">Métricas</span><span class="sxs-lookup"><span data-stu-id="b3fad-307">Metrics</span></span>

<span data-ttu-id="b3fad-308">Métricas são um recurso para certos recursos do Azure, onde você pode exibir os contadores de desempenho no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-308">Metrics are a feature for certain Azure resources where you can view performance counters in hello portal.</span></span> <span data-ttu-id="b3fad-309">Para o Gateway de Aplicativo, uma única métrica está disponível no momento.</span><span class="sxs-lookup"><span data-stu-id="b3fad-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="b3fad-310">Essa métrica é a taxa de transferência, e você pode vê-lo no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-310">This metric is throughput, and you can see it in hello portal.</span></span> <span data-ttu-id="b3fad-311">Procurar tooan gateway de aplicativo e clique em **métricas**.</span><span class="sxs-lookup"><span data-stu-id="b3fad-311">Browse tooan application gateway and click **Metrics**.</span></span> <span data-ttu-id="b3fad-312">valores de saudação tooview, selecione taxa de transferência em Olá **métricas disponíveis** seção.</span><span class="sxs-lookup"><span data-stu-id="b3fad-312">tooview hello values, select throughput in hello **Available metrics** section.</span></span> <span data-ttu-id="b3fad-313">Olá a imagem a seguir, você verá um exemplo com filtros de saudação que você pode usar dados de saudação toodisplay em intervalos de tempo diferentes.</span><span class="sxs-lookup"><span data-stu-id="b3fad-313">In hello following image, you can see an example with hello filters that you can use toodisplay hello data in different time ranges.</span></span>

![Exibição da métrica com filtros][5]

<span data-ttu-id="b3fad-315">toosee uma lista atual de métricas, consulte [suporte para métricas com o Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b3fad-315">toosee a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="b3fad-316">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="b3fad-316">Alert rules</span></span>

<span data-ttu-id="b3fad-317">Você pode iniciar as regras de alerta com base nas métricas de um recurso.</span><span class="sxs-lookup"><span data-stu-id="b3fad-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="b3fad-318">Por exemplo, um alerta pode chamar um webhook ou um administrador de email se for de taxa de transferência de saudação do gateway de aplicativo hello acima, abaixo ou em um limite por um período especificado.</span><span class="sxs-lookup"><span data-stu-id="b3fad-318">For example, an alert can call a webhook or email an administrator if hello throughput of hello application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="b3fad-319">saudação de exemplo a seguir orienta você na criação de uma regra de alerta que envia um administrador de tooan email depois de violações de taxa de transferência um limite:</span><span class="sxs-lookup"><span data-stu-id="b3fad-319">hello following example walks you through creating an alert rule that sends an email tooan administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="b3fad-320">Clique em **adicionar alerta métrica** tooopen Olá **Adicionar regra** folha.</span><span class="sxs-lookup"><span data-stu-id="b3fad-320">Click **Add metric alert** tooopen hello **Add rule** blade.</span></span> <span data-ttu-id="b3fad-321">Você também pode acessar esta folha da folha de métricas de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-321">You can also reach this blade from hello metrics blade.</span></span>

   ![Botão “Adicionar alerta de métrica”][6]

2. <span data-ttu-id="b3fad-323">Em Olá **Adicionar regra** folha, preencha o nome hello, condição e notificar seções e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b3fad-323">On hello **Add rule** blade, fill out hello name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="b3fad-324">Em Olá **condição** seletor, selecione um dos valores de saudação quatro: **maior**, **maior que ou igual**, **menor**, ou  **Menor ou igual a**.</span><span class="sxs-lookup"><span data-stu-id="b3fad-324">In hello **Condition** selector, select one of hello four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="b3fad-325">Em Olá **período** seletor, selecione um período de 5 minutos too6 horas.</span><span class="sxs-lookup"><span data-stu-id="b3fad-325">In hello **Period** selector, select a period from 5 minutes too6 hours.</span></span>

   * <span data-ttu-id="b3fad-326">Se você selecionar **proprietários, Contribuidores e leitores de Email**, email Olá pode ser dinâmica com base em usuários de saudação que têm acesso toothat recursos.</span><span class="sxs-lookup"><span data-stu-id="b3fad-326">If you select **Email owners, contributors, and readers**, hello email can be dynamic based on hello users who have access toothat resource.</span></span> <span data-ttu-id="b3fad-327">Caso contrário, você pode fornecer uma lista separada por vírgulas de usuários em Olá **email(s) administrador adicional** caixa.</span><span class="sxs-lookup"><span data-stu-id="b3fad-327">Otherwise, you can provide a comma-separated list of users in hello **Additional administrator email(s)** box.</span></span>

   ![Folha Adicionar regra][7]

<span data-ttu-id="b3fad-329">Se Olá limite for ultrapassado, chega um email que é semelhante toohello um no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3fad-329">If hello threshold is breached, an email that's similar toohello one in hello following image arrives:</span></span>

![Email para o limite violado][8]

<span data-ttu-id="b3fad-331">Uma lista de alertas é exibida após a criação de um alerta de métrica.</span><span class="sxs-lookup"><span data-stu-id="b3fad-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="b3fad-332">Ele fornece uma visão geral de todas as regras de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3fad-332">It provides an overview of all hello alert rules.</span></span>

![Lista de alertas e regras][9]

<span data-ttu-id="b3fad-334">toolearn mais informações sobre notificações de alerta, consulte [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="b3fad-334">toolearn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="b3fad-335">toounderstand mais sobre webhooks e como usá-los com alertas, visite [configurar um webhook em um alerta de métrica do Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="b3fad-335">toounderstand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3fad-336">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b3fad-336">Next steps</span></span>

* <span data-ttu-id="b3fad-337">Visualize o contador e os logs de eventos com o [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="b3fad-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="b3fad-338">Postagem no blog [Visualize your Azure Activity Log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Visualizar o log de atividades do Azure com o Power BI).</span><span class="sxs-lookup"><span data-stu-id="b3fad-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="b3fad-339">Postagem no blog [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Exibir e analisar os Logs de Atividades do Azure no Power BI e muito mais).</span><span class="sxs-lookup"><span data-stu-id="b3fad-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
