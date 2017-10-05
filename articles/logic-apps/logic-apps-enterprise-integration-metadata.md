---
title: "Gerenciar metadados de artefato de contas de integração – Aplicativo Lógico do Azure | Microsoft Docs"
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
ms.openlocfilehash: 28bb8296ddd820ec5aa9793dc0928b4b1e67bf6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="49ff5-103">Gerenciar metadados de artefato nas contas de integração de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="49ff5-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="49ff5-104">É possível definir metadados personalizados para artefatos em contas de integração e recuperar esses metadados durante o tempo de execução do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="49ff5-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="49ff5-105">Por exemplo, é possível especificar metadados para artefatos como parceiros, contratos, esquemas e mapas – todos armazenam metadados usando pares chave-valor.</span><span class="sxs-lookup"><span data-stu-id="49ff5-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="49ff5-106">Atualmente, os artefatos não podem criar metadados por meio da interface do usuário, mas é possível usar APIs REST para criar metadados.</span><span class="sxs-lookup"><span data-stu-id="49ff5-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata.</span></span> <span data-ttu-id="49ff5-107">Para adicionar metadados ao criar ou selecionar um parceiro, contrato ou esquema no portal do Azure, escolha **Editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="49ff5-107">To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="49ff5-108">Para recuperar metadados de artefato em aplicativos lógicos, é possível usar o recurso Pesquisa de Artefato da Conta de Integração.</span><span class="sxs-lookup"><span data-stu-id="49ff5-108">To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a><span data-ttu-id="49ff5-109">Adicionar metadados a artefatos em contas de integração</span><span class="sxs-lookup"><span data-stu-id="49ff5-109">Add metadata to artifacts in integration accounts</span></span>

1. <span data-ttu-id="49ff5-110">Crie uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="49ff5-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="49ff5-111">Adicione um artefato à conta de integração, por exemplo, um [parceiro](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [contrato](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements) ou [esquema](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="49ff5-111">Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="49ff5-112">Selecione o artefato, escolha **Editar como JSON** e insira os detalhes dos metadados.</span><span class="sxs-lookup"><span data-stu-id="49ff5-112">Select the artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Inserir metadados](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="49ff5-114">Recuperar metadados de artefatos de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="49ff5-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="49ff5-115">Crie um [aplicativo lógico](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="49ff5-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="49ff5-116">Crie um [link do aplicativo lógico para a conta de integração](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="49ff5-116">Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="49ff5-117">No Designer de Aplicativos Lógicos, adicione um gatilho como *Solicitação* ou *HTTP* ao aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="49ff5-117">In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.</span></span>

4.  <span data-ttu-id="49ff5-118">Escolha **Próxima Etapa** > **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="49ff5-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="49ff5-119">Pesquise *integração* para poder localizá-la e, em seguida, selecione **Conta de Integração – Pesquisa de Artefato da Conta de Integração**.</span><span class="sxs-lookup"><span data-stu-id="49ff5-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Selecionar Pesquisa de Artefato da Conta de Integração](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="49ff5-121">Selecione o **Tipo de Artefato** e forneça o **Nome do Artefato**.</span><span class="sxs-lookup"><span data-stu-id="49ff5-121">Select the **Artifact Type**, and provide the **Artifact Name**.</span></span>

    ![Selecionar tipo de artefato e especificar um nome de artefato](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="49ff5-123">Exemplo: Recuperar metadados do parceiro</span><span class="sxs-lookup"><span data-stu-id="49ff5-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="49ff5-124">Os metadados do parceiro têm estes detalhes de `routingUrl`:</span><span class="sxs-lookup"><span data-stu-id="49ff5-124">Partner metadata has these `routingUrl` details:</span></span>

![Encontrar metadados de “routingURL” do parceiro](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="49ff5-126">No aplicativo lógico, adicione o gatilho, uma ação **Conta de Integração – Pesquisa de Artefato da Conta de Integração** do parceiro e um **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="49ff5-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Adicionar gatilho, pesquisa de artefato e “HTTP” ao aplicativo lógico](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="49ff5-128">Para recuperar o URI, acesse o Modo de Exibição de Código do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="49ff5-128">To retrieve the URI, go to Code View for your logic app.</span></span> <span data-ttu-id="49ff5-129">A definição do aplicativo lógico deve ser parecida com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="49ff5-129">Your logic app definition should look like this example:</span></span>

    ![Procurar pesquisa](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="49ff5-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49ff5-131">Next steps</span></span>
* [<span data-ttu-id="49ff5-132">Saiba mais sobre os contratos</span><span class="sxs-lookup"><span data-stu-id="49ff5-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  
