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
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="232e8-103">Codificar mensagens EDIFACT para os aplicativos lógicos do Azure com hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="232e8-103">Encode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="232e8-104">Com o conector de mensagem EDIFACT codificar hello, validar EDI e propriedades específicas do parceiro, gerar um documento XML para cada conjunto de transação e solicitar uma confirmação técnica, confirmação funcional ou ambos.</span><span class="sxs-lookup"><span data-stu-id="232e8-104">With hello Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="232e8-105">toouse esse conector, você deve adicionar Olá conector tooan existente disparador em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="232e8-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="232e8-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="232e8-106">Before you start</span></span>

<span data-ttu-id="232e8-107">Aqui está a itens Olá que necessários:</span><span class="sxs-lookup"><span data-stu-id="232e8-107">Here's hello items you need:</span></span>

* <span data-ttu-id="232e8-108">Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="232e8-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="232e8-109">Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="232e8-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="232e8-110">Você deve ter um conector de mensagem integração conta toouse Olá codificar EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="232e8-110">You must have an integration account toouse hello Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="232e8-111">Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="232e8-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="232e8-112">Um [contrato EDIFACT](logic-apps-enterprise-integration-edifact.md) que já está definido em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="232e8-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="232e8-113">Codificar mensagens EDIFACT</span><span class="sxs-lookup"><span data-stu-id="232e8-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="232e8-114">[Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="232e8-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="232e8-115">conector de mensagem EDIFACT codificar Olá não tem gatilhos, portanto você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação.</span><span class="sxs-lookup"><span data-stu-id="232e8-115">hello Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="232e8-116">No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.</span><span class="sxs-lookup"><span data-stu-id="232e8-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="232e8-117">Na caixa de pesquisa hello, digite "EDIFACT" como filtro.</span><span class="sxs-lookup"><span data-stu-id="232e8-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="232e8-118">Selecione **codificar mensagem EDIFACT pelo nome do contrato** ou **Encode tooEDIFACT mensagem por identidades**.</span><span class="sxs-lookup"><span data-stu-id="232e8-118">Select either **Encode EDIFACT Message by agreement name** or **Encode tooEDIFACT message by identities**.</span></span>
   
    ![pesquisar EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="232e8-120">Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão.</span><span class="sxs-lookup"><span data-stu-id="232e8-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="232e8-121">Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect.</span><span class="sxs-lookup"><span data-stu-id="232e8-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>

    ![criar conexão com a conta de integração](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="232e8-123">As propriedades com um asterisco são obrigatórias.</span><span class="sxs-lookup"><span data-stu-id="232e8-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="232e8-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="232e8-124">Property</span></span> | <span data-ttu-id="232e8-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="232e8-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="232e8-126">Nome da Conexão *</span><span class="sxs-lookup"><span data-stu-id="232e8-126">Connection Name *</span></span> |<span data-ttu-id="232e8-127">Digite um nome para a conexão.</span><span class="sxs-lookup"><span data-stu-id="232e8-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="232e8-128">Uma conta de integração *</span><span class="sxs-lookup"><span data-stu-id="232e8-128">Integration Account *</span></span> |<span data-ttu-id="232e8-129">Insira um nome para sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="232e8-129">Enter a name for your integration account.</span></span> <span data-ttu-id="232e8-130">Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure.</span><span class="sxs-lookup"><span data-stu-id="232e8-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="232e8-131">Quando terminar, os detalhes de conexão devem ser exemplo toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="232e8-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="232e8-132">toofinish criar sua conexão, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="232e8-132">toofinish creating your connection, choose **Create**.</span></span>

    ![detalhes da conexão com a conta de integração](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="232e8-134">A conexão foi criada.</span><span class="sxs-lookup"><span data-stu-id="232e8-134">Your connection is now created.</span></span>

    ![conexão com a conta de integração criada](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="232e8-136">Codificar Mensagem EDIFACT pelo nome do contrato</span><span class="sxs-lookup"><span data-stu-id="232e8-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="232e8-137">Se você escolheu tooencode mensagens EDIFACT pelo nome do contrato, abra Olá **contrato de nome de EDIFACT** lista, digite ou selecione o nome do contrato EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="232e8-137">If you chose tooencode EDIFACT messages by agreement name, open hello **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="232e8-138">Digite hello tooencode de mensagem XML.</span><span class="sxs-lookup"><span data-stu-id="232e8-138">Enter hello XML message tooencode.</span></span>

![Insira o nome do contrato EDIFACT e tooencode de mensagem XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="232e8-140">Codificar Mensagem EDIFACT por identidades</span><span class="sxs-lookup"><span data-stu-id="232e8-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="232e8-141">Se você escolher tooencode mensagens EDIFACT por identidades, insira o identificador do remetente Olá, qualificador de remetente, destinatário identificador e qualificador do destinatário conforme configurado no seu acordo de EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="232e8-141">If you choose tooencode EDIFACT messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="232e8-142">Selecione Olá tooencode de mensagem XML.</span><span class="sxs-lookup"><span data-stu-id="232e8-142">Select hello XML message tooencode.</span></span>

![Fornecer identidades para o remetente e destinatário, selecione tooencode de mensagem XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="232e8-144">Detalhes de codificação do EDIFACT</span><span class="sxs-lookup"><span data-stu-id="232e8-144">EDIFACT Encode details</span></span>

<span data-ttu-id="232e8-145">conector de codificar EDIFACT Olá executa essas tarefas:</span><span class="sxs-lookup"><span data-stu-id="232e8-145">hello Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="232e8-146">Resolver contrato Olá correspondendo o qualificador de remetente Olá & identificador qualificador de destinatário e identificador</span><span class="sxs-lookup"><span data-stu-id="232e8-146">Resolve hello agreement by matching hello sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="232e8-147">Serializa o intercâmbio EDI hello, conversão de mensagens XML codificado em conjuntos de transações EDI no intercâmbio de saudação.</span><span class="sxs-lookup"><span data-stu-id="232e8-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="232e8-148">Aplica os segmentos de cabeçalho e rodapé do conjunto de transação</span><span class="sxs-lookup"><span data-stu-id="232e8-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="232e8-149">Gera um número de controle de intercâmbio, um número de controle de grupo e um número de controle de conjunto de transações para cada intercâmbio de saída</span><span class="sxs-lookup"><span data-stu-id="232e8-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="232e8-150">Substitui separadores em dados de carga Olá</span><span class="sxs-lookup"><span data-stu-id="232e8-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="232e8-151">Valida o EDI e as propriedades específicas de parceiro</span><span class="sxs-lookup"><span data-stu-id="232e8-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="232e8-152">Validação de esquema Olá conjunto de transação de elementos de dados com base no esquema de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="232e8-152">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="232e8-153">Validação de EDI executadas em elementos de dados do conjunto de transação.</span><span class="sxs-lookup"><span data-stu-id="232e8-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="232e8-154">Validação estendida executada em elementos de dados do conjunto de transação</span><span class="sxs-lookup"><span data-stu-id="232e8-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="232e8-155">Gera um documento XML para cada conjunto de transação.</span><span class="sxs-lookup"><span data-stu-id="232e8-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="232e8-156">Solicita uma confirmação técnica e/ou funcional (se configurado).</span><span class="sxs-lookup"><span data-stu-id="232e8-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="232e8-157">Como uma confirmação técnica, mensagem de saudação do CONTRL indica o recebimento de um intercâmbio.</span><span class="sxs-lookup"><span data-stu-id="232e8-157">As a technical acknowledgment, hello CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="232e8-158">Como uma confirmação funcional, mensagem de saudação do CONTRL indica a aceitação ou rejeição de intercâmbio de saudação recebida, grupo ou mensagem, com uma lista de erros ou a funcionalidade sem suporte</span><span class="sxs-lookup"><span data-stu-id="232e8-158">As a functional acknowledgment, hello CONTRL message indicates acceptance or rejection of hello received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="232e8-159">Exibir o arquivo do Swagger</span><span class="sxs-lookup"><span data-stu-id="232e8-159">View Swagger file</span></span>
<span data-ttu-id="232e8-160">detalhes de Swagger tooview Olá para o conector EDIFACT hello, consulte [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="232e8-160">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="232e8-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="232e8-161">Next steps</span></span>
[<span data-ttu-id="232e8-162">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="232e8-162">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

