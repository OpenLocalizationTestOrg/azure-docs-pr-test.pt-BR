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
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a>B2C de diretório ativo do Azure: Fornecer tooconsumers se inscrever e fazer logon com contas do Facebook
## <a name="create-a-facebook-application"></a>Criar um aplicativo do Facebook
toouse Facebook como provedor de identidade no B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo do Facebook e fornecê-lo com os parâmetros de saudação à direita. É necessário um toodo de conta do Facebook isso. Se você não tiver uma, poderá obtê-la em [https://www.facebook.com/](https://www.facebook.com/).

1. Vá toohello [Facebook para desenvolvedores](https://developers.facebook.com/) as credenciais de conta de site e entre com o Facebook.
2. Se você ainda não tiver feito isso, será necessário tooregister como um desenvolvedor de Facebook. toodo, clique **registrar** (na Olá canto superior direito da página de saudação), aceite as políticas do Facebook e concluir as etapas de registro de saudação.
3. Clique em **Meus Aplicativos** e em **Adicionar um Novo Aplicativo**. 
4. No formulário de hello, forneça um **nome de exibição** uma opção válida **Contact Email**.
5. Clique em **Criar ID de Aplicativo**. Isso pode exigir políticas de plataforma do Facebook tooaccept e concluir uma verificação de segurança on-line.
6. Na coluna esquerda da saudação, clique em **configurações** e, em seguida, selecione **básica** se já não foi selecionada.
7. Selecione uma **Categoria**. 
8. Clique em **+Adicionar Plataforma** e selecione **Site**.
   
    ![Facebook - Configurações](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - Configurações - Site](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. Digite `https://login.microsoftonline.com/` em Olá **URL do Site** campo e, em seguida, clique em **salvar alterações** final Olá Olá página.
   
    ![Facebook - URL do Site](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. Copie o valor de saudação do **ID do aplicativo**. Clique em **Mostrar** e copie o valor de saudação do **segredo do aplicativo**. Você precisará de ambos tooconfigure Facebook como provedor de identidade em seu locatário. **Segredo do Aplicativo** é uma credencial de segurança importante.
   
    ![Facebook - ID do Aplicativo e Segredo do Aplicativo](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. Clique em **+ adicionar produto** Olá navegação esquerdo e, em seguida, Olá **Set Up** botão para **logon do Facebook**.
   
    ![Facebook - Logon no Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. Clique em **configurações** na barra de navegação direita em Olá **logon do Facebook**

    ![Facebook - configurações de Logon no Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. Digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **URIs de redirecionamento OAuth válido** campo Olá **configurações do cliente OAuth** seção. Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com). Clique em **salvar alterações** final Olá Olá página.
    
    ![Facebook - URI de Redirecionamento de OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. toomake seu aplicativo Facebook utilizável por B2C do Azure AD, você precisa toomake publicamente disponível. Você pode fazer isso clicando em **revisão de aplicativo** em Olá barra de navegação esquerda e por saudação de ativação do comutador na parte superior de saudação da página de saudação muito**Sim** e clicando em **confirmar**.
    
    ![Facebook - Público do aplicativo](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a>Configurar o Facebook como um provedor de identidade no seu locatário
1. Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.
2. Na folha de recursos Olá B2C, clique em **provedores de identidade**.
3. Clique em **+ adicionar** na parte superior de saudação da folha de saudação.
4. Forneça um amigável **nome** para configuração do provedor de identidade hello. Por exemplo, insira “Facebook”.
5. Clique em **Tipo de provedor de identidade**, selecione **Facebook** e clique em **OK**.
6. Clique em **configurar esse provedor de identidade** e digite Olá ID e o aplicativo segredo do aplicativo (da saudação aplicativo do Facebook que você criou anteriormente) no hello **ID do cliente** e **segredo do cliente**campos respectivamente.
7. Clique em **Okey**e, em seguida, clique em **criar** toosave sua configuração do Facebook.

> [!NOTE]
> Adicionando um **provedor de identidade** tooyour locatário não modifica as políticas existentes. Lembre-se de tooupdate suas políticas, incluindo o provedor de identidade Olá que você acabou de criar.
>