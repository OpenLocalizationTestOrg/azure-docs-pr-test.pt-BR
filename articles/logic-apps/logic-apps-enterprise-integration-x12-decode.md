---
title: "mensagens de aaaDecode X12 - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Validar EDI e gerar reconhecimentos com decodificador de mensagem de saudação X12 no hello Enterprise Integration Pack para aplicativos do Azure lógica"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Decodificar X12 mensagens para aplicativos do Azure lógica com hello Enterprise Integration Pack

Com o conector de mensagem de decodificação X12 hello, você pode validar envelope Olá em relação a um acordo entre parceiros comerciais, validar EDI e propriedades específicas do parceiro, dividir intercâmbios em conjuntos de transações ou preservar intercâmbios inteiros e gerar confirmações de transações processadas. toouse esse conector, você deve adicionar Olá conector tooan existente disparador em seu aplicativo lógico.

## <a name="before-you-start"></a>Antes de começar

Aqui está a itens Olá que necessários:

* Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)
* Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure. Você deve ter um conector de mensagem integração conta toouse Olá Decode X12.
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração
* Pelo menos dois [contratos X12](logic-apps-enterprise-integration-x12.md) que já estão definidos em sua conta de integração

## <a name="decode-x12-messages"></a>Decodificar mensagens X12

1. [Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).

2. conector de mensagem de decodificação X12 Olá não tem gatilhos, portanto você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação. No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.

3.  Na caixa de pesquisa hello, digite "x12" para o filtro. Selecione **X12 - Decodificar mensagem X12**.
   
    ![Procure por “x12”](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão. Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect. 

    ![Fornece detalhes da conexão com a conta de integração](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    As propriedades com um asterisco são obrigatórias.

    | Propriedade | Detalhes |
    | --- | --- |
    | Nome da Conexão * |Digite um nome para a conexão. |
    | Uma conta de integração * |Insira um nome para sua conta de integração. Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure. |

5.  Quando terminar, os detalhes de conexão devem ser exemplo toothis semelhante. toofinish criar sua conexão, escolha **criar**.
   
    ![detalhes da conexão com a conta de integração](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. Depois de criar sua conexão, conforme mostrado neste exemplo, selecione Olá X12 toodecode de mensagem de arquivo simples.

    ![conexão com a conta de integração criada](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    Por exemplo:

    ![Selecione a mensagem de arquivo simples X12 para decodificação](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a>Detalhes da Decodificação X12

conector de decodificação Olá X12 executa essas tarefas:

* Valida o envelope Olá no acordo de parceiro comercial
* Valida o EDI e as propriedades específicas de parceiro
  * Validação estrutural de EDI e validação de esquema estendido
  * Validação da estrutura de saudação do envelope do intercâmbio de saudação.
  * Validação de esquema de envelope Olá com base no esquema de controle de saudação.
  * Validação de esquema Olá conjunto de transação de elementos de dados com base no esquema de mensagem de saudação.
  * Validação de EDI executadas em elementos de dados do conjunto de transação 
* Verifica se os números de controle de conjunto de transação, de grupo e de intercâmbio de Olá não são duplicatas
  * Verifica o número de controle de intercâmbio de saudação contra intercâmbios recebidos anteriormente.
  * Verifica o número de controle de grupo Olá contra outros números de controle de grupo no intercâmbio de saudação.
  * Verifica o número de controle de conjunto de transação de saudação em relação a outros números de controle de conjunto de transação no grupo.
* Divide o intercâmbio de saudação em conjuntos de transações ou preserva o intercâmbio inteiro hello:
  * Dividir o Intercâmbio como conjuntos de transações – suspender conjuntos de transações em caso de erro: divide o intercâmbio em conjuntos de transações e analisa cada conjunto de transações. 
  ação de decodificação Olá X12 produz apenas os conjuntos de transação com falha na validação muito`badMessages`e gera Olá transações restantes define muito`goodMessages`.
  * Dividir o Intercâmbio como conjuntos de transações – suspender o intercâmbio em caso de erro: divide o intercâmbio em conjuntos de transações e analisa cada conjunto de transações. 
  Se um ou mais conjuntos de transações na validação de falha de intercâmbio de saudação, ação de decodificação Olá X12 produz conjuntos de todas as transações de saudação em que o intercâmbio muito`badMessages`.
  * Preservar intercâmbio - suspender conjuntos de transações em erro: preservar intercâmbio de saudação e processo Olá intercâmbio em lote inteiro. 
  ação de decodificação Olá X12 produz apenas os conjuntos de transação com falha na validação muito`badMessages`e gera Olá transações restantes define muito`goodMessages`.
  * Preservar intercâmbio - suspender intercâmbio em erro: preservar intercâmbio de saudação e processo Olá intercâmbio em lote inteiro. 
  Se um ou mais conjuntos de transações na validação de falha de intercâmbio de saudação, ação de decodificação Olá X12 produz conjuntos de todas as transações de saudação em que o intercâmbio muito`badMessages`. 
* Gera uma confirmação técnica e/ou funcional (se configurado).
  * Uma confirmação técnica é gerada como resultado da validação de cabeçalho. confirmação técnica Olá relata o status de saudação do processamento de saudação de um cabeçalho de intercâmbio e trailer pelo receptor do endereço hello.
  * Uma confirmação técnica é gerada como resultado da validação do corpo. confirmação funcional Hello relata cada erro encontrado ao processar Olá recebeu um documento

## <a name="view-hello-swagger"></a>Swagger de saudação do modo de exibição
Consulte Olá [swagger detalhes](/connectors/x12/). 

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre Olá Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

