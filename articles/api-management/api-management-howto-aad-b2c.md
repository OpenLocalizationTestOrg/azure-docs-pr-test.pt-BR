---
title: contas de desenvolvedor aaaAuthorize usando o Azure Active Directory B2C - gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como tooauthorize usuários usando o Azure Active Directory B2C no gerenciamento de API."
services: api-management
documentationcenter: API Management
author: miaojiang
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="82746-103">Como desenvolvedor de tooauthorize contas usando o Azure Active Directory B2C no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="82746-103">How tooauthorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="82746-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="82746-104">Overview</span></span>
<span data-ttu-id="82746-105">O Azure Active Directory B2C é uma solução de gerenciamento de identidade na nuvem para os seus aplicativos móveis e Web voltados para o consumidor.</span><span class="sxs-lookup"><span data-stu-id="82746-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="82746-106">Você pode usá-lo portal do desenvolvedor do tooyour toomanage acesso.</span><span class="sxs-lookup"><span data-stu-id="82746-106">You can use it toomanage access tooyour developer portal.</span></span> <span data-ttu-id="82746-107">Este mostra guia Olá configuração necessária no seu toointegrate do serviço de gerenciamento de API com o Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="82746-107">This guide shows you hello configuration that's required in your API Management service toointegrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="82746-108">Para obter informações sobre como habilitar o portal do desenvolvedor toohello acesso usando clássico do Azure Active Directory, consulte [como desenvolvedor tooauthorize contas usando Active Directory do Azure].</span><span class="sxs-lookup"><span data-stu-id="82746-108">For information about enabling access toohello developer portal by using classic Azure Active Directory, see [How tooauthorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="82746-109">toocomplete Olá etapas neste guia, você deve primeiro ter um toocreate de locatário do Azure Active Directory B2C um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="82746-109">toocomplete hello steps in this guide, you must first have an Azure Active Directory B2C tenant toocreate an application in.</span></span> <span data-ttu-id="82746-110">Além disso, você precisa de políticas de inscrição e entrar toohave pronto.</span><span class="sxs-lookup"><span data-stu-id="82746-110">Also, you need toohave signup and signin policies ready.</span></span> <span data-ttu-id="82746-111">Para saber mais, veja [Visão geral do Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="82746-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="82746-112">Autorizar contas de desenvolvedor usando o Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="82746-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="82746-113">tooget iniciado, clique em **portal do publicador** no portal do Azure para seu serviço de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="82746-113">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="82746-114">Isso leva toohello portal do publicador de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="82746-114">This takes you toohello API Management publisher portal.</span></span>

   ![Portal do editor][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="82746-116">Se você ainda não criou uma instância de serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao tutorial do gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="82746-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="82746-117">Em Olá **gerenciamento de API** menu, clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="82746-117">On hello **API Management** menu, click **Security**.</span></span> <span data-ttu-id="82746-118">Em Olá **identidades** guia, escolha **do Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="82746-118">On hello **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Identidades externas 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="82746-120">Anote Olá **URL de redirecionamento** e passar tooAzure B2C do Active Directory no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="82746-120">Make a note of hello **Redirect URL** and switch over tooAzure Active Directory B2C in hello Azure portal.</span></span>

  ![Identidades externas 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="82746-122">Clique em Olá **aplicativos** botão.</span><span class="sxs-lookup"><span data-stu-id="82746-122">Click hello **Applications** button.</span></span>

  ![Registrar um novo aplicativo 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="82746-124">Clique em Olá **adicionar** botão aplicativo toocreate um novo do Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="82746-124">Click hello **Add** button toocreate a new Azure Active Directory B2C application.</span></span>

  ![Registrar um novo aplicativo 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="82746-126">Em Olá **novo aplicativo** folha, insira um nome para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="82746-126">In hello **New application** blade, enter a name for hello application.</span></span> <span data-ttu-id="82746-127">Escolha **Sim** em **API da Web do aplicativo Web**e escolha **Sim** em **permitir fluxo implícito**.</span><span class="sxs-lookup"><span data-stu-id="82746-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="82746-128">Então Olá cópia **URL de redirecionamento** de saudação **do Azure Active Directory B2C** seção Olá **identidades** guia no portal do publicador hello e cole-a saudação **URL de resposta** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="82746-128">Then copy hello **Redirect URL** from hello **Azure Active Directory B2C** section of hello **Identities** tab in hello publisher portal, and paste it into hello **Reply URL** text box.</span></span>

  ![Registrar um novo aplicativo 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="82746-130">Clique em Olá **criar** botão.</span><span class="sxs-lookup"><span data-stu-id="82746-130">Click hello **Create** button.</span></span> <span data-ttu-id="82746-131">Quando o aplicativo hello é criado, ela aparece no hello **aplicativos** folha.</span><span class="sxs-lookup"><span data-stu-id="82746-131">When hello application is created, it appears in hello **Applications** blade.</span></span> <span data-ttu-id="82746-132">Clique em toosee de nome de aplicativo hello seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="82746-132">Click hello application name toosee its details.</span></span>

  ![Registrar um novo aplicativo 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="82746-134">De saudação **propriedades** folha, Olá cópia **ID do aplicativo** toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="82746-134">From hello **Properties** blade, copy hello **Application ID** toohello clipboard.</span></span>

  ![ID do aplicativo 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="82746-136">Alternar o portal do publicador toohello back e cole ID Olá Olá **Id do cliente** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="82746-136">Switch back toohello publisher portal and paste hello ID into hello **Client Id** text box.</span></span>

  ![ID do aplicativo 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="82746-138">Toohello back portal do Azure, clique Olá **chaves** botão e, em seguida, clique em **gerar chave**.</span><span class="sxs-lookup"><span data-stu-id="82746-138">Switch back toohello Azure portal, click hello **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="82746-139">Clique em **salvar** toosave Olá Olá de configuração e exibição **chave do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="82746-139">Click **Save** toosave hello configuration and display hello **App key**.</span></span> <span data-ttu-id="82746-140">Copiar Olá chave toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="82746-140">Copy hello key toohello clipboard.</span></span>

  ![Chave do aplicativo 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="82746-142">Switch back toohello publicador portal e colar Olá chave em Olá **segredo do cliente** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="82746-142">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

  ![Chave do aplicativo 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="82746-144">Especificar nome de domínio de saudação do locatário de saudação do Azure Active Directory B2C em **permitido locatário**.</span><span class="sxs-lookup"><span data-stu-id="82746-144">Specify hello domain name of hello Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Locatário permitido][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="82746-146">Especificar Olá **inscrição política** e **Signin política**.</span><span class="sxs-lookup"><span data-stu-id="82746-146">Specify hello **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="82746-147">Opcionalmente, você também pode fornecer Olá **a política de edição de perfil** e **política de redefinição de senha**.</span><span class="sxs-lookup"><span data-stu-id="82746-147">Optionally, you can also provide hello **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Políticas][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="82746-149">Para saber mais sobre políticas, veja [Azure Active Directory B2C: estrutura de política extensível].</span><span class="sxs-lookup"><span data-stu-id="82746-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="82746-150">Depois que você especificou as configurações desejadas hello, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="82746-150">After you've specified hello desired configuration, click **Save**.</span></span>

  <span data-ttu-id="82746-151">Depois de saudação alterações são salvas, os desenvolvedores serão toocreate capaz de novas contas e entrar no portal do desenvolvedor toohello usando o Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="82746-151">After hello changes are saved, developers will be able toocreate new accounts and sign in toohello developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="82746-152">Inscrever-se para uma conta de desenvolvedor usando o Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="82746-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="82746-153">toosign uma conta de desenvolvedor usando o Azure Active Directory B2C, abra uma nova janela do navegador e acesse o portal do desenvolvedor toohello.</span><span class="sxs-lookup"><span data-stu-id="82746-153">toosign up for a developer account by using Azure Active Directory B2C, open a new browser window and go toohello developer portal.</span></span> <span data-ttu-id="82746-154">Clique em Olá **inscrever** botão.</span><span class="sxs-lookup"><span data-stu-id="82746-154">Click hello **Sign up** button.</span></span>

   ![Portal do desenvolvedor 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="82746-156">Escolha toosign com **do Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="82746-156">Choose toosign up with **Azure Active Directory B2C**.</span></span>

   ![Portal do desenvolvedor 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="82746-158">Você é redirecionado toohello inscrição política que você configurou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="82746-158">You're redirected toohello signup policy that you configured in hello previous section.</span></span> <span data-ttu-id="82746-159">Escolha toosign usando seu endereço de email ou uma de suas contas sociais existentes.</span><span class="sxs-lookup"><span data-stu-id="82746-159">Choose toosign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82746-160">Se o Azure Active Directory B2C é Olá única opção que é habilitada em Olá **identidades** guia no portal do publicador hello, você será redirecionado toohello inscrição política diretamente.</span><span class="sxs-lookup"><span data-stu-id="82746-160">If Azure Active Directory B2C is hello only option that's enabled on hello **Identities** tab in hello publisher portal, you'll be redirected toohello signup policy directly.</span></span>

   ![Portal do desenvolvedor][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="82746-162">Quando Olá inscrição for concluída, você estará toohello back redirecionado portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="82746-162">When hello signup is complete, you're redirected back toohello developer portal.</span></span> <span data-ttu-id="82746-163">Agora você está conectado no portal do desenvolvedor toohello para sua instância de serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="82746-163">You're now signed in toohello developer portal for your API Management service instance.</span></span>

    ![Registro concluído][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="82746-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="82746-165">Next steps</span></span>

*  <span data-ttu-id="82746-166">[Visão geral do Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="82746-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="82746-167">[Azure Active Directory B2C: estrutura de política extensível]</span><span class="sxs-lookup"><span data-stu-id="82746-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="82746-168">[Usar a conta da Microsoft como provedor de identidade no Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="82746-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="82746-169">[Usar a conta do Google como provedor de identidade no Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="82746-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="82746-170">[Usar a conta do Linkedin como provedor de identidade no Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="82746-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="82746-171">[Usar a conta do Facebook como provedor de identidade no Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="82746-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
[Visão geral do Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[como desenvolvedor tooauthorize contas usando Active Directory do Azure]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C: estrutura de política extensível]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Usar a conta da Microsoft como provedor de identidade no Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Usar a conta do Google como provedor de identidade no Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Usar a conta do Facebook como provedor de identidade no Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Usar a conta do Linkedin como provedor de identidade no Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
