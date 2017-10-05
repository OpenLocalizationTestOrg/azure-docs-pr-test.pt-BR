---
title: "Solução de Cofre de Chaves do Azure no Log Analytics | Microsoft Docs"
description: "Você pode usar a solução de Cofre de Chaves do Azure no Log Analytics para examinar logs do Cofre de Chaves do Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 651586e0846ffb22a23e64b73c2cc614980d9b92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a><span data-ttu-id="566c3-103">Solução do Azure Key Vault Analytics no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="566c3-103">Azure Key Vault Analytics solution in Log Analytics</span></span>

![Símbolo do Cofre de Chaves](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

<span data-ttu-id="566c3-105">Você pode usar a solução de Cofre de Chaves do Azure no Log Analytics para examinar logs AuditEvent do Cofre de Chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="566c3-105">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span>

<span data-ttu-id="566c3-106">Para usar a solução, você precisa habilitar o registro em log de diagnóstico do Azure Key Vault e direcionar tal diagnóstico para um espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="566c3-106">To use the solution, you need to enable logging of Azure Key Vault diagnostics and direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="566c3-107">Não é necessário gravar os logs no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="566c3-107">It is not necessary to write the logs to Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="566c3-108">Em janeiro de 2017, ocorreu uma mudança na maneira correta de envio de logs do Key Vault para o Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="566c3-108">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="566c3-109">Se a solução de Key Vault que você está usando mostrar *(preterido)* no título, consulte [Migrar da solução antiga de Key Vault](#migrating-from-the-old-key-vault-solution) para conhecer as etapas que você deve executar.</span><span class="sxs-lookup"><span data-stu-id="566c3-109">If the Key Vault solution you are using shows *(deprecated)* in the title, refer to [migrating from the old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need to follow.</span></span>
>
>

## <a name="install-and-configure-the-solution"></a><span data-ttu-id="566c3-110">Instale e configure a solução</span><span class="sxs-lookup"><span data-stu-id="566c3-110">Install and configure the solution</span></span>
<span data-ttu-id="566c3-111">Use as instruções a seguir para instalar e configurar a solução de Cofre de Chaves do Azure:</span><span class="sxs-lookup"><span data-stu-id="566c3-111">Use the following instructions to install and configure the Azure Key Vault solution:</span></span>

1. <span data-ttu-id="566c3-112">Habilite a solução de Azure Key Vault do [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) ou usando o processo descrito em [Adicionar soluções do Log Analytics por meio da Galeria de Soluções](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="566c3-112">Enable the Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="566c3-113">Habilitar o registro em log de diagnóstico para os recursos do Key Vault a serem monitorados usando o [portal](#enable-key-vault-diagnostics-in-the-portal) ou o [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span><span class="sxs-lookup"><span data-stu-id="566c3-113">Enable diagnostics logging for the Key Vault resources to monitor, using either the [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span></span>

### <a name="enable-key-vault-diagnostics-in-the-portal"></a><span data-ttu-id="566c3-114">Habilitar o diagnóstico de Key Vault no portal</span><span class="sxs-lookup"><span data-stu-id="566c3-114">Enable Key Vault diagnostics in the portal</span></span>

1. <span data-ttu-id="566c3-115">No Portal do Azure, navegue até o recurso do Key Vault a ser monitorado</span><span class="sxs-lookup"><span data-stu-id="566c3-115">In the Azure portal, navigate to the Key Vault resource to monitor</span></span>
2. <span data-ttu-id="566c3-116">Selecione *Logs de diagnóstico* para abrir a página seguinte</span><span class="sxs-lookup"><span data-stu-id="566c3-116">Select *Diagnostics logs* to open the following page</span></span>

   ![imagem do bloco Cofre de Chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. <span data-ttu-id="566c3-118">Clique em *Ativar diagnóstico* para abrir a página seguinte</span><span class="sxs-lookup"><span data-stu-id="566c3-118">Click *Turn on diagnostics* to open the following page</span></span>

   ![imagem do bloco Cofre de Chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. <span data-ttu-id="566c3-120">Para ativar o diagnóstico, clique em *Ativar* em *Status*</span><span class="sxs-lookup"><span data-stu-id="566c3-120">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="566c3-121">Clique na caixa de seleção para *Enviar para o Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="566c3-121">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="566c3-122">Selecione um espaço de trabalho existente do Log Analytics ou crie um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="566c3-122">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="566c3-123">Para habilitar logs do *AuditEvent*, clique na caixa de seleção sob o Log</span><span class="sxs-lookup"><span data-stu-id="566c3-123">To enable *AuditEvent* logs, click the checkbox under Log</span></span>
8. <span data-ttu-id="566c3-124">Clique em *Salvar* para habilitar o registro em log de diagnóstico para o Log Analytics</span><span class="sxs-lookup"><span data-stu-id="566c3-124">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-key-vault-diagnostics-using-powershell"></a><span data-ttu-id="566c3-125">Habilitar o diagnóstico do Key Vault usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="566c3-125">Enable Key Vault diagnostics using PowerShell</span></span>
<span data-ttu-id="566c3-126">O script do PowerShell a seguir fornece um exemplo de como usar o `Set-AzureRmDiagnosticSetting` para habilitar o registro em log de diagnóstico para o Key Vault:</span><span class="sxs-lookup"><span data-stu-id="566c3-126">The following PowerShell script provides an example of how to use `Set-AzureRmDiagnosticSetting` to enable diagnostic logging for Key Vault:</span></span>
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a><span data-ttu-id="566c3-127">Veja os detalhes da coleta de dados do Cofre de Chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="566c3-127">Review Azure Key Vault data collection details</span></span>
<span data-ttu-id="566c3-128">A solução do Azure Key Vault coleta logs de diagnóstico diretamente do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="566c3-128">Azure Key Vault solution collects diagnostics logs directly from the Key Vault.</span></span>
<span data-ttu-id="566c3-129">Não é necessário gravar os logs no Armazenamento de Blobs do Azure e nenhum agente é necessário para a coleta de dados.</span><span class="sxs-lookup"><span data-stu-id="566c3-129">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="566c3-130">A tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para o Cofre de Chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="566c3-130">The following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span></span>

| <span data-ttu-id="566c3-131">Plataforma</span><span class="sxs-lookup"><span data-stu-id="566c3-131">Platform</span></span> | <span data-ttu-id="566c3-132">Agente direto</span><span class="sxs-lookup"><span data-stu-id="566c3-132">Direct agent</span></span> | <span data-ttu-id="566c3-133">Agente do Systems Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="566c3-133">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="566c3-134">As tabelas</span><span class="sxs-lookup"><span data-stu-id="566c3-134">Azure</span></span> | <span data-ttu-id="566c3-135">Operations Manager necessário?</span><span class="sxs-lookup"><span data-stu-id="566c3-135">Operations Manager required?</span></span> | <span data-ttu-id="566c3-136">Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="566c3-136">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="566c3-137">Frequência de coleta</span><span class="sxs-lookup"><span data-stu-id="566c3-137">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="566c3-138">As tabelas</span><span class="sxs-lookup"><span data-stu-id="566c3-138">Azure</span></span> |  |  |<span data-ttu-id="566c3-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="566c3-139">&#8226;</span></span> |  |  | <span data-ttu-id="566c3-140">na chegada</span><span class="sxs-lookup"><span data-stu-id="566c3-140">on arrival</span></span> |

## <a name="use-azure-key-vault"></a><span data-ttu-id="566c3-141">Usar o Cofre de Chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="566c3-141">Use Azure Key Vault</span></span>
<span data-ttu-id="566c3-142">Após a [instalação da solução](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), consulte os dados do Key Vault clicando no bloco **Azure Key Vault** na página **Visão geral** do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="566c3-142">After you [install the solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view the Key Vault data by clicking the **Azure Key Vault** tile from the **Overview** page of Log Analytics.</span></span>

![imagem do bloco Cofre de Chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

<span data-ttu-id="566c3-144">Depois de clicar no bloco **Visão Geral**, você pode exibir resumos dos seus logs e então aprofundar-se nos detalhes das seguintes categorias:</span><span class="sxs-lookup"><span data-stu-id="566c3-144">After you click the **Overview** tile, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="566c3-145">Volume de todas as operações do Cofre de Chaves ao longo do tempo</span><span class="sxs-lookup"><span data-stu-id="566c3-145">Volume of all key vault operations over time</span></span>
* <span data-ttu-id="566c3-146">Volumes de operação com falha ao longo do tempo</span><span class="sxs-lookup"><span data-stu-id="566c3-146">Failed operation volumes over time</span></span>
* <span data-ttu-id="566c3-147">Latência operacional média por operação</span><span class="sxs-lookup"><span data-stu-id="566c3-147">Average operational latency by operation</span></span>
* <span data-ttu-id="566c3-148">Qualidade de serviço para operações com o número de operações que levam mais de 1.000 ms e uma lista das operações que levam mais de 1.000 ms</span><span class="sxs-lookup"><span data-stu-id="566c3-148">Quality of service for operations with the number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span></span>

![imagem do painel Cofre de Chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![imagem do painel Cofre de Chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="to-view-details-for-any-operation"></a><span data-ttu-id="566c3-151">Para exibir detalhes de qualquer operação</span><span class="sxs-lookup"><span data-stu-id="566c3-151">To view details for any operation</span></span>
1. <span data-ttu-id="566c3-152">Na página **Visão Geral**, clique no bloco **Cofre de Chaves do Azure**.</span><span class="sxs-lookup"><span data-stu-id="566c3-152">On the **Overview** page, click the **Azure Key Vault** tile.</span></span>
2. <span data-ttu-id="566c3-153">Na painel **Cofre de Chaves do Azure**, examine as informações resumidas em uma das folhas e, em seguida, clique em uma para exibir informações detalhadas sobre ela na página pesquisa de log.</span><span class="sxs-lookup"><span data-stu-id="566c3-153">On the **Azure Key Vault** dashboard, review the summary information in one of the blades, and then click one to view detailed information about it in the log search page.</span></span>

    <span data-ttu-id="566c3-154">Em qualquer uma das páginas de pesquisa de log, você pode exibir os resultados por tempo, resultados detalhados e o histórico de pesquisa de log.</span><span class="sxs-lookup"><span data-stu-id="566c3-154">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="566c3-155">Você também pode filtrar por facetas para restringir os resultados.</span><span class="sxs-lookup"><span data-stu-id="566c3-155">You can also filter by facets to narrow the results.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="566c3-156">Registros do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="566c3-156">Log Analytics records</span></span>
<span data-ttu-id="566c3-157">A solução de Cofre de Chaves do Azure analisa os registros que têm um tipo de **KeyVaults** que são coletados de [logs de AuditEvent](../key-vault/key-vault-logging.md) no Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="566c3-157">The Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span></span>  <span data-ttu-id="566c3-158">As propriedades desses registros são descritas na tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="566c3-158">Properties for these records are in the following table:</span></span>  

| <span data-ttu-id="566c3-159">Propriedade</span><span class="sxs-lookup"><span data-stu-id="566c3-159">Property</span></span> | <span data-ttu-id="566c3-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="566c3-160">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="566c3-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="566c3-161">Type</span></span> |<span data-ttu-id="566c3-162">*AzureDiagnostics*</span><span class="sxs-lookup"><span data-stu-id="566c3-162">*AzureDiagnostics*</span></span> |
| <span data-ttu-id="566c3-163">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="566c3-163">SourceSystem</span></span> |<span data-ttu-id="566c3-164">*As tabelas*</span><span class="sxs-lookup"><span data-stu-id="566c3-164">*Azure*</span></span> |
| <span data-ttu-id="566c3-165">CallerIpAddress</span><span class="sxs-lookup"><span data-stu-id="566c3-165">CallerIpAddress</span></span> |<span data-ttu-id="566c3-166">Endereço IP do cliente que fez a solicitação</span><span class="sxs-lookup"><span data-stu-id="566c3-166">IP address of the client who made the request</span></span> |
| <span data-ttu-id="566c3-167">Categoria</span><span class="sxs-lookup"><span data-stu-id="566c3-167">Category</span></span> | <span data-ttu-id="566c3-168">*AuditEvent*</span><span class="sxs-lookup"><span data-stu-id="566c3-168">*AuditEvent*</span></span> |
| <span data-ttu-id="566c3-169">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="566c3-169">CorrelationId</span></span> |<span data-ttu-id="566c3-170">Um GUID opcional que o cliente pode passar para correlacionar os logs do lado do cliente aos logs do lado do serviço (Chave do Cofre).</span><span class="sxs-lookup"><span data-stu-id="566c3-170">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="566c3-171">DurationMs</span><span class="sxs-lookup"><span data-stu-id="566c3-171">DurationMs</span></span> |<span data-ttu-id="566c3-172">Tempo necessário para atender à solicitação da API REST, em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="566c3-172">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="566c3-173">Esse tempo não inclui a latência de rede e, portanto, o tempo medido no lado cliente pode não corresponder a esse tempo.</span><span class="sxs-lookup"><span data-stu-id="566c3-173">This time does not include network latency, so the time that you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="566c3-174">httpStatusCode_d</span><span class="sxs-lookup"><span data-stu-id="566c3-174">httpStatusCode_d</span></span> |<span data-ttu-id="566c3-175">Código de status HTTP retornado pela solicitação (por exemplo, *200*)</span><span class="sxs-lookup"><span data-stu-id="566c3-175">HTTP status code returned by the request (for example, *200*)</span></span> |
| <span data-ttu-id="566c3-176">id_s</span><span class="sxs-lookup"><span data-stu-id="566c3-176">id_s</span></span> |<span data-ttu-id="566c3-177">ID exclusiva da solicitação</span><span class="sxs-lookup"><span data-stu-id="566c3-177">Unique ID of the request</span></span> |
| <span data-ttu-id="566c3-178">identity_claim_appid_g</span><span class="sxs-lookup"><span data-stu-id="566c3-178">identity_claim_appid_g</span></span> | <span data-ttu-id="566c3-179">GUID para a ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="566c3-179">GUID for the application id</span></span> |
| <span data-ttu-id="566c3-180">OperationName</span><span class="sxs-lookup"><span data-stu-id="566c3-180">OperationName</span></span> |<span data-ttu-id="566c3-181">Nome da operação conforme documentado no [Registro em Log do Cofre de Chaves do Azure](../key-vault/key-vault-logging.md)</span><span class="sxs-lookup"><span data-stu-id="566c3-181">Name of the operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span></span> |
| <span data-ttu-id="566c3-182">OperationVersion</span><span class="sxs-lookup"><span data-stu-id="566c3-182">OperationVersion</span></span> |<span data-ttu-id="566c3-183">Versão da API REST solicitada pelo cliente (por exemplo, *2015-06-01*)</span><span class="sxs-lookup"><span data-stu-id="566c3-183">REST API version requested by the client (for example *2015-06-01*)</span></span> |
| <span data-ttu-id="566c3-184">requestUri_s</span><span class="sxs-lookup"><span data-stu-id="566c3-184">requestUri_s</span></span> |<span data-ttu-id="566c3-185">O URI da solicitação</span><span class="sxs-lookup"><span data-stu-id="566c3-185">Uri of the request</span></span> |
| <span data-ttu-id="566c3-186">Recurso</span><span class="sxs-lookup"><span data-stu-id="566c3-186">Resource</span></span> |<span data-ttu-id="566c3-187">Nome do cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="566c3-187">Name of the key vault</span></span> |
| <span data-ttu-id="566c3-188">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="566c3-188">ResourceGroup</span></span> |<span data-ttu-id="566c3-189">Grupo de recursos do cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="566c3-189">Resource group of the key vault</span></span> |
| <span data-ttu-id="566c3-190">ResourceId</span><span class="sxs-lookup"><span data-stu-id="566c3-190">ResourceId</span></span> |<span data-ttu-id="566c3-191">ID do Recurso do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="566c3-191">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="566c3-192">Para os logs do Key Vault, isse será a ID do recurso do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="566c3-192">For Key Vault logs, this is the Key Vault resource ID.</span></span> |
| <span data-ttu-id="566c3-193">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="566c3-193">ResourceProvider</span></span> |<span data-ttu-id="566c3-194">*MICROSOFT.KEYVAULT*</span><span class="sxs-lookup"><span data-stu-id="566c3-194">*MICROSOFT.KEYVAULT*</span></span> |
| <span data-ttu-id="566c3-195">ResourceType</span><span class="sxs-lookup"><span data-stu-id="566c3-195">ResourceType</span></span> | <span data-ttu-id="566c3-196">*VAULTS*</span><span class="sxs-lookup"><span data-stu-id="566c3-196">*VAULTS*</span></span> |
| <span data-ttu-id="566c3-197">ResultSignature</span><span class="sxs-lookup"><span data-stu-id="566c3-197">ResultSignature</span></span> |<span data-ttu-id="566c3-198">Status do HTTP (por exemplo, *OK*)</span><span class="sxs-lookup"><span data-stu-id="566c3-198">HTTP status (for example, *OK*)</span></span> |
| <span data-ttu-id="566c3-199">ResultType</span><span class="sxs-lookup"><span data-stu-id="566c3-199">ResultType</span></span> |<span data-ttu-id="566c3-200">Resultado da solicitação da API REST (por exemplo, *Êxito*)</span><span class="sxs-lookup"><span data-stu-id="566c3-200">Result of REST API request (for example, *Success*)</span></span> |
| <span data-ttu-id="566c3-201">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="566c3-201">SubscriptionId</span></span> |<span data-ttu-id="566c3-202">A ID da assinatura do Azure que contém o Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="566c3-202">Azure subscription ID of the subscription containing the Key Vault</span></span> |

## <a name="migrating-from-the-old-key-vault-solution"></a><span data-ttu-id="566c3-203">Migrar da solução antiga de Key Vault</span><span class="sxs-lookup"><span data-stu-id="566c3-203">Migrating from the old Key Vault solution</span></span>
<span data-ttu-id="566c3-204">Em janeiro de 2017, ocorreu uma mudança na maneira correta de envio de logs do Key Vault para o Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="566c3-204">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="566c3-205">Essas alterações oferecem as seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="566c3-205">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="566c3-206">Os logs são gravados diretamente no Log Analytics sem a necessidade de usar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="566c3-206">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="566c3-207">Menor latência do momento em que os logs são gerados até eles serem disponibilizados no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="566c3-207">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="566c3-208">Menos etapas de configuração</span><span class="sxs-lookup"><span data-stu-id="566c3-208">Fewer configuration steps</span></span>
+ <span data-ttu-id="566c3-209">Um formato comum para todos os tipos de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="566c3-209">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="566c3-210">Para usar a solução atualizada:</span><span class="sxs-lookup"><span data-stu-id="566c3-210">To use the updated solution:</span></span>

1. [<span data-ttu-id="566c3-211">Configure o envio do diagnóstico diretamente para o Log Analytics do Key Vault</span><span class="sxs-lookup"><span data-stu-id="566c3-211">Configure diagnostics to be sent directly to Log Analytics from Key Vault</span></span>](#enable-key-vault-diagnostics-in-the-portal)  
2. <span data-ttu-id="566c3-212">Habilite a solução de Azure Key Vault usando o processo descrito em [Adicionar soluções do Log Analytics por meio da Galeria de Soluções](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="566c3-212">Enable the Azure Key Vault solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="566c3-213">Atualizar todas as consultas salvas, painéis ou alertas para usar o novo tipo de dados</span><span class="sxs-lookup"><span data-stu-id="566c3-213">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="566c3-214">O tipo mudou de KeyVaults para AzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="566c3-214">Type is change from: KeyVaults to AzureDiagnostics.</span></span> <span data-ttu-id="566c3-215">Use ResourceType para filtrar os registros do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="566c3-215">You can use the ResourceType to filter to Key Vault Logs.</span></span>
  - <span data-ttu-id="566c3-216">Em vez de: `Type=KeyVaults`, use`Type=AzureDiagnostics ResourceType=VAULTS`</span><span class="sxs-lookup"><span data-stu-id="566c3-216">Instead of: `Type=KeyVaults`, use `Type=AzureDiagnostics ResourceType=VAULTS`</span></span>
  + <span data-ttu-id="566c3-217">Campos: (os nomes de campo diferenciam maiúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="566c3-217">Fields: (Field names are case-sensitive)</span></span>
  - <span data-ttu-id="566c3-218">Para qualquer campo que tenha um sufixo de \_s, \_d ou \_g no nome, altere o primeiro caractere para minúsculo</span><span class="sxs-lookup"><span data-stu-id="566c3-218">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
  - <span data-ttu-id="566c3-219">Para qualquer campo que tenha um sufixo de \_o no nome, os dados são divididos em campos individuais com base nos nomes de campos aninhados.</span><span class="sxs-lookup"><span data-stu-id="566c3-219">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span> <span data-ttu-id="566c3-220">Por exemplo, o UPN do chamador é armazenado em um campo `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span><span class="sxs-lookup"><span data-stu-id="566c3-220">For example, the UPN of the caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span></span>
   - <span data-ttu-id="566c3-221">O campo CallerIpAddress mudou para CallerIPAddress</span><span class="sxs-lookup"><span data-stu-id="566c3-221">Field CallerIpAddress changed to CallerIPAddress</span></span>
   - <span data-ttu-id="566c3-222">O campo RemoteIPCountry não está mais presente</span><span class="sxs-lookup"><span data-stu-id="566c3-222">Field RemoteIPCountry is no longer present</span></span>
4. <span data-ttu-id="566c3-223">Remova a solução *Análise do Key Vault (preterida)*.</span><span class="sxs-lookup"><span data-stu-id="566c3-223">Remove the *Key Vault Analytics (Deprecated)* solution.</span></span> <span data-ttu-id="566c3-224">Se você estiver usando o PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="566c3-224">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span></span>

<span data-ttu-id="566c3-225">Os dados coletados antes da alteração não estão visíveis na nova solução.</span><span class="sxs-lookup"><span data-stu-id="566c3-225">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="566c3-226">Você pode continuar a consultar esses dados usando os nomes de campo e tipo antigos.</span><span class="sxs-lookup"><span data-stu-id="566c3-226">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="566c3-227">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="566c3-227">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="566c3-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="566c3-228">Next steps</span></span>
* <span data-ttu-id="566c3-229">Usar [Pesquisas de Log](log-analytics-log-searches.md) no Log Analytics para exibir dados detalhados do Cofre de Chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="566c3-229">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure Key Vault data.</span></span>
