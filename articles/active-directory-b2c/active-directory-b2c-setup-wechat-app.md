---
title: "Azure Active Directory B2C: configuração WeChat | Microsoft Docs"
description: "Forneça inscrição e conexão para consumidores com contas do WeChat em seus aplicativos protegidos pelo Azure Active Directory B2C."
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
ms.openlocfilehash: a54aec23d951610118246e9f70cdd27752ef39a6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-wechat-accounts"></a><span data-ttu-id="a1401-103">Azure Active Directory B2C: fornecer inscrição e conexão para consumidores com contas do WeChat</span><span class="sxs-lookup"><span data-stu-id="a1401-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="a1401-104">Esse recurso está em visualização.</span><span class="sxs-lookup"><span data-stu-id="a1401-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="a1401-105">Criar um aplicativo WeChat</span><span class="sxs-lookup"><span data-stu-id="a1401-105">Create a WeChat application</span></span>

<span data-ttu-id="a1401-106">Para usar o WeChat como um provedor de identidade no Azure AD (Active Directory) B2C, você precisa criar um aplicativo WeChat e fornecer a ele os parâmetros certos.</span><span class="sxs-lookup"><span data-stu-id="a1401-106">To use WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a WeChat application and supply it with the right parameters.</span></span> <span data-ttu-id="a1401-107">Para fazer isso, é necessário ter uma conta WeChat.</span><span class="sxs-lookup"><span data-stu-id="a1401-107">You need a WeChat account to do this.</span></span> <span data-ttu-id="a1401-108">Caso não tenha, você pode obter uma inscrevendo-se em um dos aplicativos móveis ou usando o número do seu QQ.</span><span class="sxs-lookup"><span data-stu-id="a1401-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="a1401-109">Depois disso, registre sua conta no programa de desenvolvedores do WeChat.</span><span class="sxs-lookup"><span data-stu-id="a1401-109">After that, get your account registered with the WeChat developer program.</span></span> <span data-ttu-id="a1401-110">Você pode encontrar mais informações [aqui](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span><span class="sxs-lookup"><span data-stu-id="a1401-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="a1401-111">Registrar um aplicativo WeChat</span><span class="sxs-lookup"><span data-stu-id="a1401-111">Register a WeChat application</span></span>

1. <span data-ttu-id="a1401-112">Acesse [https://open.weixin.qq.com/](https://open.weixin.qq.com/) e faça logon.</span><span class="sxs-lookup"><span data-stu-id="a1401-112">Go to [https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="a1401-113">Clique em **管理中心** (centro de gerenciamento).</span><span class="sxs-lookup"><span data-stu-id="a1401-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="a1401-114">Siga as etapas necessárias para registrar um novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a1401-114">Follow the necessary steps to register a new application.</span></span>
4. <span data-ttu-id="a1401-115">Para **授权回调域** (URL de retorno de chamada), digite `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="a1401-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="a1401-116">Por exemplo, se seu `tenant_name` for contoso.onmicrosoft.com, defina a URL para ser `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="a1401-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="a1401-117">Localize e copie a **ID DO APLICATIVO** e a **CHAVE DO APLICATIVO**.</span><span class="sxs-lookup"><span data-stu-id="a1401-117">Find and copy the **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="a1401-118">Você precisará delas mais tarde.</span><span class="sxs-lookup"><span data-stu-id="a1401-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="a1401-119">Configurar o WeChat como um provedor de identidade em seu locatário</span><span class="sxs-lookup"><span data-stu-id="a1401-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="a1401-120">Siga estas etapas para [navegar até a folha de recursos do B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1401-120">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="a1401-121">Na folha de recursos do B2C, clique em **Provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="a1401-121">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="a1401-122">Clique em **+Adicionar** , na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="a1401-122">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="a1401-123">Forneça um **Nome** amigável para a configuração do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="a1401-123">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="a1401-124">Por exemplo, insira "WeChat".</span><span class="sxs-lookup"><span data-stu-id="a1401-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="a1401-125">Clique em **Tipo de provedor de identidade**, selecione **WeChat** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1401-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="a1401-126">Clique em **Configurar este provedor de identidade**</span><span class="sxs-lookup"><span data-stu-id="a1401-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="a1401-127">Insira a **Chave do Aplicativo** que você copiou anteriormente como a **ID do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="a1401-127">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="a1401-128">Insira o **Segredo do Aplicativo** que você copiou anteriormente como o **Segredo do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="a1401-128">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="a1401-129">Clique em **OK** e em **Criar** para salvar sua configuração WeChat.</span><span class="sxs-lookup"><span data-stu-id="a1401-129">Click **OK** and then click **Create** to save your WeChat configuration.</span></span>

