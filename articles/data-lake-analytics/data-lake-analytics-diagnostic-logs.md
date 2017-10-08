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
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a>Acessando os logs de diagnóstico do Azure Data Lake Analytics

Log de diagnóstico permite toocollect trilhas de auditoria de acesso de dados. Esses logs fornecem informações como:

* Uma lista de usuários que Olá dados acessados.
* A frequência com dados saudação são acessados.
* A quantidade de dados é armazenado na conta de saudação.

## <a name="enable-logging"></a>Habilitar o registro em log

1. Logon toohello [portal do Azure](https://portal.azure.com).

2. Abra sua conta da análise Data Lake e selecione **logs de diagnóstico** de saudação __Monitor__ seção. Em seguida, selecione __Ativar o diagnóstico__.

    ![Ativar diagnóstico toocollect auditoria e logs de solicitação](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. De __as configurações de diagnóstico__, defina Olá status too__On__ e selecione as opções de log.

    ![Ativar diagnóstico toocollect auditoria e logs de solicitação](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "habilitar logs de diagnóstico")

   * Definir **Status** muito**na** tooenable log de diagnóstico.

   * Você pode escolher dados saudação toostore/processo de três maneiras diferentes.

     * Selecione __tooa conta de armazenamento de arquivos__ toostore logs em uma conta de armazenamento do Azure. Use esta opção se você quiser tooarchive Olá dados. Se você selecionar essa opção, você deve fornecer um armazenamento do Azure conta toosave Olá os logs para.

     * Selecione **tooan Hub de eventos de fluxo** toostream log dados tooan Hub de eventos do Azure. Use essa opção se tiver um pipeline de processamento downstream que esteja analisando logs de entrada em tempo real. Se você selecionar essa opção, você deve fornecer detalhes de saudação para Olá Hub de eventos do Azure você deseja toouse.

     * Selecione __enviar tooLog análise__ toosend Olá dados toohello serviço de análise de Log. Use esta opção se você quiser toouse toogather de análise de Log e analise logs.
   * Especifique se deseja que os logs de auditoria tooget ou logs de solicitação ou ambos.  Um log de solicitação captura todas as solicitações da API. Um log de auditoria registra todas as operações disparadas pela solicitação de API.

   * Para __tooa conta de armazenamento de arquivos__, especifique Olá número de dados de saudação tooretain dias.

   * Clique em __Salvar__.

        > [!NOTE]
        > Você deve selecionar __tooa conta de armazenamento de arquivos__, __tooan Hub de eventos de fluxo__ ou __enviar tooLog análise__ antes de clicar em Olá __salvar__botão.

Depois que você habilitou as configurações de diagnóstico, você pode retornar toohello __logs de diagnóstico__ folha tooview Olá logs.

## <a name="view-logs"></a>Exibir logs

### <a name="use-hello-data-lake-analytics-view"></a>Usar exibição da análise Data Lake Olá

1. De sua análise Data Lake conta folha, em **monitoramento**, selecione **Logs de diagnóstico** e, em seguida, selecione uma entrada toodisplay logs para.

    ![Exibir logs de diagnóstico](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Exibir logs de diagnóstico")

2. Olá logs são categorizados por **os Logs de auditoria** e **os Logs de solicitação**.

    ![entradas de log](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * Logs de solicitação de captura todas as solicitações de API feitas em Olá conta da análise Data Lake.
   * Logs de auditoria são os Logs de toorequest semelhantes, mas fornecem uma análise mais detalhada das operações de saudação. Por exemplo, uma única chamada à API de upload em um log de solicitação pode resultar em várias operações do tipo "Acréscimo" no log de auditoria.

3. Clique em Olá **baixar** link para um toodownload de entrada de registro de log.

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a>Usar conta de armazenamento do Azure Olá que contém dados de log

1. Abra a folha de conta de armazenamento do Azure Olá associada análise Data Lake para registro em log e, em seguida, clique em __Blobs__. Olá **do serviço Blob** folha lista dois contêineres.

    ![Exibir logs de diagnóstico](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Exibir logs de diagnóstico")

   * contêiner de saudação **insights de logs de auditoria** contém logs de auditoria de saudação.
   * contêiner de saudação **insights de logs de solicitações** contém logs de solicitação de saudação.
2. Dentro desses contêineres, Olá logs são armazenados em Olá estrutura a seguir:

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
   > Olá `##` entradas no caminho de saudação contêm ano hello, mês, dia e hora na qual Olá log foi criado. O Data Lake Analytics cria um arquivo a cada hora e, portanto, o `m=` sempre conterá um valor `00`.

    Por exemplo, log de auditoria do hello caminho completo tooan poderia ser:

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    Da mesma forma, o log de solicitações de tooa de caminho completo de saudação poderia ser:

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a>Estrutura de log

Olá logs de auditoria e de solicitação estão em um formato JSON estruturado.

### <a name="request-logs"></a>Logs de Solicitação

Aqui está um exemplo de entrada no log de solicitação formatada em JSON hello. Cada blob tem um objeto-raiz chamado **registros** que contém uma matriz de objetos do log.

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

#### <a name="request-log-schema"></a>Esquema do log de solicitação

| Name | Tipo | Descrição |
| --- | --- | --- |
| tempo real |Cadeia de caracteres |Olá carimbo de hora (UTC) do log de saudação |
| resourceId |Cadeia de caracteres |Identificador de saudação do recurso de saudação que levou operação colocar em |
| categoria |Cadeia de caracteres |categoria do log de saudação. Por exemplo, **Solicitações**. |
| operationName |Cadeia de caracteres |Nome da operação de saudação que é registrada. Por exemplo, GetAggregatedJobHistory. |
| resultType |Cadeia de caracteres |status de saudação da operação de hello, por exemplo, 200. |
| callerIpAddress |Cadeia de caracteres |endereço IP de saudação do cliente de saudação fazer solicitação Olá |
| correlationId |Cadeia de caracteres |Identificador de saudação do log hello. Esse valor pode ser usado toogroup um conjunto de entradas de log relacionadas. |
| identidade |Objeto |identidade de saudação que gerou o log de saudação |
| propriedades |JSON |Consulte Olá próxima seção (esquema de propriedades de log de solicitação) para obter detalhes |

#### <a name="request-log-properties-schema"></a>Esquema de propriedades do log de solicitação

| Name | Tipo | Descrição |
| --- | --- | --- |
| HttpMethod |Cadeia de caracteres |Olá método HTTP usado para operação de saudação. Por exemplo, GET. |
| Caminho |Cadeia de caracteres |Olá caminho Olá operação foi executada em |
| RequestContentLength |int |comprimento do conteúdo da solicitação HTTP de saudação Olá |
| ClientRequestId |Cadeia de caracteres |Olá identificador que identifica exclusivamente esta solicitação |
| StartTime |Cadeia de caracteres |tempo de saudação na qual solicitação de Olá Olá recebido do servidor |
| EndTime |Cadeia de caracteres |tempo de saudação no qual Olá servidor enviou uma resposta |

### <a name="audit-logs"></a>Logs de auditoria

Aqui está um exemplo de entrada no log de auditoria formatada em JSON hello. Cada blob tem um objeto-raiz chamado **registros** que contém uma matriz de objetos do log.

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

#### <a name="audit-log-schema"></a>Esquema do log de auditoria

| Name | Tipo | Descrição |
| --- | --- | --- |
| tempo real |Cadeia de caracteres |Olá carimbo de hora (UTC) do log de saudação |
| resourceId |Cadeia de caracteres |Identificador de saudação do recurso de saudação que levou operação colocar em |
| categoria |Cadeia de caracteres |categoria do log de saudação. Por exemplo, **Auditoria**. |
| operationName |Cadeia de caracteres |Nome da operação de saudação que é registrada. Por exemplo, JobSubmitted. |
| resultType |Cadeia de caracteres |Um substatus para status do trabalho hello (operationName). |
| resultSignature |Cadeia de caracteres |Obter detalhes adicionais sobre o status do trabalho de saudação (operationName). |
| identidade |Cadeia de caracteres |usuário Olá Olá a operação solicitada. Por exemplo: susan@contoso.com. |
| propriedades |JSON |Consulte Olá próxima seção (esquema de propriedades de log de auditoria) para obter detalhes |

> [!NOTE]
> **resultType** e **resultSignature** fornecem informações sobre o resultado de saudação de uma operação e conter apenas um valor se uma operação foi concluída. Por exemplo, eles contêm um valor somente quando **operationName** contém um valor **JobStarted** ou **JobEnded**.
>
>

#### <a name="audit-log-properties-schema"></a>Esquema de propriedades do log de auditoria

| Name | Tipo | Descrição |
| --- | --- | --- |
| JobId |Cadeia de caracteres |trabalho do Hello ID toohello atribuído |
| JobName |Cadeia de caracteres |nome de saudação que foi fornecido para o trabalho de saudação |
| JobRunTime |Cadeia de caracteres |tempo de execução de Olá usado o trabalho de saudação tooprocess |
| SubmitTime |Cadeia de caracteres |tempo de saudação (em UTC) que o trabalho Olá foi enviado |
| StartTime |Cadeia de caracteres |trabalho de saudação do tempo de saudação começou a ser executado após o envio (em UTC) |
| EndTime |Cadeia de caracteres |Olá tempo Olá trabalho foi concluído |
| Paralelismo |Cadeia de caracteres |número de saudação de unidades de análise Data Lake solicitadas para esse trabalho durante o envio |

> [!NOTE]
> **SubmitTime**, **StartTime**, **EndTime** e **Parallelism** fornecem informações sobre uma operação. Essas entradas contêm um valor apenas se operação tiver sido iniciada ou concluída. Por exemplo, **SubmitTime** contém apenas um valor após **operationName** tem valor Olá **JobSubmitted**.

## <a name="process-hello-log-data"></a>Dados de log do processo Olá

Análise do Azure Data Lake fornece um exemplo sobre como tooprocess e analisar dados de log hello. Você pode encontrar o exemplo hello em [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).

## <a name="next-steps"></a>Próximas etapas
* [Visão geral do Azure Data Lake Analytics](data-lake-analytics-overview.md)
