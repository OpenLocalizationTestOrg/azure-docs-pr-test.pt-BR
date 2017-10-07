---
title: "Tutorial: Integração do Azure Active Directory ao Google Apps no Azure | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>Tutorial: integração do Azure Active Directory ao Google Apps

Neste tutorial, você aprenderá como toointegrate Google Apps com o Azure Active Directory (AD do Azure).

Integração do Google Apps com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooGoogle aplicativos
- Você pode habilitar seu usuários tooautomatically get conectado tooGoogle aplicativos (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais informações sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Google Apps, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Google Apps

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="video-tutorial"></a>Tutorial em vídeo
Como tooEnable Single Sign-On tooGoogle aplicativos em 2 minutos:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>Perguntas frequentes
1. **P: Os Chromebooks e outros dispositivos Chrome são compatíveis com o logon único do AD do AD do Azure?**
   
    R: Sim, os usuários são toosign capaz em seus dispositivos Chromebook usando suas credenciais do AD do Azure. Confira este [artigo de suporte do Google Apps](https://support.google.com/chrome/a/answer/6060880) para saber mais sobre o motivo de os usuários receberem uma solicitação por credenciais duas vezes.

2. **P: se habilitar o logon único, será usuários ser capaz de toouse seu toosign de credenciais do AD do Azure em qualquer produto do Google, como Google sala de aula, GMail, Google Drive, YouTube e assim por diante?**
   
    R: Sim, dependendo da [quais aplicativos do Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) escolha tooenable ou desabilitar para sua organização.

3. **P: Posso habilitar o logon único apenas para um subconjunto de meus usuários do Google Apps?**
   
    R: não, ativar o logon único imediatamente requer que todos os seu tooauthenticate de usuários do Google Apps com suas credenciais do AD do Azure. Porque o Google Apps não oferece suporte para vários provedores de identidade, provedor de identidade Olá para o seu ambiente do Google Apps pode ser AD do Azure ou Google – mas não ambos ao Olá simultaneamente.

4. **P: se um usuário está conectado por meio do Windows, são que automaticamente eles autenticam os aplicativos tooGoogle sem obtendo for solicitada uma senha?**
   
    R: Há duas opções para este cenário. Primeiro, os usuários podem entrar em dispositivos com Windows 10 por meio do [Ingresso no Active Directory do Azure](active-directory-azureadjoin-overview.md). Como alternativa, os usuários podem entrar dispositivos Windows que estão tooan ingressado no domínio do Active Directory que tenha sido habilitado para um único logon tooAzure AD por meio do local um [os serviços de Federação do Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) implantação. Ambas as opções exigem etapas tooperform Olá Olá após tooenable tutorial logon único entre o Azure AD e Google Apps.

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar o Google Apps da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-google-apps-from-hello-gallery"></a>Adicionar o Google Apps da Galeria de saudação
integração de Olá tooconfigure do Google Apps para o AD do Azure, você precisa tooadd Google Apps na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd da Galeria de saudação do Google Apps execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Google Apps**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. No painel de resultados de saudação, selecione **Google Apps**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Google Apps, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Google Apps é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Google Apps precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Google Apps.

tooconfigure e teste de logon único do AD do Azure com o Google Apps, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Google Apps](#creating-a-google-apps-test-user)**  -toohave um equivalente do Britta Simon no Google Apps é a representação toohello vinculado AD do Azure do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Google Apps.

**tooconfigure AD do Azure-logon único com o Google Apps, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Google Apps** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. Em Olá **URLs e domínio do Google Apps** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > Esse valor não é real. Atualize o valor de saudação com URL de logon real hello. entre em contato com o hello [equipe de suporte do Google](https://www.google.com/contact/).
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado** e, em seguida, salve o certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. Em Olá **configuração do Google Apps** seção, clique em **configurar o Google Apps** tooopen **configurar o logon** janela. Saudação de cópia **URL de URL de logout, Single Sign-On URL do serviço SAML e alteração de senha** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. Abra uma nova guia no seu navegador e entrar Olá [Console de administração do Google Apps](http://admin.google.com/) usando sua conta de administrador.

8. Clique em **Segurança**. Se você não vir o link hello, podem estar ocultos em Olá **mais controles** menu na parte inferior de saudação da tela hello.
   
    ![Clique em Segurança.][10]

9. Em Olá **segurança** , clique em **configurar logon único (SSO).**
   
    ![Clique em SSO.][11]

10. Execute Olá alterações de configuração a seguir:
   
    ![Configure o SSO][12]
   
    a. Selecione **Configurar SSO com um provedor de identidade de terceiros**.

    b. No **URL da página de entrada** campo no Google Apps, cole o valor de saudação do **o URL de serviço de logon único**, que você copiou do portal do Azure.

    c. Em Olá **URL da página de logout** campo no Google Apps, cole o valor de saudação do **URL de logout**, que você copiou do portal do Azure. 

    d. Em Olá **alterar senha URL** campo no Google Apps, cole o valor de saudação do **alterar senha URL**, que você copiou do portal do Azure. 

    e. No Google Apps para Olá **certificado de verificação**, upload do certificado Olá que você baixou do portal do Azure.

    f. Clique em **Salvar Alterações**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-google-apps-test-user"></a>Criando um usuário de teste do Google Apps

Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no Software de aplicativos do Google. O Google Apps dá suporte ao provisionamento automático, que está habilitado por padrão. Não há nenhuma ação para você nesta seção. Se um usuário não existir no Software de aplicativos do Google, um novo é criado quando você tenta tooaccess Software de aplicativos do Google.

>[!NOTE] 
>Se você precisar toocreate um usuário manualmente, entre em contato com o hello [equipe de suporte do Google](https://www.google.com/contact/).

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooGoogle aplicativos.

![Atribuir usuário][200] 

**tooassign Britta Simon tooGoogle aplicativos, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Google Apps**.

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, tootest seu único-configurações de logon, abra Olá painel de acesso em [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), faça logon na conta de teste hello e clique em **Google Apps** bloco no painel de acesso de saudação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Provisionamento de Usuário](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png