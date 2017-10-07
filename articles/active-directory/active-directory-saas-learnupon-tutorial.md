---
title: "Tutorial: integração do Azure Active Directory com o LearnUpon | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a>Tutorial: Integração do Active Directory do Azure com o LearnUpon

Neste tutorial, você aprenderá como toointegrate LearnUpon com o Azure Active Directory (AD do Azure).

Integrando LearnUpon com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooLearnUpon
- Você pode habilitar seu usuários tooautomatically get conectado tooLearnUpon (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com LearnUpon, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do LearnUpon habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando LearnUpon da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-learnupon-from-hello-gallery"></a>Adicionando LearnUpon da Galeria de saudação
integração de saudação tooconfigure de LearnUpon no AD do Azure, você precisa tooadd LearnUpon da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd LearnUpon da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **LearnUpon**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. No painel de resultados de saudação, selecione **LearnUpon**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o LearnUpon, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em LearnUpon é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em LearnUpon precisa toobe estabelecida.

LearnUpon, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com LearnUpon, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste LearnUpon](#creating-a-learnupon-test-user)**  -toohave um equivalente do Britta Simon em LearnUpon é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo LearnUpon.

**tooconfigure AD do Azure-logon único com LearnUpon, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **LearnUpon** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. Em Olá **LearnUpon domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.learnupon.com/saml/consumer`

    > [!NOTE] 
    > Observe que isso não é um valor real hello. Você tem tooupdate esse valor com a URL de resposta real hello. entre em contato com tooget esse valor [a equipe de suporte LearnUpon](https://www.learnupon.com/features/support/).



4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. Em Olá **LearnUpon configuração** seção, clique em **configurar LearnUpon** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. Abra outra instância do navegador e faça logon no LearnUpon com uma conta de administrador. 

8. Clique em Olá **configurações** guia.
   
    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. Clique em **logon único - SAML**e, em seguida, clique em **configurações gerais** tooconfigure configurações do SAML.
   
    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. Em Olá **configurações gerais** , execute Olá etapas a seguir:
   
    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    a. Selecione **Habilitado**.

    b. Selecione **versão** como **2.0**.

    c. Selecione **Ignorar condições** como **Não**.

    d. Em Olá **nome do parâmetro de postagem de Token SAML** caixa de texto, nome de saudação do tipo de solicitação post parâmetro toohello SAML consumidor URL indicado acima que contém a saudação de asserção SAML toobe verificado e é autenticado - por exemplo  **SAMLResponse**.

    e. Em Olá **formato de nome de identificador** texto, o valor do tipo hello indica onde em seus usuários de saudação de asserção SAML identificador (endereço de Email) reside - por exemplo **urn: oasis: nomes: tc: SAML: 1.1 nameid-format: endereço de email**.
  
    f. Em Olá **identificar o local do provedor** caixa de texto, o valor do tipo hello indica onde hello, os usuários são enviados tooif clicarem em seu ícone carregado na sua tela de logon do portal do Azure.
  
    g. Em Olá **sair URL** caixa de texto, colar Olá **URL de logout** que você copiou de saudação portal do Azure.
    
    h. Clique em **gerenciar imprime dedo**e, em seguida, carregar a impressão digital de saudação do seu certificado baixado.

11. Clique em **as configurações do usuário**e, em seguida, executar Olá etapas a seguir:
   
     ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    a. Em Olá **formato do identificador de nome** caixa de texto valor do tipo hello informa qual em seu nome de usuários de asserção SAML Olá reside - por exemplo: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.
  
    b. Em Olá **último nome de identificador de formato** caixa de texto valor do tipo hello informa qual em seu sobrenome de usuários de asserção SAML Olá reside - por exemplo: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-learnupon-test-user"></a>Criar um usuário de teste do LearnUpon

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no LearnUpon. O LearnUpon dá suporte ao provisionamento just-in-time, que é habilitado por padrão.

Não há itens de ação para você nesta seção. Será criado um novo usuário durante uma tentativa tooaccess LearnUpon se ele ainda não existir. [Configuração do logon único do AD do Azure](#configuring-azure-ad-single-single-sign-on).

>[!NOTE]
>Se você precisar toocreate um usuário manualmente, será necessário toocontact [a equipe de suporte LearnUpon](https://www.learnupon.com/features/support/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLearnUpon.

![Atribuir usuário][200] 

**tooassign Britta Simon tooLearnUpon, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **LearnUpon**.

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco LearnUpon Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour LearnUpon aplicativo.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

