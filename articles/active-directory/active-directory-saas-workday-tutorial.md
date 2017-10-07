---
title: "Tutorial: integração do Azure Active Directory com o Workday | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Workday."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a>Tutorial: Integração do Active Directory do Azure com o Workday

Neste tutorial, você aprenderá como toointegrate dia de trabalho com o Azure Active Directory (AD do Azure).

Integrando o Workday com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooWorkday
- Você pode habilitar seu usuários tooautomatically get conectado tooWorkday (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Workday, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Workday habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Workday da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-workday-from-hello-gallery"></a>Adicionando Workday da Galeria de saudação
tooconfigure Olá integração da Workday AD do Azure, você precisa tooadd Workday na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Workday da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Workday**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. No painel de resultados de saudação, selecione **Workday**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Workday com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Workday é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Workday precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Workday.

tooconfigure e teste de logon único do AD do Azure com o Workday, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Workday](#creating-a-workday-test-user)**  -toohave um equivalente do Britta Simon no Workday é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de dia de trabalho.

**tooconfigure AD do Azure-logon único com o Workday, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Workday** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. Em Olá **domínio Workday e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    a. Em Olá **URL de logon** texto, o valor do tipo hello como:`https://impl.workday.com/<tenant>/login-saml2.htmld`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://impl.workday.com/<tenant>/login-saml.htmld`

    > [!NOTE] 
    > Esses valores não são Olá real. Atualize esses valores com URL de logon real hello e a URL de resposta. Sua URL de resposta deve ter um subdomínio, por exemplo: www, wd2, wd3, wd3-impl, wd5, wd5-impl. O uso de algo como "*http://www.myworkday.com*" funciona, mas "*http://myworkday.com*", não. Entre em contato com [equipe de suporte do Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) tooget esses valores. 
 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. Em Olá **Workday configuração** seção, clique em **configurar Workday** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS>
7. Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Workday como um administrador.

8. Vá muito**Menu \> Workbench**.
   
    ![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")

9. Vá muito**administração da conta**.
   
    ![Administração de Conta](./media/active-directory-saas-workday-tutorial/IC782924.png "Administração de Conta")

10. Vá muito**Editar configuração de locatário – segurança**.
   
    ![Editar segurança de locatário](./media/active-directory-saas-workday-tutorial/IC782925.png "Editar segurança de locatário")

11. Em Olá **URLs de redirecionamento** , execute Olá etapas a seguir:
   
    ![URLs de redirecionamento](./media/active-directory-saas-workday-tutorial/IC7829581.png "URLs de redirecionamento")
   
    a. Clique em **Adicionar Linha**.
   
    b. Em Olá **URL de redirecionamento de logon** caixa de texto e hello **URL de redirecionamento móvel** caixa de texto, Olá tipo **URL de logon** você inseriu Olá **Workday domínio e URLs** seção Olá portal do Azure.
   
    c. Em Olá portal do Azure, Olá **configurar o logon** janela, Olá cópia **URL de logout**e, em seguida, cole-Olá **URL de redirecionamento de Logout** caixa de texto.
   
    d.  Em **ambiente** caixa de texto Nome do tipo hello ambiente.  

    >[!NOTE]
    > Olá valor do atributo de ambiente hello está ligado toohello valor saudação do URL de locatário:  
    >-Se nome de domínio de saudação do URL do locatário do Workday Olá começa com impl por exemplo: *https://impl.workday.com/\<locatário\>/login-saml2.htmld*), Olá **ambiente** atributo deve ser definido como tooImplementation.  
    >-Se o nome de domínio Olá começa com outra coisa, você precisa toocontact [equipe de suporte do Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) tooget Olá correspondência **ambiente** valor.

12. Em Olá **instalação do SAML** , execute Olá etapas a seguir:
   
    ![Instalação do SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Instalação do SAML")
   
    a.  Selecione **Habilitar Autenticação SAML**.
   
    b.  Clique em **Adicionar Linha**.

13. Olá seção provedores de identidade SAML, execute Olá etapas a seguir:
   
    ![Provedores de Identidade SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "Provedores de Identidade SAML")
   
    a. Na caixa de texto de nome do provedor de identidade hello, digite um nome de provedor (por exemplo: *SPInitiatedSSO*).
   
    b. Em Olá portal do Azure, Olá **configurar o logon** janela, Olá cópia **ID da entidade SAML** valor e, em seguida, cole-Olá **emissor** caixa de texto.
   
    c. Selecione **Habilitar Logoff Iniciado pelo Workday**.
   
    d. Em Olá portal do Azure, Olá **configurar o logon** janela, Olá cópia **URL de logout** valor e, em seguida, cole-o em Olá **URL de solicitação de Logout** caixa de texto.

    e. Clique em **Certificado de Chave Pública do Provedor de Identidade** e em **Criar**. 

    ![Criar](./media/active-directory-saas-workday-tutorial/IC782928.png "Criar")

    f. Clique em **Criar Chave Pública x509**. 

    ![Criar](./media/active-directory-saas-workday-tutorial/IC782929.png "Criar")


14. Em Olá **exibir chave pública x509** , execute Olá etapas a seguir: 
   
    ![Exibir chave pública x509](./media/active-directory-saas-workday-tutorial/IC782930.png "Exibir chave pública x509") 
   
    a. Em Olá **nome** caixa de texto, digite um nome para o certificado (por exemplo: *PPE\_SP*).
   
    b. Em Olá **válido de** caixa de texto, Olá de tipo válido do valor de atributo do seu certificado.
   
    c.  Em Olá **válido até** caixa de texto valor do tipo hello tooattribute válido do seu certificado.
   
    > [!NOTE]
    > Você pode obter Olá válido de data e Olá toodate válida do certificado Olá baixado clicando duas vezes nele.  Olá datas são listadas sob Olá **detalhes** guia.
    > 
    >
   
    d.  Abra seu certificado codificado em base 64 no bloco de notas e, em seguida, Olá de copiar conteúdo dele.
   
    e.  Em Olá **certificado** caixa de texto, conteúdo de saudação colar da área de transferência.
   
    f.  Clique em **OK**.

15. Execute Olá etapas a seguir: 
   
    ![Configuração de SSO](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "Configuração de SSO")
   
    a.  Habilitar Olá **x509 par de chaves particular**.
   
    b.  Em Olá **ID do provedor de serviço** caixa de texto, tipo **http://www.workday.com**.
   
    c.  Selecione **Habilitar a Autenticação do SAML Iniciada por SP**.
   
    d.  Em Olá portal do Azure, Olá **configurar o logon** janela, Olá cópia **Single Sign-On URL do serviço SAML** valor e, em seguida, cole-o em Olá **URL do serviço IdP SSO** caixa de texto.
   
    e. Selecione **Não Esvazie a Solicitação de Autenticação iniciada por SP**.
   
    f. Para **Solicitação de Método de Autenticação de Assinatura** , selecione **SHA256**. 
   
    ![Método de assinatura da solicitação de autenticação](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Método de assinatura da solicitação de autenticação") 
   
    g. Clique em **OK**. 
   
    ![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE>

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
>

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-workday-test-user"></a>Criação de um usuário de teste do Workday

tooget um usuário de teste provisionado no Workday, você precisa Olá toocontact [equipe de suporte do Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html).
Olá [equipe de suporte do Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) cria usuário Olá para você.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWorkday.

![Atribuir usuário][200] 

**tooassign Britta Simon tooWorkday, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Workday**.

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso. Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Provisionamento de Usuário](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

