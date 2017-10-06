---
title: "Tutorial: Integração do Azure Active Directory com o OpsGenie | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e OpsGenie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 50d31c234fb9716d05d681b9bc4164740a3a662b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a>Tutorial: Integração do Active Directory do Azure com o OpsGenie

Neste tutorial, você aprenderá como toointegrate OpsGenie com o Azure Active Directory (AD do Azure).

Integrando OpsGenie com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooOpsGenie
- Você pode habilitar seu usuários tooautomatically get conectado tooOpsGenie (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com OpsGenie, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do OpsGenie

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando OpsGenie da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-opsgenie-from-hello-gallery"></a>Adicionando OpsGenie da Galeria de saudação
integração de saudação tooconfigure de OpsGenie no AD do Azure, você precisa tooadd OpsGenie da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd OpsGenie da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **OpsGenie**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. No painel de resultados de saudação, selecione **OpsGenie**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o OpsGenie, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em OpsGenie é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em OpsGenie precisa toobe estabelecida.

OpsGenie, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com OpsGenie, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste OpsGenie](#creating-a-opsgenie-test-user)**  -toohave um equivalente do Britta Simon em OpsGenie é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo OpsGenie.

**tooconfigure AD do Azure-logon único com OpsGenie, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **OpsGenie** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. Em Olá **OpsGenie domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://app.opsgenie.com/auth/login`

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. Em Olá **OpsGenie configuração** seção, clique em **configurar OpsGenie** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. Abrir outra instância do navegador e, em seguida, efetue login tooOpsGenie como um administrador.

8. Clique em **configurações**e, em seguida, clique em Olá **Single Sign On** guia.
   
    ![Logon único do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. Selecione tooenable SSO, **habilitado**.
   
    ![Configurações do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. Em Olá **provedor** seção, clique em Olá **Active Directory do Azure** guia.
   
    ![Configurações do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. Na página de diálogo do Active Directory do Azure hello, execute Olá etapas a seguir:
   
    ![Configurações do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    a. Colar **Service URL de logon único**, que você copiou de saudação portal do Azure em hello **o ponto de extremidade do SAML 2.0** caixa de texto.
    
    b. Abra seu certificado baixado de codificada de base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-Olá **certificado x. 500** caixa de texto.
    
    c. Clique em **Salvar Alterações**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-opsgenie-test-user"></a>Criação de um usuário de teste para OpsGenie

Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no OpsGenie. 

1. Em uma janela de navegador da Web, faça logon em seu locatário do OpsGenie como administrador.

2. Navegue tooUsers lista clicando **usuário** no painel esquerdo.
   
   ![Configurações do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. Clique em **Adicionar Usuário**.

4. Em Olá **adicionar usuário** caixa de diálogo, executar Olá etapas a seguir:
   
   ![Configurações do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   a. Em Olá **Email** caixa de texto, endereço de email de saudação do tipo do BrittaSimon abordada no Active Directory do Azure.
   
   b. Em Olá **nome completo** caixa de texto, tipo **Britta Simon**.
   
   c. Clique em **Salvar**. 

>[!NOTE]
>Brenda receberá um email com instruções para configurar o perfil dela.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooOpsGenie.

![Atribuir usuário][200] 

**tooassign Britta Simon tooOpsGenie, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **OpsGenie**.

    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.

Quando você clica em bloco OpsGenie Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour OpsGenie aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

