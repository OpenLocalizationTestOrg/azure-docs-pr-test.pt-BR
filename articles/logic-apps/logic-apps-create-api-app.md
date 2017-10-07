---
title: "web aaaCreate APIs e APIs REST que os conectores - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Criar web toocall APIs e APIs REST de sistemas, serviços ou APIs em fluxos de trabalho para integração do sistema com os aplicativos lógicos do Azure"
keywords: "APIs Web, APIs REST, conectores, fluxos de trabalho, integrações do sistema"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: bd229179-7199-4aab-bae0-1baf072c7659
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/26/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 2792204d1d298a6f810e75211c1789ee204c2fdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-apis-as-connectors-for-logic-apps"></a>Criar APIs personalizadas como conectores de aplicativos lógicos

Embora os aplicativos lógicos do Azure oferece [100 + conectores internos](../connectors/apis-list.md) que você pode usar em fluxos de trabalho de aplicativo de lógica, talvez você queira toocall APIs, sistemas e serviços que não estão disponíveis como conectores. Você pode criar suas próprias APIs personalizados que fornecem toouse ações e gatilhos em aplicativos lógicos. Aqui estão as outras razões por que talvez você queira toocreate sua própria muito usam APIs que os conectores de aplicativos lógicos:

* Estender os fluxos de trabalho de integração de dados e integração do sistema.
* Ajuda os clientes a usar as tarefas de serviço toomanage profissional ou pessoal.
* Expanda Olá alcance, descoberta e uso para seu serviço.

