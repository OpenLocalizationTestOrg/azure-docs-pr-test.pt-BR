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
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="7128f-103">Decodificar X12 mensagens para aplicativos do Azure lógica com hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="7128f-103">Decode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="7128f-104">Com o conector de mensagem de decodificação X12 hello, você pode validar envelope Olá em relação a um acordo entre parceiros comerciais, validar EDI e propriedades específicas do parceiro, dividir intercâmbios em conjuntos de transações ou preservar intercâmbios inteiros e gerar confirmações de transações processadas.</span><span class="sxs-lookup"><span data-stu-id="7128f-104">With hello Decode X12 message connector, you can validate hello envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="7128f-105">toouse esse conector, você deve adicionar Olá conector tooan existente disparador em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="7128f-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="7128f-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7128f-106">Before you start</span></span>

<span data-ttu-id="7128f-107">Aqui está a itens Olá que necessários:</span><span class="sxs-lookup"><span data-stu-id="7128f-107">Here's hello items you need:</span></span>

* <span data-ttu-id="7128f-108">Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="7128f-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="7128f-109">Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="7128f-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="7128f-110">Você deve ter um conector de mensagem integração conta toouse Olá Decode X12.</span><span class="sxs-lookup"><span data-stu-id="7128f-110">You must have an integration account toouse hello Decode X12 message connector.</span></span>
* <span data-ttu-id="7128f-111">Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="7128f-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="7128f-112">Pelo menos dois [contratos X12](logic-apps-enterprise-integration-x12.md) que já estão definidos em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="7128f-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="7128f-113">Decodificar mensagens X12</span><span class="sxs-lookup"><span data-stu-id="7128f-113">Decode X12 messages</span></span>

