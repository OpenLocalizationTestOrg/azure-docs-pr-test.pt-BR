---
title: "aaaCreate, link, excluir ou mover uma conta de integração de aplicativos lógicos do Azure | Microsoft Docs"
description: "Como toocreate uma integração de conta e vinculá-lo tooyour os aplicativos lógicos"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="ea23f-103">O que é uma conta de integração?</span><span class="sxs-lookup"><span data-stu-id="ea23f-103">What is an integration account?</span></span>

<span data-ttu-id="ea23f-104">Uma conta de integração permite que aplicativos de integração do enterprise toomanage artefatos, incluindo esquemas, mapas, certificados, parceiros e contratos.</span><span class="sxs-lookup"><span data-stu-id="ea23f-104">An integration account allows enterprise integration apps toomanage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="ea23f-105">Qualquer aplicativo de integração que você criar usa um tooaccess de conta de integração esses esquemas, mapas, certificados e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="ea23f-105">Any integration app you create uses an integration account tooaccess these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="ea23f-106">Criar uma conta de integração</span><span class="sxs-lookup"><span data-stu-id="ea23f-106">Create an integration account</span></span>

1.  <span data-ttu-id="ea23f-107">Entrar toohello [portal do Azure](http://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="ea23f-107">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="ea23f-108">No menu à esquerda do hello, selecione **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-108">From hello left menu, select **More services**.</span></span>

    ![Escolha “Mais serviços”](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="ea23f-110">Na caixa de pesquisa hello, digite "integração" para o filtro.</span><span class="sxs-lookup"><span data-stu-id="ea23f-110">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="ea23f-111">Na lista de resultados de saudação, selecione **contas de integração**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-111">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtre por "integração", selecione "Contas de Integração"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="ea23f-113">Na parte superior de saudação da página hello, escolha **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-113">At hello top of hello page, choose **Add**.</span></span>

    ![Escolha Adicionar](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="ea23f-115">Nome de sua conta de integração e selecione Olá assinatura do Azure que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="ea23f-115">Name your integration account and select hello Azure subscription that you want toouse.</span></span> <span data-ttu-id="ea23f-116">Você pode criar um novo **grupo de recursos** ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="ea23f-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="ea23f-117">Selecione um **Local** para hospedar sua conta de integração e um **Tipo de preço**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="ea23f-118">Quando você estiver pronto, escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-118">When you're ready, choose **Create**.</span></span>

    ![Forneça detalhes para sua conta de integração](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="ea23f-120">Azure provisiona sua conta de integração no local de saudação selecionada, que deve ser concluída em 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="ea23f-120">Azure provisions your integration account  in hello selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="ea23f-121">Atualize a página de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea23f-121">Refresh hello page.</span></span> <span data-ttu-id="ea23f-122">Você verá a nova conta de integração listada.</span><span class="sxs-lookup"><span data-stu-id="ea23f-122">You see your new integration account listed.</span></span>

    ![A nova conta de integração é exibida](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="ea23f-124">Em seguida, vincule conta de integração de saudação que você tooyour criado aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="ea23f-124">Next, link hello integration account that you created tooyour logic app.</span></span> 

## <a name="link-an-integration-account-tooa-logic-app"></a><span data-ttu-id="ea23f-125">Vincular a um aplicativo de conta tooa lógica da integração</span><span class="sxs-lookup"><span data-stu-id="ea23f-125">Link an integration account tooa logic app</span></span>

<span data-ttu-id="ea23f-126">toogive seus aplicativos lógicos acessar toomaps, esquemas, contratos e outros artefatos em sua conta de integração, aplicativo de conta da integração link Olá tooyour lógica.</span><span class="sxs-lookup"><span data-stu-id="ea23f-126">toogive your logic apps access toomaps, schemas, agreements, and other artifacts in your integration account, link hello integration account tooyour logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ea23f-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ea23f-127">Prerequisites</span></span>

* <span data-ttu-id="ea23f-128">Uma conta de integração</span><span class="sxs-lookup"><span data-stu-id="ea23f-128">An integration account</span></span>
* <span data-ttu-id="ea23f-129">Um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="ea23f-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="ea23f-130">Verifique se seu aplicativo de conta e a lógica de integração no hello *mesmo local do Azure* antes de começar.</span><span class="sxs-lookup"><span data-stu-id="ea23f-130">Make sure your integration account and logic app are in hello *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="ea23f-131">No hello portal do Azure, selecione seu aplicativo lógico e verifique o local da lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ea23f-131">In hello Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Selecionar seu aplicativo lógico, verificar o local](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="ea23f-133">Em **Configurações**, selecione **Conta de Integração**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Selecionar “Conta de Integração”](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="ea23f-135">De saudação **selecionar uma conta de integração** listar, conta de integração Olá selecione deseja toolink tooyour lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ea23f-135">From hello **Select an Integration account** list, select hello integration account you want toolink tooyour logic app.</span></span> <span data-ttu-id="ea23f-136">toofinish vinculação, escolha **salvar**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-136">toofinish linking, choose **Save**.</span></span>

    ![Selecione sua conta de integração](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="ea23f-138">Você obtém uma notificação que mostra a integração de conta é vinculado tooyour lógica aplicativo e todos os artefatos em sua conta de integração estão agora disponíveis tooyour lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ea23f-138">You get a notification that shows your integration account is linked tooyour logic app,  and that all artifacts in your integration account are now available tooyour logic app.</span></span>

    ![Seu aplicativo lógico está vinculado tooyour conta de integração](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="ea23f-140">Agora que sua conta de integração está vinculado tooyour lógica aplicativo, é possível usar conectores de saudação B2B em seus aplicativos de lógica.</span><span class="sxs-lookup"><span data-stu-id="ea23f-140">Now that your integration account is linked tooyour logic app, you can use hello B2B connectors in your logic apps.</span></span> <span data-ttu-id="ea23f-141">Alguns conectores B2B comuns incluem a validação de XML e codificação/decodificação de arquivo simples.</span><span class="sxs-lookup"><span data-stu-id="ea23f-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="ea23f-142">Excluir sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="ea23f-142">Delete your integration account</span></span>

1. <span data-ttu-id="ea23f-143">Escolha **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-143">Select **More services**.</span></span>

    ![Escolha “Mais serviços”](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="ea23f-145">Na caixa de pesquisa hello, digite "integração" para o filtro.</span><span class="sxs-lookup"><span data-stu-id="ea23f-145">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="ea23f-146">Na lista de resultados de saudação, selecione **contas de integração**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-146">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtre por "integração", selecione "Contas de Integração"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="ea23f-148">Selecione a conta de integração de saudação que você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="ea23f-148">Select hello integration account that you want toodelete.</span></span>

    ![Selecione toodelete de conta de integração](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="ea23f-150">No menu de saudação, escolha **excluir**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-150">On hello menu, choose **Delete**.</span></span>

    ![Clique em “Excluir”](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="ea23f-152">Confirme sua conta de integração de saudação toodelete choice.</span><span class="sxs-lookup"><span data-stu-id="ea23f-152">Confirm your choice toodelete hello integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="ea23f-153">Selecionar sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="ea23f-153">Move your integration account</span></span>

<span data-ttu-id="ea23f-154">toomove um tooanother de conta de integração do Azure assinatura ou grupo de recursos, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="ea23f-154">toomove an integration account tooanother Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea23f-155">Depois de mover uma conta de integração, você deve atualizar todos os scripts toouse Olá novas IDs de recurso.</span><span class="sxs-lookup"><span data-stu-id="ea23f-155">You must update all scripts toouse hello new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="ea23f-156">Escolha **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-156">Select **More services**.</span></span>

    ![Escolha “Mais serviços”](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="ea23f-158">Na caixa de pesquisa hello, digite "integração" para o filtro.</span><span class="sxs-lookup"><span data-stu-id="ea23f-158">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="ea23f-159">Na lista de resultados de saudação, selecione **contas de integração**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-159">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtre por "integração", selecione "Contas de Integração"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="ea23f-161">Selecione a conta de integração de saudação que você deseja toomove.</span><span class="sxs-lookup"><span data-stu-id="ea23f-161">Select hello integration account that you want toomove.</span></span> <span data-ttu-id="ea23f-162">Em **Configurações**, escolha **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="ea23f-162">Under **Settings**, choose **Properties**.</span></span>

    ![Selecione toomove de conta de integração.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="ea23f-165">Alterar o grupo de recursos de saudação ou assinatura do Azure associado à sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="ea23f-165">Change hello resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Escolher Alterar grupo de recursos ou Alterar assinatura](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="ea23f-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea23f-167">Next Steps</span></span>
* [<span data-ttu-id="ea23f-168">Saiba mais sobre os contratos</span><span class="sxs-lookup"><span data-stu-id="ea23f-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  

