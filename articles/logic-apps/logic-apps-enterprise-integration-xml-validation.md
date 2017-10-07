---
title: "aaaValidate XML - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Validar XML com esquemas para os aplicativos lógicos do Azure e a cenários B2B usando Olá Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="a91c5-103">Validar XML para integração corporativa</span><span class="sxs-lookup"><span data-stu-id="a91c5-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="a91c5-104">Geralmente em cenários B2B, parceiros de saudação em um contrato devem Certifique-se de que as mensagens de saudação que do exchange que são válidas antes de iniciar o processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="a91c5-104">Often in B2B scenarios, hello partners in an agreement must make sure that hello messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="a91c5-105">Você pode validar documentos em um esquema predefinido usando o conector de validação de XML de Olá Olá use em Olá Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="a91c5-105">You can validate documents against a predefined schema by using hello use hello XML Validation connector in hello Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-hello-xml-validation-connector"></a><span data-ttu-id="a91c5-106">Validar um documento com o conector de validação de XML Olá</span><span class="sxs-lookup"><span data-stu-id="a91c5-106">Validate a document with hello XML Validation connector</span></span>

1. <span data-ttu-id="a91c5-107">Criar um aplicativo lógico, e [vincular Olá aplicativo toohello integração conta](../logic-apps/logic-apps-enterprise-integration-accounts.md "Saiba toolink um aplicativo de conta tooa lógica da integração") que tem o esquema de saudação desejar toouse para validar dados XML.</span><span class="sxs-lookup"><span data-stu-id="a91c5-107">Create a logic app, and [link hello app toohello integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that has hello schema you want toouse for validating XML data.</span></span>

2. <span data-ttu-id="a91c5-108">Adicionar um **solicitar - quando HTTP de uma solicitação é recebida** gatilho tooyour lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a91c5-108">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="a91c5-109">Olá tooadd **validação de XML** ação, escolha **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="a91c5-109">tooadd hello **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="a91c5-110">toofilter todos Olá toohello de ações que você desejar, digite *xml* na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="a91c5-110">toofilter all hello actions toohello one that you want, enter *xml* in hello search box.</span></span> <span data-ttu-id="a91c5-111">Escolha **Validação de XML**.</span><span class="sxs-lookup"><span data-stu-id="a91c5-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="a91c5-112">Olá toospecify conteúdo XML que você deseja toovalidate, selecione **conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="a91c5-112">toospecify hello XML content that you want toovalidate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="a91c5-113">Selecione a marca de corpo de Olá como Olá conteúdo que você deseja toovalidate.</span><span class="sxs-lookup"><span data-stu-id="a91c5-113">Select hello body tag as hello content that you want toovalidate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="a91c5-114">esquema de saudação toospecify você deseja toouse para validar a saudação anterior *conteúdo* de entrada, escolha **nome do esquema**.</span><span class="sxs-lookup"><span data-stu-id="a91c5-114">toospecify hello schema you want toouse for validating hello previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="a91c5-115">Salve seu trabalho </span><span class="sxs-lookup"><span data-stu-id="a91c5-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="a91c5-116">Agora, a configuração do conector de validação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="a91c5-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="a91c5-117">Em um aplicativo do mundo real, você poderá toostore dados de saudação validada em um aplicativo da linha de negócios (LOB) como o SalesForce.</span><span class="sxs-lookup"><span data-stu-id="a91c5-117">In a real world application, you might want toostore hello validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="a91c5-118">toosend Olá tooSalesforce saída validado, adicione uma ação.</span><span class="sxs-lookup"><span data-stu-id="a91c5-118">toosend hello validated output tooSalesforce, add an action.</span></span>

<span data-ttu-id="a91c5-119">tootest a ação de validação, criar um ponto de extremidade de toohello HTTP de solicitação.</span><span class="sxs-lookup"><span data-stu-id="a91c5-119">tootest your validation action, make a request toohello HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a91c5-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a91c5-120">Next steps</span></span>
[<span data-ttu-id="a91c5-121">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="a91c5-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")   

