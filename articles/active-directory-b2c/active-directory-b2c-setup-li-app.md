---
title: "Azure Active Directory B2C: configuração do LinkedIn | Microsoft Docs"
description: "Fornecer tooconsumers Inscreva-se e entrar com contas LinkedIn em seus aplicativos que são protegidos pelo Azure Active Directory B2C"
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
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a><span data-ttu-id="619af-103">B2C de diretório ativo do Azure: Fornecer tooconsumers Inscreva-se e entrar com contas LinkedIn</span><span class="sxs-lookup"><span data-stu-id="619af-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="619af-104">Criar um aplicativo do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="619af-104">Create a LinkedIn application</span></span>
<span data-ttu-id="619af-105">toouse LinkedIn como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo LinkedIn e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="619af-105">toouse LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a LinkedIn application and supply it with hello right parameters.</span></span> <span data-ttu-id="619af-106">É necessário um toodo de conta LinkedIn isso.</span><span class="sxs-lookup"><span data-stu-id="619af-106">You need a LinkedIn account toodo this.</span></span> <span data-ttu-id="619af-107">Se você não tiver uma, poderá obtê-la em [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="619af-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="619af-108">Vá toohello [site de desenvolvedores do LinkedIn](https://www.developer.linkedin.com/) e entre com suas credenciais de conta do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="619af-108">Go toohello [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="619af-109">Clique em **meus aplicativos** em Olá barra de menus superior e, em seguida, clique em **criar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="619af-109">Click **My Apps** in hello top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn — Novo aplicativo](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="619af-111">Em Olá **criar um novo aplicativo** formulário, preencha informações relevantes da saudação (**nome da empresa**, **nome**, **descrição**, **URL de logotipo do aplicativo**, **aplicativo Use**, **URL do site**, **Email comerciais** e **telefone comercial**).</span><span class="sxs-lookup"><span data-stu-id="619af-111">In hello **Create a New Application** form, fill in hello relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="619af-112">Concordo toohello **LinkedIn API termos de uso** e clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="619af-112">Agree toohello **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn — Registrar aplicativo](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="619af-114">Copie os valores de saudação do **ID do cliente** e **segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="619af-114">Copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="619af-115">(Você pode encontrá-los em **Chaves de Autenticação**.) Você precisará de ambos tooconfigure LinkedIn como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="619af-115">(You can find them under **Authentication Keys**.) You will need both of them tooconfigure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="619af-116">**Segredo do Cliente** é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="619af-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="619af-117">Digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **URLs de redirecionamento autorizado** campo (em **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="619af-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="619af-118">Substitua **{tenant}** pelo nome do locatário (por exemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="619af-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="619af-119">Clique em **Adicionar** e depois em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="619af-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="619af-120">Olá **{locatário}** valor diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="619af-120">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn — Configurar aplicativo](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="619af-122">Configurar o LinkedIn como um provedor de identidade no locatário</span><span class="sxs-lookup"><span data-stu-id="619af-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="619af-123">Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="619af-123">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="619af-124">Na folha de recursos Olá B2C, clique em **provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="619af-124">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="619af-125">Clique em **+ adicionar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="619af-125">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="619af-126">Forneça um amigável **nome** para configuração do provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="619af-126">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="619af-127">Por exemplo, insira "LI".</span><span class="sxs-lookup"><span data-stu-id="619af-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="619af-128">Clique em **Tipo do provedor de identidade**, selecione **LinkedIn** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="619af-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="619af-129">Clique em **configurar esse provedor de identidade** e digite Olá ID e o cliente segredo do cliente do hello LinkedIn aplicativo que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="619af-129">Click **Set up this identity provider** and enter hello client ID and client secret of hello LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="619af-130">Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="619af-130">Click **OK** and then click **Create** toosave your LinkedIn configuration.</span></span>

