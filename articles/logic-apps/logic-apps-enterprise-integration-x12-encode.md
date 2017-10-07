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
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="5715f-103">Codificar X12 mensagens para aplicativos do Azure lógica com hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="5715f-103">Encode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="5715f-104">Com o conector de mensagem de codificação X12 hello, validar EDI e propriedades específicas do parceiro, converter mensagens XML codificado em conjuntos de transações EDI no intercâmbio de saudação e solicitar uma confirmação técnica, confirmação funcional ou ambos.</span><span class="sxs-lookup"><span data-stu-id="5715f-104">With hello Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in hello interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="5715f-105">toouse esse conector, você deve adicionar Olá conector tooan existente disparador em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="5715f-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5715f-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="5715f-106">Before you start</span></span>

<span data-ttu-id="5715f-107">Aqui está a itens Olá que necessários:</span><span class="sxs-lookup"><span data-stu-id="5715f-107">Here's hello items you need:</span></span>

* <span data-ttu-id="5715f-108">Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="5715f-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="5715f-109">Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5715f-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="5715f-110">Você deve ter um conector de mensagem integração conta toouse Olá Encode X12.</span><span class="sxs-lookup"><span data-stu-id="5715f-110">You must have an integration account toouse hello Encode X12 message connector.</span></span>
* <span data-ttu-id="5715f-111">Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="5715f-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="5715f-112">Pelo menos dois [contratos X12](logic-apps-enterprise-integration-x12.md) que já estão definidos em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="5715f-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="5715f-113">Codificar mensagens do X12</span><span class="sxs-lookup"><span data-stu-id="5715f-113">Encode X12 messages</span></span>

