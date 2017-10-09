---
title: aaaOverview do Azure sem servidor | Microsoft Docs
description: "Crie poderosas soluções na nuvem Olá sem ter toothink sobre infra-estrutura."
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
ms.openlocfilehash: 7c9c09d96e472edd1631892982ac60aae97342a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-serverless-with-functions-and-logic-apps"></a>Visão geral do Azure Serverless com Funções e Aplicativos Lógicos

Aplicativos sem servidor oferecem benefícios de um aumento na velocidade do desenvolvimento, redução no código necessário e simplicidade com escala.  Este artigo vai para atributos diferentes Olá soluções sem servidor e as ofertas do Azure sem servidor.

## <a name="what-is-serverless"></a>O que é sem servidor?

Sem servidor não significa que não existem servidores – isso apenas significa desenvolvedor Olá não tem tooworry sobre servidores.  Uma grande parte do desenvolvimento tradicional de aplicativos está respondendo perguntas sobre escala, hospedagem e monitoramento demandas de saudação toomeet soluções de aplicativo hello.  Com sem servidor, essas perguntas são manipuladas como parte da solução de saudação.  Além disso, aplicativos sem servidor são cobrados em um plano baseado em consumo.  Se o aplicativo hello nunca é usado, um encargo nunca é gerado.  Esses recursos permitem que os desenvolvedores toofocus exclusivamente na lógica de negócios de saudação de solução de saudação.

Olá principais serviços no Azure ao redor sem servidor estão [funções do Azure](https://azure.microsoft.com/services/functions/) e [aplicativos do Azure lógica](https://azure.microsoft.com/services/logic-apps/).  Essas duas soluções seguem Olá princípios acima e permitem aos desenvolvedores de aplicativos em nuvem robusto toobuild com mínimas de código.

## <a name="what-are-azure-functions"></a>O que são Azure Functions?

As funções do Azure é uma solução para executar facilmente pequenos pedaços de código ou "funções", na nuvem de saudação. Você pode gravar apenas o código Olá que é necessário para problema de saudação à mão, sem se preocupar um toorun de infraestrutura de aplicativo ou hello todo ele. Funções podem tornar o desenvolvimento ainda mais produtivo e você pode usar a linguagem de desenvolvimento de sua escolha, por exemplo, C#, F#, Node.js, Python ou PHP. Pague somente pelo tempo de saudação que seu código é executado e o Azure é dimensionado conforme necessário.

Se você quiser toojump direita e começar com funções do Azure, comece com [criar sua primeira função Azure](../azure-functions/functions-create-first-azure-function.md). Se você estiver procurando para obter informações técnicas sobre funções, consulte Olá [referência do desenvolvedor](../azure-functions/functions-reference.md).

## <a name="what-are-azure-logic-apps"></a>O que é o Aplicativo Lógico do Azure?

Aplicativos lógicos do Azure fornece uma maneira toosimplify e implementar integrações escalonáveis e fluxos de trabalho na nuvem hello. Ele fornece um toomodel designer visual e automatizar o processo de uma série de etapas chamado um fluxo de trabalho.  Há [muitos conectores](../connectors/apis-list.md) em serviços de nuvem e local tooquickly conectar tooother um aplicativo sem servidor APIs.  Um aplicativo lógico começa com um gatilho (como 'quando uma conta é adicionada tooDynamics CRM') e depois de acionamento pode começar a muitas ações de combinações, conversões e a lógica da condição.  Lógica de aplicativos é uma ótima opção quando orquestrar a diferentes funções do Azure em um processo - especialmente quando o processo de saudação requer interação com um sistema externo ou a API.

tooget iniciado com aplicativos lógicos, comece com [criando seu primeiro aplicativo lógica](logic-apps-create-a-logic-app.md).  Se você estiver procurando para obter informações técnicas sobre aplicativos lógicos, consulte Olá [referência do desenvolvedor](logic-apps-workflow-actions-triggers.md).

## <a name="how-can-i-build-and-deploy-serverless-applications-in-azure"></a>Como criar e implantar aplicativos Serverless no Azure?

O Azure fornece um rico conjunto de ferramentas em desenvolvimento, implantação e gerenciamento de aplicativos Serverless.  Aplicativos podem ser criados diretamente no portal do Azure de saudação ou com [ferramentas do Visual Studio](logic-apps-serverless-get-started-vs.md).  Depois que um aplicativo tiver sido desenvolvido, ele poderá ser [implantado instantaneamente](logic-apps-create-deploy-template.md).  O Azure também fornece monitoramento para aplicativos sem servidor.  Esse monitoramento pode ser acessado de saudação portal do Azure, por meio da API hello ou SDKs, ou tooOMS integrado de ferramentas e o Application Insights.

## <a name="next-steps"></a>Próximas etapas

* [Introdução à criação de um aplicativo Serverless no Visual Studio](logic-apps-serverless-get-started-vs.md)
* [Crie um painel do Customer Insights com o Serverless](logic-apps-scenario-social-serverless.md)
* [Criar um modelo de implantação para um aplicativo lógico](logic-apps-create-deploy-template.md)