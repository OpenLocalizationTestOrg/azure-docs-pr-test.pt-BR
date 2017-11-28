---
title: "logs de diagnóstico aaaViewing para análise do Azure Data Lake | Microsoft Docs"
description: "Entender como toosetup e acesso diagnóstico logs de dados do Azure análise Lake "
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
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="1293f-103">Acessando os logs de diagnóstico do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1293f-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="1293f-104">Log de diagnóstico permite toocollect trilhas de auditoria de acesso de dados.</span><span class="sxs-lookup"><span data-stu-id="1293f-104">Diagnostic logging allows you toocollect data access audit trails.</span></span> <span data-ttu-id="1293f-105">Esses logs fornecem informações como:</span><span class="sxs-lookup"><span data-stu-id="1293f-105">These logs provide information such as:</span></span>

* <span data-ttu-id="1293f-106">Uma lista de usuários que Olá dados acessados.</span><span class="sxs-lookup"><span data-stu-id="1293f-106">A list of users that accessed hello data.</span></span>
* <span data-ttu-id="1293f-107">A frequência com dados saudação são acessados.</span><span class="sxs-lookup"><span data-stu-id="1293f-107">How frequently hello data is accessed.</span></span>
* <span data-ttu-id="1293f-108">A quantidade de dados é armazenado na conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="1293f-108">How much data is stored in hello account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="1293f-109">Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="1293f-109">Enable logging</span></span>

