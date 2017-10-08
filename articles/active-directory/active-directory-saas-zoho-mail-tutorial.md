---
title: "Tutorial: Integração do Azure Active Directory com Zoho | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a>Tutorial: Integração do Azure Active Directory com Zoho

Neste tutorial, você aprenderá como toointegrate Zoho com o Azure Active Directory (AD do Azure).

Integrando Zoho com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooZoho.
- Você pode habilitar seu usuários tooautomatically get conectado tooZoho (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Zoho, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Zoho

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Zoho da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-zoho-from-hello-gallery"></a>Adicionando Zoho da Galeria de saudação
integração de saudação tooconfigure do Zoho no AD do Azure, você precisa tooadd Zoho da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Zoho da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Zoho**, selecione **Zoho** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Zoho na lista de resultados de saudação](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Zoho, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Zoho é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Zoho precisa toobe estabelecida.

No Zoho, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Zoho, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Zoho](#create-a-zoho-test-user)**  -toohave um equivalente do Britta Simon no Zoho é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Zoho.

**tooconfigure AD do Azure-logon único com o Zoho, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Zoho** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. Em Olá **Zoho domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único em Domínio e URLs do Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.zohomail.com`

    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com hello URL de logon real. Entre em contato com [equipe de suporte do cliente Zoho](https://www.zoho.com/mail/contact.html) tooget esse valor. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. Em Olá **Zoho configuração** seção, clique em **configurar Zoho** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML, alterar a URL da senha e URL de logout** de saudação **seção de referência rápida.**

    ![Configuração do Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. Em uma janela diferente do navegador da Web, faça logon no site da sua empresa Zoho Mail como administrador.

8. Vá toohello **painel de controle**.
   
    ![Painel de controle](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Painel de controle")

9. Clique em Olá **autenticação SAML** guia.
   
    ![Autenticação SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Autenticação SAML")

10. Em Olá **detalhes de autenticação SAML** , execute Olá etapas a seguir:
   
    ![Detalhes de Autenticação SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Detalhes de Autenticação SAML")
   
    a. Em Olá **URL de logon** caixa de texto, colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.
   
    b. Em Olá **URL de Logout** caixa de texto, colar **URL de logout** que você copiou do portal do Azure.
   
    c. Em Olá **alterar a URL da senha** caixa de texto, colar **alterar a URL da senha** que você copiou do portal do Azure.
       
    d. Abra seu certificado codificado em base 64 baixado do portal do Azure no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **PublicKey** caixa de texto.
   
    e. Para **Algoritmo**, selecione **RSA**.
   
    f. Clique em **OK**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-zoho-test-user"></a>Criar um usuário de teste do Zoho

Ordem tooenable AD do Azure usuários toolog no Zoho Mail, eles devem ser provisionados no Zoho Mail. No caso de saudação do Zoho Mail, o provisionamento é uma tarefa manual.

> [!NOTE]
> Você pode usar qualquer ferramenta de criação outros Zoho Mail usuário conta ou APIs fornecidas pelo Zoho Mail tooprovision contas de usuário do AAD.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision uma conta de usuário, execute Olá etapas a seguir:

1. Faça logon no tooyour **Zoho Mail** site da empresa como um administrador.

2. Vá muito**painel de controle \> Mail & documentos**.

3. Vá muito**detalhes do usuário \> adicionar usuário**.
   
    ![Adicionar Usuário](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Adicionar Usuário")

4. Em Olá **adicionar usuários** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Adicionar Usuário](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Adicionar Usuário")
   
    a. Em Olá **nome** caixa de texto, tipo hello primeiro nome do usuário, como **Britta**.

    b. Em Olá **Sobrenome** caixa de texto, digite Olá sobrenome do usuário como **Simon**.

    c. Em Olá **ID de Email** caixa de texto, id de email do tipo saudação do usuário como  **brittasimon@contoso.com** .

    d. Em Olá **senha** caixa de texto, digite a senha do usuário.
   
    e. Clique em **OK**.  
      
    > [!NOTE]
    > proprietário de conta do Active Directory do Azure Olá receberá um email com uma conta de saudação do link tooconfirm antes de se tornar ativa.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooZoho.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooZoho, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Zoho**.

    ![link de Zoho Olá na lista de aplicativos Olá](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Zoho Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Zoho aplicativo.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

