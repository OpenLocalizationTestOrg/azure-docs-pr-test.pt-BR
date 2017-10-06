---
title: "status de aaaCheck, configurar o log e receber alertas - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Monitorar o status e o desempenho de aplicativos lógicos, registrar dados de diagnóstico e configurar alertas"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a>Monitorar o status, configurar o log de diagnósticos e ativar alertas para os Aplicativo Lógico do Azure

Depois de [criar e executar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md), verifique seu histórico de execuções, histórico de gatilhos, status e desempenho. Para monitoramento de eventos em tempo real e depuração mais avançada, configure o [log de diagnósticos](#azure-diagnostics) do aplicativo lógico. Dessa forma, você poderá [encontrar e exibir eventos](#find-events), como eventos de gatilho, eventos de execução e eventos de ação. Use também esses [dados de diagnóstico com outros serviços](#extend-diagnostic-data), como o Armazenamento do Azure e os Hubs de Eventos do Azure. 

notificações de tooget sobre falhas ou outros problemas possíveis, configurar [alertas](#add-azure-alerts). Por exemplo, você pode criar um alerta que detecta “quando mais de cinco execuções falham em uma hora”. Você também pode configurar o monitoramento, o acompanhamento e o log de forma programática usando as [propriedades e configurações de evento do Diagnóstico do Azure](#diagnostic-event-properties).

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a>Exibir execuções e disparar o histórico do aplicativo lógico

1. toofind seu aplicativo lógica Olá [portal do Azure](https://portal.azure.com), em Olá menu principal do Azure, escolha **mais serviços**. Na caixa de pesquisa hello, localizar "aplicativos lógicos" e escolha **aplicativos lógicos**.

   ![Encontrar o aplicativo lógico](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   Olá portal do Azure mostra todos os aplicativos de lógica de saudação que estão associados a sua assinatura do Azure. 

2. Selecione o aplicativo lógico e, em seguida, escolha **Visão geral**.

   Olá portal do Azure mostra Olá execuções de histórico e o histórico de gatilho para seu aplicativo lógico. Por exemplo:

   ![Histórico de execuções e histórico de gatilhos do aplicativo lógico](media/logic-apps-monitor-your-logic-apps/overview.png)

   * **Executa o histórico** mostra todas as execuções de saudação para seu aplicativo lógico. 
   * **Disparar histórico** mostra todas as atividades de gatilho Olá para seu aplicativo lógico.

   Para obter descrições de status, consulte [Solução de problemas do aplicativo lógico](../logic-apps/logic-apps-diagnosing-failures.md).

   > [!TIP]
   > Se você não encontrar dados Olá que você espera que, na barra de ferramentas hello, escolha **atualizar**.

3. Olá tooview as etapas de uma execução específica, em **executa histórico**, selecione que são executados. 

   modo de exibição de monitor de saudação mostra cada etapa em que são executados. Por exemplo:

   ![Ações de uma execução específica](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. tooget mais detalhes sobre Olá executar, escolha **detalhes da execução**. Essas informações resumem as etapas de hello, status, entradas e saídas para Olá executar. 

   ![Escolher “Detalhes da Execução”](media/logic-apps-monitor-your-logic-apps/run-details.png)

   Por exemplo, você pode obter Olá execução **ID de correlação**, que podem ser úteis quando você usar o hello [API REST para aplicativos lógicos](https://docs.microsoft.com/rest/api/logic).

5. tooget detalhes sobre uma etapa específica, escolha essa etapa. Agora você pode examinar detalhes como entradas, saídas e todos os erros que ocorreram nessa etapa. Por exemplo:

   ![Detalhes da etapa](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > Todos os detalhes de tempo de execução e eventos são criptografados no hello serviço de aplicativos lógicos. Eles são descriptografados apenas quando um usuário solicita tooview esses dados. Você também pode controlar o acesso toothese eventos com [o Access RBAC (controle)](../active-directory/role-based-access-control-what-is.md).

6. tooget detalhes sobre um evento de gatilho específico, volte toohello **visão geral** painel. Em **disparar histórico**, selecione o evento de gatilho hello. Agora você pode examinar detalhes como entradas e saídas, por exemplo:

   ![Detalhes de saída do evento de gatilho](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a>Ativar o log de diagnósticos do aplicativo lógico

Para uma depuração mais avançada com eventos e detalhes de tempo de execução, configure o log de diagnósticos com o [Azure Log Analytics](../log-analytics/log-analytics-overview.md). Análise de log é um serviço em [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) que monitora a sua nuvem locais e ambientes toohelp manter sua disponibilidade e desempenho. 

Antes de começar, você precisa toohave um espaço de trabalho do OMS. Saiba [como toocreate um espaço de trabalho do OMS](../log-analytics/log-analytics-get-started.md).

1. Em Olá [portal do Azure](https://portal.azure.com), localize e selecione o aplicativo lógico. 

2. No menu de folha de aplicativo de lógica de hello, em **monitoramento**, escolha **diagnóstico** > **configurações de diagnóstico**.

   ![Vá tooMonitoring, diagnósticos, configurações de diagnóstico](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. Em **Configurações de diagnóstico**, escolha **Ativado**.

   ![Ativar logs de diagnóstico](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. Agora selecione categoria de evento e o espaço de trabalho OMS de saudação para registro em log conforme mostrado:

   1. Selecione **enviar tooLog análise**. 
   2. Em **Log Analytics**, escolha **Configurar**. 
   3. Em **espaços de trabalho do OMS**, selecione Olá toouse de espaço de trabalho do OMS para registro em log.
   4. Em **Log**, selecione Olá **WorkflowRuntime** categoria.
   5. Escolha o intervalo de métrica de saudação.
   6. Quando terminar, escolha **Salvar**.

   ![Selecionar o espaço de trabalho do OMS e os dados para log](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

Agora, você pode encontrar eventos e outros dados para eventos de gatilho, eventos de execução e eventos de ação.

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a>Encontrar eventos e dados do aplicativo lógico

toofind e exibir eventos em seu aplicativo lógico, como eventos de gatilho, execute os eventos e eventos de ação, siga estas etapas.

1. Em Olá [portal do Azure](https://portal.azure.com), escolha **mais serviços**. Pesquise “log analytics” e, em seguida, escolha **Log Analytics**, conforme mostrado aqui:

   ![Escolher “Log Analytics”](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. Em **Log Analytics**, encontre e selecione o espaço de trabalho do OMS. 

   ![Selecionar o espaço de trabalho do OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. Em **Gerenciamento**, escolha **Portal do OMS**.

   ![Escolher “Portal do OMS”](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. Na home page do OMS, escolha **Pesquisa de Logs**.

   ![Na home page do OMS, escolha “Pesquisa de Logs”](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   -ou-

   ![No menu OMS do hello, escolha "Pesquisa de Log"](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. Na caixa de pesquisa hello, especifique um campo que você deseja toofind e pressione **Enter**. Quando você começa a digitar, o OMS mostra as possíveis correspondências e operações que podem ser usadas. 

   Por exemplo, os primeiros 10 eventos toofind Olá que ocorreram, digite e selecione esta consulta de pesquisa: **categoria = WorkflowRuntime | top 10**

   ![Inserir a cadeia de pesquisa](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   Saiba mais sobre [como toofind dados na análise de Log](../log-analytics/log-analytics-log-searches.md).

6. Na página de resultados Olá, na barra de esquerdo de Olá, escolha o período de tempo de saudação que você deseja tooview.
Escolha de sua consulta adicionando um filtro, toorefine **+ adicionar**.

   ![Escolher período de tempo para os resultados da consulta](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. Em **adicionar filtros**, insira o nome de filtro de saudação para que você pode encontrar o filtro de saudação desejado. Selecione o filtro hello e escolha **+ adicionar**.

   Este exemplo usa hello word "status" toofind falha eventos em **AzureDiagnostics**.
   Olá aqui o filtro para **status_s** já está selecionado.

   ![Selecionar filtro](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. Na barra de esquerda hello, selecione o valor do filtro Olá que você deseja toouse e escolha **aplicar**.

   ![Selecionar valor de filtro e escolher “Aplicar”](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. Agora retorne toohello consulta que você está criando. A consulta é atualizada com o filtro e o valor selecionados. Os resultados anteriores agora são filtrados também.

   ![Retornar tooyour consultas com resultados filtrados](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. Escolha de sua consulta para uso futuro, toosave **salvar**. Saiba [como toosave sua consulta](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Estender como e onde usar os dados de diagnóstico com outros serviços

Junto com o Azure Log Analytics, você pode estender a maneira de usar os dados de diagnóstico do aplicativo lógico com outros serviços do Azure, por exemplo: 

* [Arquivar logs do Diagnóstico do Azure no Armazenamento do Azure](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Fluxo de Logs de diagnóstico do Azure tooAzure Hubs de eventos](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

Depois, obtenha o monitoramento em tempo real usando a telemetria e a análise de outros serviços, como o [Stream Analytics do Azure](../stream-analytics/stream-analytics-introduction.md) e o [Power BI](../log-analytics/log-analytics-powerbi.md). Por exemplo:

* [Dados de fluxo de Hubs de eventos tooStream análise](../stream-analytics/stream-analytics-define-inputs.md)
* [Analisar dados de streaming com o Stream Analytics e criar um painel de análise em tempo real no Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)

Com base nas opções de saudação que você deseja configurar, certifique-se de que você primeiro [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md) ou [criar um hub de eventos do Azure](../event-hubs/event-hubs-create.md). Selecione as opções de saudação para onde você deseja que os dados de diagnóstico toosend:

![Enviar dados tooAzure armazenamento conta ou evento de hub](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> Períodos de retenção se aplicam somente quando você escolher toouse uma conta de armazenamento.

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a>Configurar alertas para o aplicativo lógico

limites excedidos para o aplicativo lógico, ou métricas específicas toomonitor configurar [alertas no Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md). Saiba mais sobre as [métricas no Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md). 

tooset alertas sem [Azure Log Analytics](../log-analytics/log-analytics-overview.md), siga estas etapas. Para obter critérios mais avançados de alertas e de ações, [configure o Log Analytics](#azure-diagnostics) também.

1. No menu de folha de aplicativo de lógica de hello, em **monitoramento**, escolha **diagnóstico** > **regras de alerta** > **adicionar alerta**conforme mostrado aqui:

   ![Adicionar um alerta ao aplicativo lógico](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. Em Olá **adicionar uma regra de alerta** folha, criar o alerta, conforme mostrado:

   1. Em **Recurso**, selecione o aplicativo lógico, caso ainda não esteja selecionado. 
   2. Dê um nome e uma descrição para o alerta.
   3. Selecione um **métrica** ou eventos que você deseja tootrack.
   4. Selecione um **condição**, especifique um **limite** para métrica hello e selecione Olá **período** para esta métrica de monitoramento.
   5. Selecione se toosend de email de alerta de saudação. 
   6. Especifique qualquer outro endereço de email para enviar o alerta de saudação. 
   Você também pode especificar uma URL de webhook onde você deseja que o alerta de saudação toosend.

   Por exemplo, essa regra envia um alerta quando cinco ou mais execuções falham em uma hora:

   ![Criar uma regra de alerta de métrica](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> toorun um aplicativo lógico de um alerta, você pode incluir Olá [gatilho solicitação](../connectors/connectors-native-reqres.md) no fluxo de trabalho, que permite que você execute tarefas como estes exemplos:
> 
> * [Lançar tooSlack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [Enviar um texto](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [Adicionar uma fila de mensagens tooa](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a>Configurações e detalhes de eventos do Diagnóstico do Azure

Cada evento de diagnóstico exibe detalhes sobre a sua lógica de aplicativo e se o evento, por exemplo, status de saudação, hora de início, hora de término e assim por diante. tooprogrammatically configurar o monitoramento, rastreamento e registro em log, ou pode usar esses detalhes com hello [API REST para aplicativos do Azure lógica](https://docs.microsoft.com/rest/api/logic) e hello [API REST para diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).

Por exemplo, Olá `ActionCompleted` evento tem Olá `clientTrackingId` e `trackedProperties` propriedades que você pode usar para controlar e monitorar:

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* `clientTrackingId`: Se não for fornecido, o Azure gera essa ID e correlaciona eventos em um aplicativo lógico executado automaticamente, incluindo quaisquer fluxos de trabalho aninhados que são chamados de aplicativo lógico de saudação. Você pode especificar manualmente essa ID de um disparador, passando um `x-ms-client-tracking-id` cabeçalho com o valor de ID personalizado na solicitação de gatilho hello. Use um gatilho de solicitação, gatilho HTTP ou gatilho de webhook.

* `trackedProperties`: tootrack entradas ou saídas de dados de diagnóstico, você pode adicionar propriedades rastreadas tooactions na definição de JSON da lógica do aplicativo. Propriedades rastreadas podem controlar somente uma única ação entradas e saídas, mas você pode usar o hello `correlation` propriedades de eventos toocorrelate em ações em uma execução.

  tootrack uma ou mais propriedades, adicionar Olá `trackedProperties` seção e hello propriedades desejadas toohello definição da ação. Por exemplo, suponha que você deseja que os dados de tootrack como uma "ID de ordem" em sua telemetria:

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a>Próximas etapas

* [Criar modelos para implantação de aplicativos lógicos e gerenciamento de versão](../logic-apps/logic-apps-create-deploy-template.md)
* [Cenários B2B com o Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Monitorar mensagens do B2B](../logic-apps/logic-apps-monitor-b2b-message.md)