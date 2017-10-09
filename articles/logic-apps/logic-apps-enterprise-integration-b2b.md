---
title: "soluções aaaCreate B2B - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Receber dados em aplicativos lógicos usando recursos de saudação B2B do hello Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a><span data-ttu-id="3d32c-103">Receber dados em aplicativos de lógica com recursos de B2B Olá Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="3d32c-103">Receive data in logic apps with hello B2B features in hello Enterprise Integration Pack</span></span>

<span data-ttu-id="3d32c-104">Depois de criar uma conta de integração com parceiros e acordos, você está pronto toocreate um fluxo de trabalho do negócio toobusiness (B2B) para seu aplicativo lógico com hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d32c-104">After you create an integration account that has partners and agreements, you are ready toocreate a business toobusiness (B2B) workflow for your logic app with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d32c-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3d32c-105">Prerequisites</span></span>

<span data-ttu-id="3d32c-106">toouse Olá AS2 e X12 ações, você deve ter uma conta de integração da empresa.</span><span class="sxs-lookup"><span data-stu-id="3d32c-106">toouse hello AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="3d32c-107">Saiba [como toocreate uma integração Enterprise conta](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="3d32c-107">Learn [how toocreate an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="3d32c-108">Criar um aplicativo lógico com conectores B2B</span><span class="sxs-lookup"><span data-stu-id="3d32c-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="3d32c-109">Siga estas etapas toocreate um B2B lógica aplicativo usa hello AS2 e X12 dados de tooreceive ações de um parceiro comercial:</span><span class="sxs-lookup"><span data-stu-id="3d32c-109">Follow these steps toocreate a B2B logic app that uses hello AS2 and X12 actions tooreceive data from a trading partner:</span></span>

1. <span data-ttu-id="3d32c-110">Criar um aplicativo lógico, em seguida, [vincular sua conta de integração do aplicativo tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="3d32c-110">Create a logic app, then [link your app tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="3d32c-111">Adicionar um **solicitar - quando HTTP de uma solicitação é recebida** gatilho tooyour lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3d32c-111">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="3d32c-112">Olá tooadd **decodificar AS2** ação, selecione **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="3d32c-112">tooadd hello **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="3d32c-113">toofilter todos os toohello de ações que você deseja, insira palavras Olá **as2** na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d32c-113">toofilter all actions toohello one that you want, enter hello word **as2** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="3d32c-114">Selecione Olá **AS2 - mensagem AS2 decodificar** ação.</span><span class="sxs-lookup"><span data-stu-id="3d32c-114">Select hello **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="3d32c-115">Adicionar Olá **corpo** que você deseja toouse como entrada.</span><span class="sxs-lookup"><span data-stu-id="3d32c-115">Add hello **Body** that you want toouse as input.</span></span> <span data-ttu-id="3d32c-116">Neste exemplo, selecione o corpo da saudação de solicitação HTTP Olá gatilhos Olá aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="3d32c-116">In this example, select hello body of hello HTTP request that triggers hello logic app.</span></span> <span data-ttu-id="3d32c-117">Ou insira uma expressão que entradas cabeçalhos Olá Olá **CABEÇALHOS** campo:</span><span class="sxs-lookup"><span data-stu-id="3d32c-117">Or enter an expression that inputs hello headers in hello **HEADERS** field:</span></span>

    <span data-ttu-id="3d32c-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="3d32c-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="3d32c-119">Adicionar Olá necessário **cabeçalhos** para AS2, que pode ser encontrado nos cabeçalhos de solicitação HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d32c-119">Add hello required **Headers** for AS2, which you can find in hello HTTP request headers.</span></span> <span data-ttu-id="3d32c-120">Neste exemplo, selecione cabeçalhos Olá de solicitação HTTP Olá esse aplicativo de lógica de saudação do gatilho.</span><span class="sxs-lookup"><span data-stu-id="3d32c-120">In this example, select hello headers of hello HTTP request that trigger hello logic app.</span></span>

8. <span data-ttu-id="3d32c-121">Agora adicione ação de mensagem de decodificação X12 hello.</span><span class="sxs-lookup"><span data-stu-id="3d32c-121">Now add hello Decode X12 message action.</span></span> <span data-ttu-id="3d32c-122">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="3d32c-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="3d32c-123">toofilter todos os toohello de ações que você deseja, insira palavras Olá **x12** na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d32c-123">toofilter all actions toohello one that you want, enter hello word **x12** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="3d32c-124">Selecione Olá **X12-decodificar X12 mensagem** ação.</span><span class="sxs-lookup"><span data-stu-id="3d32c-124">Select hello **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="3d32c-125">Agora você deve especificar a ação de entrada toothis hello.</span><span class="sxs-lookup"><span data-stu-id="3d32c-125">Now you must specify hello input toothis action.</span></span> <span data-ttu-id="3d32c-126">Essa entrada é saída de saudação da ação de AS2 anterior hello.</span><span class="sxs-lookup"><span data-stu-id="3d32c-126">This input is hello output from hello previous AS2 action.</span></span>

    <span data-ttu-id="3d32c-127">conteúdo de mensagem real Hello está em um objeto JSON e é codificação base64, portanto, você deve especificar uma expressão como entrada hello.</span><span class="sxs-lookup"><span data-stu-id="3d32c-127">hello actual message content is in a JSON object and is base64 encoded, so you must specify an expression as hello input.</span></span> 
    <span data-ttu-id="3d32c-128">Digite hello seguinte expressão em Olá **X12 simples mensagem de arquivo tooDECODE** campo de entrada:</span><span class="sxs-lookup"><span data-stu-id="3d32c-128">Enter hello following expression in hello **X12 FLAT FILE MESSAGE tooDECODE** input field:</span></span>
    
    <span data-ttu-id="3d32c-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="3d32c-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="3d32c-130">Agora adicione etapas dados de saudação X12 toodecode recebida do parceiro comercial de saudação e itens em um objeto JSON de saída.</span><span class="sxs-lookup"><span data-stu-id="3d32c-130">Now add steps toodecode hello X12 data received from hello trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="3d32c-131">parceiro de saudação toonotify que Olá dados foi recebido, você pode enviar de volta uma resposta que contém a saudação AS2 mensagem disposição MDN (notificação) em uma ação de resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="3d32c-131">toonotify hello partner that hello data was received, you can send back a response containing hello AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="3d32c-132">Olá tooadd **resposta** ação, escolha **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="3d32c-132">tooadd hello **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="3d32c-133">toofilter todos os toohello de ações que você deseja, insira palavras Olá **resposta** na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d32c-133">toofilter all actions toohello one that you want, enter hello word **response** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="3d32c-134">Selecione Olá **resposta** ação.</span><span class="sxs-lookup"><span data-stu-id="3d32c-134">Select hello **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="3d32c-135">tooaccess Olá MDN de saída Olá Olá **mensagem X12 de decodificação** action, a resposta de saudação do conjunto **corpo** campo com esta expressão:</span><span class="sxs-lookup"><span data-stu-id="3d32c-135">tooaccess hello MDN from hello output of hello **Decode X12 message** action, set hello response **BODY** field with this expression:</span></span>

    <span data-ttu-id="3d32c-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="3d32c-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="3d32c-137">Salve seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="3d32c-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="3d32c-138">Você concluiu a configuração de seu aplicativo lógico de B2B.</span><span class="sxs-lookup"><span data-stu-id="3d32c-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="3d32c-139">Em um aplicativo do mundo real, você pode querer toostore Olá decodificado X12 dados em um repositório de linha de negócios (LOB) dados ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3d32c-139">In a real world application, you might want toostore hello decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="3d32c-140">tooconnect seus próprios aplicativos LOB e use essas APIs em seu aplicativo de lógica, você pode adicionar mais ações ou APIs personalizadas de gravação.</span><span class="sxs-lookup"><span data-stu-id="3d32c-140">tooconnect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="3d32c-141">Recursos e casos de uso</span><span class="sxs-lookup"><span data-stu-id="3d32c-141">Features and use cases</span></span>

* <span data-ttu-id="3d32c-142">Olá AS2 X12 decodificar e codificar ações permitem que você trocar dados entre parceiros comerciais usando protocolos padrão da indústria em aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="3d32c-142">hello AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="3d32c-143">tooexchange dados com parceiros comerciais, você pode usar AS2 e X12 com ou sem o outro.</span><span class="sxs-lookup"><span data-stu-id="3d32c-143">tooexchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="3d32c-144">ações de B2B Olá ajudarão-lo a criar facilmente parceiros e acordos em sua conta de integração e consumi-los em um aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="3d32c-144">hello B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="3d32c-145">Estendendo o seu Aplicativo Lógico com outras ações, você pode enviar e receber dados de e para outros aplicativos e serviços, como o SalesForce.</span><span class="sxs-lookup"><span data-stu-id="3d32c-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="3d32c-146">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="3d32c-146">Learn more</span></span>
[<span data-ttu-id="3d32c-147">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="3d32c-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
