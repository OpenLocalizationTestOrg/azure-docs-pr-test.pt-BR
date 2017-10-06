---
title: "Tutorial: Integração do Azure Active Directory ao 15Five | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e 15Five."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 9e531615c16331ce000e285d13d9adce13735a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a>Tutorial: Integração do Active Directory do Azure ao 15Five

Neste tutorial, você aprenderá como toointegrate 15Five com o Azure Active Directory (AD do Azure).

Integrando o 15Five com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso too15Five
- Você pode habilitar seus usuários tooautomatically get conectado too15Five (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o 15Five, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do 15Five

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando 15Five da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-15five-from-hello-gallery"></a>Adicionando 15Five da Galeria de saudação
integração de saudação tooconfigure do 15Five no AD do Azure, você precisa 15Five tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**15Five tooadd da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **15Five**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. No painel de resultados de saudação, selecione **15Five**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o 15Five, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no 15Five é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no 15Five precisa toobe estabelecida.

No 15Five, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o 15Five, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do 15Five](#creating-a-15five-test-user)**  -toohave um equivalente do Britta Simon no 15Five é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do 15Five.

**tooconfigure AD do Azure-logon único com o 15Five, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **15Five** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. Em Olá **15Five domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.15five.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.15five.com/saml2/metadata/`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do 15Five cliente](https://www.15five.com/contact/) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. tooconfigure logon único no **15Five** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do 15Five](https://www.15five.com/contact/).

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-15five-test-user"></a>Criação de um usuário de teste do 15Five

tooenable AD do Azure usuários toolog em too15Five, eles devem ser provisionados no 15Five. No caso do 15Five, o provisionamento é uma tarefa manual.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure provisionamento de usuário, execute Olá etapas a seguir:
1. Faça logon no tooyour **15Five** site da empresa como administrador.

2. Vá muito**gerenciar empresa**.
   
    ![Gerenciar Empresa](./media/active-directory-saas-15five-tutorial/IC784675.png "Gerenciar Empresa")

3. Vá muito**pessoas \> adicionar pessoas**.
   
    ![Pessoas](./media/active-directory-saas-15five-tutorial/IC784676.png "Pessoas")

4. Na seção Adicionar nova pessoa do hello, execute Olá etapas a seguir:
   
    ![Adicionar Nova Pessoa](./media/active-directory-saas-15five-tutorial/IC784677.png "Adicionar Nova Pessoa")
   
    a. Saudação de tipo **nome**, **Sobrenome**, **título**, **endereço de Email** de uma conta válida do Active Directory do Azure que você deseja tooprovision em Olá relacionados caixas de texto.

    b. Clique em **Concluído**.
   
    > [!NOTE]
    > Olá conta do AD do Azure detentor recebe um email com uma conta de saudação do link tooconfirm antes de se tornar ativa.
   
### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso too15Five.

![Atribuir usuário][200] 

**tooassign Britta Simon too15Five, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **15Five**.

    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco 15Five Olá Olá painel de acesso, você deve obter a página de logon do aplicativo do 15Five.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

