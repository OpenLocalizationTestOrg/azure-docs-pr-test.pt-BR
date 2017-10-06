---
title: "Tutorial: integração do Azure Active Directory com o Humanity | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e humanidade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a>Tutorial: integração do Azure Active Directory com o Humanity

Neste tutorial, você aprenderá como toointegrate humanidade com o Azure Active Directory (AD do Azure).

Integrando humanidade AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooHumanity
- Você pode habilitar seu usuários tooautomatically get conectado tooHumanity (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com humanidade, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Humanity habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando humanidade da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-humanity-from-hello-gallery"></a>Adicionando humanidade da Galeria de saudação
integração de saudação tooconfigure da humanidade no AD do Azure, você precisa tooadd humanidade na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd humanidade da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **humanidade**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. No painel de resultados de saudação, selecione **humanidade**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Humanity, com base em uma usuária de teste chamada "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em humanidade é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em humanidade precisa toobe estabelecida.

Humanidade, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com humanidade, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste humanidade](#creating-a-humanity-test-user)**  -toohave um equivalente do Britta Simon na humanidade que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo humanidade.

**tooconfigure AD do Azure-logon único com humanidade, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **humanidade** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. Em Olá **humanidade domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://company.humanity.com/includes/saml/`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://company.humanity.com/app/`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte de cliente humanidade](https://www.humanity.com/support/) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. Em Olá **humanidade configuração** seção, clique em **configurar humanidade** tooopen **configurar o logon** janela. Saudação de cópia **SAML Single Sign-On URL do serviço e a URL de logout** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. Em uma janela do navegador web diferente, faça logon no tooyour **humanidade** site da empresa como um administrador.

8. No menu de saudação na parte superior de saudação, clique em **Admin**.
   
    ![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")

9. Em **Integração**, clique em **Logon Único**.
   
    ![Logon Único](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Logon Único")

10. Em Olá **Single Sign-On** , execute Olá etapas a seguir:
   
    ![Logon Único](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Logon Único")
   
    a. Selecione **SAML Habilitado**.

    b. Selecione **Permitir Logon de Senha**.

    c. Saudação de colar **Single Sign-On URL do serviço SAML** valor em Olá **URL do emissor SAML** caixa de texto.

    d. Saudação de colar **URL de logout** valor em Olá **URL de Logout remoto** caixa de texto.
   
    e. Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto.

11. Clique em **Salvar Configurações**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-humanity-test-user"></a>Criar um usuário de teste do Humanity

Em ordem tooenable AD do Azure usuários toolog em tooHumanity, eles devem ser provisionados no humanidade. No caso de saudação de humanidade, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **humanidade** site da empresa como um administrador.

2. Clique em **Administrador**.
   
    ![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")

3. Clique em **Equipe**.
   
    ![Equipe](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Equipe")

4. Em **Ações**, clique em **Adicionar Funcionários**.
   
    ![Adicionar Funcionários](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Adicionar Funcionários")

5. Em Olá **adicionar funcionários** , execute Olá etapas a seguir:
   
    ![Salvar Funcionários](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Salvar Funcionários")
   
    a. Saudação de tipo **nome**, **Sobrenome**, e **Email** de uma conta válida do AAD você deseja tooprovision em Olá relacionados caixas de texto.

    b. Clique em **Salvar Funcionários**.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros humanidade usuário conta ou APIs fornecidas pelo humanidade tooprovision contas de usuário do AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHumanity.

![Atribuir usuário][200] 

**tooassign Britta Simon tooHumanity, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **humanidade**.

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco humanidade Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de humanidade.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