Basicamente, conectores são APIs Web que usam REST para interfaces conectáveis, [formatos de metadados do Swagger](http://swagger.io/specification/) para documentação e JSON como formato de troca de dados. Como os conectores são APIs REST que se comunicam por meio de pontos de extremidade HTTP, você pode usar qualquer linguagem, como .NET, Java ou Node.js, para criar conectores. Você também pode hospedar suas APIs em [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md), um plataforma-como-um-serviço (PaaS) que oferece uma das maneiras de saudação melhores, mais fácil e mais escalonáveis para API de hospedagem. 

Para toowork APIs personalizada com aplicativos lógicos, pode fornecer sua API [ *ações* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) que executam tarefas específicas em fluxos de trabalho de aplicativo lógica. Sua API também pode atuar como um [ *gatilho* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) que inicia um fluxo de trabalho do aplicativo lógico quando novos dados ou um evento atendem a uma condição especificada. Este tópico descreve os padrões comuns que você pode seguir para criar ações e gatilhos em sua API, com base no comportamento de saudação que você deseja que seu tooprovide API.

> [!TIP] 
> Embora você possa implantar suas APIs como [aplicativos web](../app-service-web/app-service-web-overview.md), considere a implantação de suas APIs como [aplicativos de API](../app-service-api/app-service-api-apps-why-best-platform.md), que pode facilitar o trabalho quando você criar, hospeda e consumir APIs na nuvem hello e no local. Você não tem qualquer código de toochange em suas APIs - apenas implantar seu aplicativo de API de tooan de código. Saiba como muito [compilar aplicativos de API criados com o ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md), [Java](../app-service-api/app-service-api-java-api-app.md), ou [Node.js](../app-service-api/app-service-api-nodejs-api-app.md). 
>
> Para obter exemplos de API App criados para aplicativos lógicos, visite Olá [repositório GitHub de aplicativos do Azure lógica](http://github.com/logicappsio) ou [blog](http://aka.ms/logicappsblog).

## <a name="helpful-tools"></a>Ferramentas úteis

Uma API personalizada funciona melhor com aplicativos lógicos quando Olá API também tem um [Swagger documento](http://swagger.io/specification/) que descreve as operações e os parâmetros de saudação da API.
Como muitas bibliotecas, [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle), pode gerar automaticamente o arquivo Swagger Olá para você. arquivo de Swagger tooannotate Olá para nomes de exibição, tipos de propriedade e assim por diante, você também pode usar [TRex](https://github.com/nihaue/TRex) para que o arquivo Swagger funciona bem com aplicativos lógicos.

<a name="actions"></a>

## <a name="action-patterns"></a>Padrões de ação

Para tarefas de tooperform de aplicativos lógica, sua API personalizada deve fornecer [ *ações*](./logic-apps-what-are-logic-apps.md#logic-app-concepts). Cada operação em sua API mapeia tooan ação. Uma ação básica é um controlador que aceita solicitações de HTTP e retorna respostas HTTP. Por exemplo, um aplicativo lógico envia um aplicativo de web de tooyour de solicitação HTTP ou o aplicativo de API. Seu aplicativo, em seguida, retorna uma resposta HTTP, juntamente com conteúdo que Olá lógica de aplicativo pode processar.

Para uma ação padrão, você pode escrever um método de solicitação HTTP em sua API e descrever esse método em um arquivo do Swagger. Em seguida, você pode chamar sua API diretamente com uma [ação HTTP](../connectors/connectors-native-http.md) ou uma ação [HTTP + Swagger](../connectors/connectors-native-http-swagger.md). Por padrão, as respostas devem ser devolvidas dentro Olá [limite de solicitação](./logic-apps-limits-and-config.md). 

![Padrão de ação padrão](./media/logic-apps-create-api-app/standard-action.png)

<a name="pattern-overview"></a>toomake um aplicativo lógico Aguarde enquanto sua API concluir tarefas de execução mais longo, sua API pode seguir Olá [assíncrona de sondagem padrão](#async-pattern) ou hello [webhook assíncrona padrão](#webhook-actions) descrito neste tópico. Para uma analogia que ajuda você a visualizar comportamentos diferentes esses padrões, imagine o processo de saudação para fazer um bolo personalizado de uma padaria. Sondagem de saudação padrão espelha comportamento Olá onde você chamar padaria Olá toocheck cada 20 minutos se bolo hello está pronto. Olá webhook padrão espelhos Olá comportamento onde padaria Olá solicita seu número de telefone para que eles podem chamar quando bolo hello está pronto.

Para obter exemplos, visite Olá [repositório GitHub de aplicativos lógica](https://github.com/logicappsio). Além disso, saiba mais sobre [medição de uso para ações](logic-apps-pricing.md).

<a name="async-pattern"></a>

### <a name="perform-long-running-tasks-with-hello-polling-action-pattern"></a>Executar tarefas de longa execução com hello sondagem padrão da ação

toohave sua API executar tarefas que podem executar mais de saudação [limite de solicitação](./logic-apps-limits-and-config.md), você pode usar padrões de sondagem assíncrona hello. Esse padrão tem seu API trabalhar em um thread separado, mas manter um mecanismo de aplicativos lógicos toohello conexão ativa. Dessa forma, o aplicativo de lógica de Olá não atinge o tempo limite ou continuar com a próxima etapa Olá no fluxo de trabalho de saudação antes de sua API concluir o trabalho.

Este é o padrão geral hello:

1. Verifique se que esse mecanismo Olá sabe que a sua API aceita a solicitação de saudação e começou a trabalhar.
2. Quando o mecanismo de saudação faz solicitações subsequentes de status do trabalho, avise mecanismo hello quando sua API termina a tarefa de saudação.
3. Retorne o mecanismo de toohello dados relevantes para que o fluxo de trabalho de aplicativo de lógica Olá possa continuar.

<a name="bakery-polling-action"></a>Agora, aplicar o padrão de sondagem de toohello analogia padaria anterior Olá e imagine que você chamar um padaria e a ordem de um bolo personalizado para entrega. processo Hello para fazer bolo de saudação leva tempo, e você não deseja toowait telefone Olá enquanto padaria Olá funciona em bolo de saudação. padaria Olá confirma seu pedido e tem a chamar a cada 20 minutos para status do bolo hello. Depois de passar de 20 minutos, chame padaria hello, mas eles indicam que o bolo não foi feito e que você deve chamar em outro 20 minutos. Esse processo back bidirecional continua até que você chamar e padaria Olá informa que o seu pedido está pronto e fornece o bolo. 

Vamos mapear esse padrão de pesquisa novamente. padaria Olá representa sua API personalizada, enquanto você, Olá bolo cliente, representa o mecanismo de aplicativos lógicos hello. Quando o mecanismo de saudação chama sua API com uma solicitação, sua API confirma a solicitação de saudação e responderá com o intervalo de tempo de saudação quando o mecanismo de saudação pode verificar o status do trabalho. mecanismo de saudação continua verificando o status do trabalho até que sua API responde que trabalho Olá é feito e retorna dados tooyour lógica app, que continua, em seguida, o fluxo de trabalho. 

![Padrão de ação de sondagem](./media/logic-apps-create-api-app/custom-api-async-action-pattern.png)

Aqui estão as etapas específicas de saudação para toofollow sua API, descrito da perspectiva de saudação da API:

1. Quando sua API obtém um HTTP solicitação toostart funcionar, retornar imediatamente um HTTP `202 ACCEPTED` resposta com hello `location` cabeçalho descrito nesta etapa. Essa resposta permite Olá aplicativos lógicos mecanismo sabe que tem sua API Olá solicitação, a carga de solicitação de saudação aceitas (dados de entrada) e está processando. 
   
   Olá `202 ACCEPTED` resposta deve incluir esses cabeçalhos:
   
   * *Necessário*: um `location` cabeçalho que especifica Olá caminho absoluto tooa URL onde o mecanismo de aplicativos lógicos Olá pode verificar status do trabalho da API

   * *Opcional*: um `retry-after` cabeçalho que especifica o número de saudação de segundos que o mecanismo de Olá deve aguardar antes de verificar Olá `location` URL para o status do trabalho. 

     Por padrão, o mecanismo de saudação verifica cada 20 segundos. toospecify um intervalo diferente, incluem hello `retry-after` cabeçalho e hello número de segundos até que a sondagem Avançar hello.

2. Após Olá especificado passar do tempo, Olá lógica aplicativos mecanismo Olá sondagens `location` status do trabalho de toocheck de URL. Sua API deve executar estas verificações e retornar estas respostas:
   
   * Se o trabalho de saudação for feito, retornar um HTTP `200 OK` resposta, juntamente com a carga de resposta da saudação (de entrada para a próxima etapa de saudação).

   * Se ainda estiver processando o trabalho hello, retornar HTTP outro `202 ACCEPTED` Olá a resposta, mas com cabeçalhos mesmo como resposta original hello.

Quando sua API segue este padrão, você não tem toodo nada no hello lógica aplicativo fluxo de trabalho definição toocontinue verificando o status do trabalho. Quando o mecanismo de saudação obtém um HTTP `202 ACCEPTED` válido e resposta `location` cabeçalho, Olá mecanismo aspectos Olá assíncrona padrão e verificações de saudação `location` cabeçalho até que sua API retorna uma resposta não 202.

> [!TIP]
> Para um padrão assíncrono de exemplo, examine o [exemplo de resposta do controlador assíncrono no GitHub](https://github.com/logicappsio/LogicAppsAsyncResponseSample).

<a name="webhook-actions"></a>

### <a name="perform-long-running-tasks-with-hello-webhook-action-pattern"></a>Executar tarefas de longa execução com padrão de ação de webhook Olá

Como alternativa, você pode usar o padrão de webhook Olá para tarefas de longa execução e o processamento assíncrono. Esse padrão tem Olá lógica aplicativo pause e aguarde de "retorno de chamada" de seu toofinish API antes de continuar o fluxo de trabalho de processamento. Esse retorno de chamada é um HTTP POST que envia a mensagem tooa URL quando ocorre um evento. 

<a name="bakery-webhook-action"></a>Agora, aplicar Olá anterior padaria analogia toohello webhook padrão e imagine que você chamar um padaria e a ordem de um bolo personalizado para entrega. processo Hello para fazer bolo de saudação leva tempo, e você não deseja toowait telefone Olá enquanto padaria Olá funciona em bolo de saudação. padaria Olá confirma sua ordem, mas desta vez, você lhes seu número de telefone para que eles podem chamar quando bolo de saudação é feito. Neste momento, padaria Olá informa quando seu pedido está pronto e entrega o bolo.

Quando é mapear esse padrão de webhook novamente, padaria Olá representa sua API personalizada, enquanto você, Olá bolo cliente, representam Olá aplicativos lógicos mecanismo. mecanismo de saudação chama sua API com uma solicitação e inclui uma URL de "retorno de chamada".
Quando terminar de trabalho hello, sua API usa o mecanismo de Olá Olá URL toonotify e retornar dados tooyour o aplicativo lógico, que continua, em seguida, o fluxo de trabalho. 

Para esse padrão, configure dois pontos de extremidade em seu controlador: `subscribe` e `unsubscribe`

*  `subscribe`ponto de extremidade: quando a execução atinge a ação da API no fluxo de trabalho hello, Olá lógica aplicativos mecanismo Olá chamadas `subscribe` ponto de extremidade. Esta etapa faz Olá lógica aplicativo toocreate uma URL de retorno de chamada que sua API armazena e, em seguida, aguarde para retorno de chamada de saudação da sua API quando o trabalho for concluído. Sua API chama novamente com uma URL de toohello HTTP POST e passa quaisquer cabeçalhos e conteúdo retornado como aplicativo de lógica de entrada toohello.

* `unsubscribe`ponto de extremidade: se Olá lógica aplicativo executar for cancelado, Olá lógica aplicativos mecanismo Olá chamadas `unsubscribe` ponto de extremidade. Sua API pode cancelar o registro de URL de retorno de chamada hello e pare todos os processos conforme necessário.

![Padrão de ação do Webhook](./media/logic-apps-create-api-app/custom-api-webhook-action-pattern.png)

> [!NOTE]
> Atualmente, Olá lógica de aplicativo Designer não dá suporte a pontos de extremidade de webhook descoberta por meio de Swagger. Para este padrão ter tooadd um [ **Webhook** ação](../connectors/connectors-native-webhook.md) e especifique a URL de hello, cabeçalhos e corpo para a sua solicitação. Confira também [Gatilhos e ações do fluxo de trabalho](logic-apps-workflow-actions-triggers.md#api-connection-webhook-action). toopass na URL de retorno de chamada hello, você pode usar o hello `@listCallbackUrl()` função de fluxo de trabalho em qualquer um dos campos de saudação anterior, conforme necessário.

> [!TIP]
> Para um padrão de webhook de exemplo, reveja o [ exemplo de gatilho webhook no GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

<a name="triggers"></a>

## <a name="trigger-patterns"></a>Padrões de gatilho

Sua API personalizada pode atuar como um [ *gatilho* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) que inicia um aplicativo lógico quando novos dados ou um evento atendem a uma condição especificada. Esse gatilho pode verificar regularmente, ou aguardar e escutar, novos dados ou eventos em seu ponto de extremidade de serviço. Se atender aos novos dados ou um evento Olá condição especificada, o gatilho de saudação é acionado e inicia o aplicativo lógico hello, o que está escutando toothat gatilho. toostart lógica aplicativos dessa forma, sua API pode seguir Olá [ *sondagem gatilho* ](#polling-triggers) ou hello [ *webhook gatilho* ](#webhook-triggers) padrão. Esses padrões são semelhantes contrapartes tootheir para [sondagem ações](#async-pattern) e [ações de webhook](#webhook-actions). Além disso, saiba mais sobre [medição de uso para gatilhos](logic-apps-pricing.md).

<a name="polling-triggers"></a>

### <a name="check-for-new-data-or-events-regularly-with-hello-polling-trigger-pattern"></a>Verificar se há novos dados ou eventos regularmente com hello sondagem padrão do gatilho

Um *sondagem gatilho* atua como Olá [sondagem ação](#async-pattern) descrito anteriormente neste tópico. mecanismo de aplicativos lógicos Olá periodicamente chama e verifica o ponto de extremidade de gatilho de saudação para novos dados ou eventos. Se o mecanismo de saudação encontrar novos dados ou um evento que atende a condição especificada, o gatilho de saudação é acionado. Em seguida, o mecanismo de Olá cria uma instância de aplicativo de lógica que processa dados hello como entrada. 

![Padrão de gatilho de sondagem](./media/logic-apps-create-api-app/custom-api-polling-trigger-pattern.png)

> [!NOTE]
> Cada solicitação de sondagem conta como uma execução de ação, mesmo quando nenhuma instância do aplicativo lógico é criada. processamento de tooprevent Olá mesmos dados várias vezes, o gatilho deve limpar os dados que já foi lido e passados toohello lógica aplicativo.

Aqui estão as etapas específicas para um gatilho de sondagem, descrito da perspectiva de saudação da API:

| Encontrou novos dados ou evento?  | Resposta da API | 
| ------------------------- | ------------ |
| Encontrado | Retornar um HTTP `200 OK` status com carga de resposta da saudação (de entrada para a próxima etapa). <br/>Essa resposta cria uma instância de aplicativo de lógica e inicia o fluxo de trabalho de saudação. |
| Não encontrado | Retornar um status HTTP `202 ACCEPTED` com um cabeçalho `location` e um cabeçalho `retry-after`. <br/>Para gatilhos, Olá `location` cabeçalho também deve conter um `triggerState` parâmetro de consulta, que geralmente é "timestamp". Sua API pode usar saudação de tootrack este identificador pela última vez Olá lógica de aplicativo foi disparado. |

Por exemplo, tooperiodically Verifique seu serviço para novos arquivos, você pode criar um gatilho de sondagem que tenha esses comportamentos:

| A solicitação inclui `triggerState`? | Resposta da API |
| -------------------------------- | -------------|
| Não | Retornar um HTTP `202 ACCEPTED` status mais um `location` cabeçalho com `triggerState` definir toohello hora atual e Olá `retry-after` too15 intervalo em segundos. |
| Sim | Verifique o seu serviço para arquivos adicionados após Olá `DateTime` para `triggerState`. |

| Número de arquivos encontrados | Resposta da API |
| --------------------- | -------------|
| Arquivo único | Retornar um HTTP `200 OK` status e hello carga conteúda, atualizar `triggerState` toohello `DateTime` para Olá retornou um arquivo e definir `retry-after` too15 intervalo em segundos. |
| Vários arquivos | Retornar um arquivo por vez e um HTTP `200 OK` status, a atualização `triggerState`e conjunto hello `retry-after` too0 intervalo em segundos. </br>Estas etapas permitem mecanismo Olá sabe que há mais dados disponíveis, e esse mecanismo Olá imediatamente deve solicitar dados de saudação de URL Olá Olá `location` cabeçalho. |
| Não há arquivos | Retornar um HTTP `202 ACCEPTED` status, não altere `triggerState`e conjunto hello `retry-after` too15 intervalo em segundos. |

> [!TIP]
> Para obter um exemplo do padrão do gatilho de sondagem, reveja este [exemplo de controlador de gatilho de sondagem no GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/PollTriggerController.cs).

<a name="webhook-triggers"></a>

### <a name="wait-and-listen-for-new-data-or-events-with-hello-webhook-trigger-pattern"></a>Aguarde e escutar eventos com padrão de gatilho de webhook hello ou novos dados

Um gatilho de webhook é um *gatilho de envio por push* que aguarda e escuta novos dados ou eventos em seu ponto de extremidade de serviço. Se atender aos novos dados ou um evento hello condição, aciona o gatilho Olá especificada e cria uma instância de aplicativo lógica, que processa dados hello como entrada.
Gatilhos de Webhook atuam como Olá [ações de webhook](#webhook-actions) anteriormente descritos neste tópico e são configurados com `subscribe` e `unsubscribe` pontos de extremidade. 

* `subscribe`ponto de extremidade: quando você adiciona e salva um gatilho de webhook em seu aplicativo de lógica, Olá lógica aplicativos mecanismo Olá chamadas `subscribe` ponto de extremidade. Esta etapa faz Olá lógica aplicativo toocreate uma URL de retorno de chamada que armazena sua API. Quando há novos dados ou um evento que atenda Olá condição especificada, sua API chama novamente com uma URL de toohello HTTP POST. cabeçalhos e carga conteúdo Olá passam como entrada toohello lógica aplicativo.

* `unsubscribe`ponto de extremidade: se o gatilho de webhook hello ou aplicativo lógico inteiro for excluído, Olá lógica aplicativos mecanismo Olá chamadas `unsubscribe` ponto de extremidade. Sua API pode cancelar o registro de URL de retorno de chamada hello e pare todos os processos conforme necessário.

![Padrão de gatilho de webhook](./media/logic-apps-create-api-app/custom-api-webhook-trigger-pattern.png)

> [!NOTE]
> Atualmente, Olá lógica de aplicativo Designer não dá suporte a pontos de extremidade de webhook descoberta por meio de Swagger. Para este padrão ter tooadd um [ **Webhook** gatilho](../connectors/connectors-native-webhook.md) e especifique a URL de hello, cabeçalhos e corpo para a sua solicitação. Confira também [Gatilho HTTPWebhook](logic-apps-workflow-actions-triggers.md#httpwebhook-trigger). toopass na URL de retorno de chamada hello, você pode usar o hello `@listCallbackUrl()` função de fluxo de trabalho em qualquer um dos campos de saudação anterior, conforme necessário.
>
> processamento de tooprevent Olá mesmos dados várias vezes, o gatilho deve limpar os dados que já foi lido e passados toohello lógica aplicativo.

> [!TIP]
> Para um padrão de webhook de exemplo, reveja o [ exemplo de controlador de gatilho webhook no GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

## <a name="deploy-call-and-secure-custom-apis"></a>Implantar, chamar e proteger APIs personalizadas

Depois de criar suas APIs personalizadas, configure-as para implantação a fim de chamá-las com segurança. Saiba como muito[implantar, chamar e proteger APIs personalizadas para os aplicativos lógicos](./logic-apps-custom-hosted-api.md).

## <a name="publish-custom-apis-tooazure"></a>Publicar tooAzure APIs personalizada

toomake suas APIs personalizadas disponíveis para uso público no Azure, envie sua toohello indicações [do programa Microsoft Azure Certified](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Obter ajuda

Para obter ajuda específica com APIs personalizadas, entre em contato com [ customapishelp@microsoft.com ](mailto:customapishelp@microsoft.com).

tooask perguntas, responder a perguntas e veja que outros usuários de aplicativos do Azure lógicos estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp melhorar a lógica de aplicativos e conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos lógicos](http://aka.ms/logicapps-wish). 

## <a name="next-steps"></a>Próximas etapas

* [Medição de uso para as ações e gatilhos](logic-apps-pricing.md)
* [Processar tipos de conteúdo](./logic-apps-content-type.md)
* [Processar erros e exceções](./logic-apps-exception-handling.md)
* [Proteger o acesso a aplicativos de lógica de tooyour](./logic-apps-securing-a-logic-app.md)
* [Chamar, disparar ou aninhar aplicativos lógicos com pontos de extremidade HTTP](./logic-apps-http-endpoint.md)