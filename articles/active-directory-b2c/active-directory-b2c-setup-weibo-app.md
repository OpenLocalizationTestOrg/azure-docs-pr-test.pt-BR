---
title: "Azure Active Directory B2C: configuração do Weibo | Microsoft Docs"
description: "Fornece tooconsumers Inscreva-se e entrar com contas Weibo em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
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
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a><span data-ttu-id="faed4-103">B2C de diretório ativo do Azure: Fornecer tooconsumers Inscreva-se e entrar com contas de Weibo</span><span class="sxs-lookup"><span data-stu-id="faed4-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="faed4-104">Esse recurso está em visualização.</span><span class="sxs-lookup"><span data-stu-id="faed4-104">This feature is in preview.</span></span> <span data-ttu-id="faed4-105">Não use esse provedor de identidade no ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="faed4-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="faed4-106">Criar um aplicativo Weibo</span><span class="sxs-lookup"><span data-stu-id="faed4-106">Create a Weibo application</span></span>

<span data-ttu-id="faed4-107">toouse Weibo como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo Weibo e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="faed4-107">toouse Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Weibo application and supply it with hello right parameters.</span></span> <span data-ttu-id="faed4-108">É necessário um toodo de conta Weibo isso.</span><span class="sxs-lookup"><span data-stu-id="faed4-108">You need a Weibo account toodo this.</span></span> <span data-ttu-id="faed4-109">Caso não tenha, você pode obter uma em [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="faed4-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-hello-weibo-developer-program"></a><span data-ttu-id="faed4-110">Registre-se para o programa para desenvolvedores Weibo Olá</span><span class="sxs-lookup"><span data-stu-id="faed4-110">Register for hello Weibo developer program</span></span>

1. <span data-ttu-id="faed4-111">Vá toohello [portal do desenvolvedor Weibo](http://open.weibo.com/) e entre com suas credenciais de conta Weibo.</span><span class="sxs-lookup"><span data-stu-id="faed4-111">Go toohello [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="faed4-112">Depois de entrar, clique em seu nome de exibição no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="faed4-112">After signing in, click on your display name in hello top-right corner.</span></span>
3. <span data-ttu-id="faed4-113">No menu suspenso hello, selecione**编辑开发者信息**(Editar informações do desenvolvedor).</span><span class="sxs-lookup"><span data-stu-id="faed4-113">In hello dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="faed4-114">Inserir informações de Olá necessárias no formulário de saudação e clique em**提交**(envio).</span><span class="sxs-lookup"><span data-stu-id="faed4-114">Enter hello required information into hello form and click **提交** (submit).</span></span>
5. <span data-ttu-id="faed4-115">Concluir o processo de verificação de email de saudação.</span><span class="sxs-lookup"><span data-stu-id="faed4-115">Complete hello email verification process.</span></span>
6. <span data-ttu-id="faed4-116">Vá toohello [página de verificação de identidade](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="faed4-116">Go toohello [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="faed4-117">Inserir informações de Olá necessárias no formulário de saudação e clique em**提交**(envio).</span><span class="sxs-lookup"><span data-stu-id="faed4-117">Enter hello required information into hello form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="faed4-118">Registrar um aplicativo Weibo</span><span class="sxs-lookup"><span data-stu-id="faed4-118">Register a Weibo application</span></span>

1. <span data-ttu-id="faed4-119">Vá toohello [nova página de registro de aplicativo Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="faed4-119">Go toohello [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="faed4-120">Insira as informações de aplicativo necessário hello.</span><span class="sxs-lookup"><span data-stu-id="faed4-120">Enter hello necessary application information.</span></span>
3. <span data-ttu-id="faed4-121">Clique em **创建** (criar).</span><span class="sxs-lookup"><span data-stu-id="faed4-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="faed4-122">Copie os valores de saudação do **chave do aplicativo** e **segredo do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="faed4-122">Copy hello values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="faed4-123">Você precisará dessas informações posteriormente.</span><span class="sxs-lookup"><span data-stu-id="faed4-123">You will need this later.</span></span>
5. <span data-ttu-id="faed4-124">Carregar fotos Olá necessários e insira informações necessárias hello.</span><span class="sxs-lookup"><span data-stu-id="faed4-124">Upload hello required photos and enter hello necessary information.</span></span>
6. <span data-ttu-id="faed4-125">Clique em **保存以上信息** (salvar).</span><span class="sxs-lookup"><span data-stu-id="faed4-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="faed4-126">Clique em **高级信息** (informações avançadas).</span><span class="sxs-lookup"><span data-stu-id="faed4-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="faed4-127">Clique em**编辑**próximo campo de toohello (Editar) para OAuth 2.0**授权设置**(URL de redirecionamento).</span><span class="sxs-lookup"><span data-stu-id="faed4-127">Click **编辑** (edit) next toohello field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="faed4-128">Insira `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` para **授权设置** (URL de redirecionamento) do OAuth2.0.</span><span class="sxs-lookup"><span data-stu-id="faed4-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="faed4-129">Por exemplo, se seu `tenant_name` é contoso.onmicrosoft.com, conjunto Olá URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="faed4-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="faed4-130">Clique em **提交** (enviar).</span><span class="sxs-lookup"><span data-stu-id="faed4-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="faed4-131">Configurar o Weibo como um provedor de identidade em seu locatário</span><span class="sxs-lookup"><span data-stu-id="faed4-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="faed4-132">Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="faed4-132">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="faed4-133">Na folha de recursos Olá B2C, clique em **provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="faed4-133">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="faed4-134">Clique em **+ adicionar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="faed4-134">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="faed4-135">Forneça um amigável **nome** para configuração do provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="faed4-135">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="faed4-136">Por exemplo, insira "Weibo".</span><span class="sxs-lookup"><span data-stu-id="faed4-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="faed4-137">Clique em **Tipo de provedor de identidade**, selecione **Weibo** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="faed4-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="faed4-138">Clique em **Configurar este provedor de identidade**</span><span class="sxs-lookup"><span data-stu-id="faed4-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="faed4-139">Digite hello **chave do aplicativo** que você copiou anteriormente como Olá **ID do cliente**.</span><span class="sxs-lookup"><span data-stu-id="faed4-139">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="faed4-140">Digite hello **segredo do aplicativo** que você copiou anteriormente como Olá **segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="faed4-140">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="faed4-141">Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração Weibo.</span><span class="sxs-lookup"><span data-stu-id="faed4-141">Click **OK** and then click **Create** toosave your Weibo configuration.</span></span>