1. <span data-ttu-id="7128f-114">[Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7128f-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="7128f-115">conector de mensagem de decodificação X12 Olá não tem gatilhos, portanto você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação.</span><span class="sxs-lookup"><span data-stu-id="7128f-115">hello Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="7128f-116">No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.</span><span class="sxs-lookup"><span data-stu-id="7128f-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="7128f-117">Na caixa de pesquisa hello, digite "x12" para o filtro.</span><span class="sxs-lookup"><span data-stu-id="7128f-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="7128f-118">Selecione **X12 - Decodificar mensagem X12**.</span><span class="sxs-lookup"><span data-stu-id="7128f-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Procure por “x12”](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="7128f-120">Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão.</span><span class="sxs-lookup"><span data-stu-id="7128f-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="7128f-121">Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect.</span><span class="sxs-lookup"><span data-stu-id="7128f-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 

    ![Fornece detalhes da conexão com a conta de integração](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="7128f-123">As propriedades com um asterisco são obrigatórias.</span><span class="sxs-lookup"><span data-stu-id="7128f-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="7128f-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="7128f-124">Property</span></span> | <span data-ttu-id="7128f-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="7128f-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="7128f-126">Nome da Conexão *</span><span class="sxs-lookup"><span data-stu-id="7128f-126">Connection Name *</span></span> |<span data-ttu-id="7128f-127">Digite um nome para a conexão.</span><span class="sxs-lookup"><span data-stu-id="7128f-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="7128f-128">Uma conta de integração *</span><span class="sxs-lookup"><span data-stu-id="7128f-128">Integration Account *</span></span> |<span data-ttu-id="7128f-129">Insira um nome para sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="7128f-129">Enter a name for your integration account.</span></span> <span data-ttu-id="7128f-130">Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure.</span><span class="sxs-lookup"><span data-stu-id="7128f-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="7128f-131">Quando terminar, os detalhes de conexão devem ser exemplo toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="7128f-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="7128f-132">toofinish criar sua conexão, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="7128f-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![detalhes da conexão com a conta de integração](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="7128f-134">Depois de criar sua conexão, conforme mostrado neste exemplo, selecione Olá X12 toodecode de mensagem de arquivo simples.</span><span class="sxs-lookup"><span data-stu-id="7128f-134">After your connection is created, as shown in this example, select hello X12 flat file message toodecode.</span></span>

    ![conexão com a conta de integração criada](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="7128f-136">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7128f-136">For example:</span></span>

    ![Selecione a mensagem de arquivo simples X12 para decodificação](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="7128f-138">Detalhes da Decodificação X12</span><span class="sxs-lookup"><span data-stu-id="7128f-138">X12 Decode details</span></span>

<span data-ttu-id="7128f-139">conector de decodificação Olá X12 executa essas tarefas:</span><span class="sxs-lookup"><span data-stu-id="7128f-139">hello X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="7128f-140">Valida o envelope Olá no acordo de parceiro comercial</span><span class="sxs-lookup"><span data-stu-id="7128f-140">Validates hello envelope against trading partner agreement</span></span>
* <span data-ttu-id="7128f-141">Valida o EDI e as propriedades específicas de parceiro</span><span class="sxs-lookup"><span data-stu-id="7128f-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="7128f-142">Validação estrutural de EDI e validação de esquema estendido</span><span class="sxs-lookup"><span data-stu-id="7128f-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="7128f-143">Validação da estrutura de saudação do envelope do intercâmbio de saudação.</span><span class="sxs-lookup"><span data-stu-id="7128f-143">Validation of hello structure of hello interchange envelope.</span></span>
  * <span data-ttu-id="7128f-144">Validação de esquema de envelope Olá com base no esquema de controle de saudação.</span><span class="sxs-lookup"><span data-stu-id="7128f-144">Schema validation of hello envelope against hello control schema.</span></span>
  * <span data-ttu-id="7128f-145">Validação de esquema Olá conjunto de transação de elementos de dados com base no esquema de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="7128f-145">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="7128f-146">Validação de EDI executadas em elementos de dados do conjunto de transação</span><span class="sxs-lookup"><span data-stu-id="7128f-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="7128f-147">Verifica se os números de controle de conjunto de transação, de grupo e de intercâmbio de Olá não são duplicatas</span><span class="sxs-lookup"><span data-stu-id="7128f-147">Verifies that hello interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="7128f-148">Verifica o número de controle de intercâmbio de saudação contra intercâmbios recebidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7128f-148">Checks hello interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="7128f-149">Verifica o número de controle de grupo Olá contra outros números de controle de grupo no intercâmbio de saudação.</span><span class="sxs-lookup"><span data-stu-id="7128f-149">Checks hello group control number against other group control numbers in hello interchange.</span></span>
  * <span data-ttu-id="7128f-150">Verifica o número de controle de conjunto de transação de saudação em relação a outros números de controle de conjunto de transação no grupo.</span><span class="sxs-lookup"><span data-stu-id="7128f-150">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="7128f-151">Divide o intercâmbio de saudação em conjuntos de transações ou preserva o intercâmbio inteiro hello:</span><span class="sxs-lookup"><span data-stu-id="7128f-151">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="7128f-152">Dividir o Intercâmbio como conjuntos de transações – suspender conjuntos de transações em caso de erro: divide o intercâmbio em conjuntos de transações e analisa cada conjunto de transações.</span><span class="sxs-lookup"><span data-stu-id="7128f-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="7128f-153">ação de decodificação Olá X12 produz apenas os conjuntos de transação com falha na validação muito`badMessages`e gera Olá transações restantes define muito`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="7128f-153">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="7128f-154">Dividir o Intercâmbio como conjuntos de transações – suspender o intercâmbio em caso de erro: divide o intercâmbio em conjuntos de transações e analisa cada conjunto de transações.</span><span class="sxs-lookup"><span data-stu-id="7128f-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="7128f-155">Se um ou mais conjuntos de transações na validação de falha de intercâmbio de saudação, ação de decodificação Olá X12 produz conjuntos de todas as transações de saudação em que o intercâmbio muito`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="7128f-155">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="7128f-156">Preservar intercâmbio - suspender conjuntos de transações em erro: preservar intercâmbio de saudação e processo Olá intercâmbio em lote inteiro.</span><span class="sxs-lookup"><span data-stu-id="7128f-156">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="7128f-157">ação de decodificação Olá X12 produz apenas os conjuntos de transação com falha na validação muito`badMessages`e gera Olá transações restantes define muito`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="7128f-157">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="7128f-158">Preservar intercâmbio - suspender intercâmbio em erro: preservar intercâmbio de saudação e processo Olá intercâmbio em lote inteiro.</span><span class="sxs-lookup"><span data-stu-id="7128f-158">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="7128f-159">Se um ou mais conjuntos de transações na validação de falha de intercâmbio de saudação, ação de decodificação Olá X12 produz conjuntos de todas as transações de saudação em que o intercâmbio muito`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="7128f-159">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span> 
* <span data-ttu-id="7128f-160">Gera uma confirmação técnica e/ou funcional (se configurado).</span><span class="sxs-lookup"><span data-stu-id="7128f-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="7128f-161">Uma confirmação técnica é gerada como resultado da validação de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="7128f-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="7128f-162">confirmação técnica Olá relata o status de saudação do processamento de saudação de um cabeçalho de intercâmbio e trailer pelo receptor do endereço hello.</span><span class="sxs-lookup"><span data-stu-id="7128f-162">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver.</span></span>
  * <span data-ttu-id="7128f-163">Uma confirmação técnica é gerada como resultado da validação do corpo.</span><span class="sxs-lookup"><span data-stu-id="7128f-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="7128f-164">confirmação funcional Hello relata cada erro encontrado ao processar Olá recebeu um documento</span><span class="sxs-lookup"><span data-stu-id="7128f-164">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="7128f-165">Swagger de saudação do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="7128f-165">View hello swagger</span></span>
<span data-ttu-id="7128f-166">Consulte Olá [swagger detalhes](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="7128f-166">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7128f-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7128f-167">Next steps</span></span>
[<span data-ttu-id="7128f-168">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="7128f-168">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

