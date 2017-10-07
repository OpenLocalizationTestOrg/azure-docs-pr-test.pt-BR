---
title: "Tutorial: Integração do Azure Active Directory com o SD Elements | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e elementos de SD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a>Tutorial: Integração do Active Directory do Azure com SD Elements

Neste tutorial, você aprenderá como toointegrate SD elementos com o Azure Active Directory (AD do Azure).

Integrando o SD elementos com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSD elementos
- Você pode habilitar seu usuários tooautomatically get conectado tooSD elementos (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com elementos de SD, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do SD Elements

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. A adição de elementos de SD da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-sd-elements-from-hello-gallery"></a>A adição de elementos de SD da Galeria de saudação
integração de saudação tooconfigure de elementos de SD no AD do Azure, você precisa tooadd SD elementos da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd SD elementos da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **SD elementos**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. No painel de resultados de saudação, selecione **SD elementos**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o SD Elements, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em elementos de SD está tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em elementos de SD precisa toobe estabelecida.

Elementos de SD, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com elementos de SD, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste de elementos de SD](#creating-a-sd-elements-test-user)**  -toohave um equivalente do Britta Simon em elementos de SD que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de elementos de SD.

**tooconfigure AD do Azure-logon único com elementos de SD, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **SD elementos** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. Em Olá **SD elementos de domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.sdelements.com/sso/saml2/metadata`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.sdelements.com/sso/saml2/acs/`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de resposta e o identificador de real de saudação. Entre em contato com [equipe de suporte a elementos de SD](mailto:support@sdelements.com) tooget esses valores.

4. Aplicativo de elementos de SD espera asserções SAML de saudação em um formato específico. Configure Olá declarações para esse aplicativo a seguir. Você pode gerenciar os valores hello desses atributos de saudação **"Atributo de usuário"** guia do aplicativo hello. Olá captura de tela a seguir mostra um exemplo.

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir: 

    | Nome do atributo | Valor do atributo |
    | --- | --- |
    | email |user.mail |
    | nome |user.givenname |
    | sobrenome |user.surname |

    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.

    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.

    d. Clique em **OK**.
 
6. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. Em Olá **SD elementos de configuração** seção, clique em **configurar SD elementos** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. tooget logon único habilitado, entre em contato com seu [equipe de suporte a elementos de SD](mailto:support@sdelements.com) e fornecê-los com o arquivo de certificado baixado hello. 

10. Em uma janela de navegador diferente, locatário de elementos de SD tooyour logon como administrador.

11. No menu de saudação na parte superior de saudação, clique em **sistema**e, em seguida, **Single Sign-on**. 
   
    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. Em Olá **configurações de logon único** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    a. Como **Tipo de SSO**, selecione **SAML**.
   
    b. Em hello **ID de entidade do provedor de identidade** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure. 
   
    c. Em Olá **serviço provedor de identidade Single Sign-On** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure. 
   
    d. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-sd-elements-test-user"></a>Criar um usuário de teste de elementos de SD

Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon em elementos de SD. No caso de saudação de elementos de SD, a criação de usuários de elementos de SD é uma tarefa manual.

**toocreate Britta Simon em elementos de SD, execute Olá etapas a seguir:**

1. Em uma janela de navegador da web, site da empresa SD elementos tooyour logon como administrador.

2. No menu de saudação na parte superior de saudação, clique em **gerenciamento de usuários**e, em seguida, **usuários**.
   
    ![Criar um usuário de teste de elementos de SD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. Clique em **Adicionar Novo Usuário**.
   
    ![Criar um usuário de teste de elementos de SD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. Em Olá **adicionar novo usuário** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Criar um usuário de teste de elementos de SD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    a. Em Olá **email** caixa de texto, insira o email de saudação do usuário como  **brittasimon@contoso.com** .
   
    b. Em Olá **nome** caixa de texto, digite Olá primeiro nome do usuário, como **Britta**.
   
    c. Em Olá **Sobrenome** caixa de texto, digite o sobrenome de saudação do usuário como **Simon**.
   
    d. Como **Função**, selecione **Usuário**. 
   
    e. Clique em **Criar Usuário**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSD elementos.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSD elementos, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **SD elementos**.

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.
  
Quando você clica em Olá SD elementos bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de elementos de SD.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

