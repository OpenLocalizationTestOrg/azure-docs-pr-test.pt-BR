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
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="af107-103">Decodificar mensagens EDIFACT para aplicativos do Azure lógica com hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="af107-103">Decode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="af107-104">Com o conector de mensagem EDIFACT decodificar hello, você pode validar EDI e propriedades específicas do parceiro, dividir intercâmbios em conjuntos de transações ou preservar intercâmbios inteiros e gerar confirmações de transações processadas.</span><span class="sxs-lookup"><span data-stu-id="af107-104">With hello Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="af107-105">toouse esse conector, você deve adicionar Olá conector tooan existente disparador em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="af107-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="af107-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="af107-106">Before you start</span></span>

<span data-ttu-id="af107-107">Aqui está a itens Olá que necessários:</span><span class="sxs-lookup"><span data-stu-id="af107-107">Here's hello items you need:</span></span>

* <span data-ttu-id="af107-108">Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="af107-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="af107-109">Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="af107-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="af107-110">Você deve ter um conector de mensagem integração conta toouse Olá decodificar EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="af107-110">You must have an integration account toouse hello Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="af107-111">Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="af107-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="af107-112">Um [contrato EDIFACT](logic-apps-enterprise-integration-edifact.md) que já está definido em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="af107-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="af107-113">Decodificar mensagens EDIFACT</span><span class="sxs-lookup"><span data-stu-id="af107-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="af107-114">[Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="af107-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="af107-115">conector de mensagem EDIFACT decodificar Olá não tem gatilhos, portanto você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação.</span><span class="sxs-lookup"><span data-stu-id="af107-115">hello Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="af107-116">No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.</span><span class="sxs-lookup"><span data-stu-id="af107-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3. <span data-ttu-id="af107-117">Na caixa de pesquisa hello, digite "EDIFACT" como filtro.</span><span class="sxs-lookup"><span data-stu-id="af107-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="af107-118">Escolha **Decodificar Mensagem EDIFACT**.</span><span class="sxs-lookup"><span data-stu-id="af107-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![pesquisar EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="af107-120">Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão.</span><span class="sxs-lookup"><span data-stu-id="af107-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="af107-121">Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect.</span><span class="sxs-lookup"><span data-stu-id="af107-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![criar uma conta de integração](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="af107-123">As propriedades com um asterisco são obrigatórias.</span><span class="sxs-lookup"><span data-stu-id="af107-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="af107-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="af107-124">Property</span></span> | <span data-ttu-id="af107-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="af107-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="af107-126">Nome da Conexão *</span><span class="sxs-lookup"><span data-stu-id="af107-126">Connection Name *</span></span> |<span data-ttu-id="af107-127">Digite um nome para a conexão.</span><span class="sxs-lookup"><span data-stu-id="af107-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="af107-128">Uma conta de integração *</span><span class="sxs-lookup"><span data-stu-id="af107-128">Integration Account *</span></span> |<span data-ttu-id="af107-129">Insira um nome para sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="af107-129">Enter a name for your integration account.</span></span> <span data-ttu-id="af107-130">Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure.</span><span class="sxs-lookup"><span data-stu-id="af107-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