1. <span data-ttu-id="5715f-114">[Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5715f-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="5715f-115">conector de mensagem Hello Encode X12 não tiver gatilhos, para que você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação.</span><span class="sxs-lookup"><span data-stu-id="5715f-115">hello Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="5715f-116">No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.</span><span class="sxs-lookup"><span data-stu-id="5715f-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="5715f-117">Na caixa de pesquisa hello, digite "x12" para o filtro.</span><span class="sxs-lookup"><span data-stu-id="5715f-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="5715f-118">Selecione **X12-codificar a mensagem tooX12 pelo nome do contrato** ou **X12-codificar a mensagem tooX12 por identidades**.</span><span class="sxs-lookup"><span data-stu-id="5715f-118">Select either **X12 - Encode tooX12 message by agreement name** or **X12 - Encode tooX12 message by identities**.</span></span>
   
    ![Procure por “x12”](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="5715f-120">Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão.</span><span class="sxs-lookup"><span data-stu-id="5715f-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="5715f-121">Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect.</span><span class="sxs-lookup"><span data-stu-id="5715f-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![conexão com a conta de integração](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="5715f-123">As propriedades com um asterisco são obrigatórias.</span><span class="sxs-lookup"><span data-stu-id="5715f-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="5715f-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5715f-124">Property</span></span> | <span data-ttu-id="5715f-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="5715f-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="5715f-126">Nome da Conexão *</span><span class="sxs-lookup"><span data-stu-id="5715f-126">Connection Name *</span></span> |<span data-ttu-id="5715f-127">Digite um nome para a conexão.</span><span class="sxs-lookup"><span data-stu-id="5715f-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="5715f-128">Uma conta de integração *</span><span class="sxs-lookup"><span data-stu-id="5715f-128">Integration Account *</span></span> |<span data-ttu-id="5715f-129">Insira um nome para sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="5715f-129">Enter a name for your integration account.</span></span> <span data-ttu-id="5715f-130">Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure.</span><span class="sxs-lookup"><span data-stu-id="5715f-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="5715f-131">Quando terminar, os detalhes de conexão devem ser exemplo toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="5715f-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="5715f-132">toofinish criar sua conexão, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="5715f-132">toofinish creating your connection, choose **Create**.</span></span>

    ![conexão com a conta de integração criada](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="5715f-134">A conexão foi criada.</span><span class="sxs-lookup"><span data-stu-id="5715f-134">Your connection is now created.</span></span>

    ![detalhes da conexão com a conta de integração](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="5715f-136">Codificar mensagens do X12 pelo nome do contrato</span><span class="sxs-lookup"><span data-stu-id="5715f-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="5715f-137">Se você escolheu tooencode X12 mensagens por nome do contrato, abra Olá **nome do X12 contrato** lista, insira ou selecione o X12 existente contrato.</span><span class="sxs-lookup"><span data-stu-id="5715f-137">If you chose tooencode X12 messages by agreement name, open hello **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="5715f-138">Digite hello tooencode de mensagem XML.</span><span class="sxs-lookup"><span data-stu-id="5715f-138">Enter hello XML message tooencode.</span></span>

![Insira X12 tooencode de mensagem XML e o nome do contrato](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="5715f-140">Codificar mensagens do X12 por identidades</span><span class="sxs-lookup"><span data-stu-id="5715f-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="5715f-141">Se você escolher tooencode X12 mensagens por identidades, insira o identificador do remetente Olá, qualificador de remetente, destinatário identificador e qualificador do receptor conforme configurado no seu X12 contrato.</span><span class="sxs-lookup"><span data-stu-id="5715f-141">If you choose tooencode X12 messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="5715f-142">Selecione Olá tooencode de mensagem XML.</span><span class="sxs-lookup"><span data-stu-id="5715f-142">Select hello XML message tooencode.</span></span>
   
![Fornecer identidades para o remetente e destinatário, selecione tooencode de mensagem XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="5715f-144">Detalhes de codificação do X12</span><span class="sxs-lookup"><span data-stu-id="5715f-144">X12 Encode details</span></span>

<span data-ttu-id="5715f-145">conector de codificação Olá X12 executa essas tarefas:</span><span class="sxs-lookup"><span data-stu-id="5715f-145">hello X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="5715f-146">Resolução de contrato ao corresponder as propriedades de contexto do remetente e destinatário.</span><span class="sxs-lookup"><span data-stu-id="5715f-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="5715f-147">Serializa o intercâmbio EDI hello, conversão de mensagens XML codificado em conjuntos de transações EDI no intercâmbio de saudação.</span><span class="sxs-lookup"><span data-stu-id="5715f-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="5715f-148">Aplica os segmentos de cabeçalho e rodapé do conjunto de transação</span><span class="sxs-lookup"><span data-stu-id="5715f-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="5715f-149">Gera um número de controle de intercâmbio, um número de controle de grupo e um número de controle de conjunto de transações para cada intercâmbio de saída</span><span class="sxs-lookup"><span data-stu-id="5715f-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="5715f-150">Substitui separadores em dados de carga Olá</span><span class="sxs-lookup"><span data-stu-id="5715f-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="5715f-151">Valida o EDI e as propriedades específicas de parceiro</span><span class="sxs-lookup"><span data-stu-id="5715f-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="5715f-152">Validação de esquema Olá conjunto de transação de elementos de dados em relação a mensagem de saudação do esquema</span><span class="sxs-lookup"><span data-stu-id="5715f-152">Schema validation of hello transaction-set data elements against hello message Schema</span></span>
  * <span data-ttu-id="5715f-153">Validação de EDI executadas em elementos de dados do conjunto de transação.</span><span class="sxs-lookup"><span data-stu-id="5715f-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="5715f-154">Validação estendida executada em elementos de dados do conjunto de transação</span><span class="sxs-lookup"><span data-stu-id="5715f-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="5715f-155">Solicita uma confirmação técnica e/ou funcional (se configurado).</span><span class="sxs-lookup"><span data-stu-id="5715f-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="5715f-156">Uma confirmação técnica é gerada como resultado da validação de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="5715f-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="5715f-157">confirmação técnica Olá relata o status de saudação do processamento de saudação de um cabeçalho de intercâmbio e trailer pelo receptor do endereço Olá</span><span class="sxs-lookup"><span data-stu-id="5715f-157">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver</span></span>
  * <span data-ttu-id="5715f-158">Uma confirmação técnica é gerada como resultado da validação do corpo.</span><span class="sxs-lookup"><span data-stu-id="5715f-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="5715f-159">confirmação funcional Hello relata cada erro encontrado ao processar Olá recebeu um documento</span><span class="sxs-lookup"><span data-stu-id="5715f-159">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="5715f-160">Swagger de saudação do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="5715f-160">View hello swagger</span></span>
<span data-ttu-id="5715f-161">Consulte Olá [swagger detalhes](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="5715f-161">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5715f-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5715f-162">Next steps</span></span>
[<span data-ttu-id="5715f-163">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="5715f-163">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

