---
title: "mensagens de aaaDecode AS2 - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Como toouse Olá decodificador de AS2 no hello Enterprise Integration Pack para aplicativos do Azure lógica"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Decodificar mensagens AS2 para aplicativos do Azure lógica com hello Enterprise Integration Pack 

tooestablish segurança e confiabilidade ao transmitir mensagens, use o conector de mensagem AS2 decodificar hello. Esse conector fornece a assinatura digital, descriptografia e confirmações por meio de MDN (notificações de disposição de mensagem).

## <a name="before-you-start"></a>Antes de começar

Aqui está a itens Olá que necessários:

* Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)
* Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure. Você deve ter um conector de mensagem integração conta toouse Olá decodificar AS2.
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração
* Um [contrato AS2](logic-apps-enterprise-integration-as2.md) que já está definido em sua conta de integração

## <a name="decode-as2-messages"></a>Decodificar mensagens AS2

1. [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

2. conector de mensagem AS2 decodificar Olá não tem gatilhos, portanto você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação. No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.

3.  Na caixa de pesquisa hello, digite "AS2" para o filtro. Selecione **AS2 – Decodificar Mensagem AS2**.
   
    ![Procure "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão. Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect.
   
    ![Criar conexão de integração](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    As propriedades com um asterisco são obrigatórias.

    | Propriedade | Detalhes |
    | --- | --- |
    | Nome da Conexão * |Digite um nome para a conexão. |
    | Uma conta de integração * |Insira um nome para sua conta de integração. Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure. |

5.  Quando terminar, os detalhes de conexão devem ser exemplo toothis semelhante. toofinish criar sua conexão, escolha **criar**.

    ![detalhes de conexão de integração](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. Depois de criar sua conexão, conforme mostrado neste exemplo, selecione **corpo** e **cabeçalhos** do hello solicitar saídas.
   
    ![conexão de integração criada](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    Por exemplo:

    ![Selecione Corpo e Cabeçalhos de saídas de Solicitação](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a>Detalhes do decodificador AS2

conector de decodificar AS2 Olá executa essas tarefas: 

* Processa cabeçalhos HTTP/AS2
* Verifica a assinatura de saudação (se configurado)
* Descriptografa mensagens de saudação (se configurado)
* Descompacta a mensagem de saudação (se configurado)
* Reconcilia um MDN recebido com a mensagem de saída original Olá
* Atualizações e correlaciona registros no banco de dados de não-repúdio Olá
* Grava os registros para o relatório de status do AS2
* Olá saída carga conteúdo é codificados na base64
* Determina se um MDN é necessário e se Olá MDN deve ser síncrona ou assíncronas baseiam na configuração no acordo AS2
* Gera um MDN síncrono ou assíncrono (com base nas configurações do contrato)
* Define propriedades e tokens de correlação de saudação em Olá MDN

## <a name="try-this-sample"></a>Experimente este exemplo

tootry implantar uma lógica totalmente operacional exemplo e aplicativo AS2 cenário, consulte Olá [AS2 cenário e o modelo de aplicativo de lógica](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Swagger de saudação do modo de exibição
Consulte Olá [swagger detalhes](/connectors/as2/). 

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md) 

