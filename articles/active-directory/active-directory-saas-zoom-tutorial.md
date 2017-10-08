---
title: "Tutorial: Integração do Azure Active Directory com o Zoom | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Zoom."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 623a1f428ad1f0aa2c8205b79d61720cad5fc6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a>Tutorial: Integração do Active Directory do Azure com o Zoom

Neste tutorial, você aprenderá como toointegrate Zoom com o Azure Active Directory (AD do Azure).

Integrando o Zoom com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooZoom.
- Você pode habilitar seu usuários tooautomatically get conectado tooZoom (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração de tooconfigure AD do Azure com Zoom, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Zoom habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. A adição de Zoom da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-zoom-from-hello-gallery"></a>A adição de Zoom da Galeria de saudação
integração de saudação tooconfigure de Zoom no AD do Azure, você precisa tooadd Zoom na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Zoom da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Zoom**, selecione **Zoom** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Aplicar zoom na lista de resultados de saudação](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Zoom, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Zoom é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e hello relacionados ao usuário no Zoom necessidades toobe estabelecida.

Zoom, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Zoom, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de Zoom](#create-a-zoom-test-user)**  -toohave um equivalente do Britta Simon de Zoom que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de Zoom.

**tooconfigure logon único do AD do Azure com Zoom, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Zoom** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. Em Olá **domínio Zoom e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.zoom.us`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.zoom.us`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte de cliente Zoom](https://support.zoom.us/hc) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. Em Olá **configuração Zoom** seção, clique em **configurar Zoom** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. Em uma janela de navegador web diferente, faça logon no site da empresa Zoom tooyour como um administrador.

8. Clique em Olá **Single Sign-On** guia.
   
    ![Guia Logon único](./media/active-directory-saas-zoom-tutorial/IC784700.png "Logon único")

9. Clique em Olá **controle de segurança** guia e, em seguida, acesse toohello **Single Sign-On** configurações.

10. Olá seção de logon único, execute Olá etapas a seguir:
   
    ![Seção Logon único](./media/active-directory-saas-zoom-tutorial/IC784701.png "Logon único")
   
    a. Em Olá **URL da página de entrada** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.
   
    b. Em Olá **URL da página de logout** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.
     
    c. Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado do provedor de identidade** caixa de texto.

    d. Em hello **emissor** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure. 

    e. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-zoom-test-user"></a>Criar um usuário de teste do Zoom

Em ordem tooenable AD do Azure usuários toolog em tooZoom, eles devem ser provisionados no Zoom. No caso de saudação de Zoom, o provisionamento é uma tarefa manual.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision uma conta de usuário, execute Olá etapas a seguir:

1. Faça logon no tooyour **Zoom** site da empresa como um administrador.
 
2. Clique em Olá **gerenciamento de conta** guia e, em seguida, clique em **gerenciamento de usuário**.

3. No hello seção Gerenciamento de usuário, clique em **adicionar usuários**.
   
    ![Gerenciamento de usuário](./media/active-directory-saas-zoom-tutorial/IC784703.png "Gerenciamento de usuário")

4. Em Olá **adicionar usuários** página, execute Olá etapas a seguir:
   
    ![Adicionar Usuários](./media/active-directory-saas-zoom-tutorial/IC784704.png "Adicionar Usuários")
   
    a. Para **Tipo de Usuário**, selecione **Básico**.

    b. Em Olá **Emails** caixa de texto, endereço de email de saudação do tipo de um válida do Azure você deseja tooprovision de conta do AD.

    c. Clique em **Adicionar**.

> [!NOTE]
> Você pode usar qualquer ferramenta de criação outros Zoom usuário conta ou APIs fornecidas pelo Zoom tooprovision Azure Active Directory as contas de usuário.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooZoom.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooZoom, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Zoom**.

    ![link de Zoom de saudação na lista de aplicativos de saudação](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em um bloco de Zoom Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Zoom.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

