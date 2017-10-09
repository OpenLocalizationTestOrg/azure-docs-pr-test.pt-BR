---
title: "falhas de aaaDiagnose - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Toounderstand de maneiras comuns onde estão os aplicativos lógicos"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a>Diagnosticar falhas nos aplicativos lógicos
Se você enfrentar falhas ou problemas com seus aplicativos lógicos, existem algumas abordagens podem ajudá-lo a entender melhor onde falhas Olá são provenientes.  

## <a name="azure-portal-tools"></a>Ferramentas do portal do Azure
Olá portal do Azure fornece muitos toodiagnose de ferramentas cada aplicativo lógica em cada etapa.

### <a name="trigger-history"></a>Histórico de gatilho

Cada aplicativo lógico tem pelo menos um gatilho. Se você perceber que os aplicativos não são acionados, procure primeiro no histórico de gatilho Olá para obter mais informações. Você pode acessar o histórico de gatilho Olá na folha principal da saudação lógica app'ss.

![Localizando o histórico de gatilho Olá][1]

histórico de gatilho Olá lista todas as tentativas de gatilho que seu aplicativo lógico feito. Você pode clicar em cada toodrill de tentativa de gatilho detalhes hello, especificamente, quaisquer entradas ou saídas que Olá tentativa de gatilho é gerado. Se você encontrar gatilhos com falha, selecione tentativa de gatilho hello e escolha Olá **saídas** link tooreview quaisquer gerado mensagens de erro, por exemplo, as credenciais de FTP que não são válidos.

Olá talvez você veja os status diferentes são:

* **Ignorado**. ponto de extremidade de saudação foi toocheck poll de dados e recebeu uma resposta que não havia dados disponíveis.
* **Êxito**. gatilho Olá recebeu uma resposta que os dados estavam disponíveis. Esse status pode ser resultado de um gatilho manual, um gatilho de recorrência ou um gatilho de sondagem. Geralmente, esse status é acompanhado por Olá **acionado** status, mas não pode ser se você tiver uma condição ou um comando de SplitOn no modo de exibição de código que não foi atendido.
* **Falha**. Um erro foi gerado.

#### <a name="start-a-trigger-manually"></a>Iniciar um gatilho manualmente

Olá lógica aplicativo toocheck para um gatilho disponível imediatamente sem aguardar a próxima recorrência de saudação, clique em **Selecionar disparador** em Olá folha principal tooforce uma verificação. Por exemplo, clicar nesse link com um gatilho Dropbox faz sondagem tooimmediately de fluxo de trabalho Olá Dropbox para novos arquivos.

### <a name="run-history"></a>Histórico da execução

Cada gatilho acionado resulta em uma execução. Você pode acessar informações de execução da folha principal hello, que contém muitos detalhes que podem ajudá-lo a entender o que aconteceu durante o fluxo de trabalho de saudação.

![Localizando Olá histórico de execução][2]

Uma execução exibe uma saudação status a seguir:

* **Êxito**. Todas as ações foram bem sucedidas. Se ocorreu uma falha, essa falha era manipulada por uma ação que ocorreu posteriormente no fluxo de trabalho de saudação. Ou seja, falha de saudação foi tratada por uma ação que foi definida toorun depois de uma ação que falhou.
* **Falha**. Pelo menos uma ação teve uma falha que não foi tratada por uma ação posteriormente no fluxo de trabalho de saudação.
* **Cancelado**. Olá estava em execução, mas recebeu uma solicitação de cancelamento.
* **Executando**. fluxo de trabalho Hello está sendo executado. Esse status pode ocorrer para fluxos de trabalho limitados ou devido a saudação atual plano de preços. Para obter detalhes, consulte [limites de ação na página de preços de saudação](https://azure.microsoft.com/pricing/details/app-service/plans/). Configuração de diagnóstico (gráficos de saudação que apareçam no histórico de execução de saudação) também pode fornecer informações sobre os eventos de limitação acontecer.

Quando você estiver observando um histórico da execução, você pode analisar para obter mais detalhes.  

#### <a name="trigger-outputs"></a>Saídas do gatilho

Gatilho gera Mostrar dados Olá originários do gatilho de saudação. Essas saídas podem ajudá-lo a determinar se todas as propriedades retornaram conforme o esperado.

> [!NOTE]
> Se você vir algum conteúdo que não consegue compreender, aprenda como o Aplicativo Lógico do Azure [lida com diferentes tipos de conteúdo](../logic-apps/logic-apps-content-type.md).
> 

![Exemplos de saída do gatilho][3]

#### <a name="action-inputs-and-outputs"></a>Entradas e saídas da ação

Você pode analisar as entradas de saudação e saídas que recebeu uma ação. Esses dados são úteis para entender o tamanho de saudação e a forma de saudação saídas e também para localizar qualquer mensagem de erro pode ter sido gerada.

![Entradas e saídas da ação][4]

## <a name="debug-workflow-runtime"></a>Tempo de execução do fluxo de trabalho de depuração

Juntamente com hello entradas, saídas e gatilhos de uma execução de monitoramento, você pode adicionar etapas tooa fluxos de trabalho que ajudam com a depuração. 
[RequestBin](http://requestb.in) é uma ferramenta poderosa que você pode adicionar como uma etapa em um fluxo de trabalho. Usando RequestBin, você pode configurar um Inspetor toodetermine Olá exato tamanho da solicitação HTTP, forma e formato de uma solicitação HTTP. Você pode criar um RequestBin e cole a URL de saudação em um aplicativo de lógica ação HTTP POST com conteúdo do corpo que você deseja tootest, por exemplo, uma expressão ou outra saída de etapa. Após executar o aplicativo de lógica de saudação, você pode atualizar seu toosee RequestBin como solicitação Olá foi formada quando gerado do mecanismo de aplicativos lógicos hello.

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
