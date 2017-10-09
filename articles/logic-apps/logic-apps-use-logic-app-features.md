---
title: "condições de aaaAdd e iniciar os fluxos de trabalho - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Controle como os fluxos de trabalho são executados em Aplicativos Lógicos do Azure adicionando parâmetros, gatilhos, ações e lógica condicional."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a>Usar recursos de aplicativos lógicos

Em um [tópico anterior](../logic-apps/logic-apps-create-a-logic-app.md), você criou seu primeiro aplicativo lógico. toocontrol fluxo de trabalho lógica do aplicativo, você pode especificar um caminho diferente para o toorun do aplicativo de lógica e muito como processar dados em lotes, coleções e matrizes. Você pode incluir esses elementos no fluxo de trabalho do aplicativo lógico:

* Condições e [instruções switch](../logic-apps/logic-apps-switch-case.md) permitem que seu aplicativo lógico execute ações diferentes com base em se condições específicas são atendidas.

* [Loops](../logic-apps/logic-apps-loops-and-scopes.md) permitem que seu aplicativo lógico execute etapas repetidamente. Por exemplo, você pode repetir ações em uma matriz quando usa um loop **For_each**. Ou você pode repetir ações até que uma condição seja atendida quando usa um loop **Until**.

* [Escopos](../logic-apps/logic-apps-loops-and-scopes.md) permitem agrupar série de ações, por exemplo, tooimplement tratamento de exceção.

* [Debatching](../logic-apps/logic-apps-loops-and-scopes.md) permite que seu aplicativo lógico iniciar fluxos de trabalho separados para itens em uma matriz ao usar Olá **SplitOn** comando.

Este tópico apresenta outros conceitos para a criação de seu aplicativo lógico:

* Exibição tooedit um aplicativo existente da lógica de código
* Opções para iniciar um fluxo de trabalho

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a>Condições: executar etapas somente depois de atender a uma condição

toohave seu aplicativo lógico executar etapas somente quando os dados atendem a critérios específicos, você pode adicionar uma condição que compara dados no fluxo de trabalho de saudação em campos específicos ou valores.

Por exemplo, suponha que você tem um aplicativo lógico que envia muitos emails para postagens no feed RSS de um site. Você pode adicionar uma condição para que seu aplicativo lógico envia email somente quando lançar Olá nova categoria específica de tooa pertence.

