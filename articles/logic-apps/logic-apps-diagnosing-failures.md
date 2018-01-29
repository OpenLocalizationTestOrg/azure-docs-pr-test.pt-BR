---
title: "Solucionar problemas e diagnosticar falhas – Aplicativos Lógicos do Azure | Microsoft Docs"
description: "Entender como e por que os aplicativos lógicos falham"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: logic-apps
ms.date: 10/15/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: de706f711e9c57b2e575d130a2a0cfd0bdc907a1
ms.sourcegitcommit: cf4c0ad6a628dfcbf5b841896ab3c78b97d4eafd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2017
---
# <a name="troubleshoot-and-diagnose-logic-app-failures"></a>Solucionar problemas e diagnosticar falhas nos aplicativos lógicos

Seu aplicativo lógico gera informações que podem ajudar você a diagnosticar e depurar problemas nele. É possível diagnosticar um aplicativo lógico revisando cada etapa no fluxo de trabalho por meio do Portal do Azure. Ou então, você pode adicionar algumas etapas a um fluxo de trabalho para depuração no tempo de execução.

## <a name="review-trigger-history"></a>Examinar histórico de gatilho

Cada aplicativo lógico começa com o gatilho. Se o gatilho não disparar, verifique primeiro o histórico de gatilho. Esse histórico relaciona todas as tentativas de disparo que seu aplicativo lógico realizou e os detalhes sobre entradas e saídas para cada tentativa de disparo.

1. Para verificar se o gatilho foi disparado, escolha **Visão geral** no menu do aplicativo lógico. Em **Histórico de gatilho**, examine o status do gatilho.

   > [!TIP]
   > Se o menu do aplicativo lógico não aparecer, tente retornar ao Painel do Azure e abra novamente o aplicativo lógico.

   ![Examinar histórico de gatilho](./media/logic-apps-diagnosing-failures/logic-app-trigger-history-overview.png)

   > [!TIP]
   > * Se você não encontrar os dados esperados, experimente selecionar **Atualizar** na barra de ferramentas.
   > * Se a lista mostrar muitas tentativas de disparo e não for possível localizar a entrada que você deseja, experimente filtrá-la.

   Aqui estão os possíveis status para uma tentativa de disparo:

   | Status | Descrição | 
   | ------ | ----------- | 
   | **Êxito** | O gatilho verificou o ponto de extremidade e encontrou dados disponíveis. Normalmente, um status de "Disparado" também é exibida junto com esse status. Caso contrário, a definição do gatilho pode ter uma condição ou comando `SplitOn` que não foi atendido. <p>Esse status pode se aplicar a um gatilho manual, gatilho recorrente ou gatilho de sondagem. Um gatilho pode ser executado com êxito, mas a execução em si ainda pode falhar quando as ações gerarem erros sem tratamento. | 
   | **Ignorado** | O gatilho verificou o ponto de extremidade, mas não encontrou dados disponíveis. | 
   | **Com falha** | Ocorreu um erro. Para examinar as mensagens de erro geradas para um disparador com falha, selecione essa tentativa de disparo e escolha **Saídas**. Por exemplo, você pode descobrir entradas que não são válidas. | 
   ||| 

   Podem existir várias entradas de gatilho com a mesma data e hora, o que acontece quando o aplicativo lógico localiza vários itens. 
   Cada vez que o gatilho é disparado, o mecanismo dos Aplicativos Lógicos cria uma instância de aplicativo lógico para executar o fluxo de trabalho. Por padrão, cada instância é executada em paralelo para que nenhum fluxo de trabalho precise esperar para iniciar uma execução.

   > [!TIP]
   > Você pode verificar novamente o gatilho sem aguardar a próxima recorrência. Na barra de ferramentas de visão geral, escolha **Executar gatilho** e selecione o gatilho, o que força uma verificação. Ou então, selecione **Executar** na barra de ferramentas do Designer de Aplicativos Lógicos.

3. Para examinar os detalhes de uma tentativa de disparo, no **Histórico de gatilho**, selecione essa tentativa de disparo. 

   ![Selecionar uma tentativa de disparo](./media/logic-apps-diagnosing-failures/logic-app-trigger-history.png)

