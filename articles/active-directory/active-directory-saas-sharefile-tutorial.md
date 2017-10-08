---
title: "Tutorial: integração do Azure Active Directory com o Citrix ShareFile | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a>Tutorial: integração do Azure Active Directory ao Citrix ShareFile

Neste tutorial, você aprenderá como toointegrate Citrix ShareFile com o Azure Active Directory (AD do Azure).

Integração do Citrix ShareFile com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooCitrix ShareFile.
- Você pode habilitar seu usuários tooautomatically get conectado tooCitrix ShareFile (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do Azure AD com Citrix ShareFile, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Citrix ShareFile

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar Citrix ShareFile da Galeria de saudação
2. Configurar e testar logon único do Azure AD

## <a name="add-citrix-sharefile-from-hello-gallery"></a>Adicionar Citrix ShareFile da Galeria de saudação
integração de saudação tooconfigure do Citrix ShareFile no AD do Azure, você precisa tooadd Citrix ShareFile da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Citrix ShareFile da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Citrix ShareFile**, selecione **Citrix ShareFile** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Lista de resultados do Citrix ShareFile em Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você vai configurar e testar o logon único do Azure AD com o Citrix ShareFile, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Citrix ShareFile é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Citrix ShareFile precisa toobe estabelecida.

No Citrix ShareFile, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Citrix ShareFile, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave um equivalente do Britta Simon no Citrix ShareFile é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo da Citrix ShareFile.

**tooconfigure AD do Azure-logon único com o Citrix ShareFile, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Citrix ShareFile** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. Em Olá **Citrix ShareFile domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.sharefile.com/saml/login`

    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com hello URL de logon real. Entre em contato com [equipe de suporte do cliente do Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html) tooget esse valor. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. Em Olá **configuração da Citrix ShareFile** seção, clique em **configurar Citrix ShareFile** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. Em outra janela do navegador da Web, faça logon em seu site de empresa do **Citrix ShareFile** como administrador.

8. Na barra de ferramentas de saudação na parte superior do hello, clique em **Admin**.

9. No painel de navegação esquerdo hello, selecione **configurar logon único**.
   
    ![Administração de Conta](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Administração de Conta")

10. Em Olá **Single Sign-On / configuração do SAML 2.0** página de diálogo em **configurações básicas**, executar Olá etapas a seguir:
   
    ![Logon Único](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Logon Único")
   
    a. Clique em **Habilitar SAML**.
    
    b. Em **emissor IDP / ID da entidade** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.

    c. Clique em **alteração** toohello próximo **certificado x. 509** campo e, em seguida, upload do certificado Olá baixado do hello portal do Azure.
    
    d. Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.
    
    e. Em **URL de Logout** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.

11. Clique em **salvar** em Olá portal de gerenciamento do Citrix ShareFile.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-citrix-sharefile-test-user"></a>Criar um usuário de teste do Citrix ShareFile

Em ordem tooenable AD do Azure usuários toolog no Citrix ShareFile, eles devem ser provisionados no Citrix ShareFile. No caso de saudação do Citrix ShareFile, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **Citrix ShareFile** locatário.

2. Clique em **Gerenciar Usuários \> Gerenciar Página Inicial dos Usuários \> + Criar Funcionário**.
   
   ![Criar Funcionário](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Criar Funcionário")

3. Em Olá **informações básicas** , execute etapas a seguir:
   
   ![Informações Básicas](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Informações Básicas")
   
   a. Em Olá **endereço de Email** caixa de texto, endereço de email de saudação do tipo do Britta Simon como  **brittasimon@contoso.com** .
   
   b. Em Olá **nome** caixa de texto, tipo **nome** do usuário como **Britta**.
   
   c. Em Olá **Sobrenome** caixa de texto, tipo **Sobrenome** do usuário como **Simon**.

4. Clique em **Adicionar Usuário**.
  
   >[!NOTE]
   >proprietário de conta do AD do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa. Você pode usar qualquer ferramenta de criação outros Citrix ShareFile usuário conta ou APIs fornecidas pelo Citrix ShareFile tooprovision contas de usuário do AD do Azure.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCitrix ShareFile.

![Atribuir função de usuário Olá][200] 

**tooassign tooCitrix Britta Simon ShareFile, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Citrix ShareFile**.

    ![Olá Citrix ShareFile link na lista de aplicativos Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá Citrix ShareFile bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo da Citrix ShareFile.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

