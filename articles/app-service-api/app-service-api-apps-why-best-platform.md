---
title: "Introdução de aplicativos aaaAPI | Microsoft Docs"
description: "Saiba como o Serviço de Aplicativo do Azure ajuda você a desenvolver, hospedar e consumir APIs RESTful."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 60049a16-8159-47aa-a34b-110be0d8dab6
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: alkarche
ms.openlocfilehash: f066e96db667d4685480001bc43c2b1bff4ea352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-apps-overview"></a>Visão geral de Aplicativos de API
Aplicativos de API em recursos de oferta de serviço de aplicativo do Azure que o tornam mais fácil toodevelop, hospedar e consumir APIs em nuvem hello e local. Com aplicativos de API, você obtém segurança de nível corporativo, controle de acesso simples, conectividade híbrida, geração automática do SDK e integração perfeita com [Aplicativos Lógicos](../logic-apps/logic-apps-what-are-logic-apps.md).

[Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) é uma plataforma completamente gerenciada para Web, móvel e situações de integração. Os Aplicativos de API são um dos quatro tipos de aplicativos oferecidos pelo [Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md).

![Tipos de aplicativos no Serviço de Aplicativo do Azure](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## <a name="why-use-api-apps"></a>Por que usar Aplicativos de API?
Aqui estão alguns dos principais recursos dos aplicativos de API:

* **Traga a sua API existente como-é** - você não tem toochange qualquer Olá código na sua vantagem de tootake APIs existente dos aplicativos de API – basta implantar seu aplicativo de tooan API de código. Sua API pode usar qualquer linguagem ou estrutura com suporte do Serviço de Aplicativo, incluindo ASP.NET e C#, Java, PHP, Node.js e Python.
* **Consumo fácil** - O suporte integrado para [Metadados de API do Swagger](http://swagger.io/) torna suas APIs facilmente consumíveis por uma variedade de clientes.  Geração automática de código do cliente para suas APIs em uma variedade de linguagens incluindo C#, Java e Javascript. Configure facilmente [CORS](app-service-api-cors-consume-javascript.md) sem alterar seu código. Para obter mais informações, consulte [Metadados de Aplicativos de API do Serviço de Aplicativo para geração de códigos e descoberta de API](app-service-api-metadata.md) e [Consumir um aplicativo de API do JavaScript usando CORS](app-service-api-cors-consume-javascript.md). 
* **Controle de acesso simples** -proteger um aplicativo de API de acesso não autenticado com o código de tooyour sem alterações. Serviços de autenticação internos protegem as APIs para acesso por outros serviços ou por clientes que representam usuários. Os provedores de identidade com suporte incluem Azure Active Directory, Facebook, Twitter, Google e Conta da Microsoft. Os clientes podem usar a biblioteca de autenticação do Active Directory (ADAL) ou hello SDK de aplicativos móveis. Para saber mais, confira [Autenticação e autorização para Aplicativos de API no Serviço de Aplicativo do Azure](app-service-api-authentication.md).
* **Integração do Visual Studio** -dedicadas ferramentas no Visual Studio simplificar o trabalho de saudação de criação, implantação, consumindo, depuração e gerenciar aplicativos de API. Para obter mais informações, consulte [apresentação dos Olá 2.8.1 do SDK do Azure para .NET](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).
* **Integração com Aplicativos lógicos** - Aplicativos de API criados por você podem ser consumidos por [Aplicativos lógicos do Serviço de Aplicativo](../logic-apps/logic-apps-what-are-logic-apps.md).  Para saber mais, confira [Usando a API personalizada hospedada no Serviço de Aplicativo com Aplicativos lógicos](../logic-apps/logic-apps-custom-hosted-api.md) e [Nova versão de esquema 2015-08-01-preview](../logic-apps/logic-apps-schema-2015-08-01.md).

Além disso, um aplicativo de API pode tirar proveito dos recursos oferecidos pelos [Aplicativos Web](../app-service-web/app-service-web-overview.md) e [Aplicativos Móveis](../app-service-mobile/app-service-mobile-value-prop.md). Olá inverso também é verdadeiro: se você usar um aplicativo web ou aplicativo móvel toohost uma API, pode levar vantagem dos recursos de aplicativos de API, como os metadados do Swagger para cliente de geração de código e CORS para acesso do navegador de domínio cruzado. Olá apenas uma diferença entre os tipos de aplicativo três hello (API, web, móvel) é Olá nome e ícone usado para eles no hello portal do Azure.

## <a name="whats-hello-difference-between-api-apps-and-azure-api-management"></a>Qual é a diferença Olá entre aplicativos de API e gerenciamento de API do Azure?
Os Aplicativos de API e o [Gerenciamento de API do Azure](../api-management/api-management-key-concepts.md) são serviços complementares:

* O Gerenciamento de API trata do gerenciamento de APIs. Você colocar um front-end de API de gerenciamento em uma API toomonitor e limitar o uso, manipular a entrada e saída, consolida várias APIs em um ponto de extremidade e assim por diante. Olá APIs que estão sendo gerenciados pode ser hospedado em qualquer lugar.
* Os Aplicativos de API tratam da hospedagem de APIs. serviço de saudação inclui recursos que facilitam o desenvolvimento e consumo de APIs, mas não faz Olá tipos de monitoramento, limitação, manipular ou consolidação de que o gerenciamento de API não. Se você não precisa de recursos do Gerenciamento de API, pode hospedar APIs em aplicativos de API sem usar o Gerenciamento de API.

Aqui está um diagrama que ilustra o Gerenciamento de API usado para APIs hospedadas em aplicativos de API e em outros lugares.

![Gerenciamento de API do Azure e Aplicativos de API](./media/app-service-api-apps-why-best-platform/apia-apim.png)

Alguns recursos de Gerenciamento de API e Aplicativos de API têm funções semelhantes.  Por exemplo, ambos podem automatizar o suporte a CORS. Quando você usa dois serviços de saudação juntos, você usaria o gerenciamento de API para CORS desde que ele funcione conforme Olá front-end tooyour API aplicativos. 

## <a name="getting-started"></a>Introdução
tooget Introdução aos aplicativos de API Implantando tooone de código de exemplo, consulte o tutorial de saudação para qualquer estrutura de sua preferência:

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.js](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

tooask perguntas sobre aplicativos de API, iniciar um thread em Olá [Fórum de aplicativos de API](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps). 

