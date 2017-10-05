---
title: "Azure Active Directory B2C: configuração do Google+ | Microsoft Docs"
description: "Forneça inscrição e entrada aos consumidores com contas do Google+ em seus aplicativos protegidos pelo Azure Active Directory B2C."
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
ms.openlocfilehash: 6ab73e5c79742ab548733f5712dee1e28461db9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-google-accounts"></a><span data-ttu-id="81277-103">Azure Active Directory B2C: fornecer inscrição e conexão aos consumidores com contas do Google+</span><span class="sxs-lookup"><span data-stu-id="81277-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="81277-104">Criar um aplicativo do Google+</span><span class="sxs-lookup"><span data-stu-id="81277-104">Create a Google+ application</span></span>
<span data-ttu-id="81277-105">Para usar o Google+ como um provedor de identidade no Azure AD (Azure Active Directory B2C), você precisará criar um aplicativo do Google+ e fornecer a ele os parâmetros certos.</span><span class="sxs-lookup"><span data-stu-id="81277-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="81277-106">Para fazer isso, é necessário ter uma conta do Google+.</span><span class="sxs-lookup"><span data-stu-id="81277-106">You need a Google+ account to do this.</span></span> <span data-ttu-id="81277-107">Se não tiver uma, você poderá obtê-la em [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="81277-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="81277-108">Acesse o [Console de Desenvolvedores do Google](https://console.developers.google.com/) e entre com suas credenciais de conta do Google+.</span><span class="sxs-lookup"><span data-stu-id="81277-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="81277-109">Clique em **Criar projeto**, insira um **Nome de projeto** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="81277-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+ – Introdução](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ – Novo projeto](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="81277-112">Clique em **Gerenciador de API** e em **Credenciais** no painel de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="81277-112">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
4. <span data-ttu-id="81277-113">Clique na guia **OAuth consent screen (Tela de consentimento do OAuth)** na parte superior.</span><span class="sxs-lookup"><span data-stu-id="81277-113">Click the **OAuth consent screen** tab at the top.</span></span>
   
    ![Google+ – Credenciais](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="81277-115">Selecione ou especifique um **Endereço de email** válido, forneça um **Nome de produto** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="81277-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+ – Tela de consentimento do OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="81277-117">Clique em **Novas credenciais** e escolha **ID do cliente OAuth**.</span><span class="sxs-lookup"><span data-stu-id="81277-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+ – Tela de consentimento do OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="81277-119">Em **Tipo de aplicativo**, selecione **Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="81277-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+ – Tela de consentimento do OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="81277-121">Forneça um **Nome** para seu aplicativo, insira `https://login.microsoftonline.com` no campo **Origens de JavaScript autorizadas** e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` no campo **URIs de redirecionamento autorizados**.</span><span class="sxs-lookup"><span data-stu-id="81277-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="81277-122">Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="81277-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="81277-123">O valor **{tenant}** diferencia letras maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="81277-123">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="81277-124">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="81277-124">Click **Create**.</span></span>
   
    ![Google+ – Criar ID do cliente](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="81277-126">Copie os valores de **ID do cliente** e **Segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="81277-126">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="81277-127">Você precisará de ambos para configurar o Google+ como um provedor de identidade no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="81277-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="81277-128">**Segredo do cliente** é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="81277-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+ – Segredo do cliente](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="81277-130">Configurar o Google+ como um provedor de identidade no locatário</span><span class="sxs-lookup"><span data-stu-id="81277-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="81277-131">Siga estas etapas para [navegar até a folha de recursos do B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="81277-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="81277-132">Na folha de recursos do B2C, clique em **Provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="81277-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="81277-133">Clique em **+Adicionar** , na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="81277-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="81277-134">Forneça um **Nome** amigável para a configuração do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="81277-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="81277-135">Por exemplo, insira "G+".</span><span class="sxs-lookup"><span data-stu-id="81277-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="81277-136">Clique em **Tipo de provedor de identidade**, selecione **Google** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="81277-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="81277-137">Clique em **Configurar este provedor de identidade** e insira a ID do cliente e o segredo do cliente do aplicativo do Google+ criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="81277-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="81277-138">Clique em **OK** e em **Criar** para salvar a configuração do Google+.</span><span class="sxs-lookup"><span data-stu-id="81277-138">Click **OK** and then click **Create** to save your Google+ configuration.</span></span>

