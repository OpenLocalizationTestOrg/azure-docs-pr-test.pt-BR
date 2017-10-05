---
title: "Azure Active Directory B2C: configuração do Facebook | Microsoft Docs"
description: "Forneça inscrição e entrada para consumidores com contas do Facebook em seus aplicativos protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 8c2154fcf33537358b549395d15b4ba937371cd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-facebook-accounts"></a><span data-ttu-id="09f7e-103">Azure Active Directory B2C: fornecer inscrição e entrada para consumidores com contas do Facebook</span><span class="sxs-lookup"><span data-stu-id="09f7e-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="09f7e-104">Criar um aplicativo do Facebook</span><span class="sxs-lookup"><span data-stu-id="09f7e-104">Create a Facebook application</span></span>
<span data-ttu-id="09f7e-105">Para usar o Facebook como provedor de identidade no Azure AD (Azure Active Directory) B2C, será necessário primeiro criar um aplicativo do Facebook e fornecê-lo com os parâmetros corretos.</span><span class="sxs-lookup"><span data-stu-id="09f7e-105">To use Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Facebook application and supply it with the right parameters.</span></span> <span data-ttu-id="09f7e-106">Você precisa de uma conta do Facebook para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="09f7e-106">You need a Facebook account to do this.</span></span> <span data-ttu-id="09f7e-107">Se você não tiver uma, poderá obtê-la em [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="09f7e-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="09f7e-108">Acesse o site [Desenvolvedores do Facebook](https://developers.facebook.com/) e entre com suas credenciais de conta do Facebook.</span><span class="sxs-lookup"><span data-stu-id="09f7e-108">Go to the [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="09f7e-109">Se ainda não tiver feito isso, você precisará registrar-se como desenvolvedor do Facebook.</span><span class="sxs-lookup"><span data-stu-id="09f7e-109">If you have not already done so, you need to register as a Facebook developer.</span></span> <span data-ttu-id="09f7e-110">Para fazer isso, clique em **Registrar** (no canto superior direito da página), aceite as políticas do Facebook e conclua as etapas de registro.</span><span class="sxs-lookup"><span data-stu-id="09f7e-110">To do this, click **Register** (on the upper-right corner of the page), accept Facebook's policies, and complete the registration steps.</span></span>
3. <span data-ttu-id="09f7e-111">Clique em **Meus Aplicativos** e em **Adicionar um Novo Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="09f7e-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="09f7e-112">No formulário, forneça um **Nome de Exibição** e um **Email de Contato** válido.</span><span class="sxs-lookup"><span data-stu-id="09f7e-112">In the form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="09f7e-113">Clique em **Criar ID de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="09f7e-113">Click **Create App ID**.</span></span> <span data-ttu-id="09f7e-114">Isso pode exigir a aceitação das políticas de plataforma do Facebook e a conclusão de uma verificação de segurança online.</span><span class="sxs-lookup"><span data-stu-id="09f7e-114">This may require you to accept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="09f7e-115">Na coluna à esquerda, clique em **Configurações** e selecione **Básica**, caso ainda não esteja selecionado.</span><span class="sxs-lookup"><span data-stu-id="09f7e-115">In the left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="09f7e-116">Selecione uma **Categoria**.</span><span class="sxs-lookup"><span data-stu-id="09f7e-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="09f7e-117">Clique em **+Adicionar Plataforma** e selecione **Site**.</span><span class="sxs-lookup"><span data-stu-id="09f7e-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - Configurações](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - Configurações - Site](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="09f7e-120">Digite `https://login.microsoftonline.com/` no campo **URL do Site** e clique em **Salvar Alterações** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="09f7e-120">Enter `https://login.microsoftonline.com/` in the **Site URL** field and then click **Save Changes** at the bottom of the page.</span></span>
   
    ![Facebook - URL do Site](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="09f7e-122">Copie o valor de **ID do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="09f7e-122">Copy the value of **App ID**.</span></span> <span data-ttu-id="09f7e-123">Clique em **Mostrar** e copie o valor de **Segredo do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="09f7e-123">Click **Show** and copy the value of **App Secret**.</span></span> <span data-ttu-id="09f7e-124">Você precisará de ambos para configurar o Facebook como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="09f7e-124">You will need both of them to configure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="09f7e-125">**Segredo do Aplicativo** é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="09f7e-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - ID do Aplicativo e Segredo do Aplicativo](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="09f7e-127">Clique em **+ Adicionar Produto** no painel de navegação esquerdo e no botão **Configurar** para **Logon do Facebook**.</span><span class="sxs-lookup"><span data-stu-id="09f7e-127">Click **+ Add Product** on the left navigation and then the **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Logon no Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="09f7e-129">Clique em **Configurações** na barra de navegação direita em **Logon do Facebook**</span><span class="sxs-lookup"><span data-stu-id="09f7e-129">Click **Settings** on the right nav under **Facebook Login**</span></span>

    ![Facebook - configurações de Logon no Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="09f7e-131">Digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` no campo **URIs de redirecionamento OAuth válidos** na seção **Configurações do Cliente OAuth**.</span><span class="sxs-lookup"><span data-stu-id="09f7e-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Valid OAuth redirect URIs** field in the **Client OAuth Settings** section.</span></span> <span data-ttu-id="09f7e-132">Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="09f7e-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="09f7e-133">Clique em **Salvar Alterações** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="09f7e-133">Click **Save Changes** at the bottom of the page.</span></span>
    
    ![Facebook - URI de Redirecionamento de OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="09f7e-135">Para tornar seu aplicativo do Facebook utilizável pelo Azure AD B2C, você precisa torná-lo público.</span><span class="sxs-lookup"><span data-stu-id="09f7e-135">To make your Facebook application usable by Azure AD B2C, you need to make it publicly available.</span></span> <span data-ttu-id="09f7e-136">É possível fazer isso clicando em **Análise de Aplicativos** na navegação à esquerda, ativando a opção na parte superior da página para **SIM** e clicando em **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="09f7e-136">You can do this by clicking **App Review** on the left navigation and by turning the switch at the top of the page to **YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - Público do aplicativo](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="09f7e-138">Configurar o Facebook como um provedor de identidade no seu locatário</span><span class="sxs-lookup"><span data-stu-id="09f7e-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="09f7e-139">Siga estas etapas para [navegar até a folha de recursos do B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="09f7e-139">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="09f7e-140">Na folha de recursos do B2C, clique em **Provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="09f7e-140">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="09f7e-141">Clique em **+Adicionar** , na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="09f7e-141">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="09f7e-142">Forneça um **Nome** amigável para a configuração do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="09f7e-142">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="09f7e-143">Por exemplo, insira “Facebook”.</span><span class="sxs-lookup"><span data-stu-id="09f7e-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="09f7e-144">Clique em **Tipo de provedor de identidade**, selecione **Facebook** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="09f7e-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="09f7e-145">Clique em **Configurar este provedor de identidade** e insira a ID e o segredo do aplicativo (do aplicativo do Facebook criado anteriormente) nos campos **ID do Cliente** e **Segredo do cliente**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="09f7e-145">Click **Set up this identity provider** and enter the app ID and app secret (of the Facebook application that you created earlier) in the **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="09f7e-146">Clique em **OK** e em **Criar** para salvar sua configuração do Facebook.</span><span class="sxs-lookup"><span data-stu-id="09f7e-146">Click **OK**, and then click **Create** to save your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="09f7e-147">A adição de um **Provedor de identidade** ao seu locatário não modifica as políticas existentes.</span><span class="sxs-lookup"><span data-stu-id="09f7e-147">Adding an **Identity provider** to your tenant does not modify your existing policies.</span></span> <span data-ttu-id="09f7e-148">Lembre-se de atualizar as políticas, incluindo o provedor de identidade que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="09f7e-148">Remember to update your policies by including the identity provider you just created.</span></span>
>