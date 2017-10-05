---
title: "Azure Active Directory B2C: configuração do QQ | Microsoft Docs"
description: "Forneça inscrição e entrada para consumidores com contas do QQ em seus aplicativos protegidos pelo Azure Active Directory B2C."
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
ms.openlocfilehash: b32e81494b8c84799485f154ae43ad30af394caa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-qq-accounts"></a><span data-ttu-id="80f95-103">Azure Active Directory B2C: fornecer inscrição e entrada para consumidores com contas do QQ</span><span class="sxs-lookup"><span data-stu-id="80f95-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="80f95-104">Esse recurso está em visualização.</span><span class="sxs-lookup"><span data-stu-id="80f95-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="80f95-105">Criar um aplicativo QQ</span><span class="sxs-lookup"><span data-stu-id="80f95-105">Create a QQ application</span></span>

<span data-ttu-id="80f95-106">Para usar o QQ como um provedor de identidade no Azure AD (Azure Active Directory B2C), você precisará criar um aplicativo do QQ e fornecer a ele os parâmetros certos.</span><span class="sxs-lookup"><span data-stu-id="80f95-106">To use QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a QQ application and supply it with the right parameters.</span></span> <span data-ttu-id="80f95-107">Para fazer isso, é necessário ter uma conta QQ.</span><span class="sxs-lookup"><span data-stu-id="80f95-107">You need a QQ account to do this.</span></span> <span data-ttu-id="80f95-108">Se você não tiver uma, poderá obtê-la em [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="80f95-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-the-qq-developer-program"></a><span data-ttu-id="80f95-109">Registrar-se no programa de desenvolvedores do QQ</span><span class="sxs-lookup"><span data-stu-id="80f95-109">Register for the QQ developer program</span></span>

1. <span data-ttu-id="80f95-110">Vá para o [portal do desenvolvedor do QQ](http://open.qq.com) e entre com suas credenciais de conta do QQ.</span><span class="sxs-lookup"><span data-stu-id="80f95-110">Go to the [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="80f95-111">Depois de entrar, vá para [http://open.qq.com/reg](http://open.qq.com/reg) para registrar-se como desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="80f95-111">After signing in, go to [http://open.qq.com/reg](http://open.qq.com/reg) to register yourself as a developer.</span></span>
3. <span data-ttu-id="80f95-112">No menu, selecione **个人** (desenvolvedor individual).</span><span class="sxs-lookup"><span data-stu-id="80f95-112">In the menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="80f95-113">Insira as informações necessárias no formulário e clique em **下一步** (próxima etapa).</span><span class="sxs-lookup"><span data-stu-id="80f95-113">Enter the required information into the form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="80f95-114">Conclua o processo de verificação de email.</span><span class="sxs-lookup"><span data-stu-id="80f95-114">Complete the email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="80f95-115">Você precisará aguardar alguns dias para ser aprovado depois de registrar-se como desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="80f95-115">You will need to wait a few days to be approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="80f95-116">Registrar um aplicativo do QQ</span><span class="sxs-lookup"><span data-stu-id="80f95-116">Register a QQ application</span></span>

1. <span data-ttu-id="80f95-117">Vá para [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="80f95-117">Go to [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="80f95-118">Clique em **应用管理** (gerenciamento de aplicativo).</span><span class="sxs-lookup"><span data-stu-id="80f95-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="80f95-119">Clique em **创建应用** (criar aplicativo).</span><span class="sxs-lookup"><span data-stu-id="80f95-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="80f95-120">Insira as informações do aplicativo necessárias.</span><span class="sxs-lookup"><span data-stu-id="80f95-120">Enter the necessary app information.</span></span>
5. <span data-ttu-id="80f95-121">Clique em **创建应用** (criar aplicativo).</span><span class="sxs-lookup"><span data-stu-id="80f95-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="80f95-122">Insira as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="80f95-122">Enter the required information.</span></span>
7. <span data-ttu-id="80f95-123">Para o campo **授权回调域** (URL de retorno de chamada), digite `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="80f95-123">For the **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="80f95-124">Por exemplo, se sua `tenant_name` é contoso.onmicrosoft.com, defina a URL como `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="80f95-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="80f95-125">Clique em **创建应用** (criar aplicativo).</span><span class="sxs-lookup"><span data-stu-id="80f95-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="80f95-126">Na página de confirmação, clique em **应用管理** (gerenciamento de aplicativo) para retornar à página de gerenciamento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80f95-126">On the confirmation page, click on **应用管理** (app management) to return to the app management page.</span></span>
10. <span data-ttu-id="80f95-127">Clique em **查看** (exibir) ao lado do aplicativo que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="80f95-127">Click on **查看** (view) next to the app you just created.</span></span>
11. <span data-ttu-id="80f95-128">Clique em **修改** (editar).</span><span class="sxs-lookup"><span data-stu-id="80f95-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="80f95-129">Na parte superior da página, copie a **ID DO APLICATIVO** e a **CHAVE DO APLICATIVO**.</span><span class="sxs-lookup"><span data-stu-id="80f95-129">From the top of the page, copy the **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="80f95-130">Configurar a QQ como um provedor de identidade em seu locatário</span><span class="sxs-lookup"><span data-stu-id="80f95-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="80f95-131">Siga estas etapas para [navegar até a folha de recursos do B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="80f95-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="80f95-132">Na folha de recursos do B2C, clique em **Provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="80f95-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="80f95-133">Clique em **+Adicionar** , na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="80f95-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="80f95-134">Forneça um **Nome** amigável para a configuração do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="80f95-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="80f95-135">Por exemplo, insira "QQ".</span><span class="sxs-lookup"><span data-stu-id="80f95-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="80f95-136">Clique em **Tipo de provedor de identidade**, selecione **QQ** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="80f95-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="80f95-137">Clique em **Configurar este provedor de identidade**</span><span class="sxs-lookup"><span data-stu-id="80f95-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="80f95-138">Insira a **Chave do Aplicativo** que você copiou anteriormente como a **ID do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="80f95-138">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="80f95-139">Insira o **Segredo do Aplicativo** que você copiou anteriormente como o **Segredo do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="80f95-139">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="80f95-140">Clique em **OK** e em **Criar** para salvar sua configuração do QQ.</span><span class="sxs-lookup"><span data-stu-id="80f95-140">Click **OK** and then click **Create** to save your QQ configuration.</span></span>

