---
title: "Tutorial: Integração do Azure Active Directory ao Marketo | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a>Tutorial: Integração do Azure Active Directory com o Marketo

Neste tutorial, você aprenderá como toointegrate Marketo com o Azure Active Directory (AD do Azure).

Integração do Marketo com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooMarketo
- Você pode habilitar seu usuários tooautomatically get conectado tooMarketo (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Marketo, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Marketo

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Marketo da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-marketo-from-hello-gallery"></a>Adicionando Marketo da Galeria de saudação
integração de saudação tooconfigure do Marketo para o AD do Azure, você precisa tooadd Marketo da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Marketo da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Marketo**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. No painel de resultados de saudação, selecione **Marketo**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Marketo, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Marketo é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Marketo precisa toobe estabelecida.

No Marketo, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Marketo, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Marketo](#creating-a-marketo-test-user)**  -toohave um equivalente do Britta Simon no Marketo é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Marketo.

**tooconfigure AD do Azure-logon único com Marketo, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Marketo** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. Em Olá **Marketo domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://saml.marketo.com/sp`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://login.marketo.com/saml/assertion/\<munchkinid\>`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de resposta e o identificador de real de saudação. Entre em contato com [equipe de suporte do Marketo](http://investors.marketo.com/contactus.cfm) tooget esses valores.
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. Em Olá **Marketo configuração** seção, clique em **configurar Marketo** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. tooget Munchkin Id do aplicativo, faça logon em tooMarketo usando credenciais de administrador e executar as seguintes ações:
   
    a. Faça logon no aplicativo tooMarketo usando credenciais de administrador.
   
    b. Clique em Olá **Admin** botão no painel de navegação superior hello.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Menu de integração toohello navegar e clique em Olá **link Munchkin**.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    d. Copie Olá Id Munchkin mostrada na tela hello e concluir sua URL de resposta no Assistente de configuração de saudação do AD do Azure.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. Olá tooconfigure SSO no aplicativo hello, siga Olá etapas a seguir:
   
    a. Faça logon no aplicativo tooMarketo usando credenciais de administrador.
   
    b. Clique em Olá **Admin** botão no painel de navegação superior hello.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Menu de integração toohello navegar e clique em **Single Sign On**.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    d. Olá tooenable configurações do SAML, clique em **editar** botão.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    e. Configurações de logon único **habilitadas**.
   
    f. Saudação de colar **ID da entidade SAML**, em Olá **ID do emissor** caixa de texto.
   
    g. Em Olá **ID da entidade** caixa de texto, digite a URL hello como `http://saml.marketo.com/sp`.
   
    h. Selecione Olá local de ID de usuário como **elemento identificador de nome**.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > Se o identificador de usuário não é valor UPN e alterar o valor de saudação no guia de atributo hello.
   
    i. Carregar certificado de saudação, que você baixou do Assistente de configuração do AD do Azure. **Salvar** Olá configurações.
   
    j. Edite configurações de redirecionamento páginas hello.
   
    k. Saudação de colar **Single Sign-On URL do serviço SAML** em Olá **URL de logon** caixa de texto.
   
    l. Saudação de colar **URL de logout** em Olá **URL de Logout** caixa de texto.
   
    m. Em Olá **URL de erro**, cópia seu **Marketo instância URL** e clique em **salvar** toosave configurações de botão.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. tooenable Olá SSO para usuários, Olá concluir ações a seguir:
   
    a. Faça logon no aplicativo tooMarketo usando credenciais de administrador.
   
    b. Clique em Olá **Admin** botão no painel de navegação superior hello.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navegue toohello **segurança** menu e clique em **configurações de logon**.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    d. Verificar Olá **exigem SSO** opção e **salvar** Olá configurações.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-marketo-test-user"></a>Criar um usuário de teste do Marketo

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Marketo. Siga essas etapas toocreate um usuário na plataforma do Marketo.

1. Faça logon no aplicativo tooMarketo usando credenciais de administrador.

2. Clique em Olá **Admin** botão no painel de navegação superior hello.
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. Navegue toohello **segurança** menu e clique em **usuários e funções**
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. Clique em Olá **convidar novo usuário** link na guia de usuários Olá
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. Em Olá convidar novo usuário assistente preenchimento Olá informações a seguir
   
    a. Insira o usuário Olá **Email** endereço na caixa de texto de saudação
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    b. Digite hello **nome** na caixa de texto de saudação
   
    c. Digite hello **Sobrenome** na caixa de texto de saudação
   
    d. Clique em **Avançar**

6. Em Olá **permissões** guia, selecione Olá **userRoles** e clique em **Avançar**
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. Clique em Olá **enviar** botão convite de usuário Olá toosend
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. Usuário recebe a notificação por email hello e tem tooclick Olá vincular e altere a conta Olá Olá senha tooactivate. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMarketo.

![Atribuir usuário][200] 

**tooassign Britta Simon tooMarketo, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Marketo**.

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Marketo Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Marketo aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

