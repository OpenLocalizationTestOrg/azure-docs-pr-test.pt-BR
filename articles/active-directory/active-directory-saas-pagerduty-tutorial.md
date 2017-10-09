---
title: "Tutorial: integração do Azure Active Directory com o PagerDuty | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a>Tutorial: integração do Azure Active Directory com o PagerDuty

Neste tutorial, você aprenderá como toointegrate PagerDuty com o Azure Active Directory (AD do Azure).

Integrando PagerDuty com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooPagerDuty
- Você pode habilitar seu usuários tooautomatically get conectado tooPagerDuty (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do Azure AD com PagerDuty, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do PagerDuty habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando PagerDuty da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-pagerduty-from-hello-gallery"></a>Adicionando PagerDuty da Galeria de saudação
integração de saudação tooconfigure do PagerDuty no AD do Azure, você precisa tooadd PagerDuty da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd PagerDuty da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **PagerDuty**, selecione **PagerDuty** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o PagerDuty, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no PagerDuty é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no PagerDuty precisa toobe estabelecida.

No PagerDuty, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do Azure AD com PagerDuty, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do PagerDuty](#create-a-pagerduty-test-user)**  -toohave um equivalente do Britta Simon no PagerDuty é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo PagerDuty.

**tooconfigure AD do Azure-logon único com o PagerDuty, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **PagerDuty** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. Em Olá **PagerDuty domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.pagerduty.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.pagerduty.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente PagerDuty](https://www.pagerduty.com/support/) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. Em Olá **PagerDuty configuração** seção, clique em **configurar PagerDuty** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. Em outra janela do navegador da Web, faça logon em seu site de empresa do Pagerduty como administrador.

8. No menu de saudação na parte superior de saudação, clique em **configurações de conta**.
   
    ![Configurações de Conta](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Configurações de Conta")

9. Clique em **Logon Único**.
   
    ![Logon Único](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Logon Único")

10. Em Olá **habilitar-logon único (SSO)** página, execute Olá etapas a seguir:
   
    ![Habilitar logon único](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Habilitar logon único")
   
    a. Abra seu certificado codificado em base 64 baixado do portal do Azure no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto
  
    b. Em Olá **URL de logon** caixa de texto, colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.
  
    c. Em Olá **URL de Logout** caixa de texto, colar **URL de logout** que você copiou do portal do Azure.
 
    d. Selecione **Ativar Logon Único**.
 
    e. Clique em **Salvar Alterações**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![botão Adicionar de saudação](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-pagerduty-test-user"></a>Criar um usuário de teste do PagerDuty

tooenable AD do Azure usuários toolog em tooPagerDuty, eles devem ser provisionados no PagerDuty.  
No caso de saudação do PagerDuty, o provisionamento é uma tarefa manual.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros Pagerduty usuário conta ou APIs fornecidas pelo Pagerduty tooprovision Azure Active Directory as contas de usuário.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **Pagerduty** locatário.

2. No menu de saudação na parte superior de saudação, clique em **usuários**.

3. Clique em **Adicionar Usuários**.
   
    ![Adicionar Usuários](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Adicionar Usuários")

4.  Em Olá **convidar sua equipe** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Convidar suas equipe](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Convidar suas equipe")

    a. Saudação de tipo **nome e Sobrenome** do usuário como **Britta Simon**. 
   
    b. Digite o endereço de **Email** do usuário, por exemplo, **brittasimon@contoso.com**.
   
    c. Clique em **Adicionar** e depois em **Enviar Convites**.
   
    >[!NOTE]
    >Todos os usuários adicionados receberão um convite toocreate uma conta no PagerDuty.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPagerDuty.

![Atribuir função de usuário Olá][200]

**tooassign Britta Simon tooPagerDuty, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **PagerDuty**.

    ![link do PagerDuty Olá na lista de aplicativos Olá](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco PagerDuty Olá Olá acesso Panelyou deve obter automaticamente assinado em tooyour PagerDuty aplicativo.

Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

