---
title: "aaaWhat é o painel de acesso Olá no Active Directory do Azure? | Microsoft Docs"
description: "Saiba como toouse variações de saudação acessam o painel (navegador da web, aplicativo do Android, aplicativo de iPhone e iPad) tooaccess aplicativos SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 800be6a69f13978c5b88e2fe28a416d4b763656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-access-panel"></a>O que é o painel de acesso Olá?

Painel de acesso de saudação é um portal baseado na web. Ele permite que um usuário com um trabalho ou escola conta em aplicativos tooview e início baseado em nuvem do Azure Active Directory um administrador do AD do Azure-los concedeu acesso ao. Você também pode usar o grupo de autoatendimento e recursos de gerenciamento de aplicativo por meio do painel de acesso de saudação.

Painel de acesso de saudação é separado do hello portal do Azure e faz a não você toohave uma assinatura do Azure.

![Painel de acesso][1]

Painel de acesso Olá permite tooedit algumas de suas configurações de perfil, incluindo Olá a capacidade de:

- Alterar senha Olá associada com uma conta corporativa ou de estudante

- Editar configurações de redefinição de senha

- Editar contato e preferência configurações relacionadas de toomulti-factor authentication (para contas que foram necessário toouse-lo por um administrador)

- Exibir detalhes da conta, como ID de usuário, email alternativo, números de celular e do escritório e dispositivos

- Exibir e iniciar aplicativos de baseado em nuvem que Olá administrador do AD do Azure-los concedeu acesso ao. Para obter mais informações sobre o painel de acesso de saudação da perspectiva dos usuários hello, consulte usando o painel de acesso hello. 

- Autogerenciar grupos. Mais especificamente, o administrador Olá pode criar e gerenciar grupos de segurança e solicitarem associações de grupo de segurança no AD do Azure. Para saber mais, confira [Gerenciamento de grupo de autoatendimento para usuários no Azure AD](active-directory-accessmanagement-self-service-group-management.md) e [Gerenciar seus grupos](active-directory-manage-groups.md).




## <a name="accessing-hello-access-panel"></a>Acessando o painel de acesso Olá

Você pode acessar o painel de acesso Olá Olá seguinte URL em um navegador da web, visite:`http://myapps.microsoft.com`

Se você tiver a identidade visual personalizada configurada para sua página de entrada, você pode carregar essa identidade visual acrescentando final de toohello de domínio da sua organização de saudação URL:`http://myapps.microsoft.com/<your domain>.com`

Nesse caso, você pode usar qualquer nome de domínio ativo ou verificado que foi configurado no portal do Azure.

![Nome de domínio Wingtip Toys][2]  

É necessário toodistribute Olá URL tooall que os usuários que se conectará tooapplications que são integrados ao AD do Azure.

## <a name="authentication"></a>Autenticação

Painel de acesso de saudação tooreach, você deve ser autenticado por meio de uma conta corporativa ou de estudante no AD do Azure. Você pode ser autenticado tooAzure AD diretamente. Como alternativa, se uma organização tiver configurado a federação usando o AD FS (Serviços de Federação do Active Directory) ou outras tecnologias, você pode ser autenticado pelo Windows Server Active Directory.

Se tiver uma assinatura do Azure ou Office 365 e você tiver sido usar Olá portal do Azure ou um aplicativo do Office 365, você pode ver a lista de saudação de aplicativos sem assinar novamente. Se você não são autenticadas são solicitada toosign em usando Olá username e password para sua conta no AD do Azure. Se sua organização configurou a federação, digitar o nome de usuário de saudação é suficiente.

Quando você está autenticado, você pode interagir com aplicativos Olá administrador integrado com o diretório de saudação. toolearn como toointegrate aplicativos com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).

## <a name="web-browser-requirements"></a>Requisitos de navegador da Web

No mínimo, o painel de acesso Olá requer um navegador que ofereça suporte ao JavaScript e CSS habilitou. Para Olá toobe de usuário conectado tooapplications por meio de baseada em senha-logon único (SSO), a extensão do painel de acesso Olá deve ser instalado em seu navegador. extensão de saudação é baixada automaticamente quando você seleciona um aplicativo que está configurado para SSO baseado em senha.

