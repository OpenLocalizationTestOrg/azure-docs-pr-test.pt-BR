---
title: "aaaScenario - criar um painel de informações do cliente com o Azure sem servidor | Microsoft Docs"
description: "Um exemplo de como você pode criar um cliente do painel toomanage comentários, dados sociais e muito mais com os aplicativos lógicos do Azure e funções do Azure."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a>Criação de um painel de informações do cliente em tempo real com aplicativos lógicos do Azure e funções do Azure

As ferramentas do Azure sem servidor fornecem recursos avançados tooquickly crie e hospede aplicativos em nuvem Olá, sem que seja toothink sobre infra-estrutura.  Nesse cenário, podemos criar um painel tootrigger nos comentários dos clientes, analisar comentários com o aprendizado de máquina e publicar informações de uma fonte como o Power BI ou o Azure Data Lake.

## <a name="overview-of-hello-scenario-and-tools-used"></a>Visão geral do cenário de saudação e ferramentas usadas

Em ordem tooimplement essa solução, estenderemos componentes-chave Olá dois dos aplicativos sem servidor no Azure: [funções do Azure](https://azure.microsoft.com/services/functions/) e [aplicativos do Azure lógica](https://azure.microsoft.com/services/logic-apps/).

Lógica de aplicativos é um mecanismo de fluxo de trabalho sem servidor na nuvem hello.  Ele fornece orquestração em componentes sem servidor e também conecta 100 serviços tooover e APIs.  Para este cenário, vamos criar um tootrigger de aplicativo lógica nos comentários dos clientes.  Alguns dos conectores de saudação que podem ajudá-lo reagindo toocustomer comentários incluem Outlook.com, Office 365, pesquisa Monkey, Twitter e uma solicitação HTTP [de um formulário web](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).  Olá fluxo de trabalho abaixo, podemos irá monitorar um hashtag no Twitter.

As funções fornecem serverless computação em nuvem hello.  Nesse cenário, usaremos funções do Azure tooflag tweets de clientes com base em uma série de palavras-chave predefinidas.

pode ser a solução inteira Olá [criados no Visual Studio](logic-apps-deploy-from-vs.md) e [implantado como parte de um modelo de recurso](logic-apps-create-deploy-template.md).  Também há vídeo passo a passo do cenário de saudação [no Channel 9](http://aka.ms/logicappsdemo).

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a>Criar hello lógica aplicativo tootrigger em dados de clientes

Depois de [criando um aplicativo lógico](logic-apps-create-a-logic-app.md) no Visual Studio ou Olá portal do Azure:

1. Adicione um gatilho para **novos tweets** do Twitter
2. Configure Olá gatilho toolisten tootweets em uma palavra-chave ou hashtag.

   > [!NOTE]
   > propriedade de recorrência Olá no disparador Olá determinará a frequência Olá lógica aplicativo verifica novos itens no disparador de sondagem

   ![Exemplo de gatilho do Twitter][1]

Agora, este aplicativo será acionado em todos os tweets novos.  Em seguida, podemos levar dados tweet e compreender melhor sentimento Olá expressado.  Para isso, usamos Olá [serviço cognitivas Azure](https://azure.microsoft.com/services/cognitive-services/) toodetect sentimento do texto.

1. Clique em **Nova Etapa**
1. Selecione ou procure Olá **análises de texto** conector
1. Selecione Olá **detectar sentimento** operação
1. Se solicitado, forneça uma chave de serviços Cognitivos válida para o serviço de análise do texto de saudação
1. Adicionar Olá **texto escrito** como Olá tooanalyze de texto.

Agora que temos Olá tweet dados e insights tweet hello, um número de outros conectores pode ser relevante:
* Power BI - adicionar linhas tooStreaming conjunto de dados: tweets de exibição em tempo real em um painel do Power BI.
* Azure Data Lake - anexar o arquivo: Adicionar cliente dados tooan Azure Data Lake dataset tooinclude em trabalhos de análise.
* SQL - Adicionar linhas: armazenar dados em um banco de dados para recuperação posterior.
* Slack - Envia a mensagem: um canal do Slack quando um comentário negativo requer ações de alerta.

Uma função do Azure também pode ser usado toodo computação personalizada mais sobre os dados de saudação.

## <a name="enriching-hello-data-with-an-azure-function"></a>Enriquecer Olá dados com uma função do Azure

Antes, podemos criar uma função, é preciso toohave um aplicativo de função em nossa assinatura do Azure.  Detalhes sobre a criação de uma função do Azure no portal de saudação podem [ser encontradas aqui](../azure-functions/functions-create-first-azure-function-azure-portal.md)

Para uma toobe função chamado diretamente de um aplicativo lógico, ele precisa toohave um HTTP disparar a associação.  É recomendável usar Olá **HttpTrigger** modelo.

Nesse cenário, o corpo de solicitação de saudação do hello Azure função seria texto escrito de saudação.  No código de função hello, simplesmente defina a lógica em se o texto do hello tweet contém uma palavra-chave ou frase.  função Hello próprio poderia ser mantida como simples ou complexa, conforme necessário para o cenário de saudação.

Final de saudação de função hello, simplesmente retorne um aplicativo de lógica de toohello de resposta com alguns dados.  Isso pode ser um valor booliano simples (por exemplo, `containsKeyword`), ou um objeto complexo.

![Etapa de função do Azure configurada][2]

> [!TIP]
> Ao acessar uma resposta complexa de uma função em um aplicativo da lógica, use a ação de analisar o JSON de saudação.

Depois que a função hello for salvo, podem ser adicionada em Olá lógica aplicativo criado acima.  No aplicativo de lógica de saudação:

1. Clique em tooadd um **nova etapa**
1. Selecione Olá **funções do Azure** conector
1. Selecione toochoose uma função existente e procurar função toohello criada
1. Enviar em Olá **texto escrito** para Olá **corpo da solicitação**

## <a name="running-and-monitoring-hello-solution"></a>Executando e Olá solução de monitoramento

Um dos benefícios de saudação de orquestrações sem servidor de aplicativos lógicos de criação é depuração avançada hello e recursos de monitoramento.  Qualquer execução (atual ou histórica) pode ser exibida no Visual Studio, Olá portal do Azure, ou por meio de hello API REST e SDKs.

Um dos tootest de maneiras mais fácil Olá um lógica de aplicativo está usando Olá **executar** botão no designer de saudação.  Clicando em **executar** continuará gatilho de saudação toopoll 5 segundos até que um evento é detectado e fornecer uma exibição ao vivo à medida que avança Olá executar.

Históricos de execução anteriores podem ser exibidos na folha de visão geral de saudação em Olá portal do Azure ou usando Olá Visual Studio Cloud Explorer.

## <a name="creating-a-deployment-template-for-automated-deployments"></a>Criação de um modelo de implantação para implantações automatizadas

Depois que uma solução foi desenvolvida, podem ser capturado e implantado por meio de um modelo de implantação do Azure tooany região do Azure no Olá, mundo.  Isso é útil para ambos os parâmetros de modificação para versões diferentes deste fluxo de trabalho, e também para a integração dessa solução em um pipeline de compilação e versão.  Detalhes sobre como criar um modelo de implantação podem ser encontrados [neste artigo](logic-apps-create-deploy-template.md).

As funções do Azure também podem ser incorporadas no modelo de implantação Olá - para a solução inteira Olá com todas as dependências que possa ser gerenciada como um único modelo.  Um exemplo de um modelo de implantação de função pode ser encontrado na Olá [repositório de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).

## <a name="next-steps"></a>Próximas etapas

* [Confira outros exemplos e cenários de aplicativos lógicos do Azure](logic-apps-examples-and-scenarios.md)
* [Assista a um vídeo passo a passo sobre como criar essa solução de ponta a ponta](http://aka.ms/logicappsdemo)
* [Saiba como toohandle e capturar exceções em um aplicativo de lógica](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png