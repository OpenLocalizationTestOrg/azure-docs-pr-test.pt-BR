---
title: "Tutorial: integração do Azure Active Directory ao CloudPassage | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e CloudPassage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 32fb007b90f071626c9b40fb5afc341dd3c1ae99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a>Tutorial: integração do Active Directory do Azure ao CloudPassage

Neste tutorial, você aprenderá como toointegrate CloudPassage com o Azure Active Directory (AD do Azure).

Integrando CloudPassage com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooCloudPassage
- Você pode habilitar seu usuários tooautomatically get conectado tooCloudPassage (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com CloudPassage, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do CloudPassage com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando CloudPassage da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-cloudpassage-from-hello-gallery"></a>Adicionando CloudPassage da Galeria de saudação
integração de saudação tooconfigure de CloudPassage no AD do Azure, você precisa tooadd CloudPassage da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd CloudPassage da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **CloudPassage**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. No painel de resultados de saudação, selecione **CloudPassage**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o CloudPassage com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em CloudPassage é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em CloudPassage precisa toobe estabelecida.

CloudPassage, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com CloudPassage, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste CloudPassage](#creating-a-cloudpassage-test-user)**  -toohave um equivalente do Britta Simon em CloudPassage é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo CloudPassage.

**tooconfigure AD do Azure-logon único com CloudPassage, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **CloudPassage** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. Em Olá **CloudPassage domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://portal.cloudpassage.com/saml/init/accountid`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir: `https://portal.cloudpassage.com/saml/consume/accountid`. Você pode obter o valor para este atributo clicando **documentação de instalação de SSO** em Olá **configurações de logon único** seção do seu portal CloudPassage.

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de resposta real hello e URL de logon. Entre em contato com [equipe de suporte do cliente CloudPassage](https://www.cloudpassage.com/company/contact/) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. Seu aplicativo CloudPassage espera as asserções de SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.   
Olá captura de tela a seguir mostra um exemplo.
   
   ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:

    | Nome do atributo | Valor do atributo |
    | --- | --- |
    | nome |user.givenname |
    | sobrenome |user.surname |
    | email |user.mail |
    
    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.

    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **OK**.

7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. Em Olá **CloudPassage configuração** seção, clique em **configurar CloudPassage** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. Em uma janela de navegador diferente, site da empresa CloudPassage tooyour logon como administrador.

10. No menu de saudação na parte superior de saudação, clique em **configurações**e, em seguida, clique em **administração de Site**. 
   
    ![Configurar Logon Único][12]

11. Clique em Olá **configurações de autenticação** guia. 
   
    ![Configurar Logon Único][13]

12. Em Olá **configurações de logon único** , execute Olá etapas a seguir: 
   
    ![Configurar Logon Único][14]

    a. Marque a caixa de seleção **Habilitar SSO (Logon Único) (Documentação de instalação de SSO)**.
    
    b. Colar **ID da entidade SAML** em Olá **URL do emissor SAML** caixa de texto.
  
    c. Colar **Single Sign-On URL do serviço SAML** em Olá **URL do ponto de extremidade do SAML** caixa de texto.
  
    d. Colar **URL de logout** em Olá **página de aterrissagem do Logout** caixa de texto.
  
    e. Abra seu certificado baixado no bloco de notas, Olá de copiar conteúdo de certificado baixado em sua área de transferência e, em seguida, cole-o em Olá **certificado X509** caixa de texto.
  
    f. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-cloudpassage-test-user"></a>Criar um usuário de teste CloudPassage

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no CloudPassage.

**toocreate um usuário chamado Britta Simon no CloudPassage, execute Olá etapas a seguir:**

1. Logon tooyour **CloudPassage** site da empresa como um administrador. 

2. Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações**e, em seguida, clique em **administração de Site**. 
   
   ![Criar um usuário de teste CloudPassage][22] 

3. Clique em Olá **usuários** guia e, em seguida, clique em **adicionar novo usuário**. 
   
   ![Criar um usuário de teste CloudPassage][23]

4. Em Olá **adicionar novo usuário** , execute Olá etapas a seguir: 
   
   ![Criar um usuário de teste CloudPassage][24]
    
    a. Em Olá **nome** caixa de texto, digite Britta. 
  
    b. Em Olá **Sobrenome** caixa de texto, digite Simon.
  
    c. Em Olá **Username** caixa de texto, Olá **Email** caixa de texto e hello **Email novamente** caixa de texto, digite o nome de usuário de Britta no AD do Azure.
  
    d. Como **Tipo de acesso**, selecione **Habilitar acesso do Portal de Halo**.
  
    e. Clique em **Adicionar**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCloudPassage.

![Atribuir usuário][200] 

**tooassign Britta Simon tooCloudPassage, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **CloudPassage**.

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em bloco CloudPassage Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour CloudPassage aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

