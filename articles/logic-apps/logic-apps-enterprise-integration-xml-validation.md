---
title: "aaaValidate XML - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Validar XML com esquemas para os aplicativos lógicos do Azure e a cenários B2B usando Olá Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a>Validar XML para integração corporativa

Geralmente em cenários B2B, parceiros de saudação em um contrato devem Certifique-se de que as mensagens de saudação que do exchange que são válidas antes de iniciar o processamento de dados. Você pode validar documentos em um esquema predefinido usando o conector de validação de XML de Olá Olá use em Olá Enterprise Integration Pack.

## <a name="validate-a-document-with-hello-xml-validation-connector"></a>Validar um documento com o conector de validação de XML Olá

1. Criar um aplicativo lógico, e [vincular Olá aplicativo toohello integração conta](../logic-apps/logic-apps-enterprise-integration-accounts.md "Saiba toolink um aplicativo de conta tooa lógica da integração") que tem o esquema de saudação desejar toouse para validar dados XML.

2. Adicionar um **solicitar - quando HTTP de uma solicitação é recebida** gatilho tooyour lógica aplicativo.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. Olá tooadd **validação de XML** ação, escolha **adicionar uma ação**.

4. toofilter todos Olá toohello de ações que você desejar, digite *xml* na caixa de pesquisa de saudação. Escolha **Validação de XML**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. Olá toospecify conteúdo XML que você deseja toovalidate, selecione **conteúdo**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. Selecione a marca de corpo de Olá como Olá conteúdo que você deseja toovalidate.

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. esquema de saudação toospecify você deseja toouse para validar a saudação anterior *conteúdo* de entrada, escolha **nome do esquema**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. Salve seu trabalho   

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

Agora, a configuração do conector de validação foi concluída. Em um aplicativo do mundo real, você poderá toostore dados de saudação validada em um aplicativo da linha de negócios (LOB) como o SalesForce. toosend Olá tooSalesforce saída validado, adicione uma ação.

tootest a ação de validação, criar um ponto de extremidade de toohello HTTP de solicitação.

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre Olá Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")   

