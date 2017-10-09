---
title: "mensagens de aaaDecode AS2 - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Como toouse Olá decodificador de AS2 no hello Enterprise Integration Pack para aplicativos do Azure lógica"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="ecc58-103">Decodificar mensagens AS2 para aplicativos do Azure lógica com hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="ecc58-103">Decode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span> 

<span data-ttu-id="ecc58-104">tooestablish segurança e confiabilidade ao transmitir mensagens, use o conector de mensagem AS2 decodificar hello.</span><span class="sxs-lookup"><span data-stu-id="ecc58-104">tooestablish security and reliability while transmitting messages, use hello Decode AS2 message connector.</span></span> <span data-ttu-id="ecc58-105">Esse conector fornece a assinatura digital, descriptografia e confirmações por meio de MDN (notificações de disposição de mensagem).</span><span class="sxs-lookup"><span data-stu-id="ecc58-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ecc58-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ecc58-106">Before you start</span></span>

<span data-ttu-id="ecc58-107">Aqui está a itens Olá que necessários:</span><span class="sxs-lookup"><span data-stu-id="ecc58-107">Here's hello items you need:</span></span>

* <span data-ttu-id="ecc58-108">Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="ecc58-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="ecc58-109">Uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md) que já esteja definida e associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc58-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="ecc58-110">Você deve ter um conector de mensagem integração conta toouse Olá decodificar AS2.</span><span class="sxs-lookup"><span data-stu-id="ecc58-110">You must have an integration account toouse hello Decode AS2 message connector.</span></span>
* <span data-ttu-id="ecc58-111">Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="ecc58-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="ecc58-112">Um [contrato AS2](logic-apps-enterprise-integration-as2.md) que já está definido em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="ecc58-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="ecc58-113">Decodificar mensagens AS2</span><span class="sxs-lookup"><span data-stu-id="ecc58-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="ecc58-114">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ecc58-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="ecc58-115">conector de mensagem AS2 decodificar Olá não tem gatilhos, portanto você deve adicionar um gatilho para iniciar seu aplicativo lógico, como um disparador de solicitação.</span><span class="sxs-lookup"><span data-stu-id="ecc58-115">hello Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="ecc58-116">No hello lógica de aplicativo Designer, adicione um gatilho e, em seguida, adicionar um aplicativo de lógica de tooyour de ação.</span><span class="sxs-lookup"><span data-stu-id="ecc58-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="ecc58-117">Na caixa de pesquisa hello, digite "AS2" para o filtro.</span><span class="sxs-lookup"><span data-stu-id="ecc58-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="ecc58-118">Selecione **AS2 – Decodificar Mensagem AS2**.</span><span class="sxs-lookup"><span data-stu-id="ecc58-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Procure "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="ecc58-120">Se anteriormente você não criar todas as conexões tooyour conta de integração, será solicitado que você toocreate agora essa conexão.</span><span class="sxs-lookup"><span data-stu-id="ecc58-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="ecc58-121">Nome de sua conexão e selecione Olá integração conta que você deseja tooconnect.</span><span class="sxs-lookup"><span data-stu-id="ecc58-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![Criar conexão de integração](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="ecc58-123">As propriedades com um asterisco são obrigatórias.</span><span class="sxs-lookup"><span data-stu-id="ecc58-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="ecc58-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ecc58-124">Property</span></span> | <span data-ttu-id="ecc58-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="ecc58-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="ecc58-126">Nome da Conexão *</span><span class="sxs-lookup"><span data-stu-id="ecc58-126">Connection Name *</span></span> |<span data-ttu-id="ecc58-127">Digite um nome para a conexão.</span><span class="sxs-lookup"><span data-stu-id="ecc58-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="ecc58-128">Uma conta de integração *</span><span class="sxs-lookup"><span data-stu-id="ecc58-128">Integration Account *</span></span> |<span data-ttu-id="ecc58-129">Insira um nome para sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="ecc58-129">Enter a name for your integration account.</span></span> <span data-ttu-id="ecc58-130">Certifique-se de que seu aplicativo de conta e a lógica de integração estão em Olá mesmo local do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc58-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="ecc58-131">Quando terminar, os detalhes de conexão devem ser exemplo toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="ecc58-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="ecc58-132">toofinish criar sua conexão, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="ecc58-132">toofinish creating your connection, choose **Create**.</span></span>

    ![detalhes de conexão de integração](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="ecc58-134">Depois de criar sua conexão, conforme mostrado neste exemplo, selecione **corpo** e **cabeçalhos** do hello solicitar saídas.</span><span class="sxs-lookup"><span data-stu-id="ecc58-134">After your connection is created, as shown in this example, select **Body** and **Headers** from hello Request outputs.</span></span>
   
    ![conexão de integração criada](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="ecc58-136">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ecc58-136">For example:</span></span>

    ![Selecione Corpo e Cabeçalhos de saídas de Solicitação](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="ecc58-138">Detalhes do decodificador AS2</span><span class="sxs-lookup"><span data-stu-id="ecc58-138">AS2 decoder details</span></span>

<span data-ttu-id="ecc58-139">conector de decodificar AS2 Olá executa essas tarefas:</span><span class="sxs-lookup"><span data-stu-id="ecc58-139">hello Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="ecc58-140">Processa cabeçalhos HTTP/AS2</span><span class="sxs-lookup"><span data-stu-id="ecc58-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="ecc58-141">Verifica a assinatura de saudação (se configurado)</span><span class="sxs-lookup"><span data-stu-id="ecc58-141">Verifies hello signature (if configured)</span></span>
* <span data-ttu-id="ecc58-142">Descriptografa mensagens de saudação (se configurado)</span><span class="sxs-lookup"><span data-stu-id="ecc58-142">Decrypts hello messages (if configured)</span></span>
* <span data-ttu-id="ecc58-143">Descompacta a mensagem de saudação (se configurado)</span><span class="sxs-lookup"><span data-stu-id="ecc58-143">Decompresses hello message (if configured)</span></span>
* <span data-ttu-id="ecc58-144">Reconcilia um MDN recebido com a mensagem de saída original Olá</span><span class="sxs-lookup"><span data-stu-id="ecc58-144">Reconciles a received MDN with hello original outbound message</span></span>
* <span data-ttu-id="ecc58-145">Atualizações e correlaciona registros no banco de dados de não-repúdio Olá</span><span class="sxs-lookup"><span data-stu-id="ecc58-145">Updates and correlates records in hello non-repudiation database</span></span>
* <span data-ttu-id="ecc58-146">Grava os registros para o relatório de status do AS2</span><span class="sxs-lookup"><span data-stu-id="ecc58-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="ecc58-147">Olá saída carga conteúdo é codificados na base64</span><span class="sxs-lookup"><span data-stu-id="ecc58-147">hello output payload contents are base64 encoded</span></span>
* <span data-ttu-id="ecc58-148">Determina se um MDN é necessário e se Olá MDN deve ser síncrona ou assíncronas baseiam na configuração no acordo AS2</span><span class="sxs-lookup"><span data-stu-id="ecc58-148">Determines whether an MDN is required, and whether hello MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="ecc58-149">Gera um MDN síncrono ou assíncrono (com base nas configurações do contrato)</span><span class="sxs-lookup"><span data-stu-id="ecc58-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="ecc58-150">Define propriedades e tokens de correlação de saudação em Olá MDN</span><span class="sxs-lookup"><span data-stu-id="ecc58-150">Sets hello correlation tokens and properties on hello MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="ecc58-151">Experimente este exemplo</span><span class="sxs-lookup"><span data-stu-id="ecc58-151">Try this sample</span></span>

<span data-ttu-id="ecc58-152">tootry implantar uma lógica totalmente operacional exemplo e aplicativo AS2 cenário, consulte Olá [AS2 cenário e o modelo de aplicativo de lógica](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="ecc58-152">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="ecc58-153">Swagger de saudação do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="ecc58-153">View hello swagger</span></span>
<span data-ttu-id="ecc58-154">Consulte Olá [swagger detalhes](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="ecc58-154">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ecc58-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ecc58-155">Next steps</span></span>
[<span data-ttu-id="ecc58-156">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="ecc58-156">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