4. <span data-ttu-id="af107-131">Quando você terminar toofinish criando sua conexão, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="af107-131">When you're done toofinish creating your connection, choose **Create**.</span></span> <span data-ttu-id="af107-132">Os detalhes de conexão devem ser exemplo toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="af107-132">Your connection details should look similar toothis example:</span></span>

    ![detalhes da conta de integração](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="af107-134">Depois de criar sua conexão, conforme mostrado neste exemplo, selecione Olá toodecode de mensagem de arquivo simples de EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="af107-134">After your connection is created, as shown in this example, select hello EDIFACT flat file message toodecode.</span></span>

    ![conexão com a conta de integração criada](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="af107-136">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="af107-136">For example:</span></span>

    ![Escolha a mensagem de arquivo simples EDIFACT para decodificação](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="af107-138">Detalhes de decodificador EDIFACT</span><span class="sxs-lookup"><span data-stu-id="af107-138">EDIFACT decoder details</span></span>

<span data-ttu-id="af107-139">conector de decodificar EDIFACT Olá executa essas tarefas:</span><span class="sxs-lookup"><span data-stu-id="af107-139">hello Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="af107-140">Valida o envelope Olá no acordo de parceiro comercial.</span><span class="sxs-lookup"><span data-stu-id="af107-140">Validates hello envelope against trading partner agreement.</span></span>
* <span data-ttu-id="af107-141">Resolve contrato Olá correspondendo o qualificador de remetente hello e identificador e qualificador de destinatário e identificador.</span><span class="sxs-lookup"><span data-stu-id="af107-141">Resolves hello agreement by matching hello sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="af107-142">Divide um intercâmbio em várias transações quando o intercâmbio de saudação tem mais de uma transação com base no contrato de saudação receber as definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="af107-142">Splits an interchange into multiple transactions when hello interchange has more than one transaction based on hello agreement's receive settings configuration.</span></span>
* <span data-ttu-id="af107-143">Desmonta o intercâmbio de saudação.</span><span class="sxs-lookup"><span data-stu-id="af107-143">Disassembles hello interchange.</span></span>
* <span data-ttu-id="af107-144">Valida propriedades específicas do parceiro e EDI, incluindo:</span><span class="sxs-lookup"><span data-stu-id="af107-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="af107-145">Validação da estrutura de envelope do intercâmbio de saudação</span><span class="sxs-lookup"><span data-stu-id="af107-145">Validation of hello interchange envelope structure</span></span>
  * <span data-ttu-id="af107-146">Validação de esquema de envelope Olá com base no esquema de controle de saudação</span><span class="sxs-lookup"><span data-stu-id="af107-146">Schema validation of hello envelope against hello control schema</span></span>
  * <span data-ttu-id="af107-147">Validação de esquema Olá conjunto de transação de elementos de dados com base no esquema de mensagem de saudação</span><span class="sxs-lookup"><span data-stu-id="af107-147">Schema validation of hello transaction-set data elements against hello message schema</span></span>
  * <span data-ttu-id="af107-148">Validação de EDI executadas em elementos de dados do conjunto de transação</span><span class="sxs-lookup"><span data-stu-id="af107-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="af107-149">Verifica se números de controle de conjunto de transação, de grupo e de intercâmbio de Olá não sejam duplicatas (se configurado)</span><span class="sxs-lookup"><span data-stu-id="af107-149">Verifies that hello interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="af107-150">Verifica o número de controle de intercâmbio de saudação contra intercâmbios recebidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af107-150">Checks hello interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="af107-151">Verifica o número de controle de grupo Olá contra outros números de controle de grupo no intercâmbio de saudação.</span><span class="sxs-lookup"><span data-stu-id="af107-151">Checks hello group control number against other group control numbers in hello interchange.</span></span> 
  * <span data-ttu-id="af107-152">Verifica o número de controle de conjunto de transação de saudação em relação a outros números de controle de conjunto de transação no grupo.</span><span class="sxs-lookup"><span data-stu-id="af107-152">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="af107-153">Divide o intercâmbio de saudação em conjuntos de transações ou preserva o intercâmbio inteiro hello:</span><span class="sxs-lookup"><span data-stu-id="af107-153">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="af107-154">Dividir o Intercâmbio como conjuntos de transações – suspender conjuntos de transações em caso de erro: divide o intercâmbio em conjuntos de transações e analisa cada conjunto de transações.</span><span class="sxs-lookup"><span data-stu-id="af107-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="af107-155">ação de decodificação Olá X12 produz apenas os conjuntos de transação com falha na validação muito`badMessages`e gera Olá transações restantes define muito`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="af107-155">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="af107-156">Dividir o Intercâmbio como conjuntos de transações – suspender o intercâmbio em caso de erro: divide o intercâmbio em conjuntos de transações e analisa cada conjunto de transações.</span><span class="sxs-lookup"><span data-stu-id="af107-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="af107-157">Se um ou mais conjuntos de transações na validação de falha de intercâmbio de saudação, ação de decodificação Olá X12 produz conjuntos de todas as transações de saudação em que o intercâmbio muito`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="af107-157">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="af107-158">Preservar intercâmbio - suspender conjuntos de transações em erro: preservar intercâmbio de saudação e processo Olá intercâmbio em lote inteiro.</span><span class="sxs-lookup"><span data-stu-id="af107-158">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="af107-159">ação de decodificação Olá X12 produz apenas os conjuntos de transação com falha na validação muito`badMessages`e gera Olá transações restantes define muito`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="af107-159">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="af107-160">Preservar intercâmbio - suspender intercâmbio em erro: preservar intercâmbio de saudação e processo Olá intercâmbio em lote inteiro.</span><span class="sxs-lookup"><span data-stu-id="af107-160">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="af107-161">Se um ou mais conjuntos de transações na validação de falha de intercâmbio de saudação, ação de decodificação Olá X12 produz conjuntos de todas as transações de saudação em que o intercâmbio muito`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="af107-161">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
* <span data-ttu-id="af107-162">Gera uma confirmação técnica (controle) e/ou funcional (se configurado).</span><span class="sxs-lookup"><span data-stu-id="af107-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="af107-163">Uma confirmação técnica ou hello CONTRL ACK relata os resultados de saudação de uma verificação de sintática de intercâmbio de saudação completa recebido.</span><span class="sxs-lookup"><span data-stu-id="af107-163">A Technical Acknowledgment or hello CONTRL ACK reports hello results of a syntactical check of hello complete received interchange.</span></span>
  * <span data-ttu-id="af107-164">Uma confirmação funcional confirma aceitar ou rejeitar um intercâmbio recebido ou um grupo</span><span class="sxs-lookup"><span data-stu-id="af107-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="af107-165">Exibir o arquivo do Swagger</span><span class="sxs-lookup"><span data-stu-id="af107-165">View Swagger file</span></span>
<span data-ttu-id="af107-166">detalhes de Swagger tooview Olá para o conector EDIFACT hello, consulte [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="af107-166">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af107-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af107-167">Next steps</span></span>
[<span data-ttu-id="af107-168">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="af107-168">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

