---
title: "Tutorial: Integração do Azure Active Directory ao Slack | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e margem de atraso."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a>Tutorial: Integração do Active Directory do Azure com o Slack

Neste tutorial, você aprenderá como toointegrate atraso com o Azure Active Directory (AD do Azure).

Integrando a margem de atraso do AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSlack
- Você pode habilitar seu usuários tooautomatically get conectado tooSlack (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com atraso, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Slack

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando o atraso da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-slack-from-hello-gallery"></a>Adicionando o atraso da Galeria de saudação
integração de saudação tooconfigure de atraso no AD do Azure, você precisa tooadd margem de atraso na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd atraso da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Slack**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. No painel de resultados de saudação, selecione **Slack**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Slack, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na margem de atraso é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em atraso precisa toobe estabelecida.

Margem de atraso, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com atraso, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Slack](#creating-a-slack-test-user)**  -toohave um equivalente do Britta Simon na margem de atraso é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo a margem de atraso.

**tooconfigure AD do Azure-logon único com atraso, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Slack** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. Em Olá **margem de atraso do domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.slack.com`

    b. Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://slack.com`

    > [!NOTE] 
    > Olá valor não é real. Você tem valor de saudação tooupdate com hello real URL de logon. Entre em contato com [a equipe de suporte de atraso](https://slack.com/help/contact) tooget valor de saudação
     
4. Margem de atraso aplicativo espera asserções SAML de saudação em um formato específico. Configure Olá declarações para esse aplicativo a seguir. Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo. Olá captura de tela a seguir mostra um exemplo.
    
    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, selecione **user.mail** como **identificador de usuário** e para cada linha mostrado na tabela de saudação abaixo, execute Olá etapas a seguir:
    
    | Nome do atributo | Valor do atributo |
    | --- | --- |
    | first_name | user.givenname |
    | last_name | user.surname |
    | User.Email | user.mail |  
    | User.Username | user.userprincipalname |

    a. Clique em **atributo** tooopen **Editar atributo** caixa de diálogo caixa e executar Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    a. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    b. De saudação **valor** lista, o valor do atributo select Olá mostrado para aquela linha.
    
    c. Clique em **OK**

6. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. Em Olá **atraso configuração** seção, clique em **configurar atraso** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  Em uma janela de navegador web diferente, faça logon no site da empresa margem de atraso de tooyour como um administrador.

10.  Navegue muito**AD do Microsoft Azure** vá muito**as configurações de equipe**.

     ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  Em Olá **as configurações de equipe** seção, clique em Olá **autenticação** guia e, em seguida, clique em **alterar configurações**.

     ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. Em Olá **configurações de autenticação SAML** caixa de diálogo, executar Olá etapas a seguir:

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    a.  Em Olá **SAML 2.0 ponto de extremidade (HTTP)** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.

    b.  Em hello **emissor do provedor de identidade** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.

    c.  Abra o arquivo de certificado baixado no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado público** caixa de texto.

    d. Configure Olá acima três configurações conforme apropriado para sua equipe de margem de atraso. Para obter mais informações sobre configurações de hello, localizar o hello **guia de configuração de SSO do atraso** aqui. `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    e.  Clique em **Salvar Configuração**.
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-slack-test-user"></a>Criar um usuário de teste do Slack

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon em atraso. O Slack dá suporte ao provisionamento just-in-time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Um novo usuário é criado durante uma tentativa tooaccess margem de atraso se ele ainda não existir.

> [!NOTE]
> Se você precisar toocreate um usuário manualmente, será necessário tooContact [a equipe de suporte de atraso](https://slack.com/help/contact).

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSlack.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSlack, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Slack**.

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco de margem de atraso de saudação em Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de margem de atraso.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

