---
title: aaaBuild um aplicativo sem servidor no Visual Studio | Microsoft Docs
description: Comece com seu primeiro aplicativo sem servidor neste guia em criar, implantar e gerenciar o aplicativo hello no Visual Studio.
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
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a>Criar um aplicativo sem servidor no Visual Studio com os Aplicativos Lógicos e o Functions

Ferramentas e funcionalidades sem servidor do Azure permitem rápido desenvolvimento e implantação de aplicativos de nuvem.  Este documento se concentra em como tooget iniciado no Visual Studio, criando um aplicativo sem servidor.  Uma visão geral do uso sem servidor no Azure [pode ser encontrada neste artigo](logic-apps-serverless-overview.md).

## <a name="getting-everything-ready"></a>Deixando tudo pronto

Aqui está Olá pré-requisitos necessários toobuild um aplicativo sem servidor do Visual Studio:

* [Visual Studio 2017](https://www.visualstudio.com/vs/) ou Visual Studio 2015 – Community, Professional ou Enterprise
* [Ferramentas de Aplicativos Lógicos para Visual Studio](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* [SDK mais recente do Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou superior)
* [PowerShell do Azure](https://github.com/Azure/azure-powershell#installation)
* [Ferramentas de núcleo de funções do Azure](https://www.npmjs.com/package/azure-functions-core-tools) toodebug funções localmente
* Web toohello de acesso ao usar o hello inseridos designer do aplicativo lógico

## <a name="getting-started-with-a-deployment-template"></a>Introdução a um modelo de implantação

O gerenciamento de recursos no Azure é realizado dentro de um grupo de recursos.  Um grupo de recursos é um agrupamento lógico de recursos.  Grupos de recursos permitem a implantação e o gerenciamento de uma coleção de recursos.  Para um aplicativo sem servidor no Azure, nosso grupo de recursos contém tanto Aplicativo Lógico do Azure quanto Azure Functions.  Usando o projeto do grupo de recursos de saudação do Visual Studio, estamos toodevelop capaz de gerenciar e implantar o aplicativo inteiro hello como um único ativo.

### <a name="create-a-resource-group-project-in-visual-studio"></a>Criar um projeto de grupo de recursos no Visual Studio

1. No Visual Studio, clique em tooadd um **novo projeto**
1. Em Olá **nuvem** categoria, selecione toocreate um Azure **grupo de recursos** projeto  
 * Se você não vir a categoria de saudação ou projeto listado, certifique-se de que você tem hello Azure SDK instalado para Visual Studio
1. Dê o projeto Olá um nome e local e selecione **Okey** toocreate Visual Studio solicitará tooselect um modelo.  Você pode selecionar toostart de espaço em branco, comece com uma lógica de aplicativo ou outro recurso.  No entanto, nesse caso é usar um tooget de modelo de início rápido do Azure que nos iniciado com um aplicativo sem servidor.
1. Selecione modelos de tooshow de **início rápido do Azure** ![modelos selecionando o início rápido do Azure][1]
1. Modelo de início rápido sem servidor selecione Olá: **101-logic-app-and-function-app** e clique em **Okey**

modelo de início rápido de saudação cria um modelo de implantação em seu projeto de grupo de recursos.  modelo de saudação contém um aplicativo lógica simples que chama uma funções do Azure e retorna o resultado de saudação.  Se você abrir Olá `azuredeploy.json` Olá de arquivo no Gerenciador de soluções, você pode ver os recursos de saudação do aplicativo sem servidor de saudação.

## <a name="deploying-hello-serverless-application"></a>Implantação de aplicativo sem servidor hello

Para abrir o designer visual do aplicativo lógico Olá no Visual Studio, deve toobe um grupo de recursos do Azure pré-instalado.  Isso permite que toocreate designer hello e use conexões tooresources e serviços no aplicativo de lógica de saudação.  tooget iniciado, simplesmente precisamos toodeploy Olá solução criada.

1. Projeto de saudação com o botão direito no Visual Studio, selecione **implantar**e criar um **novo** implantação ![selecionando nova implantação de recursos][2]
1. Selecione um Grupo de Recursos e uma assinatura válida do Azure
1. Selecione também**implantar** Olá solução
1. Insira no nome Olá Olá lógica de aplicativo e hello aplicativo de função do Azure.  o nome da função do Azure Olá necessário toobe globalmente exclusivo

solução sem servidor Olá implanta no grupo de recursos especificado hello.  Se você observar Olá **saída** no Visual Studio, você pode ver o status de saudação da implantação de saudação.

## <a name="editing-hello-logic-app-in-visual-studio"></a>Editar aplicativo de lógica de saudação no Visual Studio

Depois que a solução Olá foi implantada em qualquer grupo de recursos, designer visual Olá pode ser tooedit usado e fazer alterações toohello lógica aplicativo.

1. Saudação de atalho `azuredeploy.json` no hello Gerenciador de soluções e selecione **abrir com lógica de aplicativos Designer**
1. Selecione Olá **grupo de recursos** e **local** Olá solução tenha sido implantado selecione tooand **Okey**

designer visual do aplicativo lógico Olá agora deve ser visível com o Visual Studio.  Continuar tooadd etapas, modificar o fluxo de trabalho hello e salvar as alterações.  Você também pode criar aplicativo lógico do Visual Studio.  Se clicar Olá **recursos** no navegador de modelo hello, você pode escolher tooadd um **aplicativo lógico** toohello projeto.  Carregar aplicativos lógicos vazio no designer visual de saudação sem um pré-implantar em um grupo de recursos.

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a>Gerenciar e exibir o histórico de execução para um aplicativo lógico implantado

Você também pode gerenciar e exibir o histórico Olá executar lógica aplicativos implantados no Azure.  Se você abrir Olá **Cloud Explorer** ferramenta no Visual Studio, clique qualquer lógica de aplicativo e escolha tooedit, desabilitar, exibir propriedades ou exibir o histórico de execução.  Clicando em Editar também permite que você toodownload um aplicativo publicado lógica em um projeto do grupo de recursos do Visual Studio.  Isso significa que mesmo se você começou a criar seu aplicativo lógica Olá portal do Azure, você pode ainda importá-lo e gerenciá-lo do Visual Studio.

## <a name="developing-an-azure-function-in-visual-studio"></a>Desenvolvendo uma Função do Azure no Visual Studio

modelo de implantação Hello implanta todas as funções do Azure que estão contidos na solução Olá para repositório git de saudação especificado no hello `azuredeploy.json` variáveis.  Se você criar um projeto de função na solução hello, inclua-o no controle de origem (GitHub, Visual Studio Team Services, etc.) e atualizar Olá `repo` variável modelo Olá implantará Olá função do Azure.

### <a name="creating-an-azure-function-project"></a>Criar um projeto de Função do Azure

Se usando JavaScript, Python, F #, Bash, lote ou o PowerShell, execute Olá [etapas Olá funções CLI](../azure-functions/functions-run-local.md) toocreate um projeto.  Se o desenvolvimento de uma função em c#, você pode usar um [biblioteca de classes do c#](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) na solução atual de saudação para Olá função do Azure.

## <a name="next-steps"></a>Próximas etapas

* [Saiba como toobuild um painel social sem servidor](logic-apps-scenario-social-serverless.md)
* [Gerenciar um aplicativo lógico do Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Linguagem de definição de fluxo de trabalho de aplicativo lógico](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