1. Em Olá [portal do Azure](https://portal.azure.com), localize e abra o aplicativo lógica no Designer de lógica do aplicativo.

2. Adicione um local de fluxo de trabalho toohello de condição que você deseja. 

   condição de saudação tooadd entre etapas existentes no fluxo de trabalho app de lógica Olá, mova o ponteiro de Olá sobre Seta Olá onde deseja que a condição de saudação tooadd. 
   Escolha Olá **sinal** (**+**), em seguida, escolha **adicionar uma condição**. Por exemplo:

   ![Adicionar condição toologic aplicativo](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > Se você quiser tooadd uma condição no final de saudação do fluxo de trabalho atual, vá toohello inferior do seu aplicativo lógico e escolha **+ nova etapa**.

3. Defina condição de saudação. Especifique Olá campo de origem que você deseja tooevaluate, Olá operação tooperform e o valor de destino hello ou campo. tooadd existente campos tooyour condição, escolha Olá **Adicionar lista de conteúdo dinâmica**.

   Por exemplo:

   ![Editar condição no modo básico](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   Aqui está a condição completa hello:

   ![Condição completa](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > condição de saudação toodefine no código, escolha **Editar no modo avançado**. Por exemplo:
   > 
   > ![Editar condição no código](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. Em **Sim se** e **não se**, adicionar Olá etapas tooperform com base em se Olá condição é atendida.

   Por exemplo:

   ![Condição com caminhos SIM e NÃO](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > Você pode arrastar ações existentes para Olá **Sim se** e **não se** caminhos.

5. Quando terminar, salve o aplicativo lógico.

Agora você não receberá emails somente quando Olá postagens atendem a condição.

## <a name="repeat-actions-over-a-list-with-foreach"></a>Repita ações em uma lista com forEach

loop de forEach Olá Especifica uma matriz toorepeat uma ação. Se não for uma matriz, fluxo Olá falhará. Por exemplo, se você tiver action1 que gera uma matriz de mensagens, e você quiser que cada mensagem toosend, você pode incluir essa instrução forEach nas propriedades de saudação da ação:`forEach : "@action('action1').outputs.messages"`

## <a name="edit-hello-code-definition-for-a-logic-app"></a>Editar definição de código Olá para um aplicativo de lógica

Embora você tenha Olá lógica de aplicativo Designer, você pode editar diretamente o código de saudação que define um aplicativo lógico.

1. Na barra de comandos hello, escolha **exibição de código**.

    Um editor completo é aberto e mostra a definição Olá editado.

    ![Visualização do código](media/logic-apps-use-logic-app-features/codeview.png)

    No editor de texto de saudação, você pode copiar e colar qualquer número de ações no hello mesmo aplicativo lógica ou entre aplicativos lógicos. 
    Você pode facilmente adicionar ou remover seções inteiras da definição de saudação, e você também pode compartilhar definições com outras pessoas.

2. Escolha de suas edições, toosave **salvar**.

## <a name="parameters"></a>parâmetros

Alguns recursos de aplicativos lógicos como parâmetros estão disponíveis apenas na exibição de código. Parâmetros tornam fácil tooreuse valores ao longo de seu aplicativo lógico. Por exemplo, se você tiver um endereço de email que deseje usar em várias ações, deverá defini-lo como um parâmetro.

Parâmetros são bons para extrair os valores que são provavelmente toochange muito. Elas são especialmente úteis quando você precisar toooverride parâmetros em ambientes diferentes. toolearn como toooverride parâmetros com base no ambiente, consulte [criar definições de aplicativo lógica](../logic-apps/logic-apps-author-definitions.md) e [documentação da API REST](https://docs.microsoft.com/rest/api/logic).

Este exemplo mostra como tooupdate seu aplicativo lógico existente para que você pode usar parâmetros para o termo de consulta hello.

1. No modo de exibição de código, localize Olá `parameters : {}` do objeto e, em seguida, adicione um `currentFeedUrl` objeto:

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. Vá toohello `When_a_feed-item_is_published` ação, localizar Olá `queries` seção e substitua o valor de consulta Olá com:`"feedUrl": "#@{parameters('currentFeedUrl')}"` 

    toojoin duas ou mais cadeias de caracteres, você também pode usar o hello `concat` função. 
    Por exemplo, `"@concat('#',parameters('currentFeedUrl'))"` funciona Olá mesmo como Olá acima.

3.  Quando terminar, escolha **Salvar**. 

    Agora você pode alterar RSS do site Olá feed, passando uma URL diferente por meio de saudação `currentFeedURL` objeto.

Saiba mais sobre [como definições de aplicativo de lógica de tooauthor](../logic-apps/logic-apps-author-definitions.md).

## <a name="start-logic-app-workflows"></a>Iniciar fluxos de trabalho de aplicativo lógico

Você tem opções diferentes para iniciar o fluxo de trabalho Olá definido no seu aplicativo lógico. Você sempre pode iniciar uma fluxo de trabalho sob demanda no hello [portal do Azure].

### <a name="recurrence-triggers"></a>Gatilhos de recorrência

Um gatilho de recorrência é executado em um intervalo especificado por você. Quando o gatilho de saudação tem lógica condicional, gatilho Olá determina se o fluxo de trabalho de saudação deve toorun. Um gatilho indica o fluxo de trabalho Olá deve ser executado, retornando um `200` código de status. Quando o fluxo de trabalho de saudação não precisa toorun, gatilho Olá retorna um `202` código de status.

### <a name="callback-using-rest-apis"></a>Retorno de chamada usando APIs REST

toostart um fluxo de trabalho, serviços podem chamar um ponto de extremidade do aplicativo de lógica. toostart esse tipo de lógica aplicativo sob demanda, escolha **executar agora** na barra de comandos de saudação. Consulte [Iniciar fluxos de trabalho chamando pontos de extremidade de aplicativo lógico como gatilhos](../logic-apps/logic-apps-http-endpoint.md). 

<!-- Shared links -->
[portal do Azure]: https://portal.azure.com

## <a name="next-steps"></a>Próximas etapas

* [Instruções switch](../logic-apps/logic-apps-switch-case.md) 
* [Loops, escopos e debatching](../logic-apps/logic-apps-loops-and-scopes.md)
* [Criar definições de aplicativo lógico](../logic-apps/logic-apps-author-definitions.md)