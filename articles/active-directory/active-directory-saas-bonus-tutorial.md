---
title: "Tutorial: Integração do Azure Active Directory ao Bonusly | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a>Tutorial: integração do Azure Active Directory ao Bonusly

Neste tutorial, você aprenderá como toointegrate Bonusly com o Azure Active Directory (AD do Azure).

Integrando Bonusly com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooBonusly
- Você pode habilitar seu usuários tooautomatically get conectado tooBonusly (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Bonusly, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Bonusly habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Bonusly da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-bonusly-from-hello-gallery"></a>Adicionando Bonusly da Galeria de saudação
integração de saudação tooconfigure de Bonusly no AD do Azure, você precisa tooadd Bonusly da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Bonusly da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **Bonusly**, selecione **Bonusly** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![Bonusly na lista de resultados de saudação](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o Bonusly, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Bonusly é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Bonusly precisa toobe estabelecida.

Bonusly, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Bonusly, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Bonusly](#create-a-bonusly-test-user)**  -toohave um equivalente do Britta Simon em Bonusly é toohello vinculado do Azure AD representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Bonusly.

**tooconfigure AD do Azure-logon único com Bonusly, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Bonusly** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. Em Olá **Bonusly de domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://Bonus.ly/saml/<tenant-name>`

    > [!NOTE] 
    > Olá valor não é real. Valor de saudação de atualização com hello URL de resposta real. Entre em contato com [a equipe de suporte Bonusly](https://Bonusly/contact) tooget valor de saudação.
 
4. Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** valor de certificado hello.

    ![link de download de certificado Olá](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. Em Olá **configuração Bonusly** seção, clique em **configurar Bonusly** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. Em uma janela de navegador diferente, faça logon no tooyour **Bonusly** locatário.

8. Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações**e, em seguida, selecione **integrações e aplicativos**.
   
    ![Seção Social Bonusly](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")
9. Em **Logon Único**, selecione **SAML**.

10. Em Olá **SAML** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Página de Diálogo Saml do Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")
   
    a. Em Olá **URL de destino IdP SSO** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.
   
    b. Em hello **emissor IdP** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure. 

    c. Em Olá **URL de logon IdP** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.

    d. Colar o **impressão digital** valor copiado do portal do Azure para Olá **impressão digital do certificado** caixa de texto.
   
11. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![botão Adicionar de saudação](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-bonusly-test-user"></a>Criar um usuário de teste do Bonusly

Em ordem tooenable AD do Azure usuários toolog em tooBonusly, eles devem ser provisionados no Bonusly. No caso de saudação de Bonusly, o provisionamento é uma tarefa manual.

>[!NOTE]
>Você pode usar qualquer outra ferramenta de criação do usuário Bonusly conta ou APIs fornecidas pelo tooprovision Bonusly AAD contas de usuário.
>  

**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**

1. Em uma janela de navegador da web, faça logon no locatário Bonusly tooyour.

2. Clique em **Configurações**.
 
    ![Configurações](./media/active-directory-saas-bonus-tutorial/ic781041.png "Configurações")

3. Clique em Olá **usuários e bônus** guia.
   
    ![Usuários e bônus](./media/active-directory-saas-bonus-tutorial/ic781042.png "Usuários e bônus")

4. Clique em **Gerenciar Usuários**.
   
    ![Gerenciar Usuários](./media/active-directory-saas-bonus-tutorial/ic781043.png "Gerenciar Usuários")

5. Clique em **Adicionar Usuário**.
   
    ![Adicionar Usuário](./media/active-directory-saas-bonus-tutorial/ic781044.png "Adicionar Usuário")

6. Em Olá **adicionar usuário** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Adicionar Usuário](./media/active-directory-saas-bonus-tutorial/ic781045.png "Adicionar Usuário")  

    a. Em Olá **nome** caixa de texto, digite Olá primeiro nome do usuário, como **Britta**.

    b. Em Olá **Sobrenome** caixa de texto, digite o sobrenome de saudação do usuário como **Simon**.
 
    c. Em Olá **Email** caixa de texto, insira o email de saudação do usuário como  **brittasimon@contoso.com** .

    d. Clique em **Salvar**.
   
     >[!NOTE]
     >proprietário de conta do AD do Azure Olá recebe um email que inclui uma conta de saudação do link tooconfirm antes de se tornar ativa.
     >  

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBonusly.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooBonusly, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Bonusly**.

    ![Olá Bonusly link na lista de aplicativos Olá](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em bloco Bonusly Olá em Olá painel de acesso, você deverá obter o aplicativo Bonusly tooyour automaticamente conectado em.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

