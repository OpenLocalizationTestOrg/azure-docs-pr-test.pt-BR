---
title: "Implantar e chamar APIs Web e APIs REST de Aplicativos Lógicos do Azure | Microsoft Docs"
description: "Implantar e chamar APIs Web e APIs REST para fluxos de trabalho de integrações do sistema em Aplicativos Lógicos do Azure"
keywords: "APIs Web, APIs REST, conectores, fluxos de trabalho, integrações do sistema, autenticar"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 3df59ec172b037daaeed9e3eb69ffb990d70d8a5
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="deploy-and-call-custom-apis-from-logic-app-workflows"></a>Implantar e chamar APIs personalizadas de fluxos de trabalho do aplicativo lógico

Depois de [criar APIs personalizadas](./logic-apps-create-api-app.md) para usar em fluxos de trabalho de aplicativos lógicos, você deve implantar suas APIs antes de chamá-las. Você pode implantar suas APIs como [aplicativos Web](../app-service/app-service-web-overview.md), mas considere implantar suas APIs como [aplicativos de API](../app-service/app-service-web-tutorial-rest-api.md), o que facilita o trabalho quando você criar, hospedar e consumir APIs locais e na nuvem. Você não precisa alterar o código em suas APIs; basta implantar seu código para um aplicativo de API. Você pode hospedar suas APIs no [Serviço de Aplicativo do Azure](../app-service/app-service-web-overview.md), uma oferta de PaaS (plataforma como serviço) que fornece uma hospedagem de API fácil e altamente escalonável.

Embora você possa chamar qualquer API de um aplicativo lógico, para a melhor experiência, adicione [metadados do OpenAPI (antigo Swagger)](http://swagger.io/specification/) que descrevem as operações e os parâmetros de sua API. Este arquivo OpenAPI ajuda sua API a funcionar mais bem e se integrar aos aplicativos lógicos mais facilmente.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>Implantar sua API como um aplicativo Web ou aplicativo de API

Antes de chamar sua API personalizada de um aplicativo lógico, implante sua API como um aplicativo Web ou aplicativo de API do Serviço de Aplicativo do Azure. Além disso, para tornar o arquivo OpenAPI legível pelo Designer de Aplicativo Lógico do Azure, configure as propriedades de definição da API e ative o [CORS (compartilhamento de recursos entre origens)](../app-service/app-service-web-overview.md) para seu aplicativo Web ou de API.

1. No [portal do Azure](https://portal.azure.com), selecione seu aplicativo Web ou aplicativo de API.

2. No menu de aplicativos que é aberto, em **API**, escolha **Definição da API**. Defina o **Local da definição de API** como a URL de seu arquivo swagger.json do OpenAPI.

   Normalmente, a URL é exibida neste formato: `https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Link para o arquivo OpenAPI para sua API personalizada](./media/logic-apps-custom-api-deploy-call/custom-api-swagger-url.png)

3. Em **API**, escolha **CORS**. Defina a política de CORS de **Origens permitidas** como **'*'** (permitir todos).

   Essa configuração permite solicitações do Designer de Aplicativo Lógico.

   ![Permitir solicitações do Designer de Aplicativo Lógico para sua API personalizada](./media/logic-apps-custom-api-deploy-call/custom-api-cors.png)

Para obter mais informações, consulte [Criar uma API RESTful Node.js](../app-service/app-service-web-tutorial-rest-api.md).

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Chamar sua API personalizada de fluxos de trabalho de aplicativo lógico

Depois de configurar as propriedades de definição de API e os CORS, os gatilhos e ações da sua API personalizada devem ficar disponíveis para você incluir em seu fluxo de trabalho de aplicativo lógico. 

*  Para exibir sites que têm URLs do OpenAPI, você pode navegar pelos seus sites de assinatura no Designer de Aplicativos Lógicos.

*  Para exibir as ações e entradas disponíveis apontando para um documento do OpenAPI, use a [ação HTTP + Swagger](../connectors/connectors-native-http-swagger.md).

*  Para chamar qualquer API, incluindo APIs que não têm ou expõem um documento do OpenAPI, você sempre pode criar uma solicitação com a [ação HTTP](../connectors/connectors-native-http.md).

## <a name="next-steps"></a>Próximas etapas

* [Visão geral do conector personalizado](../logic-apps/custom-connector-overview.md)