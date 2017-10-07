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
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a>Como desenvolvedor de tooauthorize contas usando o Azure Active Directory B2C no gerenciamento de API do Azure
## <a name="overview"></a>Visão geral
O Azure Active Directory B2C é uma solução de gerenciamento de identidade na nuvem para os seus aplicativos móveis e Web voltados para o consumidor. Você pode usá-lo portal do desenvolvedor do tooyour toomanage acesso. Este mostra guia Olá configuração necessária no seu toointegrate do serviço de gerenciamento de API com o Azure Active Directory B2C. Para obter informações sobre como habilitar o portal do desenvolvedor toohello acesso usando clássico do Azure Active Directory, consulte [como desenvolvedor tooauthorize contas usando Active Directory do Azure].

> [!NOTE]
> toocomplete Olá etapas neste guia, você deve primeiro ter um toocreate de locatário do Azure Active Directory B2C um aplicativo. Além disso, você precisa de políticas de inscrição e entrar toohave pronto. Para saber mais, veja [Visão geral do Azure Active Directory B2C].

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a>Autorizar contas de desenvolvedor usando o Azure Active Directory B2C

1. tooget iniciado, clique em **portal do publicador** no portal do Azure para seu serviço de gerenciamento de API de saudação. Isso leva toohello portal do publicador de gerenciamento de API.

   ![Portal do editor][api-management-management-console]

   > [!NOTE]
   > Se você ainda não criou uma instância de serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao tutorial do gerenciamento de API do Azure][Get started with Azure API Management].

2. Em Olá **gerenciamento de API** menu, clique em **segurança**. Em Olá **identidades** guia, escolha **do Azure Active Directory B2C**.

  ![Identidades externas 1][api-management-howto-aad-b2c-security-tab]

3. Anote Olá **URL de redirecionamento** e passar tooAzure B2C do Active Directory no portal do Azure de saudação.

  ![Identidades externas 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. Clique em Olá **aplicativos** botão.

  ![Registrar um novo aplicativo 1][api-management-howto-aad-b2c-portal-menu]

5. Clique em Olá **adicionar** botão aplicativo toocreate um novo do Azure Active Directory B2C.

  ![Registrar um novo aplicativo 2][api-management-howto-aad-b2c-add-button]

6. Em Olá **novo aplicativo** folha, insira um nome para o aplicativo hello. Escolha **Sim** em **API da Web do aplicativo Web**e escolha **Sim** em **permitir fluxo implícito**. Então Olá cópia **URL de redirecionamento** de saudação **do Azure Active Directory B2C** seção Olá **identidades** guia no portal do publicador hello e cole-a saudação **URL de resposta** caixa de texto.

  ![Registrar um novo aplicativo 3][api-management-howto-aad-b2c-app-details]

7. Clique em Olá **criar** botão. Quando o aplicativo hello é criado, ela aparece no hello **aplicativos** folha. Clique em toosee de nome de aplicativo hello seus detalhes.

  ![Registrar um novo aplicativo 4][api-management-howto-aad-b2c-app-created]

8. De saudação **propriedades** folha, Olá cópia **ID do aplicativo** toohello área de transferência.

  ![ID do aplicativo 1][api-management-howto-aad-b2c-app-id]

9. Alternar o portal do publicador toohello back e cole ID Olá Olá **Id do cliente** caixa de texto.

  ![ID do aplicativo 2][api-management-howto-aad-b2c-client-id]

10. Toohello back portal do Azure, clique Olá **chaves** botão e, em seguida, clique em **gerar chave**. Clique em **salvar** toosave Olá Olá de configuração e exibição **chave do aplicativo**. Copiar Olá chave toohello área de transferência.

  ![Chave do aplicativo 1][api-management-howto-aad-b2c-app-key]

11. Switch back toohello publicador portal e colar Olá chave em Olá **segredo do cliente** caixa de texto.

  ![Chave do aplicativo 2][api-management-howto-aad-b2c-client-secret]

12. Especificar nome de domínio de saudação do locatário de saudação do Azure Active Directory B2C em **permitido locatário**.

  ![Locatário permitido][api-management-howto-aad-b2c-allowed-tenant]

13. Especificar Olá **inscrição política** e **Signin política**. Opcionalmente, você também pode fornecer Olá **a política de edição de perfil** e **política de redefinição de senha**.

  ![Políticas][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > Para saber mais sobre políticas, veja [Azure Active Directory B2C: estrutura de política extensível].

14. Depois que você especificou as configurações desejadas hello, clique em **salvar**.

  Depois de saudação alterações são salvas, os desenvolvedores serão toocreate capaz de novas contas e entrar no portal do desenvolvedor toohello usando o Azure Active Directory B2C.

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a>Inscrever-se para uma conta de desenvolvedor usando o Azure Active Directory B2C

1. toosign uma conta de desenvolvedor usando o Azure Active Directory B2C, abra uma nova janela do navegador e acesse o portal do desenvolvedor toohello. Clique em Olá **inscrever** botão.

   ![Portal do desenvolvedor 1][api-management-howto-aad-b2c-dev-portal]

2. Escolha toosign com **do Azure Active Directory B2C**.

   ![Portal do desenvolvedor 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. Você é redirecionado toohello inscrição política que você configurou na seção anterior hello. Escolha toosign usando seu endereço de email ou uma de suas contas sociais existentes.

   > [!NOTE]
   > Se o Azure Active Directory B2C é Olá única opção que é habilitada em Olá **identidades** guia no portal do publicador hello, você será redirecionado toohello inscrição política diretamente.

   ![Portal do desenvolvedor][api-management-howto-aad-b2c-dev-portal-b2c-options]

   Quando Olá inscrição for concluída, você estará toohello back redirecionado portal do desenvolvedor. Agora você está conectado no portal do desenvolvedor toohello para sua instância de serviço de gerenciamento de API.

    ![Registro concluído][api-management-registration-complete]

## <a name="next-steps"></a>Próximas etapas

*  [Visão geral do Azure Active Directory B2C]
*  [Azure Active Directory B2C: estrutura de política extensível]
*  [Usar a conta da Microsoft como provedor de identidade no Azure Active Directory B2C]
*  [Usar a conta do Google como provedor de identidade no Azure Active Directory B2C]
*  [Usar a conta do Linkedin como provedor de identidade no Azure Active Directory B2C]
*  [Usar a conta do Facebook como provedor de identidade no Azure Active Directory B2C]




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
