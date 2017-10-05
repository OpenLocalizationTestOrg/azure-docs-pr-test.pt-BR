---
title: "Azure Active Directory B2C: configuração da Amazon | Microsoft Docs"
description: "Forneça inscrição e entrada para consumidores com contas da Amazon em seus aplicativos protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: dcc97e1b7f6287bd7692c52bf068950065a26572
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-amazon-accounts"></a><span data-ttu-id="12891-103">Azure Active Directory B2C: fornecer inscrição e entrada para consumidores com contas da Amazon</span><span class="sxs-lookup"><span data-stu-id="12891-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="12891-104">Criar um aplicativo da Amazon</span><span class="sxs-lookup"><span data-stu-id="12891-104">Create an Amazon application</span></span>
<span data-ttu-id="12891-105">Para usar a Amazon como um provedor de identidade no Azure AD (Azure Active Directory) B2C, é necessário primeiro criar um aplicativo da Amazon e fornecê-lo com os parâmetros corretos.</span><span class="sxs-lookup"><span data-stu-id="12891-105">To use Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an Amazon application and supply it with the right parameters.</span></span> <span data-ttu-id="12891-106">Você precisa de uma conta do Amazon para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="12891-106">You need an Amazon account to do this.</span></span> <span data-ttu-id="12891-107">Se você não tiver uma, poderá obtê-la em [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="12891-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="12891-108">Acesse o [Centro de Desenvolvedores da Amazon](https://login.amazon.com/) e entre com suas credenciais de conta da Amazon.</span><span class="sxs-lookup"><span data-stu-id="12891-108">Go to the [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="12891-109">Se você ainda não tiver feito isso, clique em **Inscrever-se**, siga as etapas de registro do desenvolvedor e aceite a política.</span><span class="sxs-lookup"><span data-stu-id="12891-109">If you have not already done so, click **Sign Up**, follow the developer registration steps, and accept the policy.</span></span>
3. <span data-ttu-id="12891-110">Clique em **Registrar novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="12891-110">Click **Register new application**.</span></span>
   
    ![Registrando um novo aplicativo no site da Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="12891-112">Forneça as informações do aplicativo (**Nome**, **Descrição** e **URL do Aviso de Privacidade**) e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="12891-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Fornecendo informações de aplicativo para registrar um novo aplicativo na Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="12891-114">Na seção **Configurações da Web**, copie os valores de **ID do cliente** e **Segredo do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="12891-114">In the **Web Settings** section, copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="12891-115">(Você precisa clicar no botão **Mostrar Segredo** para exibi-lo.) Você precisará de ambos para configurar a Amazon como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="12891-115">(You need to click the **Show Secret** button to see this.) You need both of them to configure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="12891-116">Clique em **Editar** na parte inferior da seção.</span><span class="sxs-lookup"><span data-stu-id="12891-116">Click **Edit** at the bottom of the section.</span></span> <span data-ttu-id="12891-117">**Segredo do Cliente** é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="12891-117">**Client Secret** is an important security credential.</span></span>
   
    ![Fornecendo a ID e o Segredo do Cliente para seu novo aplicativo na Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="12891-119">Insira `https://login.microsoftonline.com` no campo **JavaScript Origins Permitido** e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` no campo **URLs de Retorno Permitidas**.</span><span class="sxs-lookup"><span data-stu-id="12891-119">Enter `https://login.microsoftonline.com` in the **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Allowed Return URLs** field.</span></span> <span data-ttu-id="12891-120">Substitua **{tenant}** pelo nome do locatário (por exemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="12891-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="12891-121">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="12891-121">Click **Save**.</span></span> <span data-ttu-id="12891-122">O valor **{tenant}** diferencia letras maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="12891-122">The **{tenant}** value is case-sensitive.</span></span>
   
    ![Fornecendo JavaScript Origins e URLs de Retorno para o novo aplicativo na Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="12891-124">Configurar a Amazon como um provedor de identidade em seu locatário</span><span class="sxs-lookup"><span data-stu-id="12891-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="12891-125">Siga estas etapas para [navegar até a folha de recursos do B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="12891-125">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="12891-126">Na folha de recursos do B2C, clique em **Provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="12891-126">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="12891-127">Clique em **+Adicionar** , na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="12891-127">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="12891-128">Forneça um **Nome** amigável para a configuração do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="12891-128">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="12891-129">Por exemplo, insira “Amzn”.</span><span class="sxs-lookup"><span data-stu-id="12891-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="12891-130">Clique em **Tipo de provedor de identidade**, selecione **Amazon** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="12891-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="12891-131">Clique em **Configurar esse provedor de identidade** e insira a ID e o segredo do cliente do aplicativo Amazon que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="12891-131">Click **Set up this identity provider** and enter the client ID and client secret of the Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="12891-132">Clique em **OK** e em **Criar** para salvar sua configuração da Amazon.</span><span class="sxs-lookup"><span data-stu-id="12891-132">Click **OK** and then click **Create** to save your Amazon configuration.</span></span>

