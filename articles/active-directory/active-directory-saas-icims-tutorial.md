---
title: "Tutorial: integração do Azure Active Directory com ICIMS | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ICIMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3fa970f008e64e84b0a1280f691f0181851b757c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a>Tutorial: integração do Azure Active Directory ao ICIMS

Neste tutorial, você aprenderá como toointegrate ICIMS com o Azure Active Directory (AD do Azure).

Integrando ICIMS com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooICIMS
- Você pode habilitar seus usuários tooautomatically get conectado tooICIMS (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com ICIMS, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do ICIMS habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando ICIMS da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-icims-from-hello-gallery"></a>Adicionando ICIMS da Galeria de saudação
integração de saudação tooconfigure de ICIMS no AD do Azure, você precisa tooadd ICIMS da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd ICIMS da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **ICIMS**, selecione **ICIMS** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![ICIMS na lista de resultados de saudação](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o ICIMS, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em ICIMS é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em ICIMS precisa toobe estabelecida.

ICIMS, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com ICIMS, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste ICIMS](#create-an-icims-test-user)**  -toohave um equivalente do Britta Simon em ICIMS é toohello vinculado do Azure AD representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ICIMS.

**tooconfigure AD do Azure-logon único com ICIMS, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **ICIMS** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. Em Olá **ICIMS domínio e URLs** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant name>.icims.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant name>.icims.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente ICIMS](https://www.icims.com/contact-us) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. Em Olá **ICIMS configuração** seção, clique em **configurar ICIMS** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. tooconfigure logon único no **ICIMS** lado, você precisa toosend Olá baixado **Metadata XML**, **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** muito [Equipe de suporte do ICIMS](https://www.icims.com/contact-us). Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![botão Adicionar de saudação](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-an-icims-test-user"></a>Criar um usuário de teste do ICIMS

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no ICIMS. Trabalhar com [ICIMS equipe de suporte](https://www.icims.com/contact-us) tooadd usuários Olá Olá conta ICIMS. 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooICIMS.

![Atribuir função de usuário Olá][200]

**tooassign Britta Simon tooICIMS, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **ICIMS**.

    ![Olá ICIMS link na lista de aplicativos Olá](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.  

Quando você clica em Olá ICIMS bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de ICIMS.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

