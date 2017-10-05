---
title: "Codificar mensagens AS2 – Aplicativo Lógico do Azure | Microsoft Docs"
description: "Como usar o codificador AS2 no Enterprise Integration Pack para o Aplicativo Lógico do Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 7889bf9e4e02143b6bb4c797531afa54f8647ce5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="1418c-103">Codificar mensagens AS2 para o Aplicativo Lógico do Azure com o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="1418c-103">Encode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="1418c-104">Para estabelecer confiabilidade e segurança ao transmitir mensagens, use o conector de mensagem AS2 de codificação.</span><span class="sxs-lookup"><span data-stu-id="1418c-104">To establish security and reliability while transmitting messages, use the Encode AS2 message connector.</span></span> <span data-ttu-id="1418c-105">Ele fornece a assinatura digital, criptografia e confirmações por meio de Notificações de Disposição de Mensagem (MDN), o que também leva a suporte para Não Repúdio.</span><span class="sxs-lookup"><span data-stu-id="1418c-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads to support for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="1418c-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="1418c-106">Before you start</span></span>

<span data-ttu-id="1418c-107">Veja os itens necessários:</span><span class="sxs-lookup"><span data-stu-id="1418c-107">Here's the items you need:</span></span>

* <span data-ttu-id="1418c-108">Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="1418c-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="1418c-109">Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1418c-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="1418c-110">Você precisa ter uma conta de integração para usar o conector de mensagem AS2 de codificação.</span><span class="sxs-lookup"><span data-stu-id="1418c-110">You must have an integration account to use the Encode AS2 message connector.</span></span>
* <span data-ttu-id="1418c-111">Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="1418c-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="1418c-112">Um [contrato AS2](logic-apps-enterprise-integration-as2.md) que já está definido em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="1418c-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="1418c-113">Codificar mensagens AS2</span><span class="sxs-lookup"><span data-stu-id="1418c-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="1418c-114">[Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1418c-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="1418c-115">O conector de mensagem AS2 de codificação não possui gatilhos. Você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um gatilho de Solicitação.</span><span class="sxs-lookup"><span data-stu-id="1418c-115">The Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="1418c-116">No Designer de Aplicativo Lógico, adicione um gatilho e uma ação ao aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1418c-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="1418c-117">Na caixa de pesquisa, digite "AS2" como filtro.</span><span class="sxs-lookup"><span data-stu-id="1418c-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="1418c-118">Selecione **AS2 - Codificar Mensagem AS2**.</span><span class="sxs-lookup"><span data-stu-id="1418c-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Procure "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="1418c-120">Se você não criou conexões à sua conta de integração previamente, terá que criá-las agora.</span><span class="sxs-lookup"><span data-stu-id="1418c-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="1418c-121">Nomeie sua conexão e selecione a conta de integração que você deseja conectar.</span><span class="sxs-lookup"><span data-stu-id="1418c-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![criar conexão com a conta de integração](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="1418c-123">As propriedades com um asterisco são obrigatórias.</span><span class="sxs-lookup"><span data-stu-id="1418c-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="1418c-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="1418c-124">Property</span></span> | <span data-ttu-id="1418c-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="1418c-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="1418c-126">Nome da Conexão *</span><span class="sxs-lookup"><span data-stu-id="1418c-126">Connection Name *</span></span> |<span data-ttu-id="1418c-127">Digite um nome para a conexão.</span><span class="sxs-lookup"><span data-stu-id="1418c-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="1418c-128">Uma conta de integração *</span><span class="sxs-lookup"><span data-stu-id="1418c-128">Integration Account *</span></span> |<span data-ttu-id="1418c-129">Insira um nome para sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="1418c-129">Enter a name for your integration account.</span></span> <span data-ttu-id="1418c-130">Verifique se sua conta de integração e o aplicativo lógico estão no mesmo local do Azure.</span><span class="sxs-lookup"><span data-stu-id="1418c-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="1418c-131">Quando terminar, os detalhes de conexão devem ser semelhantes a este exemplo.</span><span class="sxs-lookup"><span data-stu-id="1418c-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="1418c-132">Para concluir a criação da sua conexão, escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1418c-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![detalhes de conexão de integração](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="1418c-134">Depois que a conexão é criada, conforme mostrado neste exemplo, forneça detalhes para **os identificadores AS2-De**, **AS2-Para** conforme configurado no seu contrato e **Corpo**, que é a carga da mensagem.</span><span class="sxs-lookup"><span data-stu-id="1418c-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-To identifiers** as configured in your agreement, and **Body**, which is the message payload.</span></span>
   
    ![fornecer campos obrigatórios](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="1418c-136">Detalhes do codificador AS2</span><span class="sxs-lookup"><span data-stu-id="1418c-136">AS2 encoder details</span></span>

<span data-ttu-id="1418c-137">O conector codificador AS2 executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="1418c-137">The Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="1418c-138">Aplica cabeçalhos HTTP/AS2</span><span class="sxs-lookup"><span data-stu-id="1418c-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="1418c-139">Sinaliza mensagens de saída (se configurado)</span><span class="sxs-lookup"><span data-stu-id="1418c-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="1418c-140">Criptografa mensagens de saída (se configurado)</span><span class="sxs-lookup"><span data-stu-id="1418c-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="1418c-141">Compacta as mensagens (se configurado)</span><span class="sxs-lookup"><span data-stu-id="1418c-141">Compresses the message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="1418c-142">Experimente este exemplo</span><span class="sxs-lookup"><span data-stu-id="1418c-142">Try this sample</span></span>

<span data-ttu-id="1418c-143">Para tentar implantar um aplicativo lógico totalmente operacional e o cenário de AS2 de exemplo, confira o[modelo e cenário de aplicativo lógico AS2](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="1418c-143">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="1418c-144">Exibir o Swagger</span><span class="sxs-lookup"><span data-stu-id="1418c-144">View the swagger</span></span>
<span data-ttu-id="1418c-145">Consulte os [detalhes do Swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="1418c-145">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1418c-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1418c-146">Next steps</span></span>
[<span data-ttu-id="1418c-147">Saiba mais sobre o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="1418c-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o Enterprise Integration Pack") 

