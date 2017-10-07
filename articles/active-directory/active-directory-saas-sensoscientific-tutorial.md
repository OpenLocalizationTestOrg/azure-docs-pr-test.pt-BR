---
title: "Tutorial: Integração do Azure Active Directory ao Sistema de Monitoramento de Temperatura Sem Fio SensoScientific | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o sistema de monitoramento de temperatura do SensoScientific sem fio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a>Tutorial: Integração do Azure Active Directory ao Sistema de Monitoramento de Temperatura Sem Fio SensoScientific

Neste tutorial, você aprenderá como toointegrate a sistema de monitoramento de temperatura SensoScientific sem fio com o Azure Active Directory (AD do Azure).

Integração do sistema de monitoramento de temperatura do SensoScientific sem fio com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSensoScientific sistema de monitoramento de temperatura sem fio
- Você pode habilitar seu usuários tooautomatically get conectado tooSensoScientific sistema de monitoramento de temperatura sem fio (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o sistema de monitoramento de temperatura do SensoScientific sem fio, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando o sistema de monitoramento de temperatura do SensoScientific sem fio da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a>Adicionando o sistema de monitoramento de temperatura do SensoScientific sem fio da Galeria de saudação
integração de saudação tooconfigure do sistema de monitoramento de temperatura do SensoScientific sem fio no AD do Azure, você precisa tooadd sistema de monitoramento de temperatura do SensoScientific sem fio na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd a sistema de monitoramento de temperatura SensoScientific sem fio da Galeria Olá, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **sistema de monitoramento de temperatura do SensoScientific sem fio**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. No painel de resultados de saudação, selecione **sistema de monitoramento de temperatura do SensoScientific sem fio**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no sistema de monitoramento de temperatura do SensoScientific sem fio é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no sistema de monitoramento de temperatura do SensoScientific sem fio precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no sistema de monitoramento de temperatura do SensoScientific sem fio.

tooconfigure e teste de logon único do AD do Azure com o sistema de monitoramento de temperatura do SensoScientific sem fio, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do sistema de monitoramento de temperatura do SensoScientific sem fio](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave um equivalente de Britta Simon SensoScientific sem fio temperatura monitoramento de sistema que é vinculado a representação toohello AD do Azure de usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de sistema de monitoramento de temperatura do SensoScientific sem fio.

**tooconfigure logon único do AD do Azure com SensoScientific sem fio temperatura monitoramento de sistema, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **sistema de monitoramento de temperatura do SensoScientific sem fio** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. Em Olá **SensoScientific sem fio temperatura monitoramento de sistema de domínio e URLs** seção tooperform sem necessidade de que todas as etapas de como o aplicativo hello previamente já está integrado com o Azure:

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. Em Olá **configuração de sistema de monitoramento do SensoScientific sem fio temperatura** seção, clique em **configurar SensoScientific sem fio temperatura monitoramento sistema** tooopen  **Configurar o logon** janela. Saudação de cópia **URL de logout, ID da entidade SAML** e **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. Logon tooyour aplicativo de sistema de monitoramento de temperatura do SensoScientific sem fio como um administrador.

8. No menu de navegação de saudação na parte superior do hello, clique em **configuração** e goto **configurar** em **Single Sign On** tooopen Olá logon único.

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. Em **logon único** formulário executar Olá etapas a seguir:
 
    a. Selecione **Nome do Emissor** como Azure AD.
    
    b. Saudação de colar **ID da entidade SAML** que você copiou do portal do Azure na caixa de texto URL do emissor.
    
    c. Saudação de colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure na caixa de texto o URL de serviço logon único.

    d. Saudação de colar **URL de logout** que você copiou do portal do Azure na caixa de texto URL de serviço de logon único.

    e. Procure o certificado de saudação que você baixou do portal do Azure e carregar aqui.
    
    f. Clique em **Salvar**.
  
> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação](https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a>Criando um usuário de teste do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific

tooenable AD do Azure usuários toolog em tooSensoScientific sistema de monitoramento de temperatura sem fio, eles devem ser provisionados no sistema de monitoramento de temperatura do SensoScientific sem fio. Trabalhar com [equipe de suporte do sistema de monitoramento de temperatura do SensoScientific sem fio](https://www.sensoscientific.com/contact-us/) para adicionar usuários de saudação na plataforma do sistema de monitoramento de temperatura do SensoScientific sem fio hello. Os usuários devem ser criados e ativados antes de usar o logon único. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSensoScientific sistema de monitoramento de temperatura sem fio.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSensoScientific sistema de monitoramento de temperatura de sem fio, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **sistema de monitoramento de temperatura do SensoScientific sem fio**.

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação. Clique em bloco de sistema de monitoramento de temperatura do SensoScientific sem fio Olá Olá painel de acesso, será automaticamente conectado em tooyour aplicativo de sistema de monitoramento de temperatura do SensoScientific sem fio. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

