---
title: "integração aaaManage conta artefato de metadados - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Adicionar ou recuperar metadados de artefato de contas de integração dos Aplicativo Lógico do Azure"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="7846f-103">Gerenciar metadados de artefato nas contas de integração de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="7846f-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="7846f-104">É possível definir metadados personalizados para artefatos em contas de integração e recuperar esses metadados durante o tempo de execução do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="7846f-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="7846f-105">Por exemplo, é possível especificar metadados para artefatos como parceiros, contratos, esquemas e mapas – todos armazenam metadados usando pares chave-valor.</span><span class="sxs-lookup"><span data-stu-id="7846f-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="7846f-106">Atualmente, os artefatos não é possível criar metadados por meio da interface do usuário, mas você pode usar APIs REST toocreate metadados.</span><span class="sxs-lookup"><span data-stu-id="7846f-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs toocreate metadata.</span></span> <span data-ttu-id="7846f-107">metadados de tooadd ao criar ou selecionar um parceiro, o contrato ou o esquema no hello portal do Azure, escolha **editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="7846f-107">tooadd metadata when you create or select a partner, agreement, or schema in hello Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="7846f-108">metadados de artefato tooretrieve em aplicativos lógicos, você pode usar o recurso de pesquisa de artefato de conta de integração de saudação.</span><span class="sxs-lookup"><span data-stu-id="7846f-108">tooretrieve artifact metadata in logic apps, you can use hello Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a><span data-ttu-id="7846f-109">Adicionar metadados tooartifacts nas contas de integração</span><span class="sxs-lookup"><span data-stu-id="7846f-109">Add metadata tooartifacts in integration accounts</span></span>

1. <span data-ttu-id="7846f-110">Crie uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="7846f-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="7846f-111">Adicionar uma conta de integração do artefato tooyour, por exemplo, um [parceiro](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [contrato](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), ou [esquema](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="7846f-111">Add an artifact tooyour integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="7846f-112">Selecione o artefato hello, escolha **editar como JSON**e insira os detalhes de metadados.</span><span class="sxs-lookup"><span data-stu-id="7846f-112">Select hello artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Inserir metadados](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="7846f-114">Recuperar metadados de artefatos de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="7846f-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="7846f-115">Crie um [aplicativo lógico](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7846f-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="7846f-116">Criar um [link da sua conta de integração lógica aplicativo tooyour](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="7846f-116">Create a [link from your logic app tooyour integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="7846f-117">No Designer de lógica de aplicativo, adicione um disparador como *solicitação* ou *HTTP* tooyour lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7846f-117">In Logic App Designer, add a trigger like *Request* or *HTTP* tooyour logic app.</span></span>

4.  <span data-ttu-id="7846f-118">Escolha **Próxima Etapa** > **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="7846f-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="7846f-119">Pesquise *integração* para poder localizá-la e, em seguida, selecione **Conta de Integração – Pesquisa de Artefato da Conta de Integração**.</span><span class="sxs-lookup"><span data-stu-id="7846f-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Selecionar Pesquisa de Artefato da Conta de Integração](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="7846f-121">Selecione Olá **tipo de artefato**e fornecer Olá **nome do artefato**.</span><span class="sxs-lookup"><span data-stu-id="7846f-121">Select hello **Artifact Type**, and provide hello **Artifact Name**.</span></span>

    ![Selecionar tipo de artefato e especificar um nome de artefato](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="7846f-123">Exemplo: Recuperar metadados do parceiro</span><span class="sxs-lookup"><span data-stu-id="7846f-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="7846f-124">Os metadados do parceiro têm estes detalhes de `routingUrl`:</span><span class="sxs-lookup"><span data-stu-id="7846f-124">Partner metadata has these `routingUrl` details:</span></span>

![Encontrar metadados de “routingURL” do parceiro](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="7846f-126">No aplicativo lógico, adicione o gatilho, uma ação **Conta de Integração – Pesquisa de Artefato da Conta de Integração** do parceiro e um **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="7846f-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Adicionar o gatilho, pesquisa de artefato e aplicativo de lógica de tooyour "HTTP"](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="7846f-128">Olá tooretrieve URI, vá tooCode exibição para seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="7846f-128">tooretrieve hello URI, go tooCode View for your logic app.</span></span> <span data-ttu-id="7846f-129">A definição do aplicativo lógico deve ser parecida com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="7846f-129">Your logic app definition should look like this example:</span></span>

    ![Procurar pesquisa](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="7846f-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7846f-131">Next steps</span></span>
* [<span data-ttu-id="7846f-132">Saiba mais sobre os contratos</span><span class="sxs-lookup"><span data-stu-id="7846f-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  
