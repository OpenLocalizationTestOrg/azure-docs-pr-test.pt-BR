---
title: "Monitorar logs de acesso, logs de desempenho, integridade do back-end e métricas do Gateway de Aplicativo | Microsoft Docs"
description: Saiba como habilitar e gerenciar logs de acesso e de desempenho do Gateway de Aplicativo
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
ms.openlocfilehash: 12c252340b82aba5ee69b12db83353750782e7c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="3204b-103">Integridade do back-end, logs de diagnóstico e métricas do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="3204b-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="3204b-104">Com o Gateway de Aplicativo do Azure, você pode monitorar os recursos das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="3204b-104">By using Azure Application Gateway, you can monitor resources in the following ways:</span></span>

* <span data-ttu-id="3204b-105">[Integridade do back-end](#back-end-health): o Gateway de Aplicativo fornece a capacidade de monitorar a integridade dos servidores nos pools de back-end por meio do portal do Azure e do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3204b-105">[Back-end health](#back-end-health): Application Gateway provides the capability to monitor the health of the servers in the back-end pools through the Azure portal and through PowerShell.</span></span> <span data-ttu-id="3204b-106">Também é possível encontrar a integridade dos pools de back-end por meio dos logs de diagnóstico de desempenho.</span><span class="sxs-lookup"><span data-stu-id="3204b-106">You can also find the health of the back-end pools through the performance diagnostic logs.</span></span>

* <span data-ttu-id="3204b-107">[Logs](#diagnostic-logs): os logs permitem que o desempenho, o acesso e outros dados sejam salvos ou consumidos de um recurso para fins de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="3204b-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data to be saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="3204b-108">[Métricas](#metrics): atualmente, o Gateway de Aplicativo tem uma métrica.</span><span class="sxs-lookup"><span data-stu-id="3204b-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="3204b-109">Essa métrica mede a vazão de dados do gateway de aplicativo em bytes por segundo.</span><span class="sxs-lookup"><span data-stu-id="3204b-109">This metric measures the throughput of the application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="3204b-110">Integridade do back-end</span><span class="sxs-lookup"><span data-stu-id="3204b-110">Back-end health</span></span>

<span data-ttu-id="3204b-111">O Gateway de Aplicativo fornece a capacidade de monitorar a integridade de membros individuais dos pools de back-end por meio do portal, do PowerShell e da CLI (interface de linha de comando).</span><span class="sxs-lookup"><span data-stu-id="3204b-111">Application Gateway provides the capability to monitor the health of individual members of the back-end pools through the portal, PowerShell, and the command-line interface (CLI).</span></span> <span data-ttu-id="3204b-112">Também é possível encontrar um resumo de integridade agregado dos pools de back-end por meio dos logs de diagnóstico de desempenho.</span><span class="sxs-lookup"><span data-stu-id="3204b-112">You can also find an aggregated health summary of back-end pools through the performance diagnostic logs.</span></span> 

<span data-ttu-id="3204b-113">O relatório de integridade do back-end reflete o resultado da investigação de integridade do Gateway de Aplicativo nas instâncias de back-end.</span><span class="sxs-lookup"><span data-stu-id="3204b-113">The back-end health report reflects the output of the Application Gateway health probe to the back-end instances.</span></span> <span data-ttu-id="3204b-114">Quando a investigação é bem-sucedida e o back-end pode receber tráfego, ele é considerado íntegro.</span><span class="sxs-lookup"><span data-stu-id="3204b-114">When probing is successful and the back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="3204b-115">Caso contrário, ele é considerado não íntegro.</span><span class="sxs-lookup"><span data-stu-id="3204b-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3204b-116">Se houver um NSG (grupo de segurança de rede) em uma sub-rede do Gateway do Aplicativo, abra os intervalos de porta 65503 a 65534 na sub-rede do Gateway de Aplicativo para o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="3204b-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on the Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="3204b-117">Essas portas são necessárias para que a API de integridade do back-end funcione.</span><span class="sxs-lookup"><span data-stu-id="3204b-117">These ports are required for the back-end health API to work.</span></span>


### <a name="view-back-end-health-through-the-portal"></a><span data-ttu-id="3204b-118">Exibir a integridade do back-end por meio do portal</span><span class="sxs-lookup"><span data-stu-id="3204b-118">View back-end health through the portal</span></span>

<span data-ttu-id="3204b-119">No portal, a integridade do back-end é fornecida automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3204b-119">In the portal, back-end health is provided automatically.</span></span> <span data-ttu-id="3204b-120">Em um gateway de aplicativo existente, selecione **Monitoramento** > **Integridade do back-end**.</span><span class="sxs-lookup"><span data-stu-id="3204b-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="3204b-121">Cada membro no pool de back-end é listado nesta página (seja uma NIC, um IP ou um FQDN).</span><span class="sxs-lookup"><span data-stu-id="3204b-121">Each member in the back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="3204b-122">São mostrados o nome do pool de back-end, a porta, as configurações de HTTP do back-end e o status de integridade.</span><span class="sxs-lookup"><span data-stu-id="3204b-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="3204b-123">Os valores válidos para o status de integridade são **Íntegro**, **Não íntegro** e **Desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="3204b-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="3204b-124">Se o status **Desconhecido** de integridade do back-end for exibido, verifique se o acesso ao back-end não está bloqueado por uma regra do NSG, uma UDR (rota definida pelo usuário) ou um DNS personalizado na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3204b-124">If you see a back-end health status of **Unknown**, ensure that access to the back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in the virtual network.</span></span>

![Integridade do back-end][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="3204b-126">Exibir a integridade do back-end por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="3204b-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="3204b-127">O seguinte código do PowerShell mostra como exibir a integridade do back-end usando o cmdlet `Get-AzureRmApplicationGatewayBackendHealth`:</span><span class="sxs-lookup"><span data-stu-id="3204b-127">The following PowerShell code shows how to view back-end health by using the `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="3204b-128">Exibir a integridade do back-end por meio da CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="3204b-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="3204b-129">Resultados</span><span class="sxs-lookup"><span data-stu-id="3204b-129">Results</span></span>

<span data-ttu-id="3204b-130">O seguinte trecho mostra um exemplo da resposta:</span><span class="sxs-lookup"><span data-stu-id="3204b-130">The following snippet shows an example of the response:</span></span>

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

## <span data-ttu-id="3204b-131"><a name="diagnostic-logging"></a>Logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="3204b-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="3204b-132">Você pode usar tipos diferentes de logs no Azure para gerenciar e solucionar problemas de gateways de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3204b-132">You can use different types of logs in Azure to manage and troubleshoot application gateways.</span></span> <span data-ttu-id="3204b-133">Você pode acessar alguns desses logs por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="3204b-133">You can access some of these logs through the portal.</span></span> <span data-ttu-id="3204b-134">Todos os logs podem ser extraídos de um Armazenamento de blobs do Azure e exibidos em diferentes ferramentas, como [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel e Power BI.</span><span class="sxs-lookup"><span data-stu-id="3204b-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="3204b-135">Saiba mais sobre os tipos diferentes de logs na lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="3204b-135">You can learn more about the different types of logs from the following list:</span></span>

* <span data-ttu-id="3204b-136">**Log de atividades**: você pode usar os [logs de atividades do Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conhecidos como logs operacionais e logs de auditoria) para exibir todas as operações que estão sendo enviadas à sua assinatura do Azure, bem como seu status.</span><span class="sxs-lookup"><span data-stu-id="3204b-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) to view all operations that are submitted to your Azure subscription, and their status.</span></span> <span data-ttu-id="3204b-137">As entradas do log de atividades são coletadas por padrão e podem ser exibidas no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3204b-137">Activity log entries are collected by default, and you can view them in the Azure portal.</span></span>
* <span data-ttu-id="3204b-138">**Log de acesso**: você pode usar esse log para exibir os padrões de acesso do Gateway de Aplicativo e analisar informações importantes, incluindo o IP do chamador, a URL solicitada, a latência de resposta, o código de retorno e os bytes de entrada e saída. Um log de acesso é coletado a cada 300 segundos.</span><span class="sxs-lookup"><span data-stu-id="3204b-138">**Access log**: You can use this log to view Application Gateway access patterns and analyze important information, including the caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="3204b-139">Esse log contém um registro por instância do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3204b-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="3204b-140">A instância do Gateway de Aplicativo pode ser identificada pela propriedade instanceId.</span><span class="sxs-lookup"><span data-stu-id="3204b-140">The Application Gateway instance can be identified by the instanceId property.</span></span>
* <span data-ttu-id="3204b-141">**Log de desempenho**: você pode usar esse log para exibir o desempenho das instâncias do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3204b-141">**Performance log**: You can use this log to view how Application Gateway instances are performing.</span></span> <span data-ttu-id="3204b-142">Esse log captura informações de desempenho de cada instância, incluindo o total de solicitações atendidas, a vazão de dados em bytes, o total de solicitações atendidas, a contagem de solicitações com falha e a contagem de instâncias de back-end íntegras ou não íntegras.</span><span class="sxs-lookup"><span data-stu-id="3204b-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="3204b-143">Um log de desempenho é coletado a cada 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="3204b-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="3204b-144">**Logs de firewall**: use esse log para exibir as solicitações registradas por meio do modo de detecção ou prevenção de um gateway de aplicativo configurado com o firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3204b-144">**Firewall log**: You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with the web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="3204b-145">Os logs estão disponíveis apenas para os recursos implantados no modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3204b-145">Logs are available only for resources deployed in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="3204b-146">Você não pode usar logs para recursos do modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="3204b-146">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="3204b-147">Para obter um melhor entendimento dos dois modelos, consulte o artigo [Noções básicas sobre a implantação do Resource Manager e a implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3204b-147">For a better understanding of the two models, see the [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="3204b-148">Você tem três opções para armazenar os logs:</span><span class="sxs-lookup"><span data-stu-id="3204b-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="3204b-149">**Conta de armazenamento**: as contas de armazenamento são mais adequadas para os logs quando eles são armazenados por mais tempo e examinados quando necessário.</span><span class="sxs-lookup"><span data-stu-id="3204b-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="3204b-150">**Hubs de eventos**: os hubs de eventos são uma ótima opção para integração a outras ferramentas SEIM (informações de segurança e gerenciamento de evento) para receber alertas sobre os recursos.</span><span class="sxs-lookup"><span data-stu-id="3204b-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools to get alerts on your resources.</span></span>
* <span data-ttu-id="3204b-151">**Log Analytics**: o Log Analytics é mais adequado para o monitoramento geral em tempo real do aplicativo ou para a observação de tendências.</span><span class="sxs-lookup"><span data-stu-id="3204b-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="3204b-152">Habilitar o log por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="3204b-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="3204b-153">O log de atividade é habilitado automaticamente para todos os recursos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3204b-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="3204b-154">Você deve habilitar o log de acesso e de desempenho para começar a coletar os dados disponíveis por meio desses logs.</span><span class="sxs-lookup"><span data-stu-id="3204b-154">You must enable access and performance logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="3204b-155">Para habilitar o log, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3204b-155">To enable logging, use the following steps:</span></span>

1. <span data-ttu-id="3204b-156">Anote a ID do recurso da conta de armazenamento, na qual os dados de log são armazenados.</span><span class="sxs-lookup"><span data-stu-id="3204b-156">Note your storage account's resource ID, where the log data is stored.</span></span> <span data-ttu-id="3204b-157">Esse valor tem o formato /subscriptions/\<subscriptionId\>/resourceGroups/\<grupo de recursos name\>/providers/Microsoft.Storage/storageAccounts/\<nome da conta de armazenamento\>.</span><span class="sxs-lookup"><span data-stu-id="3204b-157">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="3204b-158">Use qualquer conta de armazenamento em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="3204b-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="3204b-159">Use o portal do Azure para encontrar essas informações.</span><span class="sxs-lookup"><span data-stu-id="3204b-159">You can use the Azure portal to find this information.</span></span>

    ![Portal: ID do recurso da conta de armazenamento](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="3204b-161">Anote a ID do Recurso do gateway de aplicativo para o qual o log está habilitado.</span><span class="sxs-lookup"><span data-stu-id="3204b-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="3204b-162">Esse valor tem o formato /subscriptions/\<subscriptionId\>/resourceGroups/\<grupo de recursos name\>/providers/Microsoft.Network/applicationGateways/\<nome do gateway de aplicativo\>.</span><span class="sxs-lookup"><span data-stu-id="3204b-162">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="3204b-163">Use o portal para encontrar essas informações.</span><span class="sxs-lookup"><span data-stu-id="3204b-163">You can use the portal to find this information.</span></span>

    ![Portal: ID do recurso do gateway de aplicativo](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="3204b-165">Habilite o log de diagnóstico usando o seguinte cmdlet do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3204b-165">Enable diagnostic logging by using the following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="3204b-166">Os logs de atividades não exigem uma conta de armazenamento separada.</span><span class="sxs-lookup"><span data-stu-id="3204b-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="3204b-167">O uso do armazenamento para logs de acesso e de desempenho gera encargos de serviço.</span><span class="sxs-lookup"><span data-stu-id="3204b-167">The use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-the-azure-portal"></a><span data-ttu-id="3204b-168">Habilitar o log por meio do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3204b-168">Enable logging through the Azure portal</span></span>

1. <span data-ttu-id="3204b-169">No portal do Azure, encontre o recurso e clique em **Logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="3204b-169">In the Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="3204b-170">Para o Gateway de Aplicativo, três logs estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="3204b-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="3204b-171">Log de acesso</span><span class="sxs-lookup"><span data-stu-id="3204b-171">Access log</span></span>
   * <span data-ttu-id="3204b-172">Log de desempenho</span><span class="sxs-lookup"><span data-stu-id="3204b-172">Performance log</span></span>
   * <span data-ttu-id="3204b-173">Log de firewall</span><span class="sxs-lookup"><span data-stu-id="3204b-173">Firewall log</span></span>

2. <span data-ttu-id="3204b-174">Para iniciar a coleta de dados., clique em **Ativar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="3204b-174">To start collecting data, click **Turn on diagnostics**.</span></span>

   ![Ativando o diagnóstico][1]

3. <span data-ttu-id="3204b-176">A folha **Configurações de diagnóstico** fornece as configurações dos logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="3204b-176">The **Diagnostics settings** blade provides the settings for the diagnostic logs.</span></span> <span data-ttu-id="3204b-177">Neste exemplo, o Log Analytics armazena os logs.</span><span class="sxs-lookup"><span data-stu-id="3204b-177">In this example, Log Analytics stores the logs.</span></span> <span data-ttu-id="3204b-178">Clique em **Configurar** em **Log Analytics** para configurar seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3204b-178">Click **Configure** under **Log Analytics** to configure your workspace.</span></span> <span data-ttu-id="3204b-179">Você também pode usar os hubs de eventos e uma conta de armazenamento para salvar os logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="3204b-179">You can also use event hubs and a storage account to save the diagnostic logs.</span></span>

   ![Iniciando o processo de configuração][2]

4. <span data-ttu-id="3204b-181">Escolha um espaço de trabalho do OMS (Operations Management Suite) existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="3204b-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="3204b-182">Este exemplo usa um existente.</span><span class="sxs-lookup"><span data-stu-id="3204b-182">This example uses an existing one.</span></span>

   ![Opções de espaços de trabalho do OMS][3]

5. <span data-ttu-id="3204b-184">Confirme as configurações e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3204b-184">Confirm the settings and click **Save**.</span></span>

   ![Folha Configurações de diagnóstico com seleções][4]

### <a name="activity-log"></a><span data-ttu-id="3204b-186">Log de atividades</span><span class="sxs-lookup"><span data-stu-id="3204b-186">Activity log</span></span>

<span data-ttu-id="3204b-187">O Azure gera o log de atividades por padrão.</span><span class="sxs-lookup"><span data-stu-id="3204b-187">Azure generates the activity log by default.</span></span> <span data-ttu-id="3204b-188">Os logs são preservados por 90 dias no armazenamento de logs de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3204b-188">The logs are preserved for 90 days in the Azure event logs store.</span></span> <span data-ttu-id="3204b-189">Saiba mais sobre esses logs lendo o artigo [Exibir eventos e o log de atividades](../monitoring-and-diagnostics/insights-debugging-with-events.md).</span><span class="sxs-lookup"><span data-stu-id="3204b-189">Learn more about these logs by reading the [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="3204b-190">Log de acesso</span><span class="sxs-lookup"><span data-stu-id="3204b-190">Access log</span></span>

<span data-ttu-id="3204b-191">O log de acesso é gerado apenas se você o habilitou em cada instância do Gateway de Aplicativo, conforme detalhado nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="3204b-191">The access log is generated only if you've enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="3204b-192">Os dados são armazenados na conta de armazenamento especificada quando o log foi habilitado.</span><span class="sxs-lookup"><span data-stu-id="3204b-192">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="3204b-193">Cada acesso do Gateway de Aplicativo é registrado no formato JSON, conforme mostrado no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="3204b-193">Each access of Application Gateway is logged in JSON format, as shown in the following example:</span></span>


|<span data-ttu-id="3204b-194">Valor</span><span class="sxs-lookup"><span data-stu-id="3204b-194">Value</span></span>  |<span data-ttu-id="3204b-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="3204b-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="3204b-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="3204b-196">instanceId</span></span>     | <span data-ttu-id="3204b-197">Instância do Gateway de Aplicativo que atendeu à solicitação.</span><span class="sxs-lookup"><span data-stu-id="3204b-197">Application Gateway instance that served the request.</span></span>        |
|<span data-ttu-id="3204b-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="3204b-198">clientIP</span></span>     | <span data-ttu-id="3204b-199">IP de origem da solicitação.</span><span class="sxs-lookup"><span data-stu-id="3204b-199">Originating IP for the request.</span></span>        |
|<span data-ttu-id="3204b-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="3204b-200">clientPort</span></span>     | <span data-ttu-id="3204b-201">Porta de origem da solicitação.</span><span class="sxs-lookup"><span data-stu-id="3204b-201">Originating port for the request.</span></span>       |
|<span data-ttu-id="3204b-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="3204b-202">httpMethod</span></span>     | <span data-ttu-id="3204b-203">Método HTTP usado pela solicitação.</span><span class="sxs-lookup"><span data-stu-id="3204b-203">HTTP method used by the request.</span></span>       |
|<span data-ttu-id="3204b-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="3204b-204">requestUri</span></span>     | <span data-ttu-id="3204b-205">URI da solicitação recebida.</span><span class="sxs-lookup"><span data-stu-id="3204b-205">URI of the received request.</span></span>        |
|<span data-ttu-id="3204b-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="3204b-206">RequestQuery</span></span>     | <span data-ttu-id="3204b-207">**Server-Routed**: instância do pool de back-end que recebeu a solicitação.</span><span class="sxs-lookup"><span data-stu-id="3204b-207">**Server-Routed**: Back-end pool instance that was sent the request.</span></span> </br> <span data-ttu-id="3204b-208">**X-AzureApplicationGateway-LOG-ID**: ID de Correlação usada para a solicitação.</span><span class="sxs-lookup"><span data-stu-id="3204b-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for the request.</span></span> <span data-ttu-id="3204b-209">Ela pode ser usada para solucionar problemas de tráfego nos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="3204b-209">It can be used to troubleshoot traffic issues on the back-end servers.</span></span> </br><span data-ttu-id="3204b-210">**SERVER-STATUS**: código de resposta HTTP que o Gateway de Aplicativo recebeu do back-end.</span><span class="sxs-lookup"><span data-stu-id="3204b-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from the back end.</span></span>       |
|<span data-ttu-id="3204b-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="3204b-211">UserAgent</span></span>     | <span data-ttu-id="3204b-212">Agente do usuário do cabeçalho da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="3204b-212">User agent from the HTTP request header.</span></span>        |
|<span data-ttu-id="3204b-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="3204b-213">httpStatus</span></span>     | <span data-ttu-id="3204b-214">Código de status HTTP retornado ao cliente do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3204b-214">HTTP status code returned to the client from Application Gateway.</span></span>       |
|<span data-ttu-id="3204b-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="3204b-215">httpVersion</span></span>     | <span data-ttu-id="3204b-216">Versão HTTP da solicitação.</span><span class="sxs-lookup"><span data-stu-id="3204b-216">HTTP version of the request.</span></span>        |
|<span data-ttu-id="3204b-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="3204b-217">receivedBytes</span></span>     | <span data-ttu-id="3204b-218">Tamanho do pacote recebido, em bytes.</span><span class="sxs-lookup"><span data-stu-id="3204b-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="3204b-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="3204b-219">sentBytes</span></span>| <span data-ttu-id="3204b-220">Tamanho do pacote enviado, em bytes.</span><span class="sxs-lookup"><span data-stu-id="3204b-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="3204b-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="3204b-221">timeTaken</span></span>| <span data-ttu-id="3204b-222">Duração (em milissegundos) necessária para que uma solicitação seja processada e sua resposta seja enviada.</span><span class="sxs-lookup"><span data-stu-id="3204b-222">Length of time (in milliseconds) that it takes for a request to be processed and its response to be sent.</span></span> <span data-ttu-id="3204b-223">Isso é calculado como o intervalo a partir da hora em que o Gateway de Aplicativo recebe o primeiro byte de uma solicitação HTTP até a hora em que a operação de envio de resposta é concluída.</span><span class="sxs-lookup"><span data-stu-id="3204b-223">This is calculated as the interval from the time when Application Gateway receives the first byte of an HTTP request to the time when the response send operation finishes.</span></span> <span data-ttu-id="3204b-224">É importante observar que o campo Time-Taken geralmente inclui a hora em que os pacotes de solicitação e resposta são transmitidos pela rede.</span><span class="sxs-lookup"><span data-stu-id="3204b-224">It's important to note that the Time-Taken field usually includes the time that the request and response packets are traveling over the network.</span></span> |
|<span data-ttu-id="3204b-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="3204b-225">sslEnabled</span></span>| <span data-ttu-id="3204b-226">Indica se a comunicação com os pools de back-end usou o SSL.</span><span class="sxs-lookup"><span data-stu-id="3204b-226">Whether communication to the back-end pools used SSL.</span></span> <span data-ttu-id="3204b-227">Os valores válidos são ativado e desativado.</span><span class="sxs-lookup"><span data-stu-id="3204b-227">Valid values are on and off.</span></span>|
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

### <a name="performance-log"></a><span data-ttu-id="3204b-228">Log de desempenho</span><span class="sxs-lookup"><span data-stu-id="3204b-228">Performance log</span></span>

<span data-ttu-id="3204b-229">O log de desempenho é gerado apenas se você o habilitou em cada instância do Gateway de Aplicativo, conforme detalhado nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="3204b-229">The performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="3204b-230">Os dados são armazenados na conta de armazenamento especificada quando o log foi habilitado.</span><span class="sxs-lookup"><span data-stu-id="3204b-230">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="3204b-231">Os dados do log de desempenho são gerados em intervalos de 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="3204b-231">The performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="3204b-232">Os seguintes dados são registrados em log:</span><span class="sxs-lookup"><span data-stu-id="3204b-232">The following data is logged:</span></span>


|<span data-ttu-id="3204b-233">Valor</span><span class="sxs-lookup"><span data-stu-id="3204b-233">Value</span></span>  |<span data-ttu-id="3204b-234">Descrição</span><span class="sxs-lookup"><span data-stu-id="3204b-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="3204b-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="3204b-235">instanceId</span></span>     |  <span data-ttu-id="3204b-236">Instância do Gateway de Aplicativo para a qual os dados de desempenho estão sendo gerados.</span><span class="sxs-lookup"><span data-stu-id="3204b-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="3204b-237">Para um gateway de aplicativo de várias instâncias, há uma linha por instância.</span><span class="sxs-lookup"><span data-stu-id="3204b-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="3204b-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="3204b-238">healthyHostCount</span></span>     | <span data-ttu-id="3204b-239">Número de hosts íntegros no pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="3204b-239">Number of healthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="3204b-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="3204b-240">unHealthyHostCount</span></span>     | <span data-ttu-id="3204b-241">Número de hosts não íntegros no pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="3204b-241">Number of unhealthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="3204b-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="3204b-242">requestCount</span></span>     | <span data-ttu-id="3204b-243">Número de solicitações atendidas.</span><span class="sxs-lookup"><span data-stu-id="3204b-243">Number of requests served.</span></span>        |
|<span data-ttu-id="3204b-244">latency</span><span class="sxs-lookup"><span data-stu-id="3204b-244">latency</span></span> | <span data-ttu-id="3204b-245">Latência (em milissegundos) de solicitações da instância para o back-end que atende às solicitações.</span><span class="sxs-lookup"><span data-stu-id="3204b-245">Latency (in milliseconds) of requests from the instance to the back end that serves the requests.</span></span> |
|<span data-ttu-id="3204b-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="3204b-246">failedRequestCount</span></span>| <span data-ttu-id="3204b-247">Número de solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="3204b-247">Number of failed requests.</span></span>|
|<span data-ttu-id="3204b-248">throughput</span><span class="sxs-lookup"><span data-stu-id="3204b-248">throughput</span></span>| <span data-ttu-id="3204b-249">Vazão de dados média desde o último log, medida em bytes por segundo.</span><span class="sxs-lookup"><span data-stu-id="3204b-249">Average throughput since the last log, measured in bytes per second.</span></span>|

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
> <span data-ttu-id="3204b-250">A latência é calculada a partir da hora em que o primeiro byte da solicitação HTTP é recebido até a hora em que o último byte da resposta HTTP é enviado.</span><span class="sxs-lookup"><span data-stu-id="3204b-250">Latency is calculated from the time when the first byte of the HTTP request is received to the time when the last byte of the HTTP response is sent.</span></span> <span data-ttu-id="3204b-251">É a soma do tempo de processamento do Gateway de Aplicativo e do custo de rede para o back-end, mais o tempo que o back-end leva para processar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="3204b-251">It's the sum of the Application Gateway processing time plus the network cost to the back end, plus the time that the back end takes to process the request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="3204b-252">Log de firewall</span><span class="sxs-lookup"><span data-stu-id="3204b-252">Firewall log</span></span>

<span data-ttu-id="3204b-253">O log de firewall é gerado apenas se você o habilitou em cada gateway de aplicativo, conforme detalhado nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="3204b-253">The firewall log is generated only if you have enabled it for each application gateway, as detailed in the preceding steps.</span></span> <span data-ttu-id="3204b-254">Esse log também exige a configuração de um firewall de aplicativo Web em um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3204b-254">This log also requires that the web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="3204b-255">Os dados são armazenados na conta de armazenamento especificada quando o log foi habilitado.</span><span class="sxs-lookup"><span data-stu-id="3204b-255">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="3204b-256">Os seguintes dados são registrados em log:</span><span class="sxs-lookup"><span data-stu-id="3204b-256">The following data is logged:</span></span>


|<span data-ttu-id="3204b-257">Valor</span><span class="sxs-lookup"><span data-stu-id="3204b-257">Value</span></span>  |<span data-ttu-id="3204b-258">Descrição</span><span class="sxs-lookup"><span data-stu-id="3204b-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="3204b-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="3204b-259">instanceId</span></span>     | <span data-ttu-id="3204b-260">Instância do Gateway de Aplicativo para a qual os dados de firewall estão sendo gerados.</span><span class="sxs-lookup"><span data-stu-id="3204b-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="3204b-261">Para um gateway de aplicativo de várias instâncias, há uma linha por instância.</span><span class="sxs-lookup"><span data-stu-id="3204b-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="3204b-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="3204b-262">clientIp</span></span>     |   <span data-ttu-id="3204b-263">IP de origem da solicitação.</span><span class="sxs-lookup"><span data-stu-id="3204b-263">Originating IP for the request.</span></span>      |
|<span data-ttu-id="3204b-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="3204b-264">clientPort</span></span>     |  <span data-ttu-id="3204b-265">Porta de origem da solicitação.</span><span class="sxs-lookup"><span data-stu-id="3204b-265">Originating port for the request.</span></span>       |
|<span data-ttu-id="3204b-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="3204b-266">requestUri</span></span>     | <span data-ttu-id="3204b-267">URL da solicitação recebida.</span><span class="sxs-lookup"><span data-stu-id="3204b-267">URL of the received request.</span></span>       |
|<span data-ttu-id="3204b-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="3204b-268">ruleSetType</span></span>     | <span data-ttu-id="3204b-269">Tipo de conjunto de regras.</span><span class="sxs-lookup"><span data-stu-id="3204b-269">Rule set type.</span></span> <span data-ttu-id="3204b-270">O valor disponível é OWASP.</span><span class="sxs-lookup"><span data-stu-id="3204b-270">The available value is OWASP.</span></span>        |
|<span data-ttu-id="3204b-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="3204b-271">ruleSetVersion</span></span>     | <span data-ttu-id="3204b-272">Versão utilizada do conjunto de regras.</span><span class="sxs-lookup"><span data-stu-id="3204b-272">Rule set version used.</span></span> <span data-ttu-id="3204b-273">Os valores disponíveis são 2.2.9 e 3.0.</span><span class="sxs-lookup"><span data-stu-id="3204b-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="3204b-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="3204b-274">ruleId</span></span>     | <span data-ttu-id="3204b-275">ID da Regra do evento de gatilho.</span><span class="sxs-lookup"><span data-stu-id="3204b-275">Rule ID of the triggering event.</span></span>        |
|<span data-ttu-id="3204b-276">Message</span><span class="sxs-lookup"><span data-stu-id="3204b-276">message</span></span>     | <span data-ttu-id="3204b-277">Mensagem amigável para o evento de gatilho.</span><span class="sxs-lookup"><span data-stu-id="3204b-277">User-friendly message for the triggering event.</span></span> <span data-ttu-id="3204b-278">Mais detalhes são fornecidos na seção de detalhes.</span><span class="sxs-lookup"><span data-stu-id="3204b-278">More details are provided in the details section.</span></span>        |
|<span data-ttu-id="3204b-279">ação</span><span class="sxs-lookup"><span data-stu-id="3204b-279">action</span></span>     |  <span data-ttu-id="3204b-280">Ação executada na solicitação.</span><span class="sxs-lookup"><span data-stu-id="3204b-280">Action taken on the request.</span></span> <span data-ttu-id="3204b-281">Os valores disponíveis são Bloqueada e Permitida.</span><span class="sxs-lookup"><span data-stu-id="3204b-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="3204b-282">site</span><span class="sxs-lookup"><span data-stu-id="3204b-282">site</span></span>     | <span data-ttu-id="3204b-283">Site para o qual o log foi gerado.</span><span class="sxs-lookup"><span data-stu-id="3204b-283">Site for which the log was generated.</span></span> <span data-ttu-id="3204b-284">No momento, somente Global é listado porque as regras são globais.</span><span class="sxs-lookup"><span data-stu-id="3204b-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="3204b-285">detalhes</span><span class="sxs-lookup"><span data-stu-id="3204b-285">details</span></span>     | <span data-ttu-id="3204b-286">Detalhes do evento de gatilho.</span><span class="sxs-lookup"><span data-stu-id="3204b-286">Details of the triggering event.</span></span>        |
|<span data-ttu-id="3204b-287">details.message</span><span class="sxs-lookup"><span data-stu-id="3204b-287">details.message</span></span>     | <span data-ttu-id="3204b-288">Descrição da regra.</span><span class="sxs-lookup"><span data-stu-id="3204b-288">Description of the rule.</span></span>        |
|<span data-ttu-id="3204b-289">details.data</span><span class="sxs-lookup"><span data-stu-id="3204b-289">details.data</span></span>     | <span data-ttu-id="3204b-290">Dados específicos encontrados na solicitação que corresponderam à regra.</span><span class="sxs-lookup"><span data-stu-id="3204b-290">Specific data found in request that matched the rule.</span></span>         |
|<span data-ttu-id="3204b-291">details.file</span><span class="sxs-lookup"><span data-stu-id="3204b-291">details.file</span></span>     | <span data-ttu-id="3204b-292">Arquivo de configuração que continha a regra.</span><span class="sxs-lookup"><span data-stu-id="3204b-292">Configuration file that contained the rule.</span></span>        |
|<span data-ttu-id="3204b-293">details.line</span><span class="sxs-lookup"><span data-stu-id="3204b-293">details.line</span></span>     | <span data-ttu-id="3204b-294">Número de linha no arquivo de configuração que disparou o evento.</span><span class="sxs-lookup"><span data-stu-id="3204b-294">Line number in the configuration file that triggered the event.</span></span>       |

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

### <a name="view-and-analyze-the-activity-log"></a><span data-ttu-id="3204b-295">Exibir e analisar o log de atividades</span><span class="sxs-lookup"><span data-stu-id="3204b-295">View and analyze the activity log</span></span>

<span data-ttu-id="3204b-296">Você pode exibir e analisar os dados do log de atividades usando um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="3204b-296">You can view and analyze activity log data by using any of the following methods:</span></span>

* <span data-ttu-id="3204b-297">**Ferramentas do Azure**: recupere informações do log de atividades por meio do Azure PowerShell, da CLI do Azure, da API REST do Azure ou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3204b-297">**Azure tools**: Retrieve information from the activity log through Azure PowerShell, the Azure CLI, the Azure REST API, or the Azure portal.</span></span> <span data-ttu-id="3204b-298">As instruções passo a passo para cada método são detalhadas no artigo [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) (Operações de atividade com o Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3204b-298">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="3204b-299">**Power BI**: se ainda não tiver uma conta do [Power BI](https://powerbi.microsoft.com/pricing), experimente uma gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="3204b-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="3204b-300">Com o [pacote de conteúdo dos Logs de Atividades do Azure para Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), você pode analisar seus dados com painéis pré-configurados que podem ser usados no estado em que se encontram ou ser personalizados.</span><span class="sxs-lookup"><span data-stu-id="3204b-300">By using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-the-access-performance-and-firewall-logs"></a><span data-ttu-id="3204b-301">Exibir e analisar os logs de acesso, de desempenho e de firewall</span><span class="sxs-lookup"><span data-stu-id="3204b-301">View and analyze the access, performance, and firewall logs</span></span>

<span data-ttu-id="3204b-302">O Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) pode coletar os arquivos de log de contadores e eventos de sua conta de Armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="3204b-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect the counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="3204b-303">Ele inclui visualizações e funcionalidades de pesquisa avançadas para analisar os logs.</span><span class="sxs-lookup"><span data-stu-id="3204b-303">It includes visualizations and powerful search capabilities to analyze your logs.</span></span>

<span data-ttu-id="3204b-304">Você também pode se conectar à sua conta de armazenamento e recuperar as entradas de log JSON para logs de desempenho e acesso.</span><span class="sxs-lookup"><span data-stu-id="3204b-304">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span></span> <span data-ttu-id="3204b-305">Depois de baixar os arquivos JSON, você pode convertê-los em CSV e exibi-los no Excel, no Power BI ou em qualquer outra ferramenta de visualização de dados.</span><span class="sxs-lookup"><span data-stu-id="3204b-305">After you download the JSON files, you can convert them to CSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="3204b-306">Se estiver familiarizado com o Visual Studio e os conceitos básicos de alteração de valores de constantes e variáveis em C#, você poderá usar as [ferramentas de conversor de log](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponíveis no GitHub.</span><span class="sxs-lookup"><span data-stu-id="3204b-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="3204b-307">Métricas</span><span class="sxs-lookup"><span data-stu-id="3204b-307">Metrics</span></span>

<span data-ttu-id="3204b-308">Métricas são um recurso para alguns recursos do Azure, nas quais você pode exibir os contadores de desempenho no portal.</span><span class="sxs-lookup"><span data-stu-id="3204b-308">Metrics are a feature for certain Azure resources where you can view performance counters in the portal.</span></span> <span data-ttu-id="3204b-309">Para o Gateway de Aplicativo, uma única métrica está disponível no momento.</span><span class="sxs-lookup"><span data-stu-id="3204b-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="3204b-310">Essa métrica é a vazão de dados e você pode vê-la no portal.</span><span class="sxs-lookup"><span data-stu-id="3204b-310">This metric is throughput, and you can see it in the portal.</span></span> <span data-ttu-id="3204b-311">Procure um gateway de aplicativo e clique em **Métricas**.</span><span class="sxs-lookup"><span data-stu-id="3204b-311">Browse to an application gateway and click **Metrics**.</span></span> <span data-ttu-id="3204b-312">Para exibir os valores, selecione a taxa de transferência na seção **Métricas disponíveis**.</span><span class="sxs-lookup"><span data-stu-id="3204b-312">To view the values, select throughput in the **Available metrics** section.</span></span> <span data-ttu-id="3204b-313">Na imagem a seguir, você pode ver um exemplo com os filtros que podem ser usados para exibir os dados em intervalos de tempo diferentes.</span><span class="sxs-lookup"><span data-stu-id="3204b-313">In the following image, you can see an example with the filters that you can use to display the data in different time ranges.</span></span>

![Exibição da métrica com filtros][5]

<span data-ttu-id="3204b-315">Para ver uma lista atual de métricas, consulte [Métricas com suporte no Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="3204b-315">To see a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="3204b-316">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="3204b-316">Alert rules</span></span>

<span data-ttu-id="3204b-317">Você pode iniciar as regras de alerta com base nas métricas de um recurso.</span><span class="sxs-lookup"><span data-stu-id="3204b-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="3204b-318">Por exemplo, um alerta poderá chamar um webhook ou enviar um email para um administrador se a vazão de dados do gateway de aplicativo estiver acima, abaixo ou no limite durante um período especificado.</span><span class="sxs-lookup"><span data-stu-id="3204b-318">For example, an alert can call a webhook or email an administrator if the throughput of the application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="3204b-319">O seguinte exemplo orientará você pela criação de uma regra de alerta que envia um email para um administrador após um limite de vazão de dados ter sido violado:</span><span class="sxs-lookup"><span data-stu-id="3204b-319">The following example walks you through creating an alert rule that sends an email to an administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="3204b-320">Clique em **Adicionar alerta de métrica** para abrir a folha **Adicionar regra**.</span><span class="sxs-lookup"><span data-stu-id="3204b-320">Click **Add metric alert** to open the **Add rule** blade.</span></span> <span data-ttu-id="3204b-321">Também acesse essa folha na folha de métricas.</span><span class="sxs-lookup"><span data-stu-id="3204b-321">You can also reach this blade from the metrics blade.</span></span>

   ![Botão “Adicionar alerta de métrica”][6]

2. <span data-ttu-id="3204b-323">Na folha **Adicionar regra**, preencha as seções de nome, condição e notificação e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3204b-323">On the **Add rule** blade, fill out the name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="3204b-324">No seletor **Condição**, selecione um dos quatro valores: **Maior que**, **Maior ou igual a**, **Menor que** ou **Menor ou igual a**.</span><span class="sxs-lookup"><span data-stu-id="3204b-324">In the **Condition** selector, select one of the four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="3204b-325">No seletor **Período**, selecione um período de 5 minutos a 6 horas.</span><span class="sxs-lookup"><span data-stu-id="3204b-325">In the **Period** selector, select a period from 5 minutes to 6 hours.</span></span>

   * <span data-ttu-id="3204b-326">Se você selecionar **Proprietários, colaboradores e leitores de email**, o email poderá ser dinâmico com base nos usuários que têm acesso a esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3204b-326">If you select **Email owners, contributors, and readers**, the email can be dynamic based on the users who have access to that resource.</span></span> <span data-ttu-id="3204b-327">Caso contrário, você poderá fornecer uma lista separada por vírgula de usuários na caixa **Emails de administrador adicionais**.</span><span class="sxs-lookup"><span data-stu-id="3204b-327">Otherwise, you can provide a comma-separated list of users in the **Additional administrator email(s)** box.</span></span>

   ![Folha Adicionar regra][7]

<span data-ttu-id="3204b-329">Se o limite for violado, um email semelhante ao mostrado na seguinte imagem chegará:</span><span class="sxs-lookup"><span data-stu-id="3204b-329">If the threshold is breached, an email that's similar to the one in the following image arrives:</span></span>

![Email para o limite violado][8]

<span data-ttu-id="3204b-331">Uma lista de alertas é exibida após a criação de um alerta de métrica.</span><span class="sxs-lookup"><span data-stu-id="3204b-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="3204b-332">Ela fornece uma visão geral de todas as regras de alerta.</span><span class="sxs-lookup"><span data-stu-id="3204b-332">It provides an overview of all the alert rules.</span></span>

![Lista de alertas e regras][9]

<span data-ttu-id="3204b-334">Para saber mais sobre notificações de alerta, consulte [Receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3204b-334">To learn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="3204b-335">Para entender mais sobre webhooks e como eles podem ser usados com alertas, consulte [Configurar um webhook em um alerta de métrica do Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="3204b-335">To understand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3204b-336">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3204b-336">Next steps</span></span>

* <span data-ttu-id="3204b-337">Visualize o contador e os logs de eventos com o [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="3204b-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="3204b-338">Postagem no blog [Visualize your Azure Activity Log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Visualizar o log de atividades do Azure com o Power BI).</span><span class="sxs-lookup"><span data-stu-id="3204b-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="3204b-339">Postagem no blog [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Exibir e analisar os Logs de Atividades do Azure no Power BI e muito mais).</span><span class="sxs-lookup"><span data-stu-id="3204b-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

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
