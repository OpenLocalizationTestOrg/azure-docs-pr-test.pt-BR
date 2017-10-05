---
title: Autorizar contas de desenvolvedor usando o Azure Active Directory B2C - Gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como autorizar usuários que usam o Azure Active Directory B2C no Gerenciamento de API."
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
ms.openlocfilehash: eb7deb1a79d9db9ac5cfbea69b8d3c564eb55577
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="9cc69-103">Como autorizar contas de desenvolvedor usando o Azure Active Directory B2C no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="9cc69-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="9cc69-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9cc69-104">Overview</span></span>
<span data-ttu-id="9cc69-105">O Azure Active Directory B2C é uma solução de gerenciamento de identidade na nuvem para os seus aplicativos móveis e Web voltados para o consumidor.</span><span class="sxs-lookup"><span data-stu-id="9cc69-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="9cc69-106">Você pode usá-lo para gerenciar o acesso ao portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="9cc69-106">You can use it to manage access to your developer portal.</span></span> <span data-ttu-id="9cc69-107">Este guia mostra a configuração necessária no seu serviço de gerenciamento de API para integrar com o Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="9cc69-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="9cc69-108">Para saber mais sobre como habilitar o acesso ao portal do desenvolvedor usando o Azure Active Directory clássico, veja [Como autorizar contas de desenvolvedor usando o Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="9cc69-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="9cc69-109">Para completar as etapas deste guia, primeiro tenha um locatário do Azure Active Directory B2C no qual criar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9cc69-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span></span> <span data-ttu-id="9cc69-110">Além disso, você precisa ter políticas de entrada e de inscrição prontas.</span><span class="sxs-lookup"><span data-stu-id="9cc69-110">Also, you need to have signup and signin policies ready.</span></span> <span data-ttu-id="9cc69-111">Para saber mais, veja [Visão geral do Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="9cc69-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="9cc69-112">Autorizar contas de desenvolvedor usando o Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="9cc69-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="9cc69-113">Para começar, clique em **Portal do Editor** no Portal do Azure para acessar o serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="9cc69-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="9cc69-114">Isso levará você ao portal do editor de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="9cc69-114">This takes you to the API Management publisher portal.</span></span>

   ![Portal do editor][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="9cc69-116">Se você ainda não tiver criado uma instância do serviço de Gerenciamento de API, veja [Criar uma instância do serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9cc69-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="9cc69-117">No menu **Gerenciamento de API**, clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-117">On the **API Management** menu, click **Security**.</span></span> <span data-ttu-id="9cc69-118">Na guia **Identidades**, escolha **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Identidades externas 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="9cc69-120">Anote a **URL de Redirecionamento** e alterne para seu Azure Active Directory B2C no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc69-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span></span>

  ![Identidades externas 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="9cc69-122">Clique no botão **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-122">Click the **Applications** button.</span></span>

  ![Registrar um novo aplicativo 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="9cc69-124">Clique o **adicionar** botão para criar um novo aplicativo do Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="9cc69-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span></span>

  ![Registrar um novo aplicativo 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="9cc69-126">Na folha **Novo aplicativo**, insira um nome para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9cc69-126">In the **New application** blade, enter a name for the application.</span></span> <span data-ttu-id="9cc69-127">Escolha **Sim** em **API da Web do aplicativo Web**e escolha **Sim** em **permitir fluxo implícito**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="9cc69-128">Em seguida, copie a **URL de redirecionamento** da seção **Azure Active Directory B2C** da guia **Identidades** no portal do editor e cole-a na caixa de texto **URL de resposta**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span></span>

  ![Registrar um novo aplicativo 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="9cc69-130">Selecione o botão **Criar** .</span><span class="sxs-lookup"><span data-stu-id="9cc69-130">Click the **Create** button.</span></span> <span data-ttu-id="9cc69-131">Quando o aplicativo é criado, ele aparece no **aplicativos** folha.</span><span class="sxs-lookup"><span data-stu-id="9cc69-131">When the application is created, it appears in the **Applications** blade.</span></span> <span data-ttu-id="9cc69-132">Clique no nome do aplicativo para ver seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="9cc69-132">Click the application name to see its details.</span></span>

  ![Registrar um novo aplicativo 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="9cc69-134">Do **propriedades** folha, copie o **ID do aplicativo** na área de transferência.</span><span class="sxs-lookup"><span data-stu-id="9cc69-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span></span>

  ![ID do aplicativo 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="9cc69-136">Voltar ao portal do editor e cole a ID na caixa de texto **ID do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span></span>

  ![ID do aplicativo 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="9cc69-138">Alterne para o Portal do Azure, clique no botão **Chaves** e clique em **Gerar chave**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="9cc69-139">Clique em **Salvar** para salvar a configuração e exibir a **chave de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-139">Click **Save** to save the configuration and display the **App key**.</span></span> <span data-ttu-id="9cc69-140">Copie a chave para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="9cc69-140">Copy the key to the clipboard.</span></span>

  ![Chave do aplicativo 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="9cc69-142">Voltar ao portal do editor e cole a chave na caixa de texto **Segredo do Cliente** .</span><span class="sxs-lookup"><span data-stu-id="9cc69-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

  ![Chave do aplicativo 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="9cc69-144">Especifique o campo **Locatário Permitido** com o nome de domínio do locatário do Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="9cc69-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Locatário permitido][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="9cc69-146">Especifique o **Política de Inscrição** e **Política de Entrada**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-146">Specify the **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="9cc69-147">Opcionalmente, você também pode fornecer **Política de Edição de Perfil** e **Política de Redefinição de Senha**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Políticas][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="9cc69-149">Para saber mais sobre políticas, veja [Azure Active Directory B2C: estrutura de política extensível].</span><span class="sxs-lookup"><span data-stu-id="9cc69-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="9cc69-150">Depois que a configuração desejada for especificada, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-150">After you've specified the desired configuration, click **Save**.</span></span>

  <span data-ttu-id="9cc69-151">Depois que as alterações forem salvas, os desenvolvedores poderão criar novas contas e entrar portal do desenvolvedor usando Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="9cc69-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="9cc69-152">Inscrever-se para uma conta de desenvolvedor usando o Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="9cc69-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="9cc69-153">Para se inscrever para uma conta de desenvolvedor usando o Azure Active Directory B2C, abra uma nova janela do navegador e vá para o portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="9cc69-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span></span> <span data-ttu-id="9cc69-154">Clique no botão **Inscrever**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-154">Click the **Sign up** button.</span></span>

   ![Portal do desenvolvedor 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="9cc69-156">Opte por inscrever-se no **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="9cc69-156">Choose to sign up with **Azure Active Directory B2C**.</span></span>

   ![Portal do desenvolvedor 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="9cc69-158">Você será redirecionado para a política de inscrição configurada na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="9cc69-158">You're redirected to the signup policy that you configured in the previous section.</span></span> <span data-ttu-id="9cc69-159">Escolha inscrever-se usando seu endereço de email ou uma de suas contas sociais existentes.</span><span class="sxs-lookup"><span data-stu-id="9cc69-159">Choose to sign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9cc69-160">Se o Azure Active Directory B2C for a única opção habilitada no **identidades** guia no portal do Editor, você será redirecionado para a política de inscrição diretamente.</span><span class="sxs-lookup"><span data-stu-id="9cc69-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span></span>

   ![Portal do desenvolvedor][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="9cc69-162">Quando a inscrição for concluída, você será redirecionado para o portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="9cc69-162">When the signup is complete, you're redirected back to the developer portal.</span></span> <span data-ttu-id="9cc69-163">Agora você está conectado no portal do desenvolvedor para a instância de serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="9cc69-163">You're now signed in to the developer portal for your API Management service instance.</span></span>

    ![Registro concluído][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="9cc69-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9cc69-165">Next steps</span></span>

*  <span data-ttu-id="9cc69-166">[Visão geral do Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="9cc69-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="9cc69-167">[Azure Active Directory B2C: estrutura de política extensível]</span><span class="sxs-lookup"><span data-stu-id="9cc69-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="9cc69-168">[Usar a conta da Microsoft como provedor de identidade no Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="9cc69-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="9cc69-169">[Usar a conta do Google como provedor de identidade no Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="9cc69-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="9cc69-170">[Usar a conta do Linkedin como provedor de identidade no Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="9cc69-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="9cc69-171">[Usar a conta do Facebook como provedor de identidade no Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="9cc69-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
<span data-ttu-id="9cc69-172">[Visão geral do Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span><span class="sxs-lookup"><span data-stu-id="9cc69-172">[Azure Active Directory B2C overview]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span></span>
<span data-ttu-id="9cc69-173">[Como autorizar contas de desenvolvedor usando o Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span><span class="sxs-lookup"><span data-stu-id="9cc69-173">[How to authorize developer accounts using Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span></span>
<span data-ttu-id="9cc69-174">[Azure Active Directory B2C: estrutura de política extensível]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span><span class="sxs-lookup"><span data-stu-id="9cc69-174">[Azure Active Directory B2C: Extensible policy framework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span></span>
<span data-ttu-id="9cc69-175">[Usar a conta da Microsoft como provedor de identidade no Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span><span class="sxs-lookup"><span data-stu-id="9cc69-175">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span></span>
<span data-ttu-id="9cc69-176">[Usar a conta do Google como provedor de identidade no Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span><span class="sxs-lookup"><span data-stu-id="9cc69-176">[Use a Google account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span></span>
<span data-ttu-id="9cc69-177">[Usar a conta do Facebook como provedor de identidade no Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span><span class="sxs-lookup"><span data-stu-id="9cc69-177">[Use a Facebook account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span></span>
<span data-ttu-id="9cc69-178">[Usar a conta do Linkedin como provedor de identidade no Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span><span class="sxs-lookup"><span data-stu-id="9cc69-178">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span></span>

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
