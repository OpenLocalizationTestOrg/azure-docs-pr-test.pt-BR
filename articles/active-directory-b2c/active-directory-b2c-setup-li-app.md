---
title: "Azure Active Directory B2C: configuração do LinkedIn | Microsoft Docs"
description: "Forneça inscrição e entrada para consumidores com contas do LinkedIn em seus aplicativos protegidos pelo Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 1a6c4b19261aa34e668554ccad2b6340cddf9bf5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-linkedin-accounts"></a><span data-ttu-id="91694-103">Azure Active Directory B2C: fornecer inscrição e entrada aos consumidores com contas do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="91694-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="91694-104">Criar um aplicativo do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="91694-104">Create a LinkedIn application</span></span>
<span data-ttu-id="91694-105">Para usar o LinkedIn como provedor de identidade no Azure AD (Azure Active Directory) B2C, será necessário primeiro criar um aplicativo do LinkedIn  e fornecê-lo com os parâmetros corretos.</span><span class="sxs-lookup"><span data-stu-id="91694-105">To use LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a LinkedIn application and supply it with the right parameters.</span></span> <span data-ttu-id="91694-106">Você precisa de uma conta do LinkedIn para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="91694-106">You need a LinkedIn account to do this.</span></span> <span data-ttu-id="91694-107">Se você não tiver uma, poderá obtê-la em [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="91694-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="91694-108">Acesse o [site de Desenvolvedores do LinkedIn](https://www.developer.linkedin.com/) e entre com suas credencias de conta do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="91694-108">Go to the [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="91694-109">Clique em **Meus Aplicativos** na barra de menus superior e em **Criar Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="91694-109">Click **My Apps** in the top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn — Novo aplicativo](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="91694-111">No formulário **Criar um Novo Aplicativo**, preencha as informações relevantes (**nome da empresa**, **nome**, **descrição**, **URL do logotipo do aplicativo**, **uso do aplicativo**, **URL do site**, **email comercial** e **telefone comercial**).</span><span class="sxs-lookup"><span data-stu-id="91694-111">In the **Create a New Application** form, fill in the relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="91694-112">Aceite os **Termos de Uso da API do LinkedIn** e clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="91694-112">Agree to the **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn — Registrar aplicativo](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="91694-114">Copie os valores de **ID do cliente** e **Segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="91694-114">Copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="91694-115">(Você pode encontrá-los em **Chaves de Autenticação**.) Você precisará de ambos para configurar o LinkedIn como um provedor de identidade no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="91694-115">(You can find them under **Authentication Keys**.) You will need both of them to configure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="91694-116">**Segredo do Cliente** é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="91694-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="91694-117">Digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` no campo **URLs de Redirecionamento Autorizado** (em **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="91694-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="91694-118">Substitua **{tenant}** pelo nome do locatário (por exemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="91694-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="91694-119">Clique em **Adicionar** e depois em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="91694-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="91694-120">O valor **{tenant}** diferencia letras maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="91694-120">The **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn — Configurar aplicativo](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="91694-122">Configurar o LinkedIn como um provedor de identidade no locatário</span><span class="sxs-lookup"><span data-stu-id="91694-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="91694-123">Siga estas etapas para [navegar até a folha de recursos do B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="91694-123">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="91694-124">Na folha de recursos do B2C, clique em **Provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="91694-124">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="91694-125">Clique em **+Adicionar** , na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="91694-125">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="91694-126">Forneça um **Nome** amigável para a configuração do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="91694-126">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="91694-127">Por exemplo, insira "LI".</span><span class="sxs-lookup"><span data-stu-id="91694-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="91694-128">Clique em **Tipo do provedor de identidade**, selecione **LinkedIn** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="91694-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="91694-129">Clique em **Configurar esse provedor de identidade** e insira a ID e o segredo do cliente do aplicativo do LinkedIn que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="91694-129">Click **Set up this identity provider** and enter the client ID and client secret of the LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="91694-130">Clique em **OK** e em **Criar** para salvar sua configuração do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="91694-130">Click **OK** and then click **Create** to save your LinkedIn configuration.</span></span>

