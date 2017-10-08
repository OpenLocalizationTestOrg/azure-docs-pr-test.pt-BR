---
title: "Tutorial: Integração do Azure Active Directory ao RFPIO | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a>Tutorial: Integração do Azure Active Directory ao RFPIO

Neste tutorial, você aprenderá como toointegrate RFPIO com o Azure Active Directory (AD do Azure).

Integrando RFPIO com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar quem no AD do Azure que tenha acesso tooRFPIO.
- Você pode habilitar seu usuários tooautomatically get conectado tooRFPIO (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central – Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com RFPIO, você precisa Olá itens a seguir:

- Uma assinatura do Azure AD.
- Uma assinatura habilitada para logon único do RFPIO.

> [!NOTE]
> Não é recomendável que você use um etapas Olá tootest do ambiente de produção neste tutorial.

etapas de saudação tootest neste tutorial, siga estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação que é descrito neste tutorial consiste em duas principais blocos de construção:

1. Adicionando RFPIO da Galeria de saudação.
2. Configurar e testar o logon único do Azure AD.

## <a name="add-rfpio-from-hello-gallery"></a>Adicionar RFPIO da Galeria de saudação
integração de saudação tooconfigure de RFPIO no AD do Azure, você precisa tooadd RFPIO da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

### <a name="tooadd-rfpio-from-hello-gallery"></a>tooadd RFPIO da Galeria de saudação

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, selecione Olá **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Selecione **Aplicativos da empresa**, em seguida, selecione **Todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd um novo aplicativo, selecione Olá **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **RFPIO**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. No painel de resultados de saudação, selecione **RFPIO**e, em seguida, selecione Olá **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o RFPIO, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow qual relação hello está entre o usuário correspondente em RFPIO e um usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em RFPIO precisa toobe estabelecida.

Em RFPIO, atribuir o valor de saudação do **nome de usuário** no AD do Azure como valor de saudação do **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com RFPIO, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**– tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**– tootest logon único do AD do Azure com Britta Simon.
3. **[Criar um usuário de teste RFPIO](#creating-a-rfpio-test-user)**  - toohave um equivalente do Britta Simon em RFPIO é toohello vinculado do Azure AD representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assigning-the-azure-ad-test-user)**– tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#testing-single-sign-on)**  – tooverify se Olá configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo RFPIO.

**tooconfigure AD do Azure-logon único com RFPIO, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **RFPIO** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. Em Olá **RFPIO domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    a. Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://www.rfpio.com`

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    b. Marque **Mostrar configurações de URL avançadas**.

    c. Em Olá **estado de retransmissão** caixa de texto Digite um valor de cadeia de caracteres. Entre em contato com [RFPIO equipe de suporte](https://www.rfpio.com/contact/) tooget esse valor. 

4. Marque **Mostrar configurações de URL avançadas**. Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:   

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://www.app.rfpio.com`

5. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. Em uma janela de navegador web diferente, o logon toohello **RFPIO** site como um administrador.

8. Clique em Olá inferior esquerda suspenso.

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. Clique em Olá **as configurações da organização**. 

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. Clique em Olá **recursos e integração**.

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. Em Olá **configuração de SSO de SAML** clique **editar**.

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. Nesta seção, execute as seguintes ações:

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    a. Copiar o conteúdo de saudação do hello **XML de metadados baixado** e cole-a saudação **configuração de identidade** campo.

    > [!NOTE]
    >baixado toocopy Olá conteúdo de **Metadata XML** Use **o bloco de notas + +** ou adequada **Editor XML**. 

    b. Clique em **Validar**.

    c. Depois de clicar em **validar**, inverter **SAML(Enabled)** tooon.

    d. Clique em **Enviar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-rfpio-test-user"></a>Criar um usuário de teste do RFPIO

tooenable AD do Azure usuários toolog em tooRFPIO, eles devem ser provisionados no RFPIO.  
No caso de saudação de RFPIO, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon em tooyour site da empresa RFPIO como um administrador.

2. Clique em Olá inferior esquerda suspenso.

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. Clique em Olá **as configurações da organização**. 

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. Clique em **MEMBROS DA EQUIPE**.

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. Clique em **ADICIONAR MEMBROS**.

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. Em Olá **adicionar novos membros** seção. Execute as seguintes ações:

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app8.png)

    a. Insira **endereço de Email** em Olá **Insira um email por linha** campo.

    b. Selecione **Função** de acordo com seus requisitos.

    c. Clique em **ADICIONAR MEMBROS**.
        
    > [!NOTE]
    > proprietário de conta do Active Directory do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooRFPIO.

![Atribuir usuário][200] 

**tooassign Britta Simon tooRFPIO, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **RFPIO**.

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você pode testar a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá RFPIO bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de RFPIO.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como toointegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