extensão do painel de acesso Hello está atualmente disponível para navegadores do Internet Explorer 8 e posteriores, do Edge, Chrome e Firefox.

## <a name="mobile-app-support"></a>Suporte a aplicativos móveis

equipe do Active Directory do Azure Olá publica Olá meu aplicativo móvel de aplicativos. Quando você instala o aplicativo hello, você pode entrar em aplicativos de SSO baseada em toopassword em dispositivos iOS e Android.

> [!NOTE]
> Você pode entrar no tooapplications que oferecem suporte à Federação com o Azure AD (incluindo Salesforce, Google Apps, Dropbox, caixa, Concur, Workday, Office 365 e mais de 70 outros) em praticamente qualquer navegador da web, em qualquer dispositivo, sem a necessidade de um aplicativo móvel ou plug-in. Todos os outros [experiências do painel de acesso](https://myapps.microsoft.com/) não também exigem Olá toobe de aplicativo móvel meus aplicativos usado em um dispositivo móvel.
>
>

### <a name="my-apps-for-android"></a>Meus aplicativos para Android

Meus aplicativos para Android tem suporte em qualquer dispositivo Android que esteja executando o Android versão 4.1 e posteriores.  
Ele está disponível no hello [loja Google Play](https://play.google.com/store/apps/details?id=com.microsoft.myapps).

![Meus aplicativos para Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>Meus aplicativos para iPhone e iPad

Meus aplicativos para iOS tem suporte em qualquer iPhone ou iPad que esteja executando a versão do iOS 7 e posterior.  
Ele está disponível no hello [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).

![Meus aplicativos para iOS][4]    



## <a name="managed-browser-for-my-apps"></a>Navegador gerenciado para Meus aplicativos

Meus aplicativos também é integrado no hello Managed Browser do Intune. Olá Managed Browser do Intune para dispositivos iOS e Android desempenha um papel fundamental em assegurar que os dados em dispositivos móveis permaneçam seguros. Ele permite exibir e navegar por páginas da web que podem conter informações da empresa e fornece uma experiência de navegação na web segura.  
Localizar o acesso rápido toomy aplicativos em sua home page no navegador gerenciado e em seus marcadores, fornecendo menos clica tooreach qualquer aplicativo que você deseja tooaccess.

Ele está disponível no hello [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) e [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

![Navegador gerenciado para Meus aplicativos][5]    





## <a name="tips-for-testing-hello-user-experience"></a>Dicas para a experiência de usuário de teste Olá

Se você for um administrador do Azure e você entrou toohello portal do Azure usando uma conta no diretório hello, são assinados automaticamente no painel de acesso toohello como sua conta atual. Nesse caso, você pode ver todos os aplicativos que foram atribuídos tooyou.

**tootest como um *diferentes* conta de usuário:**

1. Clique Olá usuário menu no canto superior direito de saudação do hello portal do Azure ou do painel de acesso de saudação e, em seguida, selecione **sair**. 
2. Vá toohello [painel de acesso](http://myapps.microsoft.com).
3. Na página de entrada hello, nome de usuário do tipo hello e senha para conta de saudação em seu diretório, você deseja tootest.


## <a name="starting-applications"></a>Iniciar aplicativos

Vários tipos de aplicativos podem aparecer no painel de acesso de saudação.

### <a name="office-365-applications"></a>Aplicativos do Office 365

Se sua organização estiver usando aplicativos do Office 365 e você está licenciado para eles, aplicativos do Office 365 de saudação aparecem no painel de acesso.

Quando você clica em um bloco de aplicativo para um aplicativo do Office 365, você é redirecionado toohello do aplicativo e automaticamente conectado.

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>Aplicativos da Microsoft e de terceiros configurados com o SSO baseado em federação

O administrador pode adicionar aplicativos na seção Active Directory do portal do Azure de saudação do hello com modo SSO de saudação definido muito**do Azure AD Single Sign-On**. Você só pode ver esses aplicativos se o administrador concedeu explicitamente que acesso toohello aplicativos.

Quando você clica em um bloco para um desses aplicativos, são redirecionadas e automaticamente conectado no aplicativo toohello.

### <a name="password-based-sso-without-identity-provisioning"></a>SSO baseado em senha sem provisionamento de identidade

O administrador pode adicionar aplicativos na seção Active Directory do portal do Azure de saudação do hello com modo SSO de saudação definido muito**baseada em senha Single Sign-On**. Todos os usuários no diretório Olá podem ver todos os aplicativos que foram configurados neste modo.

Olá primeira vez, você clicar em um bloco para um desses aplicativos, são solicitadas tooinstall Olá plug-in do Internet Explorer ou Chrome de SSO de senha. instalação de saudação pode exigir você toorestart seu navegador da web. Quando você retorna toohello painel de acesso e em bloco de aplicativo hello novamente, você será solicitado um nome de usuário e senha para o aplicativo hello. Quando você inseriu o nome de usuário e senha, essas credenciais são armazenadas com segurança e vinculados tooyour conta no AD do Azure.

Olá próxima vez que você clicar em bloco de aplicativo hello, você entrará automaticamente no aplicativo toohello.  
Você não tem tooenter suas credenciais novamente e ou instalar Olá plug-in do SSO de senha.

Se suas credenciais forem alteradas no aplicativo de terceiros de destino hello, você também deve atualizar as credenciais que são armazenadas no AD do Azure. 

**credenciais tooupdate:**

1. Selecione o ícone de saudação no bloco de aplicativo hello.
2. Selecione **atualizar credenciais** tooreenter Olá usuário e senha para Olá aplicativo.


### <a name="password-based-sso-with-identity-provisioning"></a>SSO baseado em senha com provisionamento de identidade

O administrador pode adicionar aplicativos Olá **do Active Directory** seção Olá portal do Azure com o modo SSO Olá definido muito**baseada em senha Single Sign-On**, juntamente com o provisionamento de identidade.

Olá primeira vez, em um bloco de aplicativo para um desses aplicativos, são solicitadas tooinstall Olá **SSO de senha plug-in do Internet Explorer ou Chrome**. instalação de saudação pode exigir você toorestart seu navegador da web.  
Quando você retorna toohello painel de acesso e em bloco de aplicativo hello novamente, você entrará automaticamente no aplicativo toohello.

Alguns aplicativos podem exigir você toochange sua senha em Olá entrar pela primeira vez. Se suas credenciais forem alteradas no aplicativo de terceiros de destino hello, você também deve atualizar credenciais de saudação que são armazenadas no AD do Azure. 

**credenciais tooupdate:**

1. Selecione o ícone de saudação no bloco de aplicativo hello.
2. Selecione **atualizar credenciais** tooreenter Olá usuário e senha para Olá aplicativo.


### <a name="application-with-existing-sso-solutions"></a>Aplicativos com soluções de SSO existentes

tooconfigure SSO para um aplicativo, Olá portal do Azure fornece uma terceira opção chamada **logon único existente**. Essa opção permite que seu administrador toocreate um aplicativo de tooan link e colocá-lo no painel de acesso Olá para os usuários selecionados.

Por exemplo, se um aplicativo for configurado tooauthenticate usuários usando AD FS 2.0, o administrador pode usar o hello **logon único existente** opção toocreate tooit um link no painel de acesso de saudação. Quando você acessa o link hello, são autenticados por meio do AD FS 2.0 ou qualquer aplicativo de saudação de solução SSO existente fornece.


## <a name="next-steps"></a>Próximas etapas

- toosee uma lista de todos os tópicos de gerenciamento de tooapplication relacionados, consulte Olá [índice do artigo para gerenciamento de aplicativos no Active Directory do Azure](active-directory-apps-index.md).
 
- toolearn como toointegrate um aplicativo SaaS no AD do Azure, consulte Olá [lista de tutoriais sobre como aplicativos de SaaS toointegrate](active-directory-saas-tutorial-list.md).
 
- toolearn mais sobre o gerenciamento de aplicativos com o AD do Azure, consulte Olá [Introdução toosingle logon e gerenciar o acesso de aplicativo com o Azure Active Directory](active-directory-appssoaccess-whatis.md).
 
- toolearn mais sobre o provisionamento do usuário, consulte [automatizar o provisionamento de usuário e desprovisionamento aplicativos tooSaaS](active-directory-saas-app-provisioning.md).

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
