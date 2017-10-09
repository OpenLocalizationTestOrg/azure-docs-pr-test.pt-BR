---
title: "Azure Active Directory B2C: configuração do Google+ | Microsoft Docs"
description: "Fornece tooconsumers se inscrever e fazer logon com contas do Google + nos aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a><span data-ttu-id="e61e1-103">B2C de diretório ativo do Azure: Fornecer tooconsumers se inscrever e fazer logon com contas do Google +</span><span class="sxs-lookup"><span data-stu-id="e61e1-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="e61e1-104">Criar um aplicativo do Google+</span><span class="sxs-lookup"><span data-stu-id="e61e1-104">Create a Google+ application</span></span>
<span data-ttu-id="e61e1-105">toouse Google + como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo do Google + e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="e61e1-105">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="e61e1-106">É necessário um toodo de conta do Google + isso.</span><span class="sxs-lookup"><span data-stu-id="e61e1-106">You need a Google+ account toodo this.</span></span> <span data-ttu-id="e61e1-107">Se não tiver uma, você poderá obtê-la em [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="e61e1-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="e61e1-108">Vá toohello [Console de desenvolvedores do Google](https://console.developers.google.com/) e entre com suas credenciais de conta do Google +.</span><span class="sxs-lookup"><span data-stu-id="e61e1-108">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="e61e1-109">Clique em **Criar projeto**, insira um **Nome de projeto** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e61e1-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+ – Introdução](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ – Novo projeto](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="e61e1-112">Clique em **Manager API** e, em seguida, clique em **credenciais** em Olá barra de navegação esquerda.</span><span class="sxs-lookup"><span data-stu-id="e61e1-112">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
4. <span data-ttu-id="e61e1-113">Clique em Olá **tela de consentimento de OAuth** guia na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="e61e1-113">Click hello **OAuth consent screen** tab at hello top.</span></span>
   
    ![Google+ – Credenciais](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="e61e1-115">Selecione ou especifique um **Endereço de email** válido, forneça um **Nome de produto** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e61e1-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+ – Tela de consentimento do OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="e61e1-117">Clique em **Novas credenciais** e escolha **ID do cliente OAuth**.</span><span class="sxs-lookup"><span data-stu-id="e61e1-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+ – Tela de consentimento do OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="e61e1-119">Em **Tipo de aplicativo**, selecione **Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="e61e1-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+ – Tela de consentimento do OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="e61e1-121">Forneça um **nome** para seu aplicativo, insira `https://login.microsoftonline.com` em Olá **origens do JavaScript autorizado** campo, e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **autorizados redirecionar URIs**campo.</span><span class="sxs-lookup"><span data-stu-id="e61e1-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="e61e1-122">Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="e61e1-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="e61e1-123">Olá **{locatário}** valor diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e61e1-123">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="e61e1-124">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e61e1-124">Click **Create**.</span></span>
   
    ![Google+ – Criar ID do cliente](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="e61e1-126">Copie os valores de saudação do **ID do cliente** e **segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="e61e1-126">Copy hello values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="e61e1-127">Você precisará de ambos tooconfigure Google + como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="e61e1-127">You will need both of them tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="e61e1-128">**Segredo do cliente** é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="e61e1-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+ – Segredo do cliente](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="e61e1-130">Configurar o Google+ como um provedor de identidade no locatário</span><span class="sxs-lookup"><span data-stu-id="e61e1-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="e61e1-131">Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e61e1-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="e61e1-132">Na folha de recursos Olá B2C, clique em **provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="e61e1-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="e61e1-133">Clique em **+ adicionar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="e61e1-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="e61e1-134">Forneça um amigável **nome** para configuração do provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="e61e1-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="e61e1-135">Por exemplo, insira "G+".</span><span class="sxs-lookup"><span data-stu-id="e61e1-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="e61e1-136">Clique em **Tipo de provedor de identidade**, selecione **Google** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e61e1-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="e61e1-137">Clique em **configurar esse provedor de identidade** e digite Olá ID e o cliente segredo do cliente do hello Google + aplicativo que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e61e1-137">Click **Set up this identity provider** and enter hello client ID and client secret of hello Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="e61e1-138">Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração do Google +.</span><span class="sxs-lookup"><span data-stu-id="e61e1-138">Click **OK** and then click **Create** toosave your Google+ configuration.</span></span>

