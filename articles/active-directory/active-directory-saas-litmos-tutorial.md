---
title: "Tutorial: Integração do Azure Active Directory ao Litmos | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a>Tutorial: Integração do Active Directory do Azure ao Litmos

Neste tutorial, você aprenderá como toointegrate Litmos com o Azure Active Directory (AD do Azure).

Integrando Litmos com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooLitmos.
- Você pode habilitar seus usuários tooautomatically get conectado tooLitmos (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Litmos, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Litmos

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Litmos da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-litmos-from-hello-gallery"></a>Adicionando Litmos da Galeria de saudação
integração de saudação tooconfigure de Litmos no AD do Azure, você precisa tooadd Litmos da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Litmos da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Litmos**, selecione **Litmos** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Litmos na lista de resultados de saudação](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Litmos, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Litmos é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Litmos precisa toobe estabelecida.

Litmos, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Litmos, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Litmos](#create-a-litmos-test-user)**  -toohave um equivalente do Britta Simon em Litmos é toohello vinculado do Azure AD representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Litmos.

**tooconfigure AD do Azure-logon único com Litmos, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Litmos** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. Em Olá **Litmos domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único em Domínio e URLs do Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.litmos.com/account/Login`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.litmos.com/integration/samllogin`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real identificador URL de resposta e, que é explicado posteriormente no tutorial ou entre em contato com [Litmos equipe de suporte](https://www.litmos.com/contact-us/) tooget esses valores.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. Como parte da configuração de saudação, você precisa Olá toocustomize **atributos de tokens SAML** para seu aplicativo Litmos.

    ![Seção Atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | Nome do atributo   | Valor do atributo |   
    | ---------------  | ----------------|
    | Nome |user.givenname |
    | Sobrenome  |user.surname |
    | Email |user.mail |

    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Adicionar atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Caixa de diálogo Adicionar atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.

    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **OK**.     

6. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. Em uma janela de navegador diferente, site da empresa Litmos tooyour logon como administrador.

8. Na barra de navegação Olá no lado esquerdo do hello, clique em **contas**.
   
    ![Seção Contas no lado do aplicativo][22] 

9. Clique em Olá **integrações** guia.
   
    ![Guia Integração][23] 

10. Em Olá **integrações** guia, role para baixo demais**integrações do 3ª parte**e, em seguida, clique em **SAML 2.0** guia.
   
    ![Seção SAML 2.0][24] 

11. Copiar valor Olá **Olá ponto de extremidade do SAML para litmos é:** e cole-a saudação **URL de resposta** textbox em Olá **Litmos domínio e URLs** seção no portal do Azure. 
   
    ![Ponto de extremidade SAML][26] 

12. No seu **Litmos** aplicativo, executar Olá etapas a seguir:
    
     ![Aplicativo Litmos][25] 
     
     a. Clique em **Habilitar SAML**.
    
     b. Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509 de SAML** caixa de texto.
     
     c. Clique em **Salvar Alterações**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
  
### <a name="create-a-litmos-test-user"></a>Criar um usuário de teste do Litmos

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Litmos.  
Olá Litmos aplicativo suporta Just-in-Time de provisionamento. Isso significa que, uma conta de usuário é criada automaticamente se necessário durante uma tentativa de tooaccess hello, o aplicativo usando o painel de acesso de saudação.

**toocreate um usuário chamado Britta Simon no Litmos, execute Olá etapas a seguir:**

1. Em uma janela de navegador diferente, site da empresa Litmos tooyour logon como administrador.

2. Na barra de navegação Olá no lado esquerdo do hello, clique em **contas**.
   
    ![Seção Contas no lado do aplicativo][22] 

3. Clique em Olá **integrações** guia.
   
    ![Guia Integrações][23] 

4. Em Olá **integrações** guia, role para baixo demais**integrações do 3ª parte**e, em seguida, clique em **SAML 2.0** guia.
   
    ![SAML 2.0][24] 
    
5. Selecione **Gerar Usuários Automaticamente**
   
    ![Gerar usuários automaticamente][27] 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLitmos.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooLitmos, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Litmos**.

    ![link de Litmos Olá na lista de aplicativos Olá](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.  

Quando você clica em Olá Litmos bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Litmos aplicativo. 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

