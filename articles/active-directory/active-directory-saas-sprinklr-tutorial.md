---
title: "Tutorial: Integração do Azure Active Directory ao Sprinklr | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a>Tutorial: Integração do Active Directory do Azure com o Sprinklr

Neste tutorial, você aprenderá como toointegrate Sprinklr com o Azure Active Directory (AD do Azure).

Integrando o Sprinklr com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSprinklr
- Você pode habilitar seu usuários tooautomatically get conectado tooSprinklr (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Sprinklr, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Sprinklr

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Sprinklr da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-sprinklr-from-hello-gallery"></a>Adicionando Sprinklr da Galeria de saudação
integração de saudação tooconfigure do Sprinklr no AD do Azure, você precisa tooadd Sprinklr da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Sprinklr da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Sprinklr**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. No painel de resultados de saudação, selecione **Sprinklr**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Sprinklr, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá sprinklr é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação sprinklr precisa toobe estabelecida.

Sprinklr, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Sprinklr, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Sprinklr](#creating-a-sprinklr-test-user)**  -toohave um equivalente de Britta Simon sprinklr é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Sprinklr.

**tooconfigure AD do Azure-logon único com o Sprinklr, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Sprinklr** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. Em Olá **Sprinklr domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.sprinklr.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.sprinklr.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualize o valor de saudação com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente Sprinklr](https://www.sprinklr.com/contact-us/) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. Em Olá **Sprinklr configuração** seção, clique em **configurar Sprinklr** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

7. Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Sprinklr como um administrador.

8. Vá muito**administração \> configurações**.
   
    ![Administração](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administração")

9. Vá muito**gerenciar parceiro \> o logon único** no painel esquerdo do hello.
   
    ![Gerenciar Parceiro](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Gerenciar Parceiro")

10. Clique em **+Adicionar Logons Únicos**.
   
    ![Logons Únicos](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Logons Únicos")

11. Em Olá **de logon único** página, execute Olá etapas a seguir:
   
    ![Logons Únicos](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Logons Únicos")

    a. Em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: *WAADSSOTest*).

    b. Selecione **Habilitado**.

    c. Selecione **Usar novo Certificado de SSO**.
             
    e. Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado do provedor de identidade** caixa de texto.

    f. Saudação de colar **ID da entidade SAML** valor que você copiou do Portal do Azure em Olá **Id da entidade** caixa de texto.

    g. Saudação de colar **Single Sign-On URL do serviço SAML** valor que você copiou do Portal do Azure em Olá **URL de logon do provedor de identidade** caixa de texto.

    h. Saudação de colar **URL de logout** valor que você copiou do Portal do Azure em Olá **URL de Logout do provedor de identidade** caixa de texto.
     
    i. Para **Tipo de ID de Usuário do SAML**, selecione **A declaração contém o nome de usuário de sprinklr.com do Usuário**.

    j. Como **local de ID de usuário SAML**, selecione **ID de usuário está no elemento de identificador de nome de saudação do hello declaração assunto**.

    k. Clique em **Salvar**.
       
    ![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-sprinklr-test-user"></a>Criar um usuário de teste do Sprinklr

1. Faça logon no tooyour site da empresa Sprinklr como um administrador.

2. Vá muito**administração \> configurações**.
   
    ![Administração](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administração")

3. Vá muito**gerenciar cliente \> usuários** no painel esquerdo do hello.
   
    ![Configurações](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Configurações")

4. Clique em **Adicionar Usuário**.
   
    ![Configurações](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Configurações")

5. Em Olá **Editar usuário** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Editar usuário](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Editar usuário") 

    a. Em Olá **Email**, **nome** e **Sobrenome** caixas de texto, informações de saudação do tipo de uma conta de usuário do AD do Azure você deseja tooprovision.

    b. Selecione **Senha Desabilitada**.

    c. Selecione **Idioma**.

    d. Selecione **Tipo de Usuário**.

    e. Clique em **Atualizar**.
   
     >[!IMPORTANT]
     >**Senha desabilitada** deve ser selecionada tooenable um toolog de usuário por meio de um provedor de identidade. 
     
6. Vá muito**função**e, em seguida, executar Olá etapas a seguir:
   
    ![Funções de Parceiro](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Funções de Parceiro")

    a. De saudação **Global** lista, selecione **todos os\_permissões**.  

    b. Clique em **Atualizar**.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros Sprinklr usuário conta ou APIs fornecidas pelo Sprinklr tooprovision contas de usuário do AD do Azure. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSprinklr.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSprinklr, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Sprinklr**.

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Sprinklr Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Sprinklr aplicativo para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

