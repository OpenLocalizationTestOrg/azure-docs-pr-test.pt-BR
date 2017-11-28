---
title: "Azure Active Directory B2C: configuração do Facebook | Microsoft Docs"
description: "Fornece tooconsumers Inscreva-se e entrar com contas do Facebook em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
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
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a><span data-ttu-id="03bb5-103">B2C de diretório ativo do Azure: Fornecer tooconsumers se inscrever e fazer logon com contas do Facebook</span><span class="sxs-lookup"><span data-stu-id="03bb5-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="03bb5-104">Criar um aplicativo do Facebook</span><span class="sxs-lookup"><span data-stu-id="03bb5-104">Create a Facebook application</span></span>
<span data-ttu-id="03bb5-105">toouse Facebook como provedor de identidade no B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo do Facebook e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="03bb5-105">toouse Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Facebook application and supply it with hello right parameters.</span></span> <span data-ttu-id="03bb5-106">É necessário um toodo de conta do Facebook isso.</span><span class="sxs-lookup"><span data-stu-id="03bb5-106">You need a Facebook account toodo this.</span></span> <span data-ttu-id="03bb5-107">Se você não tiver uma, poderá obtê-la em [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="03bb5-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="03bb5-108">Vá toohello [Facebook para desenvolvedores](https://developers.facebook.com/) as credenciais de conta de site e entre com o Facebook.</span><span class="sxs-lookup"><span data-stu-id="03bb5-108">Go toohello [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="03bb5-109">Se você ainda não tiver feito isso, será necessário tooregister como um desenvolvedor de Facebook.</span><span class="sxs-lookup"><span data-stu-id="03bb5-109">If you have not already done so, you need tooregister as a Facebook developer.</span></span> <span data-ttu-id="03bb5-110">toodo, clique **registrar** (na Olá canto superior direito da página de saudação), aceite as políticas do Facebook e concluir as etapas de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="03bb5-110">toodo this, click **Register** (on hello upper-right corner of hello page), accept Facebook's policies, and complete hello registration steps.</span></span>
3. <span data-ttu-id="03bb5-111">Clique em **Meus Aplicativos** e em **Adicionar um Novo Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="03bb5-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="03bb5-112">No formulário de hello, forneça um **nome de exibição** uma opção válida **Contact Email**.</span><span class="sxs-lookup"><span data-stu-id="03bb5-112">In hello form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="03bb5-113">Clique em **Criar ID de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="03bb5-113">Click **Create App ID**.</span></span> <span data-ttu-id="03bb5-114">Isso pode exigir políticas de plataforma do Facebook tooaccept e concluir uma verificação de segurança on-line.</span><span class="sxs-lookup"><span data-stu-id="03bb5-114">This may require you tooaccept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="03bb5-115">Na coluna esquerda da saudação, clique em **configurações** e, em seguida, selecione **básica** se já não foi selecionada.</span><span class="sxs-lookup"><span data-stu-id="03bb5-115">In hello left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="03bb5-116">Selecione uma **Categoria**.</span><span class="sxs-lookup"><span data-stu-id="03bb5-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="03bb5-117">Clique em **+Adicionar Plataforma** e selecione **Site**.</span><span class="sxs-lookup"><span data-stu-id="03bb5-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - Configurações](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - Configurações - Site](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="03bb5-120">Digite `https://login.microsoftonline.com/` em Olá **URL do Site** campo e, em seguida, clique em **salvar alterações** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="03bb5-120">Enter `https://login.microsoftonline.com/` in hello **Site URL** field and then click **Save Changes** at hello bottom of hello page.</span></span>
   
    ![Facebook - URL do Site](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="03bb5-122">Copie o valor de saudação do **ID do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="03bb5-122">Copy hello value of **App ID**.</span></span> <span data-ttu-id="03bb5-123">Clique em **Mostrar** e copie o valor de saudação do **segredo do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="03bb5-123">Click **Show** and copy hello value of **App Secret**.</span></span> <span data-ttu-id="03bb5-124">Você precisará de ambos tooconfigure Facebook como provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="03bb5-124">You will need both of them tooconfigure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="03bb5-125">**Segredo do Aplicativo** é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="03bb5-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - ID do Aplicativo e Segredo do Aplicativo](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="03bb5-127">Clique em **+ adicionar produto** Olá navegação esquerdo e, em seguida, Olá **Set Up** botão para **logon do Facebook**.</span><span class="sxs-lookup"><span data-stu-id="03bb5-127">Click **+ Add Product** on hello left navigation and then hello **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Logon no Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="03bb5-129">Clique em **configurações** na barra de navegação direita em Olá **logon do Facebook**</span><span class="sxs-lookup"><span data-stu-id="03bb5-129">Click **Settings** on hello right nav under **Facebook Login**</span></span>

    ![Facebook - configurações de Logon no Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="03bb5-131">Digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **URIs de redirecionamento OAuth válido** campo Olá **configurações do cliente OAuth** seção.</span><span class="sxs-lookup"><span data-stu-id="03bb5-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Valid OAuth redirect URIs** field in hello **Client OAuth Settings** section.</span></span> <span data-ttu-id="03bb5-132">Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="03bb5-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="03bb5-133">Clique em **salvar alterações** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="03bb5-133">Click **Save Changes** at hello bottom of hello page.</span></span>
    
    ![Facebook - URI de Redirecionamento de OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="03bb5-135">toomake seu aplicativo Facebook utilizável por B2C do Azure AD, você precisa toomake publicamente disponível.</span><span class="sxs-lookup"><span data-stu-id="03bb5-135">toomake your Facebook application usable by Azure AD B2C, you need toomake it publicly available.</span></span> <span data-ttu-id="03bb5-136">Você pode fazer isso clicando em **revisão de aplicativo** em Olá barra de navegação esquerda e por saudação de ativação do comutador na parte superior de saudação da página de saudação muito**Sim** e clicando em **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="03bb5-136">You can do this by clicking **App Review** on hello left navigation and by turning hello switch at hello top of hello page too**YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - Público do aplicativo](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="03bb5-138">Configurar o Facebook como um provedor de identidade no seu locatário</span><span class="sxs-lookup"><span data-stu-id="03bb5-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="03bb5-139">Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="03bb5-139">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="03bb5-140">Na folha de recursos Olá B2C, clique em **provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="03bb5-140">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="03bb5-141">Clique em **+ adicionar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="03bb5-141">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="03bb5-142">Forneça um amigável **nome** para configuração do provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="03bb5-142">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="03bb5-143">Por exemplo, insira “Facebook”.</span><span class="sxs-lookup"><span data-stu-id="03bb5-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="03bb5-144">Clique em **Tipo de provedor de identidade**, selecione **Facebook** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="03bb5-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="03bb5-145">Clique em **configurar esse provedor de identidade** e digite Olá ID e o aplicativo segredo do aplicativo (da saudação aplicativo do Facebook que você criou anteriormente) no hello **ID do cliente** e **segredo do cliente**campos respectivamente.</span><span class="sxs-lookup"><span data-stu-id="03bb5-145">Click **Set up this identity provider** and enter hello app ID and app secret (of hello Facebook application that you created earlier) in hello **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="03bb5-146">Clique em **Okey**e, em seguida, clique em **criar** toosave sua configuração do Facebook.</span><span class="sxs-lookup"><span data-stu-id="03bb5-146">Click **OK**, and then click **Create** toosave your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="03bb5-147">Adicionando um **provedor de identidade** tooyour locatário não modifica as políticas existentes.</span><span class="sxs-lookup"><span data-stu-id="03bb5-147">Adding an **Identity provider** tooyour tenant does not modify your existing policies.</span></span> <span data-ttu-id="03bb5-148">Lembre-se de tooupdate suas políticas, incluindo o provedor de identidade Olá que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="03bb5-148">Remember tooupdate your policies by including hello identity provider you just created.</span></span>
>