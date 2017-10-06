---
title: "Azure Active Directory B2C: configuração do QQ | Microsoft Docs"
description: "Fornece tooconsumers Inscreva-se e entrar com contas TQ em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a><span data-ttu-id="d9649-103">B2C de diretório ativo do Azure: Fornecer tooconsumers se inscrever e fazer logon com contas de TQ</span><span class="sxs-lookup"><span data-stu-id="d9649-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="d9649-104">Esse recurso está em visualização.</span><span class="sxs-lookup"><span data-stu-id="d9649-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="d9649-105">Criar um aplicativo QQ</span><span class="sxs-lookup"><span data-stu-id="d9649-105">Create a QQ application</span></span>

<span data-ttu-id="d9649-106">toouse TQ como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo TQ e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="d9649-106">toouse QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a QQ application and supply it with hello right parameters.</span></span> <span data-ttu-id="d9649-107">É necessário um toodo de conta TQ isso.</span><span class="sxs-lookup"><span data-stu-id="d9649-107">You need a QQ account toodo this.</span></span> <span data-ttu-id="d9649-108">Se você não tiver uma, poderá obtê-la em [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="d9649-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-hello-qq-developer-program"></a><span data-ttu-id="d9649-109">Registre-se para o programa para desenvolvedores TQ Olá</span><span class="sxs-lookup"><span data-stu-id="d9649-109">Register for hello QQ developer program</span></span>

1. <span data-ttu-id="d9649-110">Vá toohello [portal do desenvolvedor TQ](http://open.qq.com) e entre com suas credenciais de conta TQ.</span><span class="sxs-lookup"><span data-stu-id="d9649-110">Go toohello [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="d9649-111">Depois de entrar, vá muito[http://open.qq.com/reg](http://open.qq.com/reg) tooregister como um desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="d9649-111">After signing in, go too[http://open.qq.com/reg](http://open.qq.com/reg) tooregister yourself as a developer.</span></span>
3. <span data-ttu-id="d9649-112">No menu de saudação, selecione**个人**(desenvolvedor individuais).</span><span class="sxs-lookup"><span data-stu-id="d9649-112">In hello menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="d9649-113">Inserir informações de Olá necessárias no formulário de saudação e clique em**下一步**(próxima etapa).</span><span class="sxs-lookup"><span data-stu-id="d9649-113">Enter hello required information into hello form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="d9649-114">Concluir o processo de verificação de email de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9649-114">Complete hello email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="d9649-115">Você precisará toowait alguns toobe dias após registrar como um desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="d9649-115">You will need toowait a few days toobe approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="d9649-116">Registrar um aplicativo do QQ</span><span class="sxs-lookup"><span data-stu-id="d9649-116">Register a QQ application</span></span>

1. <span data-ttu-id="d9649-117">Vá muito[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="d9649-117">Go too[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="d9649-118">Clique em **应用管理** (gerenciamento de aplicativo).</span><span class="sxs-lookup"><span data-stu-id="d9649-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="d9649-119">Clique em **创建应用** (criar aplicativo).</span><span class="sxs-lookup"><span data-stu-id="d9649-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="d9649-120">Insira as informações de aplicativo necessário hello.</span><span class="sxs-lookup"><span data-stu-id="d9649-120">Enter hello necessary app information.</span></span>
5. <span data-ttu-id="d9649-121">Clique em **创建应用** (criar aplicativo).</span><span class="sxs-lookup"><span data-stu-id="d9649-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="d9649-122">Insira as informações de saudação necessária.</span><span class="sxs-lookup"><span data-stu-id="d9649-122">Enter hello required information.</span></span>
7. <span data-ttu-id="d9649-123">Para Olá**授权回调域**(URL de retorno de chamada), digite `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="d9649-123">For hello **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="d9649-124">Por exemplo, se seu `tenant_name` é contoso.onmicrosoft.com, conjunto Olá URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="d9649-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="d9649-125">Clique em **创建应用** (criar aplicativo).</span><span class="sxs-lookup"><span data-stu-id="d9649-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="d9649-126">Na página de confirmação de saudação, clique em**应用管理**página de gerenciamento (gerenciamento de aplicativo) tooreturn toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9649-126">On hello confirmation page, click on **应用管理** (app management) tooreturn toohello app management page.</span></span>
10. <span data-ttu-id="d9649-127">Clique em**查看**(exibição) próximo toohello aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="d9649-127">Click on **查看** (view) next toohello app you just created.</span></span>
11. <span data-ttu-id="d9649-128">Clique em **修改** (editar).</span><span class="sxs-lookup"><span data-stu-id="d9649-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="d9649-129">Da parte superior de saudação da página hello, copie Olá **ID do aplicativo** e **chave do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="d9649-129">From hello top of hello page, copy hello **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="d9649-130">Configurar a QQ como um provedor de identidade em seu locatário</span><span class="sxs-lookup"><span data-stu-id="d9649-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="d9649-131">Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9649-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="d9649-132">Na folha de recursos Olá B2C, clique em **provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="d9649-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="d9649-133">Clique em **+ adicionar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9649-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="d9649-134">Forneça um amigável **nome** para configuração do provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="d9649-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="d9649-135">Por exemplo, insira "QQ".</span><span class="sxs-lookup"><span data-stu-id="d9649-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="d9649-136">Clique em **Tipo de provedor de identidade**, selecione **QQ** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d9649-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="d9649-137">Clique em **Configurar este provedor de identidade**</span><span class="sxs-lookup"><span data-stu-id="d9649-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="d9649-138">Digite hello **chave do aplicativo** que você copiou anteriormente como Olá **ID do cliente**.</span><span class="sxs-lookup"><span data-stu-id="d9649-138">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="d9649-139">Digite hello **segredo do aplicativo** que você copiou anteriormente como Olá **segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="d9649-139">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="d9649-140">Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração TQ.</span><span class="sxs-lookup"><span data-stu-id="d9649-140">Click **OK** and then click **Create** toosave your QQ configuration.</span></span>

