---
title: "soluções aaaCreate B2B - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Receber dados em aplicativos lógicos usando recursos de saudação B2B do hello Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a>Receber dados em aplicativos de lógica com recursos de B2B Olá Olá Enterprise Integration Pack

Depois de criar uma conta de integração com parceiros e acordos, você está pronto toocreate um fluxo de trabalho do negócio toobusiness (B2B) para seu aplicativo lógico com hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).

## <a name="prerequisites"></a>Pré-requisitos

toouse Olá AS2 e X12 ações, você deve ter uma conta de integração da empresa. Saiba [como toocreate uma integração Enterprise conta](../logic-apps/logic-apps-enterprise-integration-accounts.md).

## <a name="create-a-logic-app-with-b2b-connectors"></a>Criar um aplicativo lógico com conectores B2B

Siga estas etapas toocreate um B2B lógica aplicativo usa hello AS2 e X12 dados de tooreceive ações de um parceiro comercial:

1. Criar um aplicativo lógico, em seguida, [vincular sua conta de integração do aplicativo tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).

2. Adicionar um **solicitar - quando HTTP de uma solicitação é recebida** gatilho tooyour lógica aplicativo.

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. Olá tooadd **decodificar AS2** ação, selecione **adicionar uma ação**.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. toofilter todos os toohello de ações que você deseja, insira palavras Olá **as2** na caixa de pesquisa de saudação.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. Selecione Olá **AS2 - mensagem AS2 decodificar** ação.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. Adicionar Olá **corpo** que você deseja toouse como entrada. Neste exemplo, selecione o corpo da saudação de solicitação HTTP Olá gatilhos Olá aplicativo lógico. Ou insira uma expressão que entradas cabeçalhos Olá Olá **CABEÇALHOS** campo:

    @triggerOutputs()['headers']

7. Adicionar Olá necessário **cabeçalhos** para AS2, que pode ser encontrado nos cabeçalhos de solicitação HTTP de saudação. Neste exemplo, selecione cabeçalhos Olá de solicitação HTTP Olá esse aplicativo de lógica de saudação do gatilho.

8. Agora adicione ação de mensagem de decodificação X12 hello. Escolha **Adicionar uma ação**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. toofilter todos os toohello de ações que você deseja, insira palavras Olá **x12** na caixa de pesquisa de saudação.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. Selecione Olá **X12-decodificar X12 mensagem** ação.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. Agora você deve especificar a ação de entrada toothis hello. Essa entrada é saída de saudação da ação de AS2 anterior hello.

    conteúdo de mensagem real Hello está em um objeto JSON e é codificação base64, portanto, você deve especificar uma expressão como entrada hello. 
    Digite hello seguinte expressão em Olá **X12 simples mensagem de arquivo tooDECODE** campo de entrada:
    
    @base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])

    Agora adicione etapas dados de saudação X12 toodecode recebida do parceiro comercial de saudação e itens em um objeto JSON de saída. 
    parceiro de saudação toonotify que Olá dados foi recebido, você pode enviar de volta uma resposta que contém a saudação AS2 mensagem disposição MDN (notificação) em uma ação de resposta HTTP.

12. Olá tooadd **resposta** ação, escolha **adicionar uma ação**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. toofilter todos os toohello de ações que você deseja, insira palavras Olá **resposta** na caixa de pesquisa de saudação.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. Selecione Olá **resposta** ação.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. tooaccess Olá MDN de saída Olá Olá **mensagem X12 de decodificação** action, a resposta de saudação do conjunto **corpo** campo com esta expressão:

    @base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. Salve seu trabalho.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

Você concluiu a configuração de seu aplicativo lógico de B2B. Em um aplicativo do mundo real, você pode querer toostore Olá decodificado X12 dados em um repositório de linha de negócios (LOB) dados ou aplicativo. tooconnect seus próprios aplicativos LOB e use essas APIs em seu aplicativo de lógica, você pode adicionar mais ações ou APIs personalizadas de gravação.

## <a name="features-and-use-cases"></a>Recursos e casos de uso

* Olá AS2 X12 decodificar e codificar ações permitem que você trocar dados entre parceiros comerciais usando protocolos padrão da indústria em aplicativos lógicos.
* tooexchange dados com parceiros comerciais, você pode usar AS2 e X12 com ou sem o outro.
* ações de B2B Olá ajudarão-lo a criar facilmente parceiros e acordos em sua conta de integração e consumi-los em um aplicativo de lógica.
* Estendendo o seu Aplicativo Lógico com outras ações, você pode enviar e receber dados de e para outros aplicativos e serviços, como o SalesForce.

## <a name="learn-more"></a>Saiba mais
[Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md)
