---
title: "Tutorial: Integração do Azure Active Directory ao Samanage | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a>Tutorial: Integração do Azure Active Directory ao Samanage

Neste tutorial, você aprenderá como toointegrate Samanage com o Azure Active Directory (AD do Azure).

Integrando o Samanage com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSamanage
- Você pode habilitar seu usuários tooautomatically get conectado tooSamanage (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Samanage, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Samanage

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Samanage da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-samanage-from-hello-gallery"></a>Adicionando Samanage da Galeria de saudação
integração de saudação tooconfigure do Samanage no AD do Azure, você precisa tooadd Samanage da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Samanage da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Samanage**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. No painel de resultados de saudação, selecione **Samanage**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Samanage, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Samanage é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Samanage precisa toobe estabelecida.

No Samanage, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Samanage, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Samanage](#creating-a-samanage-test-user)**  -toohave um equivalente do Britta Simon no Samanage é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Samanage.

**tooconfigure AD do Azure-logon único com o Samanage, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Samanage** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. Em Olá **Samanage domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<Company Name>.samanage.com/saml_login/<Company Name>`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<Company Name>.samanage.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de logon real hello e o identificador que é explicada posteriormente no tutorial de saudação. Para obter mais detalhes, contate a [equipe de suporte ao Cliente do Samanage](https://www.samanage.com/support).    
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. Em Olá **Samanage configuração** seção, clique em **configurar Samanage** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e a ID da entidade SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Samanage como administrador.

8. Clique em **Painel** e selecione **Configuração** no painel de navegação à esquerda.
   
    ![Painel](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Painel")

9. Clique em **Logon Único**.
   
    ![Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Logon Único")

10. Navegue muito**logon usando SAML** , execute Olá etapas a seguir:
   
    ![Logon usando SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Logon usando SAML")
 
    a. Clique em **Habilitar o Logon Único com SAML**.  
 
    b. Em hello **URL do provedor de identidade** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.    
 
    c. Confirmar Olá **URL de logon** correspondências Olá **URL de logon** de **Samanage domínio e URLs** seção no portal do Azure.
 
    d. Em Olá **URL de Logout** caixa de texto, insira o valor de saudação do **URL de logout** que você copiou do portal do Azure.
 
    e. Em Olá **emissor SAML** caixa de texto, a id do tipo de aplicativo hello URI definido no seu provedor de identidade.
 
    f. Abra seu certificado codificado em base 64 baixado do portal do Azure no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **cole seu provedor de identidade x. 509 certificado abaixo** caixa de texto.
 
    g. Clique em **Criar usuários se eles não existirem no Samanage**.
 
    h. Clique em **Atualizar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-samanage-test-user"></a>Criação de um usuário de teste de Samanage

tooenable AD do Azure usuários toolog em tooSamanage, eles devem ser provisionados no Samanage.  
No caso de saudação do Samanage, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon em seu site de empresa Samanage como um administrador.

2. Clique em **Painel** e selecione **Configuração** no painel de navegação à esquerda.
   
    ![Configuração](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Configuração")

3. Clique em Olá **usuários** guia
   
    ![Usuários](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Usuários")

4. Clique em **Novo Usuário**.
   
    ![Novo Usuário](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Novo Usuário")

5. Saudação de tipo **nome** e hello **endereço de Email** de uma conta do Active Directory do Azure que deseja tooprovision e clique **criar usuário**.
   
    ![Criar usuário](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Criar usuário")
   
   >[!NOTE]
   >proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa. Você pode usar qualquer ferramenta de criação outros Samanage usuário conta ou APIs fornecidas pelo Samanage tooprovision Azure Active Directory as contas de usuário.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSamanage.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSamanage, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Samanage**.

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Samanage Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Samanage aplicativo.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

