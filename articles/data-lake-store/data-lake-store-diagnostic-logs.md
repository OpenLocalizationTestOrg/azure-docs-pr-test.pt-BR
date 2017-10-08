---
title: "logs de diagnóstico aaaViewing para repositório Azure Data Lake | Microsoft Docs"
description: "Entender como toosetup e acessar logs de diagnóstico para o repositório Azure Data Lake "
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
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>Acessando os logs de diagnóstico do Azure Data Lake Store
Saiba mais sobre como tooenable log de diagnóstico para sua conta do repositório Data Lake e como tooview Olá logs coletados para sua conta.

As organizações podem habilitar o log de diagnóstico para seu repositório Azure Data Lake conta toocollect dados acesso trilhas de auditoria que fornece informações como a lista de usuários que acessam dados hello, frequência dados saudação são acessados, a quantidade de dados é armazenado no Olá conta, etc.

## <a name="prerequisites"></a>Pré-requisitos
* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Conta do Repositório Azure Data Lake**. Siga as instruções de saudação em [Introdução ao repositório Azure Data Lake usando hello Azure Portal](data-lake-store-get-started-portal.md).

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>Habilitar o log de diagnóstico em sua conta do Data Lake Store
1. Logon toohello novo [Portal do Azure](https://portal.azure.com).
2. Abra sua conta Data Lake Store e na folha da conta Data Lake Store, clique em **Configurações**, em seguida, clique em **Logs de diagnóstico**.
3. Em Olá **logs de diagnóstico** folha, clique em **Ativar diagnóstico**.

    ![Habilitar o log de diagnóstico](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "habilitar logs de diagnóstico")

3. Em Olá **diagnóstico** folha, fazer Olá alterações tooconfigure log de diagnóstico a seguir.
   
    ![Habilitar o log de diagnóstico](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "habilitar logs de diagnóstico")
   
   * Definir **Status** muito**na** tooenable log de diagnóstico.
   * Você pode escolher dados toostore/processo saudação de maneiras diferentes.
     
        * Selecione a opção de saudação muito**tooa conta de armazenamento de arquivos** toostore logs tooan conta de armazenamento do Azure. Você usar essa opção se você quiser tooarchive Olá dados que serão processadas em lote em uma data posterior. Se você selecionar essa opção deve fornecer uma conta de armazenamento do Azure logs Olá toosave.
        
        * Selecione a opção de saudação muito**hub de eventos do fluxo tooan** tooan de dados de log toostream Hub de eventos do Azure. Provavelmente você usará essa opção se você tiver um processamento downstream pipeline tooanalyze logs de entrada em tempo real. Se você selecionar essa opção, você deve fornecer detalhes de saudação para Olá Hub de eventos do Azure você deseja toouse.

        * Selecione a opção de saudação muito**enviar tooLog análise** toouse Olá dados de log do Azure Log Analytics serviço tooanalyze Olá gerado. Se você selecionar essa opção, você deve fornecer Olá detalhes para o espaço de trabalho do hello Operations Management Suite que você use Olá executaria análise de log.
     
   * Especifique se deseja que os logs de auditoria tooget ou logs de solicitação ou ambos.
   * Especifique o número de saudação de dias para o qual os dados de saudação devem ser mantidos. Retenção só é aplicável se você estiver usando dados de log de tooarchive de conta de armazenamento do Azure.
   * Clique em **Salvar**.

Depois que você habilitou as configurações de diagnóstico, você pode assistir Olá registra no hello **Logs de diagnóstico** guia.

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>Veja os logs de diagnóstico em sua conta do Data Lake Store
Há duas maneiras de dados de log de saudação tooview para sua conta do repositório Data Lake.

* Na conta do repositório Data Lake Olá exibir configurações
* Da conta de armazenamento do Azure Olá onde são armazenados dados Olá

### <a name="using-hello-data-lake-store-settings-view"></a>Exibir usando Olá de configurações de armazenamento do Data Lake
1. Na folha **Configurações** da conta Data Lake Store, clique em **Logs de Diagnóstico**.
   
    ![Exibir logs de diagnóstico](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "Exibir logs de diagnóstico") 
2. Em Olá **Logs de diagnóstico** folha, você deve ver logs Olá categorizadas por **os Logs de auditoria** e **os Logs de solicitação**.
   
   * Logs de solicitação de captura todas as solicitações de API feitas na conta do repositório Data Lake do hello.
   * Logs de auditoria são os Logs de toorequest semelhantes, mas fornecem uma análise mais detalhada das operações de saudação que está sendo executada na conta do repositório Data Lake hello. Por exemplo, uma chamada à API único carregamento nos logs de solicitação pode resultar em várias operações de "Append" hello logs de auditoria.
3. Clique em Olá **baixar** link em cada entrada toodownload Olá registros de log.

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a>De saudação conta de armazenamento do Azure que contém dados de log
1. Abra a folha de conta de armazenamento do Azure Olá associada a repositório Data Lake para registro em log e, em seguida, clique em Blobs. Olá **do serviço Blob** folha lista dois contêineres.
   
    ![Exibir logs de diagnóstico](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "Exibir logs de diagnóstico")
   
   * contêiner de saudação **insights de logs de auditoria** contém logs de auditoria de saudação.
   * contêiner de saudação **insights de logs de solicitações** contém logs de solicitação de saudação.
2. Dentro desses contêineres, Olá logs são armazenados em Olá estrutura a seguir.
   
    ![Exibir logs de diagnóstico](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "Exibir logs de diagnóstico")
   
    Como exemplo, o log de auditoria de tooan Olá caminho completo pode ser`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    Da mesma forma, seria o log de solicitações de tooa Olá caminho completo`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-hello-structure-of-hello-log-data"></a>Entender a estrutura Olá Olá dos dados de log
Olá logs de auditoria e de solicitação estão em um formato JSON. Nesta seção, vamos examinar a estrutura de saudação do JSON para a solicitação e logs de auditoria.

### <a name="request-logs"></a>Logs de Solicitação
Aqui está um exemplo de entrada no log de solicitação formatada em JSON hello. Cada blob tem um objeto-raiz chamado **registros** que contém uma matriz de objetos do log.

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

#### <a name="request-log-schema"></a>Esquema do log de solicitação
| Name | Tipo | Descrição |
| --- | --- | --- |
| tempo real |Cadeia de caracteres |Olá carimbo de hora (UTC) do log de saudação |
| resourceId |Cadeia de caracteres |ID de saudação do recurso de saudação que levou operação colocar em |
| categoria |Cadeia de caracteres |categoria do log de saudação. Por exemplo, **Solicitações**. |
| operationName |Cadeia de caracteres |Nome da operação de saudação que é registrada. Por exemplo, getfilestatus. |
| resultType |Cadeia de caracteres |status de saudação da operação de hello, por exemplo, 200. |
| callerIpAddress |Cadeia de caracteres |endereço IP de saudação do cliente de saudação fazer solicitação Olá |
| correlationId |Cadeia de caracteres |id de saudação do log de saudação que podem usados toogroup juntos um conjunto de entradas de log relacionadas |
| identidade |Objeto |identidade de saudação que gerou o log de saudação |
| propriedades |JSON |Confira abaixo para obter os detalhes |

#### <a name="request-log-properties-schema"></a>Esquema de propriedades do log de solicitação
| Name | Tipo | Descrição |
| --- | --- | --- |
| HttpMethod |Cadeia de caracteres |Olá método HTTP usado para operação de saudação. Por exemplo, GET. |
| Caminho |Cadeia de caracteres |Olá caminho Olá operação foi executada em |
| RequestContentLength |int |comprimento do conteúdo da solicitação HTTP de saudação Olá |
| ClientRequestId |Cadeia de caracteres |Olá Id que identifica exclusivamente esta solicitação |
| StartTime |Cadeia de caracteres |tempo de saudação na qual solicitação de Olá Olá recebido do servidor |
| EndTime |Cadeia de caracteres |tempo de saudação no qual Olá servidor enviou uma resposta |

### <a name="audit-logs"></a>Logs de auditoria
Aqui está um exemplo de entrada no log de auditoria formatada em JSON hello. Cada blob tem um objeto-raiz chamado **registros** que contém uma matriz de objetos do log

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

#### <a name="audit-log-schema"></a>Esquema do log de auditoria
| Name | Tipo | Descrição |
| --- | --- | --- |
| tempo real |Cadeia de caracteres |Olá carimbo de hora (UTC) do log de saudação |
| resourceId |Cadeia de caracteres |ID de saudação do recurso de saudação que levou operação colocar em |
| categoria |Cadeia de caracteres |categoria do log de saudação. Por exemplo, **Auditoria**. |
| operationName |Cadeia de caracteres |Nome da operação de saudação que é registrada. Por exemplo, getfilestatus. |
| resultType |Cadeia de caracteres |status de saudação da operação de hello, por exemplo, 200. |
| correlationId |Cadeia de caracteres |id de saudação do log de saudação que podem usados toogroup juntos um conjunto de entradas de log relacionadas |
| identidade |Objeto |identidade de saudação que gerou o log de saudação |
| propriedades |JSON |Confira abaixo para obter os detalhes |

#### <a name="audit-log-properties-schema"></a>Esquema de propriedades do log de auditoria
| Name | Tipo | Descrição |
| --- | --- | --- |
| StreamName |Cadeia de caracteres |Olá caminho Olá operação foi executada em |

## <a name="samples-tooprocess-hello-log-data"></a>Dados de log exemplos tooprocess Olá
Repositório Azure Data Lake fornece um exemplo sobre como tooprocess e analisar dados de log hello. Você pode encontrar o exemplo hello em [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample). 

## <a name="see-also"></a>Consulte também
* [Visão geral do repositório Azure Data Lake](data-lake-store-overview.md)
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)

