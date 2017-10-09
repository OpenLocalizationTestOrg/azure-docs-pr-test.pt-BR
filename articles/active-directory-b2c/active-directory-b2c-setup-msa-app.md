---
title: "Azure Active Directory B2C: configuração da conta da Microsoft | Microsoft Docs"
description: "Fornece tooconsumers Inscreva-se e entrar com contas da Microsoft em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a><span data-ttu-id="4cd4d-103">B2C de diretório ativo do Azure: Fornecer tooconsumers Inscreva-se e entrar com contas da Microsoft</span><span class="sxs-lookup"><span data-stu-id="4cd4d-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="4cd4d-104">Criar um aplicativo de conta da Microsoft</span><span class="sxs-lookup"><span data-stu-id="4cd4d-104">Create a Microsoft account application</span></span>
<span data-ttu-id="4cd4d-105">toouse Microsoft conta como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo de conta da Microsoft e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-105">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="4cd4d-106">É necessário um toodo de conta Microsoft isso.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-106">You need a Microsoft account toodo this.</span></span> <span data-ttu-id="4cd4d-107">Se não tiver uma, você poderá obtê-la em [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="4cd4d-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="4cd4d-108">Vá toohello [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e entre com suas credenciais de conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-108">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="4cd4d-109">Clique em **Adicionar um aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-109">Click **Add an app**.</span></span>
   
    ![Conta da Microsoft – Adicionar um novo aplicativo](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="4cd4d-111">Forneça um **Nome** para seu aplicativo e clique em **Criar aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Conta da Microsoft – Nome do aplicativo](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="4cd4d-113">Copie o valor de saudação do **Id do aplicativo**. Você precisará dele tooconfigure conta da Microsoft como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-113">Copy hello value of **Application Id**. You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Conta da Microsoft - Id do Aplicativo](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="4cd4d-115">Clique em **Adicionar plataforma** e escolha **Web**.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Conta da Microsoft - Adicionar plataforma](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Conta da Microsoft - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="4cd4d-118">Digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **URIs de redirecionamento** campo.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="4cd4d-119">Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4cd4d-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Conta da Microsoft – URL de redirecionamento](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="4cd4d-121">Clique em **gerar nova senha** em Olá **segredos do aplicativo** seção.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-121">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="4cd4d-122">Cópia Olá nova senha exibida na tela.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-122">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="4cd4d-123">Você precisará dele tooconfigure conta da Microsoft como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-123">You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="4cd4d-124">A senha é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-124">This password is an important security credential.</span></span>
   
    ![Conta da Microsoft - Gerar nova senha](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Conta da Microsoft - Nova senha](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="4cd4d-127">Caixa de saudação de seleção que diz **suporte do SDK do Live** em Olá **opções avançadas de** seção.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-127">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="4cd4d-128">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-128">Click **Save**.</span></span>
   
    ![Conta da Microsoft - Suporte ao SDK do Live](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="4cd4d-130">Configurar a conta da Microsoft como um provedor de identidade no locatário</span><span class="sxs-lookup"><span data-stu-id="4cd4d-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="4cd4d-131">Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="4cd4d-132">Na folha de recursos Olá B2C, clique em **provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="4cd4d-133">Clique em **+ adicionar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="4cd4d-134">Forneça um amigável **nome** para configuração do provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="4cd4d-135">Por exemplo, insira "MSA".</span><span class="sxs-lookup"><span data-stu-id="4cd4d-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="4cd4d-136">Clique em **Tipo do provedor de identidade**, selecione **Conta da Microsoft** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="4cd4d-137">Clique em **configurar esse provedor de identidade** e digite Olá Id do aplicativo e a senha da saudação aplicativo de conta da Microsoft que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-137">Click **Set up this identity provider** and enter hello Application Id and password of hello Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="4cd4d-138">Clique em **Okey** e, em seguida, clique em **criar** toosave configuração de conta do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4cd4d-138">Click **OK** and then click **Create** toosave your Microsoft account configuration.</span></span>

