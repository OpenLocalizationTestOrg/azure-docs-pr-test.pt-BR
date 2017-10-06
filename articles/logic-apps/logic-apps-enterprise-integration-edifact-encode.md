---
title: "mensagens de EDIFACT aaaEncode - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Validar EDI e gerar um XML com o codificador de mensagem EDIFACT em Olá Enterprise Integration Pack para aplicativos da lógica do Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Codificar mensagens EDIFACT para os aplicativos lógicos do Azure com hello Enterprise Integration Pack

Com o conector de mensagem EDIFACT codificar hello, validar EDI e propriedades específicas do parceiro, gerar um documento XML para cada conjunto de transação e solicitar uma confirmação técnica, confirmação funcional ou ambos.
toouse esse conector, você deve adicionar Olá conector tooan existente disparador em seu aplicativo lógico.

## <a name="before-you-start"></a>Antes de começar

Aqui está a itens Olá que necessários:

* Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)
* Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure. Você deve ter um conector de mensagem integração conta toouse Olá codificar EDIFACT. 
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração
* Um [contrato EDIFACT](logic-apps-enterprise-integration-edifact.md) que já está definido em sua conta de integração

## <a name="encode-edifact-messages"></a>Codificar mensagens EDIFACT

1. [Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).

2. conector de mensagem EDIFACT codificar Olá não tem gatilhos, portanto você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação. No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.

3.  Na caixa de pesquisa hello, digite "EDIFACT" como filtro. Selecione **codificar mensagem EDIFACT pelo nome do contrato** ou **Encode tooEDIFACT mensagem por identidades**.
   
    ![pesquisar EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão. Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect.

    ![criar conexão com a conta de integração](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    As propriedades com um asterisco são obrigatórias.

    | Propriedade | Detalhes |
    | --- | --- |
    | Nome da Conexão * |Digite um nome para a conexão. |
    | Uma conta de integração * |Insira um nome para sua conta de integração. Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure. |

5.  Quando terminar, os detalhes de conexão devem ser exemplo toothis semelhante. toofinish criar sua conexão, escolha **criar**.

    ![detalhes da conexão com a conta de integração](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    A conexão foi criada.

    ![conexão com a conta de integração criada](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a>Codificar Mensagem EDIFACT pelo nome do contrato

Se você escolheu tooencode mensagens EDIFACT pelo nome do contrato, abra Olá **contrato de nome de EDIFACT** lista, digite ou selecione o nome do contrato EDIFACT. Digite hello tooencode de mensagem XML.

![Insira o nome do contrato EDIFACT e tooencode de mensagem XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a>Codificar Mensagem EDIFACT por identidades

Se você escolher tooencode mensagens EDIFACT por identidades, insira o identificador do remetente Olá, qualificador de remetente, destinatário identificador e qualificador do destinatário conforme configurado no seu acordo de EDIFACT. Selecione Olá tooencode de mensagem XML.

![Fornecer identidades para o remetente e destinatário, selecione tooencode de mensagem XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a>Detalhes de codificação do EDIFACT

conector de codificar EDIFACT Olá executa essas tarefas: 

* Resolver contrato Olá correspondendo o qualificador de remetente Olá & identificador qualificador de destinatário e identificador
* Serializa o intercâmbio EDI hello, conversão de mensagens XML codificado em conjuntos de transações EDI no intercâmbio de saudação.
* Aplica os segmentos de cabeçalho e rodapé do conjunto de transação
* Gera um número de controle de intercâmbio, um número de controle de grupo e um número de controle de conjunto de transações para cada intercâmbio de saída
* Substitui separadores em dados de carga Olá
* Valida o EDI e as propriedades específicas de parceiro
  * Validação de esquema Olá conjunto de transação de elementos de dados com base no esquema de mensagem de saudação.
  * Validação de EDI executadas em elementos de dados do conjunto de transação.
  * Validação estendida executada em elementos de dados do conjunto de transação
* Gera um documento XML para cada conjunto de transação.
* Solicita uma confirmação técnica e/ou funcional (se configurado).
  * Como uma confirmação técnica, mensagem de saudação do CONTRL indica o recebimento de um intercâmbio.
  * Como uma confirmação funcional, mensagem de saudação do CONTRL indica a aceitação ou rejeição de intercâmbio de saudação recebida, grupo ou mensagem, com uma lista de erros ou a funcionalidade sem suporte

## <a name="view-swagger-file"></a>Exibir o arquivo do Swagger
detalhes de Swagger tooview Olá para o conector EDIFACT hello, consulte [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

