---
title: "aaaExamples & comuns cenários - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Saiba mais sobre os aplicativos lógicos com tutoriais, exemplos e cenários"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/9/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 17caa8539ec6a57726b9c6c07a71fb74caa07ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a>Exemplos e cenários comuns para Aplicativos Lógicos do Azure

toohelp Saiba mais sobre Olá muitos recursos em aplicativos do Azure lógica e padrões, aqui estão exemplos e cenários comuns.

## <a name="key-scenarios-for-logic-apps"></a>Principais cenários de aplicativos lógicos

O Aplicativo Lógico do Azure fornece orquestração e integração resiliente para serviços diferentes. saudação de serviço de aplicativos lógicos é "sem servidor", para que você não tem tooworry sobre escala ou instâncias – tudo o que você tem toodo é definir o fluxo de trabalho de saudação (gatilho e ações). plataforma subjacente Olá lida com a escala, disponibilidade e desempenho. Qualquer cenário em que você precisa toocoordinate várias ações, especialmente em vários sistemas, é um ótimo caso de uso para os aplicativos lógicos do Azure. Confira aqui alguns padrões e exemplos.

## <a name="respond-tootriggers-and-extend-actions"></a>Responder tootriggers e estender ações

Cada aplicativo lógico começa com um gatilho. Por exemplo, o fluxo de trabalho pode começar com um evento de agendamento, uma invocação manual ou um evento de um sistema externo, como Olá gatilho "quando um arquivo é adicionado tooan FTP server". Aplicativos lógicos do Azure atualmente oferece suporte a mais de 100 conectores prontos para uso, variando de local SAP tooMicrosoft serviços Cognitivos. Para sistemas e serviços que talvez não tenham conectores publicados, também é possível estender os aplicativos lógicos.

* [Criar gatilhos ou ações personalizadas](../logic-apps/logic-apps-create-api-app.md)
* [Configurar ações de longa execução para execução de fluxo de trabalho](../logic-apps/logic-apps-create-api-app.md)
* [Responder a eventos de tooexternal e as ações com webhooks](../logic-apps/logic-apps-create-api-app.md)
* [Chamada, gatilho, ou aninhar fluxos de trabalho com solicitações de tooHTTP respostas síncrona](../logic-apps/logic-apps-http-endpoint.md)
* [Tutorial: Responder tooTwilio SMS webhooks e enviar uma resposta de texto](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [Tutorial: Compilar um painel social capacitado por IA em minutos com o Aplicativo Lógicos e o Power BI](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a>Tratamento de erros, registro em log e recursos de fluxo de controle

Os aplicativos lógicos incluem recursos avançados para o fluxo de controle avançado, como comutadores, condições, loops e escopos. soluções de tooensure resiliente, você também pode implementar erro e tratamento de exceção no seus fluxos de trabalho. Para receber notificação e logs de diagnóstico para status de execução de fluxo de trabalho, o Aplicativo Lógico do Azure também fornece monitoramento e alertas.

* [Executar ações diferentes com instruções switch](../logic-apps/logic-apps-switch-case.md)
* [Processar itens em matrizes e coleções com loops e lotes em aplicativos lógicos](../logic-apps/logic-apps-loops-and-scopes.md)
* [Manipulação de erro e exceções do autor em um fluxo de trabalho](../logic-apps/logic-apps-exception-handling.md)
* [Ativar o monitoramento, o registro em log e alertas para aplicativos lógicos existentes](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Ativar o monitoramento e o registro em log de diagnóstico durante a criação de aplicativos lógicos](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [Caso de uso: Como uma empresa de assistência médica usa a manipulação de exceção do aplicativo lógico para fluxos de trabalho HL7 FHIR](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a>Implantar e gerenciar aplicativos lógicos

Você pode desenvolver e implantar totalmente aplicativos lógicos com o Visual Studio, o Visual Studio Team Services ou qualquer outra ferramenta de controle do código-fonte e compilação automatizada. implantação de toosupport para fluxos de trabalho e conexões dependentes em um modelo de recurso, aplicativos lógicos usam modelos de implantação de recursos do Azure. Ferramentas do Visual Studio geram automaticamente esses modelos, o que você pode ver no controle toosource para controle de versão.

* [Criar modelos um modelo de implantação automatizado](../logic-apps/logic-apps-create-deploy-template.md)
* [Compilar e implantar aplicativos lógicos do Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md)
* [Olá monitorar a integridade de seus aplicativos lógicos](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a>Tipos de conteúdo, conversões e transformações em uma execução

Você pode acessar, converter e transformar vários tipos de conteúdo usando Olá muitas funções em hello Azure lógica aplicativos [linguagem de definição de fluxo de trabalho](http://aka.ms/logicappsdocs). Por exemplo, você pode converter entre uma cadeia de caracteres, JSON e XML com hello `@json()` e `@xml()` expressões de fluxo de trabalho. mecanismo de aplicativos lógicos Olá preserva a transferência de conteúdo de toosupport de tipos de conteúdo de uma maneira sem perda entre serviços.

* [Lidar com tipos de conteúdo não JSON](../logic-apps/logic-apps-content-type.md), como `application/xml`, `application/octet-stream` e `multipart/formdata`
* [Como funcionam as expressões de fluxo de trabalho em aplicativos lógicos](../logic-apps/logic-apps-author-definitions.md)
* [Referência: Linguagem de definição de fluxo de trabalho do Aplicativo Lógico do Azure](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a>Outros recursos e integrações

Os aplicativos lógicos também oferecem integração com muitos serviços, como o Azure Functions, O Gerenciamento de API do Azure, Serviços de Aplicativo do Azure e pontos de extremidade HTTP personalizados, por exemplo, REST e SOAP.

* [Criar um painel social em tempo real com o Azure sem servidor](../logic-apps/logic-apps-scenario-social-serverless.md)
* [Chamar o Azure Functions de aplicativos lógicos](../logic-apps/logic-apps-azure-functions.md)
* [Cenário: Disparar aplicativos lógicos com o Azure Functions](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [Blog: Chamar pontos de extremidade SOAP de aplicativos lógicos](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a>Cenários de ponta a ponta

* [White paper: Gerenciamento de casos completos de integração empresarial com serviços do Azure, como Aplicativos Lógicos](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="next-steps"></a>Próximas etapas

- [Tratar erros e exceções em aplicativos lógicos](../logic-apps/logic-apps-exception-handling.md)
- [Criar definições de fluxo de trabalho com a linguagem de definição de fluxo de trabalho Olá](../logic-apps/logic-apps-author-definitions.md)
- [Envie seus comentários, dúvidas ou sugestões para podermos aprimorar o Aplicativo Lógico do Azure](https://feedback.azure.com/forums/287593-logic-apps)