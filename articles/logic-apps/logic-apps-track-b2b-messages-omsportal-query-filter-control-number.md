---
title: "aaaQuery para mensagens B2B no Operations Management Suite - os aplicativos lógicos do Azure | Microsoft Docs"
description: Criar consultas tootrack AS2, X12 E mensagens EDIFACT no hello Operations Management Suite
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
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a>Mensagens de consulta para AS2, X12 E EDIFACT no hello Microsoft Operations Management Suite (OMS)

Olá toofind AS2, X 12 ou mensagens EDIFACT que você está acompanhando com [Azure Log Analytics](../log-analytics/log-analytics-overview.md) em Olá [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), você pode criar consultas que filtrem ações com base em específica critérios. Por exemplo, você pode encontrar mensagens baseado em um número de controle de intercâmbio específico.

## <a name="requirements"></a>Requisitos

* Um aplicativo lógico configurado com o log de diagnósticos. Saiba [como toocreate um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) e [como tooset o registro em log para esse aplicativo lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Uma conta de integração configurada com o monitoramento e log. Saiba [como uma conta de integração de toocreate](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) e [como tooset o monitoramento e registro em log para essa conta](../logic-apps/logic-apps-monitor-b2b-message.md).

* Se você ainda não o fez, [publicar dados de diagnóstico tooLog análise](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) e [configurar mensagens de rastreamento no OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

> [!NOTE]
> Depois que você cumpriu requisitos anteriores hello, você deve ter um espaço de trabalho Olá [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Você deve usar Olá mesmo espaço de trabalho do OMS para controlar a comunicação de B2B no OMS. 
>  
> Se você não tiver um espaço de trabalho do OMS, saiba [como toocreate um espaço de trabalho do OMS](../log-analytics/log-analytics-get-started.md).

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a>Criar consultas de mensagem com filtros no portal do Operations Management Suite Olá

Este exemplo mostra como você pode encontrar mensagens com base no número de controle de intercâmbio.

> [!TIP] 
> Se você souber o nome de espaço de trabalho do OMS, vá home page do espaço de trabalho de tooyour (`https://{your-workspace-name}.portal.mms.microsoft.com`) e iniciar na etapa 4. Caso contrário, comece na etapa 1.

1. Em Olá [portal do Azure](https://portal.azure.com), escolha **mais serviços**. Pesquise “log analytics” e, em seguida, escolha **Log Analytics**, conforme mostrado aqui:

   ![Encontrar o Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. Em **Log Analytics**, encontre e selecione o espaço de trabalho do OMS.

   ![Selecionar o espaço de trabalho do OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. Em **Gerenciamento**, escolha **Portal do OMS**.

   ![Escolher o portal do OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. Na home page do OMS, escolha **Pesquisa de Logs**.

   ![Na home page do OMS, escolha “Pesquisa de Logs”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -ou-

   ![No menu OMS do hello, escolha "Pesquisa de Log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. Na caixa de pesquisa hello, insira um campo que você deseja toofind e pressione **Enter**. Quando você começa a digitar, o OMS mostra as possíveis correspondências e operações que podem ser usadas. Saiba mais sobre [como toofind dados na análise de Log](../log-analytics/log-analytics-log-searches.md).

   Este exemplo pesquisa eventos com **Type=AzureDiagnostics**.

   ![Começar a digitar a cadeia de consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. Na barra de esquerda hello, escolha Olá período de tempo que você deseja tooview. tooadd uma consulta de tooyour de filtro, escolha **+ adicionar**.

   ![Adicionar filtro tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. Em **adicionar filtros**, insira o nome de filtro de saudação para que você pode encontrar o filtro de saudação desejado. Selecione o filtro hello e escolha **+ adicionar**.

   número de controle de intercâmbio de saudação toofind, este exemplo procura a palavra hello "intercâmbio" e seleciona **event_record_messageProperties_interchangeControlNumber_s** como filtro de saudação.

   ![Selecionar filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. Na barra de esquerda hello, selecione o valor do filtro Olá que você deseja toouse e escolha **aplicar**.

   Este exemplo seleciona o número de controle de intercâmbio Olá para mensagens de saudação que desejamos.

   ![Selecionar o valor do filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. Agora retorne toohello consulta que você está criando. A consulta foi atualizada com o evento de filtro e o valor selecionado. Os resultados anteriores agora são filtrados também.

    ![Retornar tooyour consultas com resultados filtrados](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a>Salvar a consulta para uso futuro

1. Da consulta em Olá **pesquisa de Log** escolha **salvar**. Dê um nome à consulta, selecione uma categoria e escolha **Salvar**.

   ![Dê um nome à consulta e uma categoria](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. tooview sua consulta, escolha **Favoritos**.

   ![Escolher “Favoritos”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. Em **pesquisas salvas**, selecione a consulta para que você pode exibir resultados de saudação. consulta de saudação tooupdate para que você possa encontrar resultados diferentes, editar consulta hello.

   ![Selecionar a consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a>Localizar e executar consultas salvas no portal do Operations Management Suite Olá

1. Abra a home page do espaço de trabalho do OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) e escolha **Pesquisa de Logs**.

   ![Na home page do OMS, escolha “Pesquisa de Logs”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -ou-

   ![No menu OMS do hello, escolha "Pesquisa de Log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. Em Olá **pesquisa de Log** da home page, escolha **Favoritos**.

   ![Escolher “Favoritos”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. Em **pesquisas salvas**, selecione a consulta para que você pode exibir resultados de saudação. consulta de saudação tooupdate para que você possa encontrar resultados diferentes, editar consulta hello.

   ![Selecionar a consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a>Próximas etapas

* [Esquemas de acompanhamento de AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Esquemas de acompanhamento de X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Esquemas de acompanhamento personalizado](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)