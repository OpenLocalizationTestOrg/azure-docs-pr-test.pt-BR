---
title: "Tutorial: Integração do Active Directory do Azure com @Task| Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a>Tutorial: Integração do Active Directory do Azure com @Task
Olá objetivo deste tutorial é tooshow você como toointegrate @Task com o Azure Active Directory (AD do Azure).  
Integrando @Task com o Azure AD fornece Olá benefícios a seguir: 

* Você pode controlar no AD do Azure que tenha acessotoo@Task
* Você pode permitir que os usuários tooautomatically obter conectado too@Task (logon único) com suas contas do AD do Azure
* Você pode gerenciar suas contas em um local central - Olá Portal clássico do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
integração tooconfigure AD do Azure com @Task, você precisa Olá itens a seguir:

* Uma assinatura do AD do Azure
* Uma assinatura habilitada para logon único @Task

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.
> 
> 

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

* Não use o ambiente de produção, a menos que seja necessário.
* Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descrição do cenário
Olá objetivo deste tutorial é tooenable tootest logon único do AD do Azure em um ambiente de teste.  
cenário de saudação descrito neste tutorial consiste em três principais blocos de construção:

1. Adicionando @Task da Galeria de saudação 
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-task-from-hello-gallery"></a>Adicionando @Task da Galeria de saudação
integração de saudação tooconfigure do @Task no AD do Azure, você precisa tooadd @Task da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd @Task da Galeria hello, executar Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**. 
   
    ![Active Directory][1] 
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Aplicativos][2] 
4. Clique em **adicionar** final Olá Olá página.
   
    ![Aplicativos][3] 
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Aplicativos][4] 
6. Na caixa de pesquisa hello, digite  **@Task** .
   
    ![Aplicativos][5] 
7. No painel de resultados de saudação, selecione  **@Task** e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
    ![Aplicativos][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Olá, o objetivo desta seção é tooshow você como um único teste AD do Azure e tooconfigure logon com @Task com base em um usuário de teste chamado "Britta Simon".

Para toowork de logon único, AD do Azure precisa tooknow que usuário de contraparte Olá no @Task tooan usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em @Task precisa toobe estabelecida.   
Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** em @Task.

teste do AD do Azure e tooconfigure o logon único com @Task, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criando um @Tasktest usuário](#creating-a-halogen-software-test-user)**  -toohave a contraparte de Britta Simon em @Taskthat é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do AD do Azure
Olá objetivo desta seção é tooenable AD do Azure-logon único no hello portal clássico do Azure e tooconfigure logon único no seu @Task aplicativo.

**tooconfigure logon único do AD do Azure com @Task, executar Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá  **@Task**  página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**  caixa de diálogo.
   
    ![Configurar Logon Único][6] 
2. Em Olá **como você gostaria que os usuários toosign em too@Task**  página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Logon Único do AD do Azure][7] 
3. Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Definir configurações de aplicativo][8] 
   
     a. Em Olá **URL de logon** caixa de texto, digite a URL Olá usada por seu usuários em toosign tooyour @Task aplicativo (por exemplo:*https://<Tenant name>.attask ondemand.com*).
   
     b. Clique em **Avançar**.
4. Em Olá **configurar logon único no @Task**  , clique em **baixar metadados**, salvar o arquivo de metadados de saudação localmente no seu computador e, em seguida, clique em **próximo**.
   
    ![O que é o Azure AD Connect][9] 
5. Logon tooyour @Task site da empresa como administrador.
6. Vá muito**logon único na configuração**.
7. Em Olá **Single Sign-On** caixa de diálogo, executar Olá etapas
   
    ![Configurar Logon Único][23]
   
    a. Como **Tipo**, selecione **SAML 2.0**.
   
    b. Selecione **ID do Provedor de Serviços**.
   
    c. No hello portal clássico do Azure, copie Olá **URL de logon remoto**e, em seguida, cole-Olá **URL de logon do Portal** caixa de texto.
   
    d. No hello portal clássico do Azure, copie Olá **URL do serviço de logon único**e, em seguida, cole-Olá **URL de logout** caixa de texto.
   
    e. No hello portal clássico do Azure, copie Olá **alterar a URL da senha**e, em seguida, cole-Olá **alterar a URL da senha** caixa de texto.
   
    f. Clique em **Salvar**.
8. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**. 
   
    ![O que é o Azure AD Connect][10]
9. Em Olá **único logon confirmação** , clique em **concluir**.  
   
    ![O que é o Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello portal clássico do Azure chamado Britta Simon.  

![Criar um usuário do AD do Azure][20]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**. 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir: 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    a. Em Tipo de Usuário, selecione Novo usuário na organização.
   
    b. Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.
   
    c. Clique em **Avançar**.
6. Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir: 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    a. Em Olá **nome** caixa de texto, tipo **Britta**.  
   
    b. Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.
   
    c. Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.
   
    d. Em Olá **função** lista, selecione **usuário**.

    e. Clique em **Avançar**.

7. Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    a. Anote o valor Olá Olá **nova senha**.
   
    b. Clique em **Concluído**.   

### <a name="creating-an-task-test-user"></a>Criando um usuário de teste de @Task
Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no @Task.

**toocreate um usuário chamado Britta Simon no @Task, executar Olá etapas a seguir:**

1. Logon tooyour @Task site da empresa como administrador.
2. No menu de saudação na parte superior de saudação, clique em **pessoas**.
3. Clique em **Nova Pessoa**. 
4. Na caixa de diálogo de nova pessoa hello, execute Olá etapas a seguir:
   
    ![Criar um usuário de teste de @Task][21] 
   
    a. Em Olá **nome** caixa de texto, digite "Britta".
   
    b. Em Olá **Sobrenome** caixa de texto, digite "Simon".
   
    c. Em Olá **endereço de Email** caixa de texto, digite o endereço de email Britta Simon no Active Directory do Azure.
   
    d. Clique em **Adicionar Pessoa**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure
Olá objetivo desta seção é tooenabling Britta Simon toouse logon único do Azure, concedendo o acesso too@Task.

![Atribuir usuário][200] 

**tooassign Britta Simon too@Task, executar Olá etapas a seguir:**

1. No hello Azure portal clássico, exibição de aplicativos tooopen hello, no modo de exibição de diretório hello, clique em **aplicativos** no menu superior hello.
   
    ![Atribuir usuário][201] 
2. Na lista de aplicativos hello, selecione  **@Task** .
   
    ![Atribuir usuário][202] 
3. No menu de saudação na parte superior de saudação, clique em **usuários**.
   
    ![Atribuir usuário][203] 
4. Na lista de usuários hello, selecione **Britta Simon**.
5. Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.
   
    ![Atribuir usuário][205]

### <a name="testing-single-sign-on"></a>Teste do logon único
Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.  
Quando você clica em Olá @Task Olá de bloco no painel de acesso, você deve obter automaticamente assinado em tooyour @Task aplicativo.

## <a name="additional-resources"></a>Recursos adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






