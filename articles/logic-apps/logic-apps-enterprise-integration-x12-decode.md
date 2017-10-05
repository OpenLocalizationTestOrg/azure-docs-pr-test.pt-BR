---
title: "Decodificar mensagens X12 - Aplicativo Lógico do Azure | Microsoft Docs"
description: "Validar EDI e gerar confirmações com o decodificador de mensagem X12 no Enterprise Integration Pack para Aplicativo Lógico do Azure"
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
ms.openlocfilehash: 18719a8f49c74973947517161f7306c233a9323f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="db1b2-103">Decodificar mensagens X12 para o Aplicativo Lógico do Azure com o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="db1b2-103">Decode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="db1b2-104">Com o conector de mensagem Decodificar X12, você pode validar o envelope no acordo entre parceiros comerciais, validar o EDI e propriedades específicas ao parceiro, dividir intercâmbios em conjuntos de transações ou preservar intercâmbios inteiros e gerar confirmações para transações processadas.</span><span class="sxs-lookup"><span data-stu-id="db1b2-104">With the Decode X12 message connector, you can validate the envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="db1b2-105">Para usar esse conector, você deve adicionar o conector para um gatilho existente em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="db1b2-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="db1b2-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="db1b2-106">Before you start</span></span>

<span data-ttu-id="db1b2-107">Veja os itens necessários:</span><span class="sxs-lookup"><span data-stu-id="db1b2-107">Here's the items you need:</span></span>

* <span data-ttu-id="db1b2-108">Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="db1b2-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="db1b2-109">Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="db1b2-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="db1b2-110">Você precisa ter uma conta de integração para usar o conector de mensagem X12 de decodificação.</span><span class="sxs-lookup"><span data-stu-id="db1b2-110">You must have an integration account to use the Decode X12 message connector.</span></span>
* <span data-ttu-id="db1b2-111">Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="db1b2-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="db1b2-112">Pelo menos dois [contratos X12](logic-apps-enterprise-integration-x12.md) que já estão definidos em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="db1b2-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="db1b2-113">Decodificar mensagens X12</span><span class="sxs-lookup"><span data-stu-id="db1b2-113">Decode X12 messages</span></span>

