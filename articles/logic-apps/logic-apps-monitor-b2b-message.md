---
title: "transações aaaMonitor B2B e configurar o log - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Monitorar mensagens AS2, X12 e EDIFACT e iniciar o log de diagnósticos da conta de integração"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a>Monitorar e configurar o log de diagnósticos para a comunicação B2B nas contas de integração

Depois de configurar a comunicação B2B entre dois processos ou aplicativos de negócios em execução por meio de sua conta de integração, essas entidades poderão trocar mensagens entre si. tooconfirm essa comunicação funciona conforme o esperado, você pode configurar o monitoramento de AS2, X12, EDIFACT mensagens e, juntamente com o log de diagnóstico para sua conta de integração por meio de saudação [Azure Log Analytics](../log-analytics/log-analytics-overview.md) serviço. Esse serviço do [OMS (Operations Management Suite)](../operations-management-suite/operations-management-suite-overview.md) monitora os ambientes locais e de nuvem, ajudando você a manter a disponibilidade e o desempenho deles e também coleta detalhes e eventos de tempo de execução para uma depuração mais avançada. Use também [os dados de diagnóstico com outros serviços](#extend-diagnostic-data), como o Armazenamento do Azure e os Hubs de Eventos do Azure.

## <a name="requirements"></a>Requisitos

* Um aplicativo lógico configurado com o log de diagnósticos. Saiba [como tooset o registro em log para esse aplicativo lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

  > [!NOTE]
  > Depois de atender esse requisito, você deve ter um espaço de trabalho Olá [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Você deve usar Olá mesmo espaço de trabalho do OMS ao configurar o registro em log para sua conta de integração. Se você não tiver um espaço de trabalho do OMS, saiba [como toocreate um espaço de trabalho do OMS](../log-analytics/log-analytics-get-started.md).

* Uma conta de integração que foi vinculada tooyour lógica aplicativo. Saiba [como a conta toocreate uma integração com um aplicativo de lógica de tooyour link](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a>Ativar o log de diagnósticos da conta de integração

Você pode ativar registro em log diretamente de sua conta de integração ou [por meio de hello Azure Monitor service](#azure-monitor-service). O Azure Monitor fornece monitoramento básico com os dados no nível de infraestrutura. Saiba mais sobre o [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a>Ativar o log de diagnósticos diretamente na conta de integração

1. Em Olá [portal do Azure](https://portal.azure.com), localize e selecione sua conta de integração. Em **Monitoramento**, escolha **Logs de diagnóstico**, conforme mostrado aqui:

   ![Encontrar e selecionar a conta de integração e escolher “Logs de diagnóstico”](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. Depois de selecionar a conta de integração, Olá valores a seguir é selecionada automaticamente. Se esses valores estiverem corretos, escolha **Ativar diagnóstico**. Caso contrário, selecione os valores hello que você deseja:

   1. Em **assinatura**, selecione Olá assinatura do Azure que você usa com sua conta de integração.
   2. Em **grupo de recursos**, selecione grupo de recursos de saudação que você usa com sua conta de integração.
   3. Em **Tipo de recurso**, selecione **Contas de integração**. 
   4. Em **Recurso**, selecione a conta de integração. 
   5. Escolha **Ativar diagnóstico**.

   ![Configurar o diagnóstico para sua conta de integração](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. Em **Configurações de diagnóstico** e, em seguida, **Status**, escolha **Ativado**.

   ![Ativar o Diagnóstico do Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. Agora selecione toouse de espaço de trabalho e dados OMS de saudação para registro em log conforme mostrado:

   1. Selecione **enviar tooLog análise**. 
   2. Em **Log Analytics**, escolha **Configurar**. 
   3. Em **espaços de trabalho do OMS**, selecione Olá toouse de espaço de trabalho do OMS para registro em log.
   4. Em **Log**, selecione Olá **IntegrationAccountTrackingEvents** categoria.
   5. Escolha **Salvar**.

   ![Configurar a análise de Log para enviar o log de tooa de dados de diagnóstico](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. Agora, [configure o acompanhamento das mensagens B2B no OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a>Ativar o log de diagnósticos por meio do Azure Monitor

1. Em Olá [portal do Azure](https://portal.azure.com), em Olá menu principal do Azure, escolha **Monitor**, **logs de diagnóstico**. Depois, selecione sua conta de integração, conforme mostrado aqui:

   ![Escolher “Monitorar”, “Logs de diagnóstico” e selecionar a conta de integração](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. Depois de selecionar a conta de integração, Olá valores a seguir é selecionada automaticamente. Se esses valores estiverem corretos, escolha **Ativar diagnóstico**. Caso contrário, selecione os valores hello que você deseja:

   1. Em **assinatura**, selecione Olá assinatura do Azure que você usa com sua conta de integração.
   2. Em **grupo de recursos**, selecione grupo de recursos de saudação que você usa com sua conta de integração.
   3. Em **Tipo de recurso**, selecione **Contas de integração**.
   4. Em **Recurso**, selecione a conta de integração.
   5. Escolha **Ativar diagnóstico**.

   ![Configurar o diagnóstico para sua conta de integração](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. Em **Configurações de diagnóstico**, escolha **Ativado**.

   ![Ativar o Diagnóstico do Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. Agora selecione categoria de evento e o espaço de trabalho OMS de saudação para registro em log conforme mostrado:

   1. Selecione **enviar tooLog análise**. 
   2. Em **Log Analytics**, escolha **Configurar**. 
   3. Em **espaços de trabalho do OMS**, selecione Olá toouse de espaço de trabalho do OMS para registro em log.
   4. Em **Log**, selecione Olá **IntegrationAccountTrackingEvents** categoria.
   5. Quando terminar, escolha **Salvar**.

   ![Configurar a análise de Log para enviar o log de tooa de dados de diagnóstico](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. Agora, [configure o acompanhamento das mensagens B2B no OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Estender como e onde usar os dados de diagnóstico com outros serviços

Junto com o Azure Log Analytics, você pode estender a maneira de usar os dados de diagnóstico do aplicativo lógico com outros serviços do Azure, por exemplo: 

* [Arquivar logs do Diagnóstico do Azure no Armazenamento do Azure](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Fluxo de Logs de diagnóstico do Azure tooAzure Hubs de eventos](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

Depois, obtenha o monitoramento em tempo real usando a telemetria e a análise de outros serviços, como o [Stream Analytics do Azure](../stream-analytics/stream-analytics-introduction.md) e o [Power BI](../log-analytics/log-analytics-powerbi.md). Por exemplo:

* [Dados de fluxo de Hubs de eventos tooStream análise](../stream-analytics/stream-analytics-define-inputs.md)
* [Analisar dados de streaming com o Stream Analytics e criar um painel de análise em tempo real no Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)

Com base nas opções de saudação que você deseja configurar, certifique-se de que você primeiro [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md) ou [criar um hub de eventos do Azure](../event-hubs/event-hubs-create.md). Selecione as opções de saudação para onde você deseja que os dados de diagnóstico toosend:

![Enviar dados tooAzure armazenamento conta ou evento de hub](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> Períodos de retenção se aplicam somente quando você escolher toouse uma conta de armazenamento.

## <a name="supported-tracking-schemas"></a>Esquemas de acompanhamento com suporte

Azure oferece suporte a esses tipos de esquema que têm fixos esquemas exceto Olá tipo personalizado de controle.

* [Esquema de acompanhamento do AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Esquema de acompanhamento do X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Esquema de acompanhamento personalizado](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a>Próximas etapas

* [Acompanhar mensagens B2B no OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Acompanhar mensagens B2B no OMS")
* [Saiba mais sobre Olá Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")

