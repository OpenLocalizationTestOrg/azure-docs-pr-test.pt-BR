---
title: "aaaMonitor e obter informações sobre sua lógica de aplicativo é executado usando o OMS - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Monitorar a execução do seu aplicativo lógica com insights tooget de análise de Log e Operations Management Suite (OMS) e detalhes de depuração mais avançados para solução de problemas e diagnóstico"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>Monitorar e obter informações sobre execuções de aplicativo lógico com o OMS (Operations Management Suite) e o Log Analytics

Para obter informações de depuração mais avançadas e monitoramento, você pode ativar a análise de Log em Olá simultaneamente, quando você cria um aplicativo lógico. Análise de log fornece o diagnóstico, logs e monitoramento para seu aplicativo de lógica é executada por meio do portal do Operations Management Suite (OMS) hello. Quando você adiciona Olá tooOMS de solução de lógica de gerenciamento de aplicativos, você obterá o status agregado para sua lógica de aplicativo será executado e os detalhes específicos, como status, tempo de execução, o status de reenvio e IDs de correlação.

Este tópico mostra como tooturn na análise de Log ou instale Olá solução lógica de gerenciamento de aplicativos no OMS para que você pode exibir eventos de tempo de execução e dados para seu aplicativo de lógica de execução.

 > [!TIP]
 > toomonitor seus aplicativos existentes da lógica, siga estas etapas muito [ativar o log de diagnóstico e enviar lógica tooOMS de dados de tempo de execução de aplicativo](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

## <a name="requirements"></a>Requisitos

Antes de começar, você precisa toohave um espaço de trabalho do OMS. Saiba [como toocreate um espaço de trabalho do OMS](../log-analytics/log-analytics-get-started.md). 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>Ativar o registro em log de diagnóstico durante a criação de aplicativos lógicos

1. No [Portal do Azure](https://portal.azure.com), crie um aplicativo lógico. Escolha **Novo** > **Enterprise Integration** > **Aplicativo Lógico** > **Criar**.

   ![Criar um aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. Em Olá **criar lógica aplicativo** página, executar essas tarefas, conforme mostrado:

   1. Dê um nome para seu aplicativo lógico e selecione sua assinatura do Azure. 
   2. Crie ou selecione um grupo de recursos do Azure.
   3. Definir **análise de Log** muito**em**. 
   Espaço de trabalho do OMS hello selecione onde você deseja muito enviar dados para seu aplicativo lógica é executada. 
   4. Quando você estiver pronto, escolha **Pin toodashboard** > **criar**.

      ![Criar aplicativo lógico](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      Após a conclusão dessa etapa, o Azure criará seu aplicativo lógico, que agora está associado ao seu espaço de trabalho do OMS. 
      Além disso, esta etapa instala automaticamente solução de gerenciamento de aplicativos de lógica de saudação em seu espaço de trabalho do OMS.

3. tooview sua lógica de aplicativo é executado no OMS, [continuar com estas etapas](#view-logic-app-runs-oms).

## <a name="install-hello-logic-apps-management-solution-in-oms"></a>Instalar a solução de gerenciamento de aplicativos de lógica de saudação do OMS

Se você já ativou o Log Analytics durante a criação de seu aplicativo lógico, ignore esta etapa. Você já tem a solução de gerenciamento de aplicativos de lógica de Olá instalada no OMS.

1. Em Olá [portal do Azure](https://portal.azure.com), escolha **mais serviços**. Pesquise por "log analytics" enquanto filtra e, em seguida, escolha **Log Analytics**, conforme exibido:

   ![Escolher “Log Analytics”](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. Em **Log Analytics**, encontre e selecione o espaço de trabalho do OMS. 

   ![Selecionar o espaço de trabalho do OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. Em **Gerenciamento**, escolha **Portal do OMS**.

   ![Escolher “Portal do OMS”](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. Na home page do OMS, se faixa atualização Olá for exibida, escolha faixa Olá para que você atualizar seu espaço de trabalho do OMS primeiro. Então escolha **Galeria de Soluções**.

   ![Escolha "Galeria de Soluções"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. Em **todas as soluções**, localizar e escolha o bloco de saudação do hello **lógica de gerenciamento de aplicativos** solução.

   ![Escolha "Gerenciamento de Aplicativos Lógicos"](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. solução de saudação tooinstall em seu espaço de trabalho do OMS, escolha **adicionar**.

   ![Escolha "Adicionar" para "Gerenciamento de Aplicativos Lógicos"](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>Exibir as execuções de seu aplicativo lógico em seu espaço de trabalho do OMS

1. Contagem de saudação tooview e o status de sua lógica de aplicativo é executado, página de visão geral de toohello vá para seu espaço de trabalho do OMS. Examine os detalhes de saudação na Olá **lógica de gerenciamento de aplicativos** lado a lado.

   ![Bloco de visão geral mostrando a contagem e o status da execução do aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > Se esse cabeçalho de atualização é exibida em vez de bloco de lógica de gerenciamento de aplicativos de saudação, escolha faixa Olá para que você atualizar seu espaço de trabalho do OMS primeiro.
  
   > ![Atualizar "Espaço de Trabalho do OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. tooview um resumo com mais detalhes sobre seu aplicativo lógica será executado, escolha Olá **lógica de gerenciamento de aplicativos** lado a lado.

   Aqui, as execuções de seu aplicativo lógica são agrupadas por nome ou por status de execução.

   ![Resumo do status das execuções de seu aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. tooview que todos Olá é executado de um aplicativo lógico específico ou de status, linha hello selecione um aplicativo lógico ou um status.

   Aqui está um exemplo que mostra todas as execuções de saudação para um aplicativo lógica específica:

   ![Exibir execuções de um aplicativo lógico ou um status](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > Olá **reenvio** coluna mostra "Sim" para execuções que resultam de uma execução reenviada.

4. toofilter esses resultados, você pode executar a filtragem do lado do cliente e do servidor.

   * O filtro do cliente: para cada coluna, escolha os filtros de saudação que você deseja. 
   Estes são alguns exemplos:

     ![Exemplo de filtros de coluna](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * Filtro do servidor: toochoose um horário específico janela ou toolimit Olá número de execuções que aparecem, usar o controle de escopo de saudação na parte superior de saudação da página de saudação. 
   Por padrão, apenas 1.000 registros aparecem por vez. 
   
     ![Janela de tempo de saudação de alteração](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. tooview todos os Olá ações e os detalhes para uma execução, específico, selecione uma linha, o que abre a página de pesquisa de Log de saudação. 

   * tooview essas informações em uma tabela, escolha **tabela**.
   * consulta de saudação toochange, você pode editar cadeia de caracteres de consulta de saudação na barra de pesquisa de saudação. 
   Para ter uma experiência melhor, escolha **Análise Avançada**.

     ![Exibir ações e detalhes da execução de um aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     Aqui na página do Azure Log Analytics hello, você pode atualizar consultas e exibição Olá resulta da tabela de saudação. 
     Essa consulta usa [Kusto a linguagem de consulta](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que pode ser editado se você quiser tooview diferentes resultados. 

     ![Azure Log Analytics – modo de exibição de consulta](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>Próximas etapas

* [Monitorar mensagens do B2B](../logic-apps/logic-apps-monitor-b2b-message.md)
