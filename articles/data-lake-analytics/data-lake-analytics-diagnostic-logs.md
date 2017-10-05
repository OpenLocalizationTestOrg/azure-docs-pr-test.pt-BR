---
title: "Exibindo logs de diagnóstico para o Azure Data Lake Analytics | Microsoft Docs"
description: "Entenda como configurar e acessar os logs de diagnóstico do Azure Data Lake Analytics  "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 6c74db1659742aa41306388273bec46800ba7609
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="eca84-103">Acessando os logs de diagnóstico do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="eca84-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="eca84-104">O registro em log de diagnóstico permite que você colete as trilhas de auditoria de acesso a dados.</span><span class="sxs-lookup"><span data-stu-id="eca84-104">Diagnostic logging allows you to collect data access audit trails.</span></span> <span data-ttu-id="eca84-105">Esses logs fornecem informações como:</span><span class="sxs-lookup"><span data-stu-id="eca84-105">These logs provide information such as:</span></span>

* <span data-ttu-id="eca84-106">Uma lista de usuários que acessaram os dados.</span><span class="sxs-lookup"><span data-stu-id="eca84-106">A list of users that accessed the data.</span></span>
* <span data-ttu-id="eca84-107">Com que frequência os dados são acessados.</span><span class="sxs-lookup"><span data-stu-id="eca84-107">How frequently the data is accessed.</span></span>
* <span data-ttu-id="eca84-108">Quantos dados são armazenados na conta.</span><span class="sxs-lookup"><span data-stu-id="eca84-108">How much data is stored in the account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="eca84-109">Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="eca84-109">Enable logging</span></span>

