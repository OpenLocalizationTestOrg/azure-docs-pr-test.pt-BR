---
title: "Tutorial: Integração do Azure Active Directory ao Mimecast Personal Portal | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Portal pessoal do Mimecast."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a>Tutorial: Integração do Azure Active Directory ao Mimecast Personal Portal

Neste tutorial, você aprenderá como toointegrate Portal pessoal do Mimecast com o Azure Active Directory (AD do Azure).

Integração do Portal pessoal do Mimecast com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooMimecast Portal pessoal
- Você pode habilitar seu usuários tooautomatically get conectado tooMimecast Portal pessoal (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Portal pessoal do Mimecast, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Mimecast Personal Portal com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar Portal pessoal do Mimecast da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a>Adicionar Portal pessoal do Mimecast da Galeria de saudação
integração de saudação tooconfigure do Portal pessoal do Mimecast no AD do Azure, você precisa tooadd Portal pessoal do Mimecast da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Portal pessoal do Mimecast da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Portal pessoal do Mimecast**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. No painel de resultados de saudação, selecione **Portal pessoal do Mimecast**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Mimecast Personal Portal, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Portal pessoal do Mimecast é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Portal pessoal do Mimecast precisa toobe estabelecida.

No Portal pessoal do Mimecast, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Portal pessoal do Mimecast, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Portal pessoal do Mimecast](#creating-a-mimecast-personal-portal-test-user)**  -toohave um equivalente do Britta Simon no Portal pessoal do Mimecast que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de Portal pessoal do Mimecast.

**tooconfigure logon único do AD do Azure com o Portal pessoal do Mimecast, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Portal pessoal do Mimecast** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. Em Olá **URLs e domínio de Portal pessoal do Mimecast** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir: 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente de Portal pessoal do Mimecast](https://www.mimecast.com/customer-success/technical-support/) tooget esses valores. 
 


4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. Em Olá **configuração de Portal pessoal do Mimecast** seção, clique em **configurar Portal pessoal do Mimecast** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. Em outra janela do navegador da Web, faça logon em seu Mimecast Personal Portal como um administrador.

8. Vá muito**serviços \> aplicativos**.
   
    ![Aplicativos](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Aplicativos")

9. Clique em **Perfis de Autenticação**.
   
    ![Perfis de Autenticação](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Perfis de Autenticação")

10. Clique em **Novo Perfil de Autenticação**.
   
    ![Novo Perfil de Autenticação](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "Novo Perfil de Autenticação")

11. Em Olá **o perfil de autenticação** , execute Olá etapas a seguir:
   
    ![Perfil de Autenticação](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Perfil de Autenticação")
   
    a. Em Olá **descrição** caixa de texto, digite um nome para a sua configuração.
   
    b. Selecione **Impor Autenticação SAML para o Mimecast Personal Portal**.
   
    c. Como **Provedor**, selecione **Azure Active Directory**.
   
    d. Em **URL do emissor** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.
   
    e. Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.
   
    f. Em **URL de Logout** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.

    g. Abra o **base 64** codificado certificado baixado do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência, o bloco de notas e, em seguida, cole-o toohello **certificado do provedor de identidade (metadados)** caixa de texto.

    h. Selecione **Permitir Logon Único**.
   
    i. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a>Criando um usuário de teste do Mimecast Personal Portal

Em ordem tooenable AD do Azure toolog usuários no Portal pessoal do Mimecast, eles devem ser provisionados no Portal pessoal do Mimecast. No caso de saudação do Portal pessoal do Mimecast, o provisionamento é uma tarefa manual.

Antes de criar os usuários, você precisa tooregister um domínio.

**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**

1. Logon tooyour **Portal pessoal do Mimecast** como administrador.

2. Vá muito**diretórios \> interno**.
   
    ![Diretórios](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Diretórios")

3. Clique em **Registrar Novo Domínio**.
   
    ![Registrar Novo Domínio](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Registrar Novo Domínio")

4. Depois de criar o novo domínio, clique em **Novo Endereço**.
   
    ![Novo Endereço](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "Novo Endereço")

5. Na caixa de diálogo Olá de novo endereço, executar Olá seguindo as etapas de uma válida do Azure você deseja tooprovision de conta do AD:
   
    ![Salvar](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Salvar")
   
    a. Em Olá **endereço de Email** caixa de texto, tipo **endereço de Email** do usuário hello como  **BrittaSimon@contoso.com** .
    
    b. Em Olá **nome Global** caixa de texto, Olá tipo **username** como **BrittaSimon**.

    c. Em Olá **senha**, e **Confirmar senha** caixas de texto, Olá tipo **senha** do usuário hello.
   
    b. Clique em **Salvar**.

>[!NOTE]
>Você pode usar qualquer outra ferramenta de criação de conta de usuário do Portal pessoal do Mimecast ou APIs fornecidos pelo Portal pessoal do Mimecast tooprovision contas de usuário. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMimecast Portal pessoal.

![Atribuir usuário][200] 

**tooassign Britta Simon tooMimecast Portal pessoal, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Portal pessoal do Mimecast**.

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único
Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Portal pessoal do Mimecast Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Portal pessoal do Mimecast. Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

