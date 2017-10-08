---
title: "Tutorial: Integração do Azure Active Directory com o Splunk Enterprise e o Splunk Cloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Splunk Enterprise e Splunk nuvem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a>Tutorial: Integração do Azure Active Directory com o Splunk Enterprise e o Splunk Cloud

Neste tutorial, você aprenderá como toointegrate Splunk Enterprise e Splunk nuvem com o Azure Active Directory (AD do Azure).

Integração Splunk Enterprise e Splunk nuvem com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSplunk Enterprise e nuvem Splunk
- Você pode habilitar seu usuários tooautomatically get conectado tooSplunk Enterprise e nuvem Splunk-logon único (SSO) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Splunk Enterprise e Splunk nuvem, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Splunk Enterprise ou do Splunk Cloud habilitada para SSO


>[!NOTE]
>Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.
>

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.

cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Splunk Enterprise e nuvem Splunk da Galeria de saudação
2. Configurar e testar o SSO do Azure AD


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a>Adicionar Splunk Enterprise e nuvem Splunk da Galeria de saudação
integração de saudação tooconfigure do Splunk Enterprise e Splunk nuvem no Azure AD, você precisa tooadd Splunk Enterprise e gerenciado de nuvem Splunk de lista de tooyour Olá Galeria de aplicativos SaaS.

**tooadd Splunk Enterprise e nuvem Splunk da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.

    ![Active Directory][1]

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.

    ![Aplicativos][2]

4. Clique em **adicionar** final Olá Olá página.

    ![Aplicativos][3]

5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.

    ![Aplicativos][4]

6. Na caixa de pesquisa hello, digite **Splunk Enterprise ou nuvem Splunk**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. No painel de resultados de saudação, selecione **Splunk Enterprise e nuvem Splunk**e, em seguida, clique em **concluir** aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o Splunk Enterprise e o Splunk Cloud, com base em uma usuária de teste chamada "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá Splunk Enterprise e nuvem Splunk é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Splunk Enterprise e nuvem Splunk precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Splunk Enterprise e Splunk nuvem.

tooconfigure e teste de logon único do AD do Azure com Splunk Enterprise e Splunk nuvem, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurar o logon único do AD do Azure](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Splunk Enterprise e nuvem Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave um equivalente de Britta Simon Splunk empresa e Splunk em nuvem que é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o SSO de AD do Azure no portal clássico do hello e configurar SSO em seu aplicativo Splunk Enterprise e Splunk nuvem.


**tooconfigure logon único do AD do Azure com Splunk Enterprise e nuvem Splunk, execute Olá etapas a seguir:**

1. No portal clássico hello, em Olá **Splunk Enterprise e nuvem Splunk** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.
     
    ![Configurar Logon Único][6] 

2. Em Olá **como você gostaria que usuários toosign em tooSplunk Enterprise e nuvem Splunk** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.

    ![Configurar Logon Único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. Em Olá **URL de logon** caixa de texto, digite a URL Olá usada por seus usuários em toosign tooyour Splunk Enterprise e o aplicativo de nuvem Splunk usando saudação padrão a seguir:`https://<splunkserverUrl>/en-US/app/launcher/home`
  2. Em Olá **identificador** caixa de texto, digite a URL de saudação do servidor Splunk.
  3. Em Olá **URL de resposta** caixa de texto, digite a URL de saudação com saudação padrão a seguir:`https://<splunkserver>/saml/acs`
  4. Clique em **Avançar**.
 
4. Em Olá **configurar logon único no Splunk Enterprise e nuvem Splunk** página, execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. Clique em **baixar metadados**e, em seguida, salve o arquivo de saudação em seu computador.
  2. Clique em **Avançar**.

5. tooget SSO configurado para o seu aplicativo, entre em contato com Splunk Enterprise e a equipe de suporte de nuvem Splunk e fornecê-los com os seguintes hello:

    * Olá baixado **federaton metadados**
6. No portal clássico do hello, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.
    
    ![Logon Único do AD do Azure][10]

7. Em Olá **único logon confirmação** , clique em **concluir**.  
 
    ![Logon Único do AD do Azure][11]

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Nesta seção, você pode criar um usuário de teste no portal clássico do hello chamado Britta Simon.

![Criar um usuário do AD do Azure][20]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. Em Tipo de Usuário, selecione Novo usuário na organização.
  2. Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.
  3. Clique em **Avançar**.

6.  Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:
  
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. Em Olá **nome** caixa de texto, tipo **Britta**.  
  2. Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.
  3. Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.
  4. Em Olá **função** lista, selecione **usuário**.
  5. Clique em **Avançar**.

7. Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. Anote o valor Olá Olá **nova senha**.
  2. Clique em **Concluído**.   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a>Criar um usuário de teste do Splunk Enterprise e do Splunk Cloud

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Splunk Enterprise e no Splunk Cloud. Trabalhe com Splunk Enterprise e nuvem Splunk suporte team tooadd Olá usuários Olá Splunk Enterprise e plataforma de nuvem Splunk.


### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você deve habilitar Britta Simon toouse SSOy Azure concedendo o acesso tooSplunk Enterprise e Splunk nuvem.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSplunk Enterprise e nuvem Splunk, execute Olá etapas a seguir:**

1. No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Splunk Enterprise e nuvem Splunk**.

    ![Configurar Logon Único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. No menu de saudação na parte superior de saudação, clique em **usuários**.

    ![Atribuir usuário][203]

4. Na lista de usuários hello, selecione **Britta Simon**.

5. Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.

    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você deve testar seu SSOonfiguration do AD do Azure usando o painel de acesso de saudação.

Quando você clica em hello Splunk Enterprise e o bloco de nuvem Splunk no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Splunk Enterprise e nuvem Splunk o aplicativo.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
