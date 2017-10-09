---
title: "mensagens de aaaEncode AS2 - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Como toouse Olá codificador AS2 Olá Enterprise Integration Pack para aplicativos do Azure lógica"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Codificar mensagens AS2 para os aplicativos lógicos do Azure com hello Enterprise Integration Pack

tooestablish segurança e confiabilidade ao transmitir mensagens, use o conector de mensagem AS2 codificar hello. Esse conector fornece confirmações por meio de mensagem disposição notificações MDN (), que também leva toosupport para não-repúdio, criptografia e assinatura digital.

## <a name="before-you-start"></a>Antes de começar

Aqui está a itens Olá que necessários:

* Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)
* Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure. Você deve ter um conector de mensagem integração conta toouse Olá codificar AS2.
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração
* Um [contrato AS2](logic-apps-enterprise-integration-as2.md) que já está definido em sua conta de integração

## <a name="encode-as2-messages"></a>Codificar mensagens AS2

1. [Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).

2. conector de mensagem AS2 codificar Olá não tem gatilhos, portanto você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação. No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.

3.  Na caixa de pesquisa hello, digite "AS2" para o filtro. Selecione **AS2 - Codificar Mensagem AS2**.
   
    ![Procure "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão. Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect. 
   
    ![Criar conexão toointegration conta](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    As propriedades com um asterisco são obrigatórias.

    | Propriedade | Detalhes |
    | --- | --- |
    | Nome da Conexão * |Digite um nome para a conexão. |
    | Uma conta de integração * |Insira um nome para sua conta de integração. Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure. |

5.  Quando terminar, os detalhes de conexão devem ser exemplo toothis semelhante. toofinish criar sua conexão, escolha **criar**.
   
    ![detalhes de conexão de integração](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. Depois de criar sua conexão, conforme mostrado neste exemplo, forneça detalhes para **AS2-de**, **AS2 tooidentifiers** conforme configurado no seu contrato e **corpo**, que é carga de mensagem de saudação.
   
    ![fornecer campos obrigatórios](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a>Detalhes do codificador AS2

conector de codificar AS2 Olá executa essas tarefas: 

* Aplica cabeçalhos HTTP/AS2
* Sinaliza mensagens de saída (se configurado)
* Criptografa mensagens de saída (se configurado)
* Compacta a mensagem de saudação (se configurado)

## <a name="try-this-sample"></a>Experimente este exemplo

tootry implantar uma lógica totalmente operacional exemplo e aplicativo AS2 cenário, consulte Olá [AS2 cenário e o modelo de aplicativo de lógica](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Swagger de saudação do modo de exibição
Consulte Olá [swagger detalhes](/connectors/as2/). 

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