1. <span data-ttu-id="1293f-110">Logon toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1293f-110">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="1293f-111">Abra sua conta da análise Data Lake e selecione **logs de diagnóstico** de saudação __Monitor__ seção.</span><span class="sxs-lookup"><span data-stu-id="1293f-111">Open your Data Lake Analytics account and select **Diagnostic logs** from hello __Monitor__ section.</span></span> <span data-ttu-id="1293f-112">Em seguida, selecione __Ativar o diagnóstico__.</span><span class="sxs-lookup"><span data-stu-id="1293f-112">Next, select __Turn on diagnostics__.</span></span>

    ![Ativar diagnóstico toocollect auditoria e logs de solicitação](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="1293f-114">De __as configurações de diagnóstico__, defina Olá status too__On__ e selecione as opções de log.</span><span class="sxs-lookup"><span data-stu-id="1293f-114">From __Diagnostics settings__, set hello status too__On__ and select logging options.</span></span>

    <span data-ttu-id="1293f-115">![Ativar diagnóstico toocollect auditoria e logs de solicitação](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "habilitar logs de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="1293f-115">![Turn on diagnostics toocollect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="1293f-116">Definir **Status** muito**na** tooenable log de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="1293f-116">Set **Status** too**On** tooenable diagnostic logging.</span></span>

   * <span data-ttu-id="1293f-117">Você pode escolher dados saudação toostore/processo de três maneiras diferentes.</span><span class="sxs-lookup"><span data-stu-id="1293f-117">You can choose toostore/process hello data in three different ways.</span></span>

     * <span data-ttu-id="1293f-118">Selecione __tooa conta de armazenamento de arquivos__ toostore logs em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1293f-118">Select __Archive tooa storage account__ toostore logs in an Azure storage account.</span></span> <span data-ttu-id="1293f-119">Use esta opção se você quiser tooarchive Olá dados.</span><span class="sxs-lookup"><span data-stu-id="1293f-119">Use this option if you want tooarchive hello data.</span></span> <span data-ttu-id="1293f-120">Se você selecionar essa opção, você deve fornecer um armazenamento do Azure conta toosave Olá os logs para.</span><span class="sxs-lookup"><span data-stu-id="1293f-120">If you select this option, you must provide an Azure storage account toosave hello logs to.</span></span>

     * <span data-ttu-id="1293f-121">Selecione **tooan Hub de eventos de fluxo** toostream log dados tooan Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1293f-121">Select **Stream tooan Event Hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="1293f-122">Use essa opção se tiver um pipeline de processamento downstream que esteja analisando logs de entrada em tempo real.</span><span class="sxs-lookup"><span data-stu-id="1293f-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="1293f-123">Se você selecionar essa opção, você deve fornecer detalhes de saudação para Olá Hub de eventos do Azure você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="1293f-123">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

     * <span data-ttu-id="1293f-124">Selecione __enviar tooLog análise__ toosend Olá dados toohello serviço de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="1293f-124">Select __Send tooLog Analytics__ toosend hello data toohello Log Analytics service.</span></span> <span data-ttu-id="1293f-125">Use esta opção se você quiser toouse toogather de análise de Log e analise logs.</span><span class="sxs-lookup"><span data-stu-id="1293f-125">Use this option if you want toouse Log Analytics toogather and analyze logs.</span></span>
   * <span data-ttu-id="1293f-126">Especifique se deseja que os logs de auditoria tooget ou logs de solicitação ou ambos.</span><span class="sxs-lookup"><span data-stu-id="1293f-126">Specify whether you want tooget audit logs or request logs or both.</span></span>  <span data-ttu-id="1293f-127">Um log de solicitação captura todas as solicitações da API.</span><span class="sxs-lookup"><span data-stu-id="1293f-127">A request log captures every API request.</span></span> <span data-ttu-id="1293f-128">Um log de auditoria registra todas as operações disparadas pela solicitação de API.</span><span class="sxs-lookup"><span data-stu-id="1293f-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="1293f-129">Para __tooa conta de armazenamento de arquivos__, especifique Olá número de dados de saudação tooretain dias.</span><span class="sxs-lookup"><span data-stu-id="1293f-129">For __Archive tooa storage account__, specify hello number of days tooretain hello data.</span></span>

   * <span data-ttu-id="1293f-130">Clique em __Salvar__.</span><span class="sxs-lookup"><span data-stu-id="1293f-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="1293f-131">Você deve selecionar __tooa conta de armazenamento de arquivos__, __tooan Hub de eventos de fluxo__ ou __enviar tooLog análise__ antes de clicar em Olá __salvar__botão.</span><span class="sxs-lookup"><span data-stu-id="1293f-131">You must select either __Archive tooa storage account__, __Stream tooan Event Hub__ or __Send tooLog Analytics__ before clicking hello __Save__ button.</span></span>

<span data-ttu-id="1293f-132">Depois que você habilitou as configurações de diagnóstico, você pode retornar toohello __logs de diagnóstico__ folha tooview Olá logs.</span><span class="sxs-lookup"><span data-stu-id="1293f-132">Once you have enabled diagnostic settings, you can return toohello __Diagnostics logs__ blade tooview hello logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="1293f-133">Exibir logs</span><span class="sxs-lookup"><span data-stu-id="1293f-133">View logs</span></span>

### <a name="use-hello-data-lake-analytics-view"></a><span data-ttu-id="1293f-134">Usar exibição da análise Data Lake Olá</span><span class="sxs-lookup"><span data-stu-id="1293f-134">Use hello Data Lake Analytics view</span></span>

1. <span data-ttu-id="1293f-135">De sua análise Data Lake conta folha, em **monitoramento**, selecione **Logs de diagnóstico** e, em seguida, selecione uma entrada toodisplay logs para.</span><span class="sxs-lookup"><span data-stu-id="1293f-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry toodisplay logs for.</span></span>

    <span data-ttu-id="1293f-136">![Exibir logs de diagnóstico](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Exibir logs de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="1293f-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="1293f-137">Olá logs são categorizados por **os Logs de auditoria** e **os Logs de solicitação**.</span><span class="sxs-lookup"><span data-stu-id="1293f-137">hello logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![entradas de log](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="1293f-139">Logs de solicitação de captura todas as solicitações de API feitas em Olá conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1293f-139">Request logs capture every API request made on hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="1293f-140">Logs de auditoria são os Logs de toorequest semelhantes, mas fornecem uma análise mais detalhada das operações de saudação.</span><span class="sxs-lookup"><span data-stu-id="1293f-140">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations.</span></span> <span data-ttu-id="1293f-141">Por exemplo, uma única chamada à API de upload em um log de solicitação pode resultar em várias operações do tipo "Acréscimo" no log de auditoria.</span><span class="sxs-lookup"><span data-stu-id="1293f-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="1293f-142">Clique em Olá **baixar** link para um toodownload de entrada de registro de log.</span><span class="sxs-lookup"><span data-stu-id="1293f-142">Click hello **Download** link for a log entry toodownload that log.</span></span>

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="1293f-143">Usar conta de armazenamento do Azure Olá que contém dados de log</span><span class="sxs-lookup"><span data-stu-id="1293f-143">Use hello Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="1293f-144">Abra a folha de conta de armazenamento do Azure Olá associada análise Data Lake para registro em log e, em seguida, clique em __Blobs__.</span><span class="sxs-lookup"><span data-stu-id="1293f-144">Open hello Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="1293f-145">Olá **do serviço Blob** folha lista dois contêineres.</span><span class="sxs-lookup"><span data-stu-id="1293f-145">hello **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="1293f-146">![Exibir logs de diagnóstico](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Exibir logs de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="1293f-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="1293f-147">contêiner de saudação **insights de logs de auditoria** contém logs de auditoria de saudação.</span><span class="sxs-lookup"><span data-stu-id="1293f-147">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="1293f-148">contêiner de saudação **insights de logs de solicitações** contém logs de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1293f-148">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="1293f-149">Dentro desses contêineres, Olá logs são armazenados em Olá estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="1293f-149">Within these containers, hello logs are stored under hello following structure:</span></span>

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
   > <span data-ttu-id="1293f-150">Olá `##` entradas no caminho de saudação contêm ano hello, mês, dia e hora na qual Olá log foi criado.</span><span class="sxs-lookup"><span data-stu-id="1293f-150">hello `##` entries in hello path contain hello year, month, day, and hour in which hello log was created.</span></span> <span data-ttu-id="1293f-151">O Data Lake Analytics cria um arquivo a cada hora e, portanto, o `m=` sempre conterá um valor `00`.</span><span class="sxs-lookup"><span data-stu-id="1293f-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="1293f-152">Por exemplo, log de auditoria do hello caminho completo tooan poderia ser:</span><span class="sxs-lookup"><span data-stu-id="1293f-152">As an example, hello complete path tooan audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="1293f-153">Da mesma forma, o log de solicitações de tooa de caminho completo de saudação poderia ser:</span><span class="sxs-lookup"><span data-stu-id="1293f-153">Similarly, hello complete path tooa request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="1293f-154">Estrutura de log</span><span class="sxs-lookup"><span data-stu-id="1293f-154">Log structure</span></span>

<span data-ttu-id="1293f-155">Olá logs de auditoria e de solicitação estão em um formato JSON estruturado.</span><span class="sxs-lookup"><span data-stu-id="1293f-155">hello audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="1293f-156">Logs de Solicitação</span><span class="sxs-lookup"><span data-stu-id="1293f-156">Request logs</span></span>

<span data-ttu-id="1293f-157">Aqui está um exemplo de entrada no log de solicitação formatada em JSON hello.</span><span class="sxs-lookup"><span data-stu-id="1293f-157">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="1293f-158">Cada blob tem um objeto-raiz chamado **registros** que contém uma matriz de objetos do log.</span><span class="sxs-lookup"><span data-stu-id="1293f-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="request-log-schema"></a><span data-ttu-id="1293f-159">Esquema do log de solicitação</span><span class="sxs-lookup"><span data-stu-id="1293f-159">Request log schema</span></span>

| <span data-ttu-id="1293f-160">Name</span><span class="sxs-lookup"><span data-stu-id="1293f-160">Name</span></span> | <span data-ttu-id="1293f-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="1293f-161">Type</span></span> | <span data-ttu-id="1293f-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="1293f-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1293f-163">tempo real</span><span class="sxs-lookup"><span data-stu-id="1293f-163">time</span></span> |<span data-ttu-id="1293f-164">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-164">String</span></span> |<span data-ttu-id="1293f-165">Olá carimbo de hora (UTC) do log de saudação</span><span class="sxs-lookup"><span data-stu-id="1293f-165">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="1293f-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="1293f-166">resourceId</span></span> |<span data-ttu-id="1293f-167">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-167">String</span></span> |<span data-ttu-id="1293f-168">Identificador de saudação do recurso de saudação que levou operação colocar em</span><span class="sxs-lookup"><span data-stu-id="1293f-168">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="1293f-169">categoria</span><span class="sxs-lookup"><span data-stu-id="1293f-169">category</span></span> |<span data-ttu-id="1293f-170">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-170">String</span></span> |<span data-ttu-id="1293f-171">categoria do log de saudação.</span><span class="sxs-lookup"><span data-stu-id="1293f-171">hello log category.</span></span> <span data-ttu-id="1293f-172">Por exemplo, **Solicitações**.</span><span class="sxs-lookup"><span data-stu-id="1293f-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="1293f-173">operationName</span><span class="sxs-lookup"><span data-stu-id="1293f-173">operationName</span></span> |<span data-ttu-id="1293f-174">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-174">String</span></span> |<span data-ttu-id="1293f-175">Nome da operação de saudação que é registrada.</span><span class="sxs-lookup"><span data-stu-id="1293f-175">Name of hello operation that is logged.</span></span> <span data-ttu-id="1293f-176">Por exemplo, GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="1293f-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="1293f-177">resultType</span><span class="sxs-lookup"><span data-stu-id="1293f-177">resultType</span></span> |<span data-ttu-id="1293f-178">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-178">String</span></span> |<span data-ttu-id="1293f-179">status de saudação da operação de hello, por exemplo, 200.</span><span class="sxs-lookup"><span data-stu-id="1293f-179">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="1293f-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="1293f-180">callerIpAddress</span></span> |<span data-ttu-id="1293f-181">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-181">String</span></span> |<span data-ttu-id="1293f-182">endereço IP de saudação do cliente de saudação fazer solicitação Olá</span><span class="sxs-lookup"><span data-stu-id="1293f-182">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="1293f-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="1293f-183">correlationId</span></span> |<span data-ttu-id="1293f-184">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-184">String</span></span> |<span data-ttu-id="1293f-185">Identificador de saudação do log hello.</span><span class="sxs-lookup"><span data-stu-id="1293f-185">hello identifier of hello log.</span></span> <span data-ttu-id="1293f-186">Esse valor pode ser usado toogroup um conjunto de entradas de log relacionadas.</span><span class="sxs-lookup"><span data-stu-id="1293f-186">This value can be used toogroup a set of related log entries.</span></span> |
| <span data-ttu-id="1293f-187">identidade</span><span class="sxs-lookup"><span data-stu-id="1293f-187">identity</span></span> |<span data-ttu-id="1293f-188">Objeto</span><span class="sxs-lookup"><span data-stu-id="1293f-188">Object</span></span> |<span data-ttu-id="1293f-189">identidade de saudação que gerou o log de saudação</span><span class="sxs-lookup"><span data-stu-id="1293f-189">hello identity that generated hello log</span></span> |
| <span data-ttu-id="1293f-190">propriedades</span><span class="sxs-lookup"><span data-stu-id="1293f-190">properties</span></span> |<span data-ttu-id="1293f-191">JSON</span><span class="sxs-lookup"><span data-stu-id="1293f-191">JSON</span></span> |<span data-ttu-id="1293f-192">Consulte Olá próxima seção (esquema de propriedades de log de solicitação) para obter detalhes</span><span class="sxs-lookup"><span data-stu-id="1293f-192">See hello next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="1293f-193">Esquema de propriedades do log de solicitação</span><span class="sxs-lookup"><span data-stu-id="1293f-193">Request log properties schema</span></span>

| <span data-ttu-id="1293f-194">Name</span><span class="sxs-lookup"><span data-stu-id="1293f-194">Name</span></span> | <span data-ttu-id="1293f-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="1293f-195">Type</span></span> | <span data-ttu-id="1293f-196">Descrição</span><span class="sxs-lookup"><span data-stu-id="1293f-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1293f-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="1293f-197">HttpMethod</span></span> |<span data-ttu-id="1293f-198">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-198">String</span></span> |<span data-ttu-id="1293f-199">Olá método HTTP usado para operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1293f-199">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="1293f-200">Por exemplo, GET.</span><span class="sxs-lookup"><span data-stu-id="1293f-200">For example, GET.</span></span> |
| <span data-ttu-id="1293f-201">Caminho</span><span class="sxs-lookup"><span data-stu-id="1293f-201">Path</span></span> |<span data-ttu-id="1293f-202">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-202">String</span></span> |<span data-ttu-id="1293f-203">Olá caminho Olá operação foi executada em</span><span class="sxs-lookup"><span data-stu-id="1293f-203">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="1293f-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="1293f-204">RequestContentLength</span></span> |<span data-ttu-id="1293f-205">int</span><span class="sxs-lookup"><span data-stu-id="1293f-205">int</span></span> |<span data-ttu-id="1293f-206">comprimento do conteúdo da solicitação HTTP de saudação Olá</span><span class="sxs-lookup"><span data-stu-id="1293f-206">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="1293f-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="1293f-207">ClientRequestId</span></span> |<span data-ttu-id="1293f-208">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-208">String</span></span> |<span data-ttu-id="1293f-209">Olá identificador que identifica exclusivamente esta solicitação</span><span class="sxs-lookup"><span data-stu-id="1293f-209">hello identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="1293f-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="1293f-210">StartTime</span></span> |<span data-ttu-id="1293f-211">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-211">String</span></span> |<span data-ttu-id="1293f-212">tempo de saudação na qual solicitação de Olá Olá recebido do servidor</span><span class="sxs-lookup"><span data-stu-id="1293f-212">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="1293f-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="1293f-213">EndTime</span></span> |<span data-ttu-id="1293f-214">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-214">String</span></span> |<span data-ttu-id="1293f-215">tempo de saudação no qual Olá servidor enviou uma resposta</span><span class="sxs-lookup"><span data-stu-id="1293f-215">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="1293f-216">Logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="1293f-216">Audit logs</span></span>

<span data-ttu-id="1293f-217">Aqui está um exemplo de entrada no log de auditoria formatada em JSON hello.</span><span class="sxs-lookup"><span data-stu-id="1293f-217">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="1293f-218">Cada blob tem um objeto-raiz chamado **registros** que contém uma matriz de objetos do log.</span><span class="sxs-lookup"><span data-stu-id="1293f-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="audit-log-schema"></a><span data-ttu-id="1293f-219">Esquema do log de auditoria</span><span class="sxs-lookup"><span data-stu-id="1293f-219">Audit log schema</span></span>

| <span data-ttu-id="1293f-220">Name</span><span class="sxs-lookup"><span data-stu-id="1293f-220">Name</span></span> | <span data-ttu-id="1293f-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="1293f-221">Type</span></span> | <span data-ttu-id="1293f-222">Descrição</span><span class="sxs-lookup"><span data-stu-id="1293f-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1293f-223">tempo real</span><span class="sxs-lookup"><span data-stu-id="1293f-223">time</span></span> |<span data-ttu-id="1293f-224">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-224">String</span></span> |<span data-ttu-id="1293f-225">Olá carimbo de hora (UTC) do log de saudação</span><span class="sxs-lookup"><span data-stu-id="1293f-225">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="1293f-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="1293f-226">resourceId</span></span> |<span data-ttu-id="1293f-227">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-227">String</span></span> |<span data-ttu-id="1293f-228">Identificador de saudação do recurso de saudação que levou operação colocar em</span><span class="sxs-lookup"><span data-stu-id="1293f-228">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="1293f-229">categoria</span><span class="sxs-lookup"><span data-stu-id="1293f-229">category</span></span> |<span data-ttu-id="1293f-230">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-230">String</span></span> |<span data-ttu-id="1293f-231">categoria do log de saudação.</span><span class="sxs-lookup"><span data-stu-id="1293f-231">hello log category.</span></span> <span data-ttu-id="1293f-232">Por exemplo, **Auditoria**.</span><span class="sxs-lookup"><span data-stu-id="1293f-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="1293f-233">operationName</span><span class="sxs-lookup"><span data-stu-id="1293f-233">operationName</span></span> |<span data-ttu-id="1293f-234">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-234">String</span></span> |<span data-ttu-id="1293f-235">Nome da operação de saudação que é registrada.</span><span class="sxs-lookup"><span data-stu-id="1293f-235">Name of hello operation that is logged.</span></span> <span data-ttu-id="1293f-236">Por exemplo, JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="1293f-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="1293f-237">resultType</span><span class="sxs-lookup"><span data-stu-id="1293f-237">resultType</span></span> |<span data-ttu-id="1293f-238">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-238">String</span></span> |<span data-ttu-id="1293f-239">Um substatus para status do trabalho hello (operationName).</span><span class="sxs-lookup"><span data-stu-id="1293f-239">A substatus for hello job status (operationName).</span></span> |
| <span data-ttu-id="1293f-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="1293f-240">resultSignature</span></span> |<span data-ttu-id="1293f-241">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-241">String</span></span> |<span data-ttu-id="1293f-242">Obter detalhes adicionais sobre o status do trabalho de saudação (operationName).</span><span class="sxs-lookup"><span data-stu-id="1293f-242">Additional details on hello job status (operationName).</span></span> |
| <span data-ttu-id="1293f-243">identidade</span><span class="sxs-lookup"><span data-stu-id="1293f-243">identity</span></span> |<span data-ttu-id="1293f-244">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-244">String</span></span> |<span data-ttu-id="1293f-245">usuário Olá Olá a operação solicitada.</span><span class="sxs-lookup"><span data-stu-id="1293f-245">hello user that requested hello operation.</span></span> <span data-ttu-id="1293f-246">Por exemplo: susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1293f-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="1293f-247">propriedades</span><span class="sxs-lookup"><span data-stu-id="1293f-247">properties</span></span> |<span data-ttu-id="1293f-248">JSON</span><span class="sxs-lookup"><span data-stu-id="1293f-248">JSON</span></span> |<span data-ttu-id="1293f-249">Consulte Olá próxima seção (esquema de propriedades de log de auditoria) para obter detalhes</span><span class="sxs-lookup"><span data-stu-id="1293f-249">See hello next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="1293f-250">**resultType** e **resultSignature** fornecem informações sobre o resultado de saudação de uma operação e conter apenas um valor se uma operação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="1293f-250">**resultType** and **resultSignature** provide information on hello result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="1293f-251">Por exemplo, eles contêm um valor somente quando **operationName** contém um valor **JobStarted** ou **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="1293f-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="1293f-252">Esquema de propriedades do log de auditoria</span><span class="sxs-lookup"><span data-stu-id="1293f-252">Audit log properties schema</span></span>

| <span data-ttu-id="1293f-253">Name</span><span class="sxs-lookup"><span data-stu-id="1293f-253">Name</span></span> | <span data-ttu-id="1293f-254">Tipo</span><span class="sxs-lookup"><span data-stu-id="1293f-254">Type</span></span> | <span data-ttu-id="1293f-255">Descrição</span><span class="sxs-lookup"><span data-stu-id="1293f-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1293f-256">JobId</span><span class="sxs-lookup"><span data-stu-id="1293f-256">JobId</span></span> |<span data-ttu-id="1293f-257">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-257">String</span></span> |<span data-ttu-id="1293f-258">trabalho do Hello ID toohello atribuído</span><span class="sxs-lookup"><span data-stu-id="1293f-258">hello ID assigned toohello job</span></span> |
| <span data-ttu-id="1293f-259">JobName</span><span class="sxs-lookup"><span data-stu-id="1293f-259">JobName</span></span> |<span data-ttu-id="1293f-260">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-260">String</span></span> |<span data-ttu-id="1293f-261">nome de saudação que foi fornecido para o trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="1293f-261">hello name that was provided for hello job</span></span> |
| <span data-ttu-id="1293f-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="1293f-262">JobRunTime</span></span> |<span data-ttu-id="1293f-263">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-263">String</span></span> |<span data-ttu-id="1293f-264">tempo de execução de Olá usado o trabalho de saudação tooprocess</span><span class="sxs-lookup"><span data-stu-id="1293f-264">hello runtime used tooprocess hello job</span></span> |
| <span data-ttu-id="1293f-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="1293f-265">SubmitTime</span></span> |<span data-ttu-id="1293f-266">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-266">String</span></span> |<span data-ttu-id="1293f-267">tempo de saudação (em UTC) que o trabalho Olá foi enviado</span><span class="sxs-lookup"><span data-stu-id="1293f-267">hello time (in UTC) that hello job was submitted</span></span> |
| <span data-ttu-id="1293f-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="1293f-268">StartTime</span></span> |<span data-ttu-id="1293f-269">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-269">String</span></span> |<span data-ttu-id="1293f-270">trabalho de saudação do tempo de saudação começou a ser executado após o envio (em UTC)</span><span class="sxs-lookup"><span data-stu-id="1293f-270">hello time hello job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="1293f-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="1293f-271">EndTime</span></span> |<span data-ttu-id="1293f-272">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-272">String</span></span> |<span data-ttu-id="1293f-273">Olá tempo Olá trabalho foi concluído</span><span class="sxs-lookup"><span data-stu-id="1293f-273">hello time hello job ended</span></span> |
| <span data-ttu-id="1293f-274">Paralelismo</span><span class="sxs-lookup"><span data-stu-id="1293f-274">Parallelism</span></span> |<span data-ttu-id="1293f-275">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1293f-275">String</span></span> |<span data-ttu-id="1293f-276">número de saudação de unidades de análise Data Lake solicitadas para esse trabalho durante o envio</span><span class="sxs-lookup"><span data-stu-id="1293f-276">hello number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="1293f-277">**SubmitTime**, **StartTime**, **EndTime** e **Parallelism** fornecem informações sobre uma operação.</span><span class="sxs-lookup"><span data-stu-id="1293f-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="1293f-278">Essas entradas contêm um valor apenas se operação tiver sido iniciada ou concluída.</span><span class="sxs-lookup"><span data-stu-id="1293f-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="1293f-279">Por exemplo, **SubmitTime** contém apenas um valor após **operationName** tem valor Olá **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="1293f-279">For example, **SubmitTime** only contains a value after **operationName** has hello value **JobSubmitted**.</span></span>

## <a name="process-hello-log-data"></a><span data-ttu-id="1293f-280">Dados de log do processo Olá</span><span class="sxs-lookup"><span data-stu-id="1293f-280">Process hello log data</span></span>

<span data-ttu-id="1293f-281">Análise do Azure Data Lake fornece um exemplo sobre como tooprocess e analisar dados de log hello.</span><span class="sxs-lookup"><span data-stu-id="1293f-281">Azure Data Lake Analytics provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="1293f-282">Você pode encontrar o exemplo hello em [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="1293f-282">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1293f-283">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1293f-283">Next steps</span></span>
* [<span data-ttu-id="1293f-284">Visão geral do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1293f-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
