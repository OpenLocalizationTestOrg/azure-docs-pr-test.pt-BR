---
title: "mensagens de aaaEncode X12 - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Validar EDI e converter XML codificado mensagens com X12 mensagem codificador Olá Enterprise Integration Pack para aplicativos do Azure lógica"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Codificar X12 mensagens para aplicativos do Azure lógica com hello Enterprise Integration Pack

Com o conector de mensagem de codificação X12 hello, validar EDI e propriedades específicas do parceiro, converter mensagens XML codificado em conjuntos de transações EDI no intercâmbio de saudação e solicitar uma confirmação técnica, confirmação funcional ou ambos.
toouse esse conector, você deve adicionar Olá conector tooan existente disparador em seu aplicativo lógico.

## <a name="before-you-start"></a>Antes de começar

Aqui está a itens Olá que necessários:

* Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)
* Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure. Você deve ter um conector de mensagem integração conta toouse Olá Encode X12.
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração
* Pelo menos dois [contratos X12](logic-apps-enterprise-integration-x12.md) que já estão definidos em sua conta de integração

## <a name="encode-x12-messages"></a>Codificar mensagens do X12

1. [Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).

2. conector de mensagem Hello Encode X12 não tiver gatilhos, para que você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação. No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.

3.  Na caixa de pesquisa hello, digite "x12" para o filtro. Selecione **X12-codificar a mensagem tooX12 pelo nome do contrato** ou **X12-codificar a mensagem tooX12 por identidades**.
   
    ![Procure por “x12”](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão. Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect. 
   
    ![conexão com a conta de integração](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    As propriedades com um asterisco são obrigatórias.

    | Propriedade | Detalhes |
    | --- | --- |
    | Nome da Conexão * |Digite um nome para a conexão. |
    | Uma conta de integração * |Insira um nome para sua conta de integração. Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure. |

5.  Quando terminar, os detalhes de conexão devem ser exemplo toothis semelhante. toofinish criar sua conexão, escolha **criar**.

    ![conexão com a conta de integração criada](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    A conexão foi criada.

    ![detalhes da conexão com a conta de integração](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a>Codificar mensagens do X12 pelo nome do contrato

Se você escolheu tooencode X12 mensagens por nome do contrato, abra Olá **nome do X12 contrato** lista, insira ou selecione o X12 existente contrato. Digite hello tooencode de mensagem XML.

![Insira X12 tooencode de mensagem XML e o nome do contrato](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a>Codificar mensagens do X12 por identidades

Se você escolher tooencode X12 mensagens por identidades, insira o identificador do remetente Olá, qualificador de remetente, destinatário identificador e qualificador do receptor conforme configurado no seu X12 contrato. Selecione Olá tooencode de mensagem XML.
   
![Fornecer identidades para o remetente e destinatário, selecione tooencode de mensagem XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a>Detalhes de codificação do X12

conector de codificação Olá X12 executa essas tarefas:

* Resolução de contrato ao corresponder as propriedades de contexto do remetente e destinatário.
* Serializa o intercâmbio EDI hello, conversão de mensagens XML codificado em conjuntos de transações EDI no intercâmbio de saudação.
* Aplica os segmentos de cabeçalho e rodapé do conjunto de transação
* Gera um número de controle de intercâmbio, um número de controle de grupo e um número de controle de conjunto de transações para cada intercâmbio de saída
* Substitui separadores em dados de carga Olá
* Valida o EDI e as propriedades específicas de parceiro
  * Validação de esquema Olá conjunto de transação de elementos de dados em relação a mensagem de saudação do esquema
  * Validação de EDI executadas em elementos de dados do conjunto de transação.
  * Validação estendida executada em elementos de dados do conjunto de transação
* Solicita uma confirmação técnica e/ou funcional (se configurado).
  * Uma confirmação técnica é gerada como resultado da validação de cabeçalho. confirmação técnica Olá relata o status de saudação do processamento de saudação de um cabeçalho de intercâmbio e trailer pelo receptor do endereço Olá
  * Uma confirmação técnica é gerada como resultado da validação do corpo. confirmação funcional Hello relata cada erro encontrado ao processar Olá recebeu um documento

## <a name="view-hello-swagger"></a>Swagger de saudação do modo de exibição
Consulte Olá [swagger detalhes](/connectors/x12/). 

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