4. Examine as entradas e as saídas que o gatilho gerou. As saídas do gatilho mostrarão os dados recebidos do gatilho. Essas saídas podem ajudá-lo a determinar se todas as propriedades retornaram conforme o esperado.

   > [!NOTE]
   > Se você encontrar algum conteúdo que não consegue compreender, entenda como os Aplicativos Lógicos do Azure [lida com diferentes tipos de conteúdo](../logic-apps/logic-apps-content-type.md).

   ![Saídas do gatilho](./media/logic-apps-diagnosing-failures/trigger-outputs.png)

## <a name="review-run-history"></a>Examinar o histórico de execuções

Cada gatilho disparado inicia uma execução de fluxo de trabalho. É possível examinar o que aconteceu durante essa execução, incluindo o status de cada etapa no fluxo de trabalho, mais as entradas e as saídas para cada etapa.

1. No menu do aplicativo lógico, escolha **Visão geral**. Em **Histórico de execuções**, examine a execução do gatilho disparado.

   > [!TIP]
   > Se o menu do aplicativo lógico não aparecer, tente retornar ao Painel do Azure e abra novamente o aplicativo lógico.

   ![Examinar o histórico de execuções](./media/logic-apps-diagnosing-failures/logic-app-runs-history-overview.png)

   > [!TIP]
   > * Se você não encontrar os dados esperados, experimente selecionar **Atualizar** na barra de ferramentas.
   > * Se a lista mostrar muitas execuções e não for possível localizar a entrada que você deseja, experimente filtrá-la.

   Estes são os possíveis status para uma execução:

   | Status | Descrição | 
   | ------ | ----------- | 
   | **Êxito** | Todas as ações foram bem sucedidas. <p>Caso tenha ocorrido alguma falha em uma ação específica, uma ação posterior no fluxo de trabalho a tratou. | 
   | **Com falha** | Pelo menos uma ação falhou e nenhuma ação posterior no fluxo de trabalho estava configurada para tratar essa falha. | 
   | **Cancelado** | O fluxo de trabalho estava em execução, mas recebeu uma solicitação de cancelamento. | 
   | **Executando** | O fluxo de trabalho está em execução atualmente. <p>Esse status pode ocorrer em fluxos de trabalho restritos ou devido ao plano de preços atual. Para saber mais, consulte os [limites de ações na página de preço](https://azure.microsoft.com/pricing/details/logic-apps/). Se você configurar o [log de diagnósticos](../logic-apps/logic-apps-monitor-your-logic-apps.md), também será possível obter informações sobre os possíveis eventos de restrição que ocorrerem. | 
   ||| 

2. Examine os detalhes de cada etapa em uma execução específica. No **Histórico de execuções**, selecione a execução que você deseja examinar.

   ![Examinar o histórico de execuções](./media/logic-apps-diagnosing-failures/logic-app-run-history.png)

   A exibição Detalhes da execução mostra se cada etapa da execução teve êxito ou falhou, independente da execução em si ter tido êxito ou falhado.

   ![Exibir os detalhes de uma execução de aplicativo lógico](./media/logic-apps-diagnosing-failures/logic-app-run-details.png)

3. Para examinar as entradas, saídas e as mensagens de erro para uma etapa específica, escolha essa etapa para que a forma se expanda e mostre os detalhes. Por exemplo:

   ![Exibir detalhes da etapa](./media/logic-apps-diagnosing-failures/logic-app-run-details-expanded.png)

## <a name="perform-runtime-debugging"></a>Realizar depuração de tempo de execução

Para ajudar na depuração, você pode adicionar etapas de diagnóstico a um fluxo de trabalho, bem como examinar os históricos de gatilho e de execuções. Por exemplo, você pode adicionar etapas que usam o serviço [RequestBin](http://requestb.in) para poder inspecionar solicitações HTTP e determinar seu tamanho, forma e formato exatos.

1. Crie um RequestBin, que poderá ser privado e visualizável apenas no seu navegador.

2. No seu aplicativo lógico, adicione uma ação HTTP POST com o conteúdo do corpo que você deseja testar, como por exemplo, uma expressão ou outra saída da etapa.

3. Cole a URL para o RequestBin na ação HTTP POST.

4. Para examinar como a solicitação é formada quando é gerada pelo mecanismo de Aplicativos Lógicos, execute o aplicativo lógico e atualize seu RequestBin.

## <a name="next-steps"></a>Próximas etapas

[Monitorar seu aplicativo lógico](../logic-apps/logic-apps-monitor-your-logic-apps.md)