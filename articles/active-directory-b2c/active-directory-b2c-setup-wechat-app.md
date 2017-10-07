---
title: "Azure Active Directory B2C: configuração WeChat | Microsoft Docs"
description: "Fornece tooconsumers Inscreva-se e entrar com contas WeChat em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a><span data-ttu-id="b12bc-103">B2C de diretório ativo do Azure: Fornecer tooconsumers Inscreva-se e entrar com contas de WeChat</span><span class="sxs-lookup"><span data-stu-id="b12bc-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="b12bc-104">Esse recurso está em visualização.</span><span class="sxs-lookup"><span data-stu-id="b12bc-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="b12bc-105">Criar um aplicativo WeChat</span><span class="sxs-lookup"><span data-stu-id="b12bc-105">Create a WeChat application</span></span>

<span data-ttu-id="b12bc-106">toouse WeChat como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo WeChat e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="b12bc-106">toouse WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a WeChat application and supply it with hello right parameters.</span></span> <span data-ttu-id="b12bc-107">É necessário um toodo de conta WeChat isso.</span><span class="sxs-lookup"><span data-stu-id="b12bc-107">You need a WeChat account toodo this.</span></span> <span data-ttu-id="b12bc-108">Caso não tenha, você pode obter uma inscrevendo-se em um dos aplicativos móveis ou usando o número do seu QQ.</span><span class="sxs-lookup"><span data-stu-id="b12bc-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="b12bc-109">Depois disso, obter sua conta registrada com o programa para desenvolvedores WeChat hello.</span><span class="sxs-lookup"><span data-stu-id="b12bc-109">After that, get your account registered with hello WeChat developer program.</span></span> <span data-ttu-id="b12bc-110">Você pode encontrar mais informações [aqui](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span><span class="sxs-lookup"><span data-stu-id="b12bc-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="b12bc-111">Registrar um aplicativo WeChat</span><span class="sxs-lookup"><span data-stu-id="b12bc-111">Register a WeChat application</span></span>

1. <span data-ttu-id="b12bc-112">Vá muito[https://open.weixin.qq.com/](https://open.weixin.qq.com/) e faça logon.</span><span class="sxs-lookup"><span data-stu-id="b12bc-112">Go too[https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="b12bc-113">Clique em **管理中心** (centro de gerenciamento).</span><span class="sxs-lookup"><span data-stu-id="b12bc-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="b12bc-114">Siga as etapas necessárias de saudação tooregister um novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b12bc-114">Follow hello necessary steps tooregister a new application.</span></span>
4. <span data-ttu-id="b12bc-115">Para **授权回调域** (URL de retorno de chamada), digite `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="b12bc-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="b12bc-116">Por exemplo, se seu `tenant_name` é contoso.onmicrosoft.com, conjunto Olá URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="b12bc-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="b12bc-117">Localizar e copiar Olá **ID do aplicativo** e **chave do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="b12bc-117">Find and copy hello **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="b12bc-118">Você precisará delas mais tarde.</span><span class="sxs-lookup"><span data-stu-id="b12bc-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="b12bc-119">Configurar o WeChat como um provedor de identidade em seu locatário</span><span class="sxs-lookup"><span data-stu-id="b12bc-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="b12bc-120">Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12bc-120">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="b12bc-121">Na folha de recursos Olá B2C, clique em **provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="b12bc-121">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="b12bc-122">Clique em **+ adicionar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="b12bc-122">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="b12bc-123">Forneça um amigável **nome** para configuração do provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="b12bc-123">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="b12bc-124">Por exemplo, insira "WeChat".</span><span class="sxs-lookup"><span data-stu-id="b12bc-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="b12bc-125">Clique em **Tipo de provedor de identidade**, selecione **WeChat** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b12bc-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="b12bc-126">Clique em **Configurar este provedor de identidade**</span><span class="sxs-lookup"><span data-stu-id="b12bc-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="b12bc-127">Digite hello **chave do aplicativo** que você copiou anteriormente como Olá **ID do cliente**.</span><span class="sxs-lookup"><span data-stu-id="b12bc-127">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="b12bc-128">Digite hello **segredo do aplicativo** que você copiou anteriormente como Olá **segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="b12bc-128">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="b12bc-129">Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração WeChat.</span><span class="sxs-lookup"><span data-stu-id="b12bc-129">Click **OK** and then click **Create** toosave your WeChat configuration.</span></span>

