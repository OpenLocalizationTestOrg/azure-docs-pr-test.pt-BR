---
title: "mensagens de aaaEncode AS2 - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Como toouse Olá codificador AS2 Olá Enterprise Integration Pack para aplicativos do Azure lógica"
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
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="509d8-103">Codificar mensagens AS2 para os aplicativos lógicos do Azure com hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="509d8-103">Encode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="509d8-104">tooestablish segurança e confiabilidade ao transmitir mensagens, use o conector de mensagem AS2 codificar hello.</span><span class="sxs-lookup"><span data-stu-id="509d8-104">tooestablish security and reliability while transmitting messages, use hello Encode AS2 message connector.</span></span> <span data-ttu-id="509d8-105">Esse conector fornece confirmações por meio de mensagem disposição notificações MDN (), que também leva toosupport para não-repúdio, criptografia e assinatura digital.</span><span class="sxs-lookup"><span data-stu-id="509d8-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads toosupport for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="509d8-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="509d8-106">Before you start</span></span>

<span data-ttu-id="509d8-107">Aqui está a itens Olá que necessários:</span><span class="sxs-lookup"><span data-stu-id="509d8-107">Here's hello items you need:</span></span>

* <span data-ttu-id="509d8-108">Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="509d8-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="509d8-109">Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="509d8-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="509d8-110">Você deve ter um conector de mensagem integração conta toouse Olá codificar AS2.</span><span class="sxs-lookup"><span data-stu-id="509d8-110">You must have an integration account toouse hello Encode AS2 message connector.</span></span>
* <span data-ttu-id="509d8-111">Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="509d8-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="509d8-112">Um [contrato AS2](logic-apps-enterprise-integration-as2.md) que já está definido em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="509d8-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="509d8-113">Codificar mensagens AS2</span><span class="sxs-lookup"><span data-stu-id="509d8-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="509d8-114">[Criar um aplicativo lógico](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="509d8-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="509d8-115">conector de mensagem AS2 codificar Olá não tem gatilhos, portanto você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação.</span><span class="sxs-lookup"><span data-stu-id="509d8-115">hello Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="509d8-116">No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.</span><span class="sxs-lookup"><span data-stu-id="509d8-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="509d8-117">Na caixa de pesquisa hello, digite "AS2" para o filtro.</span><span class="sxs-lookup"><span data-stu-id="509d8-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="509d8-118">Selecione **AS2 - Codificar Mensagem AS2**.</span><span class="sxs-lookup"><span data-stu-id="509d8-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Procure "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="509d8-120">Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão.</span><span class="sxs-lookup"><span data-stu-id="509d8-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="509d8-121">Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect.</span><span class="sxs-lookup"><span data-stu-id="509d8-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![Criar conexão toointegration conta](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="509d8-123">As propriedades com um asterisco são obrigatórias.</span><span class="sxs-lookup"><span data-stu-id="509d8-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="509d8-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="509d8-124">Property</span></span> | <span data-ttu-id="509d8-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="509d8-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="509d8-126">Nome da Conexão *</span><span class="sxs-lookup"><span data-stu-id="509d8-126">Connection Name *</span></span> |<span data-ttu-id="509d8-127">Digite um nome para a conexão.</span><span class="sxs-lookup"><span data-stu-id="509d8-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="509d8-128">Uma conta de integração *</span><span class="sxs-lookup"><span data-stu-id="509d8-128">Integration Account *</span></span> |<span data-ttu-id="509d8-129">Insira um nome para sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="509d8-129">Enter a name for your integration account.</span></span> <span data-ttu-id="509d8-130">Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure.</span><span class="sxs-lookup"><span data-stu-id="509d8-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="509d8-131">Quando terminar, os detalhes de conexão devem ser exemplo toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="509d8-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="509d8-132">toofinish criar sua conexão, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="509d8-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![detalhes de conexão de integração](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="509d8-134">Depois de criar sua conexão, conforme mostrado neste exemplo, forneça detalhes para **AS2-de**, **AS2 tooidentifiers** conforme configurado no seu contrato e **corpo**, que é carga de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="509d8-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-tooidentifiers** as configured in your agreement, and **Body**, which is hello message payload.</span></span>
   
    ![fornecer campos obrigatórios](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="509d8-136">Detalhes do codificador AS2</span><span class="sxs-lookup"><span data-stu-id="509d8-136">AS2 encoder details</span></span>

<span data-ttu-id="509d8-137">conector de codificar AS2 Olá executa essas tarefas:</span><span class="sxs-lookup"><span data-stu-id="509d8-137">hello Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="509d8-138">Aplica cabeçalhos HTTP/AS2</span><span class="sxs-lookup"><span data-stu-id="509d8-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="509d8-139">Sinaliza mensagens de saída (se configurado)</span><span class="sxs-lookup"><span data-stu-id="509d8-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="509d8-140">Criptografa mensagens de saída (se configurado)</span><span class="sxs-lookup"><span data-stu-id="509d8-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="509d8-141">Compacta a mensagem de saudação (se configurado)</span><span class="sxs-lookup"><span data-stu-id="509d8-141">Compresses hello message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="509d8-142">Experimente este exemplo</span><span class="sxs-lookup"><span data-stu-id="509d8-142">Try this sample</span></span>

<span data-ttu-id="509d8-143">tootry implantar uma lógica totalmente operacional exemplo e aplicativo AS2 cenário, consulte Olá [AS2 cenário e o modelo de aplicativo de lógica](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="509d8-143">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="509d8-144">Swagger de saudação do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="509d8-144">View hello swagger</span></span>
<span data-ttu-id="509d8-145">Consulte Olá [swagger detalhes](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="509d8-145">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="509d8-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="509d8-146">Next steps</span></span>
[<span data-ttu-id="509d8-147">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="509d8-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