1. <span data-ttu-id="eca84-110">Entre no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eca84-110">Sign on to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="eca84-111">Abra sua conta do Data Lake Analytics e selecione **Logs de diagnóstico** na seção __Monitorar__.</span><span class="sxs-lookup"><span data-stu-id="eca84-111">Open your Data Lake Analytics account and select **Diagnostic logs** from the __Monitor__ section.</span></span> <span data-ttu-id="eca84-112">Em seguida, selecione __Ativar o diagnóstico__.</span><span class="sxs-lookup"><span data-stu-id="eca84-112">Next, select __Turn on diagnostics__.</span></span>

    ![Ativar o diagnóstico para coletar logs de auditoria e de solicitações](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="eca84-114">Em __Configurações de diagnóstico__, defina o status como __Ativado__ e selecione as opções de registro em log.</span><span class="sxs-lookup"><span data-stu-id="eca84-114">From __Diagnostics settings__, set the status to __On__ and select logging options.</span></span>

    <span data-ttu-id="eca84-115">![Ativar o diagnóstico para coletar logs de auditoria e de solicitações](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Habilitar os logs de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="eca84-115">![Turn on diagnostics to collect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="eca84-116">Defina **Status** para **Ativado** para habilitar o log de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="eca84-116">Set **Status** to **On** to enable diagnostic logging.</span></span>

   * <span data-ttu-id="eca84-117">Você pode optar por armazenar/processar os dados de três maneiras diferentes.</span><span class="sxs-lookup"><span data-stu-id="eca84-117">You can choose to store/process the data in three different ways.</span></span>

     * <span data-ttu-id="eca84-118">Selecione __Arquivar em uma conta de armazenamento__ para armazenar os logs em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="eca84-118">Select __Archive to a storage account__ to store logs in an Azure storage account.</span></span> <span data-ttu-id="eca84-119">Use esta opção se quiser arquivar os dados.</span><span class="sxs-lookup"><span data-stu-id="eca84-119">Use this option if you want to archive the data.</span></span> <span data-ttu-id="eca84-120">Se escolher esta opção, você deverá fornecer uma conta de armazenamento do Azure para salvar os logs.</span><span class="sxs-lookup"><span data-stu-id="eca84-120">If you select this option, you must provide an Azure storage account to save the logs to.</span></span>

     * <span data-ttu-id="eca84-121">Selecione **Transmitir para um Hub de Eventos** para transmitir os dados de log para um Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="eca84-121">Select **Stream to an Event Hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="eca84-122">Use essa opção se tiver um pipeline de processamento downstream que esteja analisando logs de entrada em tempo real.</span><span class="sxs-lookup"><span data-stu-id="eca84-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="eca84-123">Se escolher esta opção, você deverá fornecer os detalhes no Hub de Eventos do Azure que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="eca84-123">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

     * <span data-ttu-id="eca84-124">Selecione __Enviar para o Log Analytics__ para enviar os dados ao serviço Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="eca84-124">Select __Send to Log Analytics__ to send the data to the Log Analytics service.</span></span> <span data-ttu-id="eca84-125">Use essa opção se você quiser usar o Log Analytics para coletar e analisar logs.</span><span class="sxs-lookup"><span data-stu-id="eca84-125">Use this option if you want to use Log Analytics to gather and analyze logs.</span></span>
   * <span data-ttu-id="eca84-126">Especifique se deseja obter os logs de auditoria, os logs de solicitação ou ambos.</span><span class="sxs-lookup"><span data-stu-id="eca84-126">Specify whether you want to get audit logs or request logs or both.</span></span>  <span data-ttu-id="eca84-127">Um log de solicitação captura todas as solicitações da API.</span><span class="sxs-lookup"><span data-stu-id="eca84-127">A request log captures every API request.</span></span> <span data-ttu-id="eca84-128">Um log de auditoria registra todas as operações disparadas pela solicitação de API.</span><span class="sxs-lookup"><span data-stu-id="eca84-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="eca84-129">Para __Arquivar para uma conta de armazenamento__, especifique o número de dias a reter os dados.</span><span class="sxs-lookup"><span data-stu-id="eca84-129">For __Archive to a storage account__, specify the number of days to retain the data.</span></span>

   * <span data-ttu-id="eca84-130">Clique em __Salvar__.</span><span class="sxs-lookup"><span data-stu-id="eca84-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="eca84-131">Selecione __Arquivar em uma conta de armazenamento__, __Transmitir para um Hub de Eventos__ ou __Enviar para o Log Analytics__ antes de clicar no botão __Salvar__.</span><span class="sxs-lookup"><span data-stu-id="eca84-131">You must select either __Archive to a storage account__, __Stream to an Event Hub__ or __Send to Log Analytics__ before clicking the __Save__ button.</span></span>

<span data-ttu-id="eca84-132">Depois de habilitar as configurações de diagnóstico, retorne à folha __Logs de diagnóstico__ para exibir os logs.</span><span class="sxs-lookup"><span data-stu-id="eca84-132">Once you have enabled diagnostic settings, you can return to the __Diagnostics logs__ blade to view the logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="eca84-133">Exibir logs</span><span class="sxs-lookup"><span data-stu-id="eca84-133">View logs</span></span>

### <a name="use-the-data-lake-analytics-view"></a><span data-ttu-id="eca84-134">Use a exibição do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="eca84-134">Use the Data Lake Analytics view</span></span>

1. <span data-ttu-id="eca84-135">Na folha de sua conta do Data Lake Analytics, em **Monitoramento**, selecione **Logs de Diagnóstico** e então selecione uma entrada para a qual exibir os logs.</span><span class="sxs-lookup"><span data-stu-id="eca84-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry to display logs for.</span></span>

    <span data-ttu-id="eca84-136">![Exibir logs de diagnóstico](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Exibir logs de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="eca84-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="eca84-137">Os logs são categorizados em **Logs de Auditoria** e **Logs de Solicitação**.</span><span class="sxs-lookup"><span data-stu-id="eca84-137">The logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![entradas de log](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="eca84-139">Os Logs de Solicitação capturam todas as solicitações de API feitas na conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="eca84-139">Request logs capture every API request made on the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="eca84-140">Logs de auditoria são semelhantes aos Logs de solicitação, mas fornecem uma análise muito mais detalhada das operações.</span><span class="sxs-lookup"><span data-stu-id="eca84-140">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations.</span></span> <span data-ttu-id="eca84-141">Por exemplo, uma única chamada à API de upload em um log de solicitação pode resultar em várias operações do tipo "Acréscimo" no log de auditoria.</span><span class="sxs-lookup"><span data-stu-id="eca84-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="eca84-142">Clique no link **Download** para uma entrada de log para baixar o log.</span><span class="sxs-lookup"><span data-stu-id="eca84-142">Click the **Download** link for a log entry to download that log.</span></span>

### <a name="use-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="eca84-143">Use a conta de Armazenamento do Azure que contém dados de log</span><span class="sxs-lookup"><span data-stu-id="eca84-143">Use the Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="eca84-144">Abra a folha Conta de Armazenamento do Azure associada ao Data Lake Analytics para registro em log e clique em __Blobs__.</span><span class="sxs-lookup"><span data-stu-id="eca84-144">Open the Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="eca84-145">A folha **serviço Blob** lista dois contêineres.</span><span class="sxs-lookup"><span data-stu-id="eca84-145">The **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="eca84-146">![Exibir logs de diagnóstico](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Exibir logs de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="eca84-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="eca84-147">O contêiner **insights-logs-audit** contém os logs de auditoria.</span><span class="sxs-lookup"><span data-stu-id="eca84-147">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="eca84-148">O contêiner **insights-logs-requests** contém os logs de solicitação.</span><span class="sxs-lookup"><span data-stu-id="eca84-148">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="eca84-149">Nesses contêineres, os logs são armazenados na estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="eca84-149">Within these containers, the logs are stored under the following structure:</span></span>

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > <span data-ttu-id="eca84-150">A folha `##` no caminho contêm o ano, o mês, o dia e a hora em que o log foi criado.</span><span class="sxs-lookup"><span data-stu-id="eca84-150">The `##` entries in the path contain the year, month, day, and hour in which the log was created.</span></span> <span data-ttu-id="eca84-151">O Data Lake Analytics cria um arquivo a cada hora e, portanto, o `m=` sempre conterá um valor `00`.</span><span class="sxs-lookup"><span data-stu-id="eca84-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="eca84-152">Como um exemplo, o caminho completo para um log de auditoria poderia ser:</span><span class="sxs-lookup"><span data-stu-id="eca84-152">As an example, the complete path to an audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="eca84-153">De modo semelhante, o caminho completo para um log de solicitação poderia ser:</span><span class="sxs-lookup"><span data-stu-id="eca84-153">Similarly, the complete path to a request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="eca84-154">Estrutura de log</span><span class="sxs-lookup"><span data-stu-id="eca84-154">Log structure</span></span>

<span data-ttu-id="eca84-155">Os logs de auditoria e solicitação estão em um formato JSON estruturado.</span><span class="sxs-lookup"><span data-stu-id="eca84-155">The audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="eca84-156">Logs de Solicitação</span><span class="sxs-lookup"><span data-stu-id="eca84-156">Request logs</span></span>

<span data-ttu-id="eca84-157">Aqui está um exemplo de entrada no log de solicitação formatado em JSON.</span><span class="sxs-lookup"><span data-stu-id="eca84-157">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="eca84-158">Cada blob tem um objeto-raiz chamado **registros** que contém uma matriz de objetos do log.</span><span class="sxs-lookup"><span data-stu-id="eca84-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="eca84-159">Esquema do log de solicitação</span><span class="sxs-lookup"><span data-stu-id="eca84-159">Request log schema</span></span>

| <span data-ttu-id="eca84-160">Name</span><span class="sxs-lookup"><span data-stu-id="eca84-160">Name</span></span> | <span data-ttu-id="eca84-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="eca84-161">Type</span></span> | <span data-ttu-id="eca84-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="eca84-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eca84-163">tempo real</span><span class="sxs-lookup"><span data-stu-id="eca84-163">time</span></span> |<span data-ttu-id="eca84-164">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-164">String</span></span> |<span data-ttu-id="eca84-165">O carimbo de data/hora (em UTC) do log</span><span class="sxs-lookup"><span data-stu-id="eca84-165">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="eca84-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="eca84-166">resourceId</span></span> |<span data-ttu-id="eca84-167">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-167">String</span></span> |<span data-ttu-id="eca84-168">O identificador do recurso em que a operação ocorreu</span><span class="sxs-lookup"><span data-stu-id="eca84-168">The identifier of the resource that operation took place on</span></span> |
| <span data-ttu-id="eca84-169">categoria</span><span class="sxs-lookup"><span data-stu-id="eca84-169">category</span></span> |<span data-ttu-id="eca84-170">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-170">String</span></span> |<span data-ttu-id="eca84-171">A categoria do log.</span><span class="sxs-lookup"><span data-stu-id="eca84-171">The log category.</span></span> <span data-ttu-id="eca84-172">Por exemplo, **Solicitações**.</span><span class="sxs-lookup"><span data-stu-id="eca84-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="eca84-173">operationName</span><span class="sxs-lookup"><span data-stu-id="eca84-173">operationName</span></span> |<span data-ttu-id="eca84-174">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-174">String</span></span> |<span data-ttu-id="eca84-175">Nome da operação que está registrada.</span><span class="sxs-lookup"><span data-stu-id="eca84-175">Name of the operation that is logged.</span></span> <span data-ttu-id="eca84-176">Por exemplo, GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="eca84-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="eca84-177">resultType</span><span class="sxs-lookup"><span data-stu-id="eca84-177">resultType</span></span> |<span data-ttu-id="eca84-178">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-178">String</span></span> |<span data-ttu-id="eca84-179">O status da operação, por exemplo, 200.</span><span class="sxs-lookup"><span data-stu-id="eca84-179">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="eca84-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="eca84-180">callerIpAddress</span></span> |<span data-ttu-id="eca84-181">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-181">String</span></span> |<span data-ttu-id="eca84-182">O endereço IP do cliente que está fazendo a solicitação</span><span class="sxs-lookup"><span data-stu-id="eca84-182">The IP address of the client making the request</span></span> |
| <span data-ttu-id="eca84-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="eca84-183">correlationId</span></span> |<span data-ttu-id="eca84-184">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-184">String</span></span> |<span data-ttu-id="eca84-185">O identificador do log.</span><span class="sxs-lookup"><span data-stu-id="eca84-185">The identifier of the log.</span></span> <span data-ttu-id="eca84-186">Esse valor pode ser usado para agrupar um conjunto de entradas de log relacionadas.</span><span class="sxs-lookup"><span data-stu-id="eca84-186">This value can be used to group a set of related log entries.</span></span> |
| <span data-ttu-id="eca84-187">identidade</span><span class="sxs-lookup"><span data-stu-id="eca84-187">identity</span></span> |<span data-ttu-id="eca84-188">Objeto</span><span class="sxs-lookup"><span data-stu-id="eca84-188">Object</span></span> |<span data-ttu-id="eca84-189">A identidade que gerou o log</span><span class="sxs-lookup"><span data-stu-id="eca84-189">The identity that generated the log</span></span> |
| <span data-ttu-id="eca84-190">propriedades</span><span class="sxs-lookup"><span data-stu-id="eca84-190">properties</span></span> |<span data-ttu-id="eca84-191">JSON</span><span class="sxs-lookup"><span data-stu-id="eca84-191">JSON</span></span> |<span data-ttu-id="eca84-192">Veja a próxima seção (Esquema de propriedades do log de solicitação) para obter detalhes</span><span class="sxs-lookup"><span data-stu-id="eca84-192">See the next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="eca84-193">Esquema de propriedades do log de solicitação</span><span class="sxs-lookup"><span data-stu-id="eca84-193">Request log properties schema</span></span>

| <span data-ttu-id="eca84-194">Name</span><span class="sxs-lookup"><span data-stu-id="eca84-194">Name</span></span> | <span data-ttu-id="eca84-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="eca84-195">Type</span></span> | <span data-ttu-id="eca84-196">Descrição</span><span class="sxs-lookup"><span data-stu-id="eca84-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eca84-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="eca84-197">HttpMethod</span></span> |<span data-ttu-id="eca84-198">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-198">String</span></span> |<span data-ttu-id="eca84-199">O método HTTP usado para a operação.</span><span class="sxs-lookup"><span data-stu-id="eca84-199">The HTTP Method used for the operation.</span></span> <span data-ttu-id="eca84-200">Por exemplo, GET.</span><span class="sxs-lookup"><span data-stu-id="eca84-200">For example, GET.</span></span> |
| <span data-ttu-id="eca84-201">Caminho</span><span class="sxs-lookup"><span data-stu-id="eca84-201">Path</span></span> |<span data-ttu-id="eca84-202">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-202">String</span></span> |<span data-ttu-id="eca84-203">O caminho em que a operação foi executada</span><span class="sxs-lookup"><span data-stu-id="eca84-203">The path the operation was performed on</span></span> |
| <span data-ttu-id="eca84-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="eca84-204">RequestContentLength</span></span> |<span data-ttu-id="eca84-205">int</span><span class="sxs-lookup"><span data-stu-id="eca84-205">int</span></span> |<span data-ttu-id="eca84-206">O comprimento do conteúdo da solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="eca84-206">The content length of the HTTP request</span></span> |
| <span data-ttu-id="eca84-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="eca84-207">ClientRequestId</span></span> |<span data-ttu-id="eca84-208">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-208">String</span></span> |<span data-ttu-id="eca84-209">O identificador que identifica essa solicitação com exclusividade</span><span class="sxs-lookup"><span data-stu-id="eca84-209">The identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="eca84-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="eca84-210">StartTime</span></span> |<span data-ttu-id="eca84-211">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-211">String</span></span> |<span data-ttu-id="eca84-212">A hora em que o servidor recebeu a solicitação</span><span class="sxs-lookup"><span data-stu-id="eca84-212">The time at which the server received the request</span></span> |
| <span data-ttu-id="eca84-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="eca84-213">EndTime</span></span> |<span data-ttu-id="eca84-214">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-214">String</span></span> |<span data-ttu-id="eca84-215">A hora em que o servidor enviou uma resposta</span><span class="sxs-lookup"><span data-stu-id="eca84-215">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="eca84-216">Logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="eca84-216">Audit logs</span></span>

<span data-ttu-id="eca84-217">Aqui está um exemplo de entrada no log de auditoria formatado em JSON.</span><span class="sxs-lookup"><span data-stu-id="eca84-217">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="eca84-218">Cada blob tem um objeto-raiz chamado **registros** que contém uma matriz de objetos do log.</span><span class="sxs-lookup"><span data-stu-id="eca84-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="eca84-219">Esquema do log de auditoria</span><span class="sxs-lookup"><span data-stu-id="eca84-219">Audit log schema</span></span>

| <span data-ttu-id="eca84-220">Name</span><span class="sxs-lookup"><span data-stu-id="eca84-220">Name</span></span> | <span data-ttu-id="eca84-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="eca84-221">Type</span></span> | <span data-ttu-id="eca84-222">Descrição</span><span class="sxs-lookup"><span data-stu-id="eca84-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eca84-223">tempo real</span><span class="sxs-lookup"><span data-stu-id="eca84-223">time</span></span> |<span data-ttu-id="eca84-224">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-224">String</span></span> |<span data-ttu-id="eca84-225">O carimbo de data/hora (em UTC) do log</span><span class="sxs-lookup"><span data-stu-id="eca84-225">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="eca84-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="eca84-226">resourceId</span></span> |<span data-ttu-id="eca84-227">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-227">String</span></span> |<span data-ttu-id="eca84-228">O identificador do recurso em que a operação ocorreu</span><span class="sxs-lookup"><span data-stu-id="eca84-228">The identifier of the resource that operation took place on</span></span> |
| <span data-ttu-id="eca84-229">categoria</span><span class="sxs-lookup"><span data-stu-id="eca84-229">category</span></span> |<span data-ttu-id="eca84-230">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-230">String</span></span> |<span data-ttu-id="eca84-231">A categoria do log.</span><span class="sxs-lookup"><span data-stu-id="eca84-231">The log category.</span></span> <span data-ttu-id="eca84-232">Por exemplo, **Auditoria**.</span><span class="sxs-lookup"><span data-stu-id="eca84-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="eca84-233">operationName</span><span class="sxs-lookup"><span data-stu-id="eca84-233">operationName</span></span> |<span data-ttu-id="eca84-234">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-234">String</span></span> |<span data-ttu-id="eca84-235">Nome da operação que está registrada.</span><span class="sxs-lookup"><span data-stu-id="eca84-235">Name of the operation that is logged.</span></span> <span data-ttu-id="eca84-236">Por exemplo, JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="eca84-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="eca84-237">resultType</span><span class="sxs-lookup"><span data-stu-id="eca84-237">resultType</span></span> |<span data-ttu-id="eca84-238">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-238">String</span></span> |<span data-ttu-id="eca84-239">Um substatus para o status do trabalho (operationName).</span><span class="sxs-lookup"><span data-stu-id="eca84-239">A substatus for the job status (operationName).</span></span> |
| <span data-ttu-id="eca84-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="eca84-240">resultSignature</span></span> |<span data-ttu-id="eca84-241">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-241">String</span></span> |<span data-ttu-id="eca84-242">Detalhes adicionais sobre o status do trabalho (operationName).</span><span class="sxs-lookup"><span data-stu-id="eca84-242">Additional details on the job status (operationName).</span></span> |
| <span data-ttu-id="eca84-243">identidade</span><span class="sxs-lookup"><span data-stu-id="eca84-243">identity</span></span> |<span data-ttu-id="eca84-244">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-244">String</span></span> |<span data-ttu-id="eca84-245">O usuário que solicitou a operação.</span><span class="sxs-lookup"><span data-stu-id="eca84-245">The user that requested the operation.</span></span> <span data-ttu-id="eca84-246">Por exemplo: susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="eca84-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="eca84-247">propriedades</span><span class="sxs-lookup"><span data-stu-id="eca84-247">properties</span></span> |<span data-ttu-id="eca84-248">JSON</span><span class="sxs-lookup"><span data-stu-id="eca84-248">JSON</span></span> |<span data-ttu-id="eca84-249">Veja a próxima seção (Esquema de propriedades do log de auditoria) para obter detalhes</span><span class="sxs-lookup"><span data-stu-id="eca84-249">See the next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="eca84-250">**resultType** e **resultSignature** fornecem informações sobre o resultado de uma operação e conter apenas um valor caso uma operação tenha sido concluída.</span><span class="sxs-lookup"><span data-stu-id="eca84-250">**resultType** and **resultSignature** provide information on the result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="eca84-251">Por exemplo, eles contêm um valor somente quando **operationName** contém um valor **JobStarted** ou **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="eca84-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="eca84-252">Esquema de propriedades do log de auditoria</span><span class="sxs-lookup"><span data-stu-id="eca84-252">Audit log properties schema</span></span>

| <span data-ttu-id="eca84-253">Name</span><span class="sxs-lookup"><span data-stu-id="eca84-253">Name</span></span> | <span data-ttu-id="eca84-254">Tipo</span><span class="sxs-lookup"><span data-stu-id="eca84-254">Type</span></span> | <span data-ttu-id="eca84-255">Descrição</span><span class="sxs-lookup"><span data-stu-id="eca84-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eca84-256">JobId</span><span class="sxs-lookup"><span data-stu-id="eca84-256">JobId</span></span> |<span data-ttu-id="eca84-257">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-257">String</span></span> |<span data-ttu-id="eca84-258">A ID atribuída ao trabalho</span><span class="sxs-lookup"><span data-stu-id="eca84-258">The ID assigned to the job</span></span> |
| <span data-ttu-id="eca84-259">JobName</span><span class="sxs-lookup"><span data-stu-id="eca84-259">JobName</span></span> |<span data-ttu-id="eca84-260">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-260">String</span></span> |<span data-ttu-id="eca84-261">O nome fornecido para o trabalho</span><span class="sxs-lookup"><span data-stu-id="eca84-261">The name that was provided for the job</span></span> |
| <span data-ttu-id="eca84-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="eca84-262">JobRunTime</span></span> |<span data-ttu-id="eca84-263">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-263">String</span></span> |<span data-ttu-id="eca84-264">O tempo de execução usado para processar o trabalho</span><span class="sxs-lookup"><span data-stu-id="eca84-264">The runtime used to process the job</span></span> |
| <span data-ttu-id="eca84-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="eca84-265">SubmitTime</span></span> |<span data-ttu-id="eca84-266">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-266">String</span></span> |<span data-ttu-id="eca84-267">A hora (em UTC) em que o trabalho foi enviado</span><span class="sxs-lookup"><span data-stu-id="eca84-267">The time (in UTC) that the job was submitted</span></span> |
| <span data-ttu-id="eca84-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="eca84-268">StartTime</span></span> |<span data-ttu-id="eca84-269">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-269">String</span></span> |<span data-ttu-id="eca84-270">A hora em que o trabalho começou a ser executado após o envio (em UTC)</span><span class="sxs-lookup"><span data-stu-id="eca84-270">The time the job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="eca84-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="eca84-271">EndTime</span></span> |<span data-ttu-id="eca84-272">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-272">String</span></span> |<span data-ttu-id="eca84-273">A hora em que o trabalho foi concluído</span><span class="sxs-lookup"><span data-stu-id="eca84-273">The time the job ended</span></span> |
| <span data-ttu-id="eca84-274">Paralelismo</span><span class="sxs-lookup"><span data-stu-id="eca84-274">Parallelism</span></span> |<span data-ttu-id="eca84-275">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eca84-275">String</span></span> |<span data-ttu-id="eca84-276">O número de unidades do Data Lake Analytics solicitadas para esse trabalho durante o envio</span><span class="sxs-lookup"><span data-stu-id="eca84-276">The number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="eca84-277">**SubmitTime**, **StartTime**, **EndTime** e **Parallelism** fornecem informações sobre uma operação.</span><span class="sxs-lookup"><span data-stu-id="eca84-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="eca84-278">Essas entradas contêm um valor apenas se operação tiver sido iniciada ou concluída.</span><span class="sxs-lookup"><span data-stu-id="eca84-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="eca84-279">Por exemplo, **SubmitTime** somente contém um valor após **operationName** ter o valor **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="eca84-279">For example, **SubmitTime** only contains a value after **operationName** has the value **JobSubmitted**.</span></span>

## <a name="process-the-log-data"></a><span data-ttu-id="eca84-280">Processar os dados de log</span><span class="sxs-lookup"><span data-stu-id="eca84-280">Process the log data</span></span>

<span data-ttu-id="eca84-281">O Azure Data Lake Analytics fornece um exemplo sobre como processar e analisar os dados do log.</span><span class="sxs-lookup"><span data-stu-id="eca84-281">Azure Data Lake Analytics provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="eca84-282">Você pode encontrar o exemplo em [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="eca84-282">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eca84-283">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eca84-283">Next steps</span></span>
* [<span data-ttu-id="eca84-284">Visão geral do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="eca84-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
