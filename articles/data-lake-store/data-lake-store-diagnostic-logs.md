---
title: "Exibindo logs de diagnóstico do Azure Data Lake Store| Microsoft Docs"
description: "Entenda como configurar e acessar os logs de diagnóstico do Azure Data Lake Store  "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: b7a38ec445ef0ce13f3f1931e8ee246dce6412a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="77fcb-103">Acessando os logs de diagnóstico do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="77fcb-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="77fcb-104">Saiba mais sobre como habilitar o log de diagnóstico em sua conta do Data Lake Store e como exibir os logs coletados em sua conta.</span><span class="sxs-lookup"><span data-stu-id="77fcb-104">Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.</span></span>

<span data-ttu-id="77fcb-105">As organizações podem habilitar o log de diagnóstico para que suas contas do Azure Data Lake Store coletem trilhas de auditoria de acesso a dados que forneçam informações, como a lista de usuários que acessam os dados, a frequência que os dados são acessados, a quantidade de dados armazenados na conta, etc.</span><span class="sxs-lookup"><span data-stu-id="77fcb-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77fcb-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="77fcb-106">Prerequisites</span></span>
* <span data-ttu-id="77fcb-107">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="77fcb-107">**An Azure subscription**.</span></span> <span data-ttu-id="77fcb-108">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77fcb-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="77fcb-109">**Conta do Repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="77fcb-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="77fcb-110">Siga as instruções em [Introdução ao Repositório Azure Data Lake usando o Portal do Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="77fcb-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="77fcb-111">Habilitar o log de diagnóstico em sua conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="77fcb-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="77fcb-112">Entre no novo [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="77fcb-112">Sign on to the new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="77fcb-113">Abra sua conta Data Lake Store e na folha da conta Data Lake Store, clique em **Configurações**, em seguida, clique em **Logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="77fcb-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="77fcb-114">No **os logs de diagnóstico** folha, clique em **Ativar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="77fcb-114">In the **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="77fcb-115">![Habilitar o log de diagnóstico](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "habilitar logs de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="77fcb-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="77fcb-116">Na folha **Diagnóstico** , faça as seguintes alterações para configurar o log de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="77fcb-116">In the **Diagnostic** blade, make the following changes to configure diagnostic logging.</span></span>
   
    <span data-ttu-id="77fcb-117">![Habilitar o log de diagnóstico](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "habilitar logs de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="77fcb-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="77fcb-118">Defina **Status** para **Ativado** para habilitar o log de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="77fcb-118">Set **Status** to **On** to enable diagnostic logging.</span></span>
   * <span data-ttu-id="77fcb-119">Você pode optar por armazenar/processar os dados de maneiras diferentes.</span><span class="sxs-lookup"><span data-stu-id="77fcb-119">You can choose to store/process the data in different ways.</span></span>
     
        * <span data-ttu-id="77fcb-120">Selecione a opção **Arquivar em uma conta de armazenamento** para armazenar os logs em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="77fcb-120">Select the option to **Archive to a storage account** to store logs to an Azure Storage account.</span></span> <span data-ttu-id="77fcb-121">Use esta opção se quiser arquivar os dados que serão processados em lote em uma data posterior.</span><span class="sxs-lookup"><span data-stu-id="77fcb-121">You use this option if you want to archive the data that will be batch-processed at a later date.</span></span> <span data-ttu-id="77fcb-122">Se escolher esta opção, você deverá fornecer uma conta de armazenamento do Azure para salvar os logs.</span><span class="sxs-lookup"><span data-stu-id="77fcb-122">If you select this option you must provide an Azure Storage account to save the logs to.</span></span>
        
        * <span data-ttu-id="77fcb-123">Selecione a opção **Transmitir pra um hub de eventos** para transmitir os dados de log para um Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="77fcb-123">Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="77fcb-124">Provavelmente, você usará esta opção se tiver um pipeline de processamento de downstream para analisar os logs de entrada em tempo real.</span><span class="sxs-lookup"><span data-stu-id="77fcb-124">Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time.</span></span> <span data-ttu-id="77fcb-125">Se escolher esta opção, você deverá fornecer os detalhes no Hub de Eventos do Azure que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="77fcb-125">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

        * <span data-ttu-id="77fcb-126">Selecione a opção de **enviar para Log Analytics** para usar o serviço do Azure Log Analytics para analisar os dados de log gerado.</span><span class="sxs-lookup"><span data-stu-id="77fcb-126">Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data.</span></span> <span data-ttu-id="77fcb-127">Se você selecionar essa opção, você deve fornecer os detalhes para o espaço de trabalho do Operations Management Suite que você usaria a análise de log de executar.</span><span class="sxs-lookup"><span data-stu-id="77fcb-127">If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.</span></span>
     
   * <span data-ttu-id="77fcb-128">Especifique se deseja obter os logs de auditoria, os logs de solicitação ou ambos.</span><span class="sxs-lookup"><span data-stu-id="77fcb-128">Specify whether you want to get audit logs or request logs or both.</span></span>
   * <span data-ttu-id="77fcb-129">Especifique o número de dias que os dados devem ser mantidos.</span><span class="sxs-lookup"><span data-stu-id="77fcb-129">Specify the number of days for which the data must be retained.</span></span> <span data-ttu-id="77fcb-130">Retenção só é aplicável se você estiver usando a conta de armazenamento do Azure para arquivar dados de log.</span><span class="sxs-lookup"><span data-stu-id="77fcb-130">Retention is only applicable if you are using Azure storage account to archive log data.</span></span>
   * <span data-ttu-id="77fcb-131">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="77fcb-131">Click **Save**.</span></span>

<span data-ttu-id="77fcb-132">Depois de habilitar as configurações de diagnóstico, você poderá observar os logs na guia **Logs de Diagnóstico** .</span><span class="sxs-lookup"><span data-stu-id="77fcb-132">Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="77fcb-133">Veja os logs de diagnóstico em sua conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="77fcb-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="77fcb-134">Há duas maneiras de exibir os dados do log da sua conta no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="77fcb-134">There are two ways to view the log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="77fcb-135">Na exibição de configurações da conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="77fcb-135">From the Data Lake Store account settings view</span></span>
* <span data-ttu-id="77fcb-136">Na conta de Armazenamento do Azure onde os dados são armazenados</span><span class="sxs-lookup"><span data-stu-id="77fcb-136">From the Azure Storage account where the data is stored</span></span>

### <a name="using-the-data-lake-store-settings-view"></a><span data-ttu-id="77fcb-137">Usando a exibição de configurações do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="77fcb-137">Using the Data Lake Store Settings view</span></span>
1. <span data-ttu-id="77fcb-138">Na folha **Configurações** da conta Data Lake Store, clique em **Logs de Diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="77fcb-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="77fcb-139">![Log de diagnóstico de exibição](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "exibir logs de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="77fcb-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="77fcb-140">Na folha **Logs de Diagnóstico**, você deve ver os logs categorizados por **Logs de Auditoria** e **Logs de Solicitação**.</span><span class="sxs-lookup"><span data-stu-id="77fcb-140">In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="77fcb-141">Os Logs de Solicitação capturam todas as solicitações de API feitas na conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="77fcb-141">Request logs capture every API request made on the Data Lake Store account.</span></span>
   * <span data-ttu-id="77fcb-142">Os Logs de Auditoria são semelhantes aos Logs de Solicitação, mas fornecem uma análise mais detalhada das operações que estão sendo executadas na conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="77fcb-142">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account.</span></span> <span data-ttu-id="77fcb-143">Por exemplo, uma única chamada à API de upload nos logs de solicitação poderá resultar em várias operações do tipo "Anexar" nos logs de auditoria.</span><span class="sxs-lookup"><span data-stu-id="77fcb-143">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span></span>
3. <span data-ttu-id="77fcb-144">Clique no link **Download** em cada entrada de log para baixar os logs.</span><span class="sxs-lookup"><span data-stu-id="77fcb-144">Click the **Download** link against each log entry to download the logs.</span></span>

### <a name="from-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="77fcb-145">Na conta de Armazenamento do Azure que contém dados de log</span><span class="sxs-lookup"><span data-stu-id="77fcb-145">From the Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="77fcb-146">Abra a folha Conta de armazenamento do Azure associada ao Data Lake Store para registro em log e clique em Blobs.</span><span class="sxs-lookup"><span data-stu-id="77fcb-146">Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="77fcb-147">A folha **serviço Blob** lista dois contêineres.</span><span class="sxs-lookup"><span data-stu-id="77fcb-147">The **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="77fcb-148">![Exibir logs de diagnóstico](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "Exibir logs de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="77fcb-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="77fcb-149">O contêiner **insights-logs-audit** contém os logs de auditoria.</span><span class="sxs-lookup"><span data-stu-id="77fcb-149">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="77fcb-150">O contêiner **insights-logs-requests** contém os logs de solicitação.</span><span class="sxs-lookup"><span data-stu-id="77fcb-150">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="77fcb-151">Dentro desses contêineres, os logs são armazenados na estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="77fcb-151">Within these containers, the logs are stored under the following structure.</span></span>
   
    <span data-ttu-id="77fcb-152">![Log de diagnóstico de exibição](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "exibir logs de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="77fcb-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="77fcb-153">Por exemplo, o caminho completo para um log de auditoria poderia ser `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="77fcb-153">As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="77fcb-154">De modo semelhante, o caminho completo para um log de solicitação poderia ser `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="77fcb-154">Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-the-structure-of-the-log-data"></a><span data-ttu-id="77fcb-155">Compreenda a estrutura dos dados de log</span><span class="sxs-lookup"><span data-stu-id="77fcb-155">Understand the structure of the log data</span></span>
<span data-ttu-id="77fcb-156">Os logs de auditoria e solicitação estão em formato JSON.</span><span class="sxs-lookup"><span data-stu-id="77fcb-156">The audit and request logs are in a JSON format.</span></span> <span data-ttu-id="77fcb-157">Nesta seção, examinaremos a estrutura do JSON nos logs de solicitação e auditoria.</span><span class="sxs-lookup"><span data-stu-id="77fcb-157">In this section, we look at the structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="77fcb-158">Logs de Solicitação</span><span class="sxs-lookup"><span data-stu-id="77fcb-158">Request logs</span></span>
<span data-ttu-id="77fcb-159">Aqui está um exemplo de entrada no log de solicitação formatado em JSON.</span><span class="sxs-lookup"><span data-stu-id="77fcb-159">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="77fcb-160">Cada blob tem um objeto-raiz chamado **registros** que contém uma matriz de objetos do log.</span><span class="sxs-lookup"><span data-stu-id="77fcb-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="77fcb-161">Esquema do log de solicitação</span><span class="sxs-lookup"><span data-stu-id="77fcb-161">Request log schema</span></span>
| <span data-ttu-id="77fcb-162">Name</span><span class="sxs-lookup"><span data-stu-id="77fcb-162">Name</span></span> | <span data-ttu-id="77fcb-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="77fcb-163">Type</span></span> | <span data-ttu-id="77fcb-164">Descrição</span><span class="sxs-lookup"><span data-stu-id="77fcb-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77fcb-165">tempo real</span><span class="sxs-lookup"><span data-stu-id="77fcb-165">time</span></span> |<span data-ttu-id="77fcb-166">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-166">String</span></span> |<span data-ttu-id="77fcb-167">O carimbo de data/hora (em UTC) do log</span><span class="sxs-lookup"><span data-stu-id="77fcb-167">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="77fcb-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="77fcb-168">resourceId</span></span> |<span data-ttu-id="77fcb-169">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-169">String</span></span> |<span data-ttu-id="77fcb-170">A ID do recurso em que a operação ocorreu</span><span class="sxs-lookup"><span data-stu-id="77fcb-170">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="77fcb-171">categoria</span><span class="sxs-lookup"><span data-stu-id="77fcb-171">category</span></span> |<span data-ttu-id="77fcb-172">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-172">String</span></span> |<span data-ttu-id="77fcb-173">A categoria do log.</span><span class="sxs-lookup"><span data-stu-id="77fcb-173">The log category.</span></span> <span data-ttu-id="77fcb-174">Por exemplo, **Solicitações**.</span><span class="sxs-lookup"><span data-stu-id="77fcb-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="77fcb-175">operationName</span><span class="sxs-lookup"><span data-stu-id="77fcb-175">operationName</span></span> |<span data-ttu-id="77fcb-176">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-176">String</span></span> |<span data-ttu-id="77fcb-177">Nome da operação que está registrada.</span><span class="sxs-lookup"><span data-stu-id="77fcb-177">Name of the operation that is logged.</span></span> <span data-ttu-id="77fcb-178">Por exemplo, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="77fcb-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="77fcb-179">resultType</span><span class="sxs-lookup"><span data-stu-id="77fcb-179">resultType</span></span> |<span data-ttu-id="77fcb-180">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-180">String</span></span> |<span data-ttu-id="77fcb-181">O status da operação, por exemplo, 200.</span><span class="sxs-lookup"><span data-stu-id="77fcb-181">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="77fcb-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="77fcb-182">callerIpAddress</span></span> |<span data-ttu-id="77fcb-183">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-183">String</span></span> |<span data-ttu-id="77fcb-184">O endereço IP do cliente que está fazendo a solicitação</span><span class="sxs-lookup"><span data-stu-id="77fcb-184">The IP address of the client making the request</span></span> |
| <span data-ttu-id="77fcb-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="77fcb-185">correlationId</span></span> |<span data-ttu-id="77fcb-186">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-186">String</span></span> |<span data-ttu-id="77fcb-187">A ID do log que pode ser usada para agrupar um conjunto de entradas de log relacionadas</span><span class="sxs-lookup"><span data-stu-id="77fcb-187">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="77fcb-188">identidade</span><span class="sxs-lookup"><span data-stu-id="77fcb-188">identity</span></span> |<span data-ttu-id="77fcb-189">Objeto</span><span class="sxs-lookup"><span data-stu-id="77fcb-189">Object</span></span> |<span data-ttu-id="77fcb-190">A identidade que gerou o log</span><span class="sxs-lookup"><span data-stu-id="77fcb-190">The identity that generated the log</span></span> |
| <span data-ttu-id="77fcb-191">propriedades</span><span class="sxs-lookup"><span data-stu-id="77fcb-191">properties</span></span> |<span data-ttu-id="77fcb-192">JSON</span><span class="sxs-lookup"><span data-stu-id="77fcb-192">JSON</span></span> |<span data-ttu-id="77fcb-193">Confira abaixo para obter os detalhes</span><span class="sxs-lookup"><span data-stu-id="77fcb-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="77fcb-194">Esquema de propriedades do log de solicitação</span><span class="sxs-lookup"><span data-stu-id="77fcb-194">Request log properties schema</span></span>
| <span data-ttu-id="77fcb-195">Name</span><span class="sxs-lookup"><span data-stu-id="77fcb-195">Name</span></span> | <span data-ttu-id="77fcb-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="77fcb-196">Type</span></span> | <span data-ttu-id="77fcb-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="77fcb-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77fcb-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="77fcb-198">HttpMethod</span></span> |<span data-ttu-id="77fcb-199">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-199">String</span></span> |<span data-ttu-id="77fcb-200">O método HTTP usado para a operação.</span><span class="sxs-lookup"><span data-stu-id="77fcb-200">The HTTP Method used for the operation.</span></span> <span data-ttu-id="77fcb-201">Por exemplo, GET.</span><span class="sxs-lookup"><span data-stu-id="77fcb-201">For example, GET.</span></span> |
| <span data-ttu-id="77fcb-202">Caminho</span><span class="sxs-lookup"><span data-stu-id="77fcb-202">Path</span></span> |<span data-ttu-id="77fcb-203">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-203">String</span></span> |<span data-ttu-id="77fcb-204">O caminho em que a operação foi executada</span><span class="sxs-lookup"><span data-stu-id="77fcb-204">The path the operation was performed on</span></span> |
| <span data-ttu-id="77fcb-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="77fcb-205">RequestContentLength</span></span> |<span data-ttu-id="77fcb-206">int</span><span class="sxs-lookup"><span data-stu-id="77fcb-206">int</span></span> |<span data-ttu-id="77fcb-207">O comprimento do conteúdo da solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="77fcb-207">The content length of the HTTP request</span></span> |
| <span data-ttu-id="77fcb-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="77fcb-208">ClientRequestId</span></span> |<span data-ttu-id="77fcb-209">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-209">String</span></span> |<span data-ttu-id="77fcb-210">A ID que identifica esta solicitação exclusivamente</span><span class="sxs-lookup"><span data-stu-id="77fcb-210">The Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="77fcb-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="77fcb-211">StartTime</span></span> |<span data-ttu-id="77fcb-212">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-212">String</span></span> |<span data-ttu-id="77fcb-213">A hora em que o servidor recebeu a solicitação</span><span class="sxs-lookup"><span data-stu-id="77fcb-213">The time at which the server received the request</span></span> |
| <span data-ttu-id="77fcb-214">EndTime</span><span class="sxs-lookup"><span data-stu-id="77fcb-214">EndTime</span></span> |<span data-ttu-id="77fcb-215">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-215">String</span></span> |<span data-ttu-id="77fcb-216">A hora em que o servidor enviou uma resposta</span><span class="sxs-lookup"><span data-stu-id="77fcb-216">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="77fcb-217">Logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="77fcb-217">Audit logs</span></span>
<span data-ttu-id="77fcb-218">Aqui está um exemplo de entrada no log de auditoria formatado em JSON.</span><span class="sxs-lookup"><span data-stu-id="77fcb-218">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="77fcb-219">Cada blob tem um objeto-raiz chamado **registros** que contém uma matriz de objetos do log</span><span class="sxs-lookup"><span data-stu-id="77fcb-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="77fcb-220">Esquema do log de auditoria</span><span class="sxs-lookup"><span data-stu-id="77fcb-220">Audit log schema</span></span>
| <span data-ttu-id="77fcb-221">Name</span><span class="sxs-lookup"><span data-stu-id="77fcb-221">Name</span></span> | <span data-ttu-id="77fcb-222">Tipo</span><span class="sxs-lookup"><span data-stu-id="77fcb-222">Type</span></span> | <span data-ttu-id="77fcb-223">Descrição</span><span class="sxs-lookup"><span data-stu-id="77fcb-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77fcb-224">tempo real</span><span class="sxs-lookup"><span data-stu-id="77fcb-224">time</span></span> |<span data-ttu-id="77fcb-225">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-225">String</span></span> |<span data-ttu-id="77fcb-226">O carimbo de data/hora (em UTC) do log</span><span class="sxs-lookup"><span data-stu-id="77fcb-226">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="77fcb-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="77fcb-227">resourceId</span></span> |<span data-ttu-id="77fcb-228">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-228">String</span></span> |<span data-ttu-id="77fcb-229">A ID do recurso em que a operação ocorreu</span><span class="sxs-lookup"><span data-stu-id="77fcb-229">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="77fcb-230">categoria</span><span class="sxs-lookup"><span data-stu-id="77fcb-230">category</span></span> |<span data-ttu-id="77fcb-231">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-231">String</span></span> |<span data-ttu-id="77fcb-232">A categoria do log.</span><span class="sxs-lookup"><span data-stu-id="77fcb-232">The log category.</span></span> <span data-ttu-id="77fcb-233">Por exemplo, **Auditoria**.</span><span class="sxs-lookup"><span data-stu-id="77fcb-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="77fcb-234">operationName</span><span class="sxs-lookup"><span data-stu-id="77fcb-234">operationName</span></span> |<span data-ttu-id="77fcb-235">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-235">String</span></span> |<span data-ttu-id="77fcb-236">Nome da operação que está registrada.</span><span class="sxs-lookup"><span data-stu-id="77fcb-236">Name of the operation that is logged.</span></span> <span data-ttu-id="77fcb-237">Por exemplo, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="77fcb-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="77fcb-238">resultType</span><span class="sxs-lookup"><span data-stu-id="77fcb-238">resultType</span></span> |<span data-ttu-id="77fcb-239">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-239">String</span></span> |<span data-ttu-id="77fcb-240">O status da operação, por exemplo, 200.</span><span class="sxs-lookup"><span data-stu-id="77fcb-240">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="77fcb-241">correlationId</span><span class="sxs-lookup"><span data-stu-id="77fcb-241">correlationId</span></span> |<span data-ttu-id="77fcb-242">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-242">String</span></span> |<span data-ttu-id="77fcb-243">A ID do log que pode ser usada para agrupar um conjunto de entradas de log relacionadas</span><span class="sxs-lookup"><span data-stu-id="77fcb-243">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="77fcb-244">identidade</span><span class="sxs-lookup"><span data-stu-id="77fcb-244">identity</span></span> |<span data-ttu-id="77fcb-245">Objeto</span><span class="sxs-lookup"><span data-stu-id="77fcb-245">Object</span></span> |<span data-ttu-id="77fcb-246">A identidade que gerou o log</span><span class="sxs-lookup"><span data-stu-id="77fcb-246">The identity that generated the log</span></span> |
| <span data-ttu-id="77fcb-247">propriedades</span><span class="sxs-lookup"><span data-stu-id="77fcb-247">properties</span></span> |<span data-ttu-id="77fcb-248">JSON</span><span class="sxs-lookup"><span data-stu-id="77fcb-248">JSON</span></span> |<span data-ttu-id="77fcb-249">Confira abaixo para obter os detalhes</span><span class="sxs-lookup"><span data-stu-id="77fcb-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="77fcb-250">Esquema de propriedades do log de auditoria</span><span class="sxs-lookup"><span data-stu-id="77fcb-250">Audit log properties schema</span></span>
| <span data-ttu-id="77fcb-251">Name</span><span class="sxs-lookup"><span data-stu-id="77fcb-251">Name</span></span> | <span data-ttu-id="77fcb-252">Tipo</span><span class="sxs-lookup"><span data-stu-id="77fcb-252">Type</span></span> | <span data-ttu-id="77fcb-253">Descrição</span><span class="sxs-lookup"><span data-stu-id="77fcb-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77fcb-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="77fcb-254">StreamName</span></span> |<span data-ttu-id="77fcb-255">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="77fcb-255">String</span></span> |<span data-ttu-id="77fcb-256">O caminho em que a operação foi executada</span><span class="sxs-lookup"><span data-stu-id="77fcb-256">The path the operation was performed on</span></span> |

## <a name="samples-to-process-the-log-data"></a><span data-ttu-id="77fcb-257">Exemplos para processar os dados do log</span><span class="sxs-lookup"><span data-stu-id="77fcb-257">Samples to process the log data</span></span>
<span data-ttu-id="77fcb-258">O Azure Data Lake Store fornece um exemplo sobre como processar e analisar os dados do log.</span><span class="sxs-lookup"><span data-stu-id="77fcb-258">Azure Data Lake Store provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="77fcb-259">Você pode encontrar o exemplo em [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="77fcb-259">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="77fcb-260">Confira também</span><span class="sxs-lookup"><span data-stu-id="77fcb-260">See also</span></span>
* [<span data-ttu-id="77fcb-261">Visão geral do repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="77fcb-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="77fcb-262">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="77fcb-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