1. <span data-ttu-id="db1b2-114">[Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="db1b2-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="db1b2-115">O conector de mensagem X12 de decodificação não possui gatilhos, você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um gatilho de Solicitação.</span><span class="sxs-lookup"><span data-stu-id="db1b2-115">The Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="db1b2-116">No Designer de Aplicativo Lógico, adicione um gatilho e uma ação ao aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="db1b2-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="db1b2-117">Na caixa de pesquisa, digite "x12" como filtro.</span><span class="sxs-lookup"><span data-stu-id="db1b2-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="db1b2-118">Selecione **X12 - Decodificar mensagem X12**.</span><span class="sxs-lookup"><span data-stu-id="db1b2-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Procure por “x12”](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="db1b2-120">Se você não criou conexões à sua conta de integração previamente, terá que criá-las agora.</span><span class="sxs-lookup"><span data-stu-id="db1b2-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="db1b2-121">Nomeie sua conexão e selecione a conta de integração que você deseja conectar.</span><span class="sxs-lookup"><span data-stu-id="db1b2-121">Name your connection, and select the integration account that you want to connect.</span></span> 

    ![Fornece detalhes da conexão com a conta de integração](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="db1b2-123">As propriedades com um asterisco são obrigatórias.</span><span class="sxs-lookup"><span data-stu-id="db1b2-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="db1b2-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="db1b2-124">Property</span></span> | <span data-ttu-id="db1b2-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="db1b2-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="db1b2-126">Nome da Conexão *</span><span class="sxs-lookup"><span data-stu-id="db1b2-126">Connection Name *</span></span> |<span data-ttu-id="db1b2-127">Digite um nome para a conexão.</span><span class="sxs-lookup"><span data-stu-id="db1b2-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="db1b2-128">Uma conta de integração *</span><span class="sxs-lookup"><span data-stu-id="db1b2-128">Integration Account *</span></span> |<span data-ttu-id="db1b2-129">Insira um nome para sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="db1b2-129">Enter a name for your integration account.</span></span> <span data-ttu-id="db1b2-130">Verifique se sua conta de integração e o aplicativo lógico estão no mesmo local do Azure.</span><span class="sxs-lookup"><span data-stu-id="db1b2-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="db1b2-131">Quando terminar, os detalhes de conexão devem ser semelhantes a este exemplo.</span><span class="sxs-lookup"><span data-stu-id="db1b2-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="db1b2-132">Para concluir a criação da sua conexão, escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="db1b2-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![detalhes da conexão com a conta de integração](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="db1b2-134">Após a conexão ter sido criada, conforme mostrado neste exemplo, selecione a mensagem de arquivo simples X12 para decodificação.</span><span class="sxs-lookup"><span data-stu-id="db1b2-134">After your connection is created, as shown in this example, select the X12 flat file message to decode.</span></span>

    ![conexão com a conta de integração criada](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="db1b2-136">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="db1b2-136">For example:</span></span>

    ![Selecione a mensagem de arquivo simples X12 para decodificação](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="db1b2-138">Detalhes da Decodificação X12</span><span class="sxs-lookup"><span data-stu-id="db1b2-138">X12 Decode details</span></span>

<span data-ttu-id="db1b2-139">O conector de Decodificação X12 executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="db1b2-139">The X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="db1b2-140">Valida o envelope no contrato de parceiro comercial</span><span class="sxs-lookup"><span data-stu-id="db1b2-140">Validates the envelope against trading partner agreement</span></span>
* <span data-ttu-id="db1b2-141">Valida o EDI e as propriedades específicas de parceiro</span><span class="sxs-lookup"><span data-stu-id="db1b2-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="db1b2-142">Validação estrutural de EDI e validação de esquema estendido</span><span class="sxs-lookup"><span data-stu-id="db1b2-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="db1b2-143">Validação da estrutura do envelope de intercâmbio.</span><span class="sxs-lookup"><span data-stu-id="db1b2-143">Validation of the structure of the interchange envelope.</span></span>
  * <span data-ttu-id="db1b2-144">Validação de esquema do envelope em relação ao esquema de controle.</span><span class="sxs-lookup"><span data-stu-id="db1b2-144">Schema validation of the envelope against the control schema.</span></span>
  * <span data-ttu-id="db1b2-145">Validação de esquema dos elementos de dados do conjunto de transações em relação ao esquema de mensagem.</span><span class="sxs-lookup"><span data-stu-id="db1b2-145">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="db1b2-146">Validação de EDI executadas em elementos de dados do conjunto de transação</span><span class="sxs-lookup"><span data-stu-id="db1b2-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="db1b2-147">Verifica se os números de controle de conjunto de intercâmbio, grupo e transações não são duplicatas</span><span class="sxs-lookup"><span data-stu-id="db1b2-147">Verifies that the interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="db1b2-148">Verifica o número de controle de intercâmbio em relação aos intercâmbios recebidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="db1b2-148">Checks the interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="db1b2-149">Verifica o número de controle de grupo em relação a outros números de controle no intercâmbio.</span><span class="sxs-lookup"><span data-stu-id="db1b2-149">Checks the group control number against other group control numbers in the interchange.</span></span>
  * <span data-ttu-id="db1b2-150">Verifica o número de controle do conjunto de transações em relação a outros números de controle de conjunto de transações nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="db1b2-150">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="db1b2-151">Divide o intercâmbio em conjuntos de transações ou preserva todo o intercâmbio:</span><span class="sxs-lookup"><span data-stu-id="db1b2-151">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="db1b2-152">Dividir o Intercâmbio como conjuntos de transações – suspender conjuntos de transações em caso de erro: divide o intercâmbio em conjuntos de transações e analisa cada conjunto de transações.</span><span class="sxs-lookup"><span data-stu-id="db1b2-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="db1b2-153">A ação Decodificar X12 gera apenas os conjuntos de transações que falharam na validação em `badMessages` e gera os conjuntos de transações restantes em `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="db1b2-153">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="db1b2-154">Dividir o Intercâmbio como conjuntos de transações – suspender o intercâmbio em caso de erro: divide o intercâmbio em conjuntos de transações e analisa cada conjunto de transações.</span><span class="sxs-lookup"><span data-stu-id="db1b2-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="db1b2-155">Se um ou mais conjuntos de transações no intercâmbio falharem na validação, a ação Decodificar X12 gerará todos os conjuntos de transações no intercâmbio em `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="db1b2-155">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="db1b2-156">Preservar intercâmbio – suspender conjuntos de transação em caso de erro: preserve o intercâmbio e processe todo o intercâmbio em lote.</span><span class="sxs-lookup"><span data-stu-id="db1b2-156">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="db1b2-157">A ação Decodificar X12 gera apenas os conjuntos de transações que falharam na validação em `badMessages` e gera os conjuntos de transações restantes em `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="db1b2-157">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="db1b2-158">Preservar intercâmbio – suspender intercâmbio em caso de erro: preserve o intercâmbio e processe todo o intercâmbio em lote.</span><span class="sxs-lookup"><span data-stu-id="db1b2-158">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="db1b2-159">Se um ou mais conjuntos de transações no intercâmbio falharem na validação, a ação Decodificar X12 gerará todos os conjuntos de transações no intercâmbio em `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="db1b2-159">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span> 
* <span data-ttu-id="db1b2-160">Gera uma confirmação técnica e/ou funcional (se configurado).</span><span class="sxs-lookup"><span data-stu-id="db1b2-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="db1b2-161">Uma confirmação técnica é gerada como resultado da validação de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="db1b2-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="db1b2-162">A confirmação técnica relata o status do processamento de um cabeçalho e rodapé de intercâmbio pelo destinatário no endereço.</span><span class="sxs-lookup"><span data-stu-id="db1b2-162">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver.</span></span>
  * <span data-ttu-id="db1b2-163">Uma confirmação técnica é gerada como resultado da validação do corpo.</span><span class="sxs-lookup"><span data-stu-id="db1b2-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="db1b2-164">A confirmação funcional relata cada erro encontrado durante o processamento de documentos recebidos</span><span class="sxs-lookup"><span data-stu-id="db1b2-164">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="db1b2-165">Exibir o Swagger</span><span class="sxs-lookup"><span data-stu-id="db1b2-165">View the swagger</span></span>
<span data-ttu-id="db1b2-166">Consulte os [detalhes do Swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="db1b2-166">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="db1b2-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="db1b2-167">Next steps</span></span>
[<span data-ttu-id="db1b2-168">Saiba mais sobre o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="db1b2-168">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o Enterprise Integration Pack") 

