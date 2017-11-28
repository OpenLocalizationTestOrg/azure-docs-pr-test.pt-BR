---
title: "Azure Active Directory B2C: configuração da conta da Microsoft | Microsoft Docs"
description: "Forneça inscrição e entrada aos consumidores com contas da Microsoft em seus aplicativos protegidos pelo Azure Active Directory B2C."
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
ms.openlocfilehash: 59879dc0b3fc1d7af3e2a1f67f1701f451de9126
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-microsoft-accounts"></a><span data-ttu-id="3c2a7-103">Azure Active Directory B2C: fornecer inscrição e entrada aos consumidores com contas da Microsoft</span><span class="sxs-lookup"><span data-stu-id="3c2a7-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="3c2a7-104">Criar um aplicativo de conta da Microsoft</span><span class="sxs-lookup"><span data-stu-id="3c2a7-104">Create a Microsoft account application</span></span>
<span data-ttu-id="3c2a7-105">Para usar a conta da Microsoft como um provedor de identidade no Azure AD (Azure Active Directory) B2C, você precisará criar um aplicativo de conta da Microsoft e fornecer a ele os parâmetros certos.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-105">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="3c2a7-106">Para fazer isso, é necessário ter uma conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-106">You need a Microsoft account to do this.</span></span> <span data-ttu-id="3c2a7-107">Se não tiver uma, você poderá obtê-la em [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="3c2a7-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="3c2a7-108">Vá para o [Portal de Registro de Aplicativos da Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e entre com suas credenciais da conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-108">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="3c2a7-109">Clique em **Adicionar um aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-109">Click **Add an app**.</span></span>
   
    ![Conta da Microsoft – Adicionar um novo aplicativo](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="3c2a7-111">Forneça um **Nome** para seu aplicativo e clique em **Criar aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Conta da Microsoft – Nome do aplicativo](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="3c2a7-113">Copie o valor de **ID do Aplicativo**. Você precisará dele para configurar a conta da Microsoft como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-113">Copy the value of **Application Id**. You will need it to configure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Conta da Microsoft - Id do Aplicativo](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="3c2a7-115">Clique em **Adicionar plataforma** e escolha **Web**.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Conta da Microsoft - Adicionar plataforma](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Conta da Microsoft - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="3c2a7-118">Insira `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` no campo **URLs de Redirecionamento** .</span><span class="sxs-lookup"><span data-stu-id="3c2a7-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="3c2a7-119">Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="3c2a7-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Conta da Microsoft – URL de redirecionamento](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="3c2a7-121">Clique em **Gerar Nova Senha** na seção **Segredos do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-121">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="3c2a7-122">Copie a nova senha exibida na tela.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-122">Copy the new password displayed on screen.</span></span> <span data-ttu-id="3c2a7-123">Você precisará dele para configurar a conta da Microsoft como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-123">You will need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="3c2a7-124">A senha é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-124">This password is an important security credential.</span></span>
   
    ![Conta da Microsoft - Gerar nova senha](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Conta da Microsoft - Nova senha](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="3c2a7-127">Marque a caixa que diz **suporte do SDK do Live** na seção **Opções Avançadas**.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-127">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="3c2a7-128">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-128">Click **Save**.</span></span>
   
    ![Conta da Microsoft - Suporte ao SDK do Live](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="3c2a7-130">Configurar a conta da Microsoft como um provedor de identidade no locatário</span><span class="sxs-lookup"><span data-stu-id="3c2a7-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="3c2a7-131">Siga estas etapas para [navegar até a folha de recursos do B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="3c2a7-132">Na folha de recursos do B2C, clique em **Provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="3c2a7-133">Clique em **+Adicionar** , na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="3c2a7-134">Forneça um **Nome** amigável para a configuração do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="3c2a7-135">Por exemplo, insira "MSA".</span><span class="sxs-lookup"><span data-stu-id="3c2a7-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="3c2a7-136">Clique em **Tipo do provedor de identidade**, selecione **Conta da Microsoft** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="3c2a7-137">Clique em **Configurar este provedor de identidade** e insira a ID do cliente e o segredo do cliente do aplicativo da conta da Microsoft criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-137">Click **Set up this identity provider** and enter the Application Id and password of the Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="3c2a7-138">Clique em **OK** e em **Criar** para salvar a configuração da conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3c2a7-138">Click **OK** and then click **Create** to save your Microsoft account configuration.</span></span>

