---
title: "Azure Active Directory B2C: configuração do Weibo | Microsoft Docs"
description: "Forneça inscrição e conexão para consumidores com contas do Weibo em seus aplicativos protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 00c5d3781455c80b33bdbb4c872ae354531baf3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-weibo-accounts"></a><span data-ttu-id="73f48-103">Azure Active Directory B2C: fornecer inscrição e conexão para consumidores com contas do Weibo</span><span class="sxs-lookup"><span data-stu-id="73f48-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="73f48-104">Esse recurso está em visualização.</span><span class="sxs-lookup"><span data-stu-id="73f48-104">This feature is in preview.</span></span> <span data-ttu-id="73f48-105">Não use esse provedor de identidade no ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="73f48-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="73f48-106">Criar um aplicativo Weibo</span><span class="sxs-lookup"><span data-stu-id="73f48-106">Create a Weibo application</span></span>

<span data-ttu-id="73f48-107">Para usar o Weibo como um provedor de identidade no Azure AD (Active Directory) B2C, você precisa criar um aplicativo Weibo e fornecer a ele os parâmetros certos.</span><span class="sxs-lookup"><span data-stu-id="73f48-107">To use Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Weibo application and supply it with the right parameters.</span></span> <span data-ttu-id="73f48-108">Para fazer isso, é necessário ter uma conta Weibo.</span><span class="sxs-lookup"><span data-stu-id="73f48-108">You need a Weibo account to do this.</span></span> <span data-ttu-id="73f48-109">Caso não tenha, você pode obter uma em [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="73f48-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-the-weibo-developer-program"></a><span data-ttu-id="73f48-110">Registrar-se no programa de desenvolvedores do Weibo</span><span class="sxs-lookup"><span data-stu-id="73f48-110">Register for the Weibo developer program</span></span>

1. <span data-ttu-id="73f48-111">Vá para o [portal do desenvolvedor do Weibo](http://open.weibo.com/) e entre com suas credenciais de conta do Weibo.</span><span class="sxs-lookup"><span data-stu-id="73f48-111">Go to the [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="73f48-112">Depois de entrar, clique no seu nome de exibição no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="73f48-112">After signing in, click on your display name in the top-right corner.</span></span>
3. <span data-ttu-id="73f48-113">No menu suspenso, selecione **编辑开发者信息** (editar informações do desenvolvedor).</span><span class="sxs-lookup"><span data-stu-id="73f48-113">In the dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="73f48-114">Insira as informações necessárias no formulário e clique em **提交** (enviar).</span><span class="sxs-lookup"><span data-stu-id="73f48-114">Enter the required information into the form and click **提交** (submit).</span></span>
5. <span data-ttu-id="73f48-115">Conclua o processo de verificação de email.</span><span class="sxs-lookup"><span data-stu-id="73f48-115">Complete the email verification process.</span></span>
6. <span data-ttu-id="73f48-116">Acesse a [página de verificação de identidade](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="73f48-116">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="73f48-117">Insira as informações necessárias no formulário e clique em **提交** (enviar).</span><span class="sxs-lookup"><span data-stu-id="73f48-117">Enter the required information into the form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="73f48-118">Registrar um aplicativo Weibo</span><span class="sxs-lookup"><span data-stu-id="73f48-118">Register a Weibo application</span></span>

1. <span data-ttu-id="73f48-119">Acesse a [nova página de registro de aplicativo Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="73f48-119">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="73f48-120">Insira as informações necessárias de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="73f48-120">Enter the necessary application information.</span></span>
3. <span data-ttu-id="73f48-121">Clique em **创建** (criar).</span><span class="sxs-lookup"><span data-stu-id="73f48-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="73f48-122">Copie os valores de **Chave do Aplicativo** e **Segredo do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="73f48-122">Copy the values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="73f48-123">Você precisará dessas informações posteriormente.</span><span class="sxs-lookup"><span data-stu-id="73f48-123">You will need this later.</span></span>
5. <span data-ttu-id="73f48-124">Carregue as fotos necessárias e insira as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="73f48-124">Upload the required photos and enter the necessary information.</span></span>
6. <span data-ttu-id="73f48-125">Clique em **保存以上信息** (salvar).</span><span class="sxs-lookup"><span data-stu-id="73f48-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="73f48-126">Clique em **高级信息** (informações avançadas).</span><span class="sxs-lookup"><span data-stu-id="73f48-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="73f48-127">Clique em **编辑** (editar) ao lado do campo para **授权设置** (URL de redirecionamento) do OAuth2.0.</span><span class="sxs-lookup"><span data-stu-id="73f48-127">Click **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="73f48-128">Insira `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` para **授权设置** (URL de redirecionamento) do OAuth2.0.</span><span class="sxs-lookup"><span data-stu-id="73f48-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="73f48-129">Por exemplo, se seu `tenant_name` for contoso.onmicrosoft.com, defina a URL para ser `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="73f48-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="73f48-130">Clique em **提交** (enviar).</span><span class="sxs-lookup"><span data-stu-id="73f48-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="73f48-131">Configurar o Weibo como um provedor de identidade em seu locatário</span><span class="sxs-lookup"><span data-stu-id="73f48-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="73f48-132">Siga estas etapas para [navegar até a folha de recursos do B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="73f48-132">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="73f48-133">Na folha de recursos do B2C, clique em **Provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="73f48-133">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="73f48-134">Clique em **+Adicionar** , na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="73f48-134">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="73f48-135">Forneça um **Nome** amigável para a configuração do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="73f48-135">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="73f48-136">Por exemplo, insira "Weibo".</span><span class="sxs-lookup"><span data-stu-id="73f48-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="73f48-137">Clique em **Tipo de provedor de identidade**, selecione **Weibo** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="73f48-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="73f48-138">Clique em **Configurar este provedor de identidade**</span><span class="sxs-lookup"><span data-stu-id="73f48-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="73f48-139">Insira a **Chave do Aplicativo** que você copiou anteriormente como a **ID do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="73f48-139">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="73f48-140">Insira o **Segredo do Aplicativo** que você copiou anteriormente como o **Segredo do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="73f48-140">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="73f48-141">Clique em **OK** e em **Criar** para salvar sua configuração Weibo.</span><span class="sxs-lookup"><span data-stu-id="73f48-141">Click **OK** and then click **Create** to save your Weibo configuration.</span></span>

