---
title: "mensagens de EDIFACT aaaDecode - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Validar EDI e gerar reconhecimentos com decodificador de mensagem EDIFACT Olá no hello Enterprise Integration Pack para aplicativos do Azure lógica"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Decodificar mensagens EDIFACT para aplicativos do Azure lógica com hello Enterprise Integration Pack

Com o conector de mensagem EDIFACT decodificar hello, você pode validar EDI e propriedades específicas do parceiro, dividir intercâmbios em conjuntos de transações ou preservar intercâmbios inteiros e gerar confirmações de transações processadas. toouse esse conector, você deve adicionar Olá conector tooan existente disparador em seu aplicativo lógico.

## <a name="before-you-start"></a>Antes de começar

Aqui está a itens Olá que necessários:

* Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)
* Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure. Você deve ter um conector de mensagem integração conta toouse Olá decodificar EDIFACT. 
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração
* Um [contrato EDIFACT](logic-apps-enterprise-integration-edifact.md) que já está definido em sua conta de integração

## <a name="decode-edifact-messages"></a>Decodificar mensagens EDIFACT

1. [Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).

2. conector de mensagem EDIFACT decodificar Olá não tem gatilhos, portanto você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação. No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.

3. Na caixa de pesquisa hello, digite "EDIFACT" como filtro. Escolha **Decodificar Mensagem EDIFACT**.
   
    ![pesquisar EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão. Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect.
   
    ![criar uma conta de integração](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    As propriedades com um asterisco são obrigatórias.

    | Propriedade | Detalhes |
    | --- | --- |
    | Nome da Conexão * |Digite um nome para a conexão. |
    | Uma conta de integração * |Insira um nome para sua conta de integração. Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure. |

4. Quando você terminar toofinish criando sua conexão, escolha **criar**. Os detalhes de conexão devem ser exemplo toothis semelhante:

    ![detalhes da conta de integração](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. Depois de criar sua conexão, conforme mostrado neste exemplo, selecione Olá toodecode de mensagem de arquivo simples de EDIFACT.

    ![conexão com a conta de integração criada](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    Por exemplo:

    ![Escolha a mensagem de arquivo simples EDIFACT para decodificação](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a>Detalhes de decodificador EDIFACT

conector de decodificar EDIFACT Olá executa essas tarefas: 

* Valida o envelope Olá no acordo de parceiro comercial.
* Resolve contrato Olá correspondendo o qualificador de remetente hello e identificador e qualificador de destinatário e identificador.
* Divide um intercâmbio em várias transações quando o intercâmbio de saudação tem mais de uma transação com base no contrato de saudação receber as definições de configuração.
* Desmonta o intercâmbio de saudação.
* Valida propriedades específicas do parceiro e EDI, incluindo:
  * Validação da estrutura de envelope do intercâmbio de saudação
  * Validação de esquema de envelope Olá com base no esquema de controle de saudação
  * Validação de esquema Olá conjunto de transação de elementos de dados com base no esquema de mensagem de saudação
  * Validação de EDI executadas em elementos de dados do conjunto de transação
* Verifica se números de controle de conjunto de transação, de grupo e de intercâmbio de Olá não sejam duplicatas (se configurado) 
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
* Gera uma confirmação técnica (controle) e/ou funcional (se configurado).
  * Uma confirmação técnica ou hello CONTRL ACK relata os resultados de saudação de uma verificação de sintática de intercâmbio de saudação completa recebido.
  * Uma confirmação funcional confirma aceitar ou rejeitar um intercâmbio recebido ou um grupo

## <a name="view-swagger-file"></a>Exibir o arquivo do Swagger
detalhes de Swagger tooview Olá para o conector EDIFACT hello, consulte [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

