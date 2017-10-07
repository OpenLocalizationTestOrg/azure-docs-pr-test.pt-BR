---
title: "Tutorial: Integração do Azure Active Directory com o SciQuest Spend Director | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SciQuest diretor de gastos."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a>Tutorial: Integração do Active Directory do Azure com o SciQuest Spend Director
Olá objetivo deste tutorial é tooshow você como toointegrate SciQuest diretor de gastos no Azure Active Directory (AD do Azure).  
Integrando SciQuest diretor de gastos do Azure AD oferece Olá benefícios a seguir: 

* Você pode controlar no AD do Azure que tenha acesso tooSciQuest diretor de gastos 
* Você pode habilitar seu usuários tooautomatically get conectado tooSciQuest diretor de gastos (logon único) com suas contas do AD do Azure
* Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
tooconfigure integração do AD do Azure com o Diretor de gastar SciQuest, você precisa Olá itens a seguir:

* Uma assinatura do AD do Azure
* Uma assinatura do SciQuest Spend Director com o logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.
> 
> 

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

* Não use o ambiente de produção, a menos que seja necessário.
* Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descrição do cenário
Olá objetivo deste tutorial é tooenable tootest logon único do AD do Azure em um ambiente de teste.  
cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando SciQuest gastar Diretor da Galeria de saudação 
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a>Adicionando SciQuest gastar Diretor da Galeria de saudação
integração de saudação tooconfigure do SciQuest diretor de gastos no AD do Azure, você precisa tooadd SciQuest diretor de gastar na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd SciQuest diretor de gastos da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**. 
   
    ![Active Directory][1]

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Aplicativos][2]

4. Clique em **adicionar** final Olá Olá página.
   
    ![Aplicativos][3]

5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Aplicativos][4]

6. Na caixa de pesquisa hello, digite **sciQuest gastar director**.
   
    ![Aplicativos][5]

7. No painel de resultados de saudação, selecione **SciQuest gastar Director**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
    ![Aplicativos][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Olá o objetivo desta seção é tooshow como tooconfigure e teste de logon único do AD do Azure com o Diretor de gastar SciQuest com base em um usuário de teste chamado "Britta Simon".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá diretor de gastar SciQuest tooan usuário no AD do Azure é. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no SciQuest gastar Director precisa toobe estabelecida.  
Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em SciQuest diretor de gastos.

tooconfigure e teste de logon único do AD do Azure com o Diretor de gastar SciQuest, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD único Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criando um usuário de teste de diretor de gastar SciQuest](#creating-a-halogen-software-test-user)**  -toohave um equivalente do Britta Simon no Director gastar SciQuest que é a representação toohello vinculado do Azure AD de seus.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-single-sign-on"></a>Configuração do logon único do Azure AD
objetivo Olá desta seção é tooenable AD do Azure-logon único no hello portal clássico do Azure e tooconfigure logon único no aplicativo SciQuest diretor de gastos.

**tooconfigure logon único do AD do Azure com o Diretor de gastar SciQuest, execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá **SciQuest gastar Director** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**caixa de diálogo.
   
    ![Configurar Logon Único][8]

2. Em Olá **como você gostaria usuários toosign em tooSciQuest diretor de gastos** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Logon Único do AD do Azure][9]

3. Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir: 
   
    ![Definir configurações de aplicativo][10]
   
     a. Em Olá **URL de logon** caixa de texto, digite a URL usada pelos seu toosign usuários no aplicativo de diretor de gastar SciQuest tooyour usando saudação padrão a seguir: *https://.* SciQuest.com/.**
   
     b. Em Olá **URL de resposta** caixa de texto, Olá tipo mesmo valor que você digitou em Olá **URL de logon** caixa de texto. 
   
     c. Clique em **Avançar**.

4. Em Olá **configurar logon único no diretor de gastar SciQuest** , clique em **baixar metadados**e, em seguida, salve o arquivo de metadados de saudação localmente no seu computador.
   
    ![O que é o Azure AD Connect][11]

5. Entre em contato com SciQuest tooenable de suporte a esse método de autenticação usando metadados de saudação acima baixado.

6. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo. 
   
    ![O que é o Azure AD Connect][15]

7. Em Olá **único logon confirmação** , clique em **concluir**.  

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello portal clássico do Azure chamado Britta Simon.

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![O que é o Azure AD Connect][100] 

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.
   
    ![O que é o Azure AD Connect][101] 

4. Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**. 
   
    ![O que é o Azure AD Connect][102] 

5. Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![O que é o Azure AD Connect][103] 
   
    a. Em **Tipo de Usuário**, selecione **Novo usuário na organização**.
   
    b. Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.
   
    c. Clique em **Avançar**.

6. Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir: 
   
    ![O que é o Azure AD Connect][104] 
   
    a. Em Olá **nome** caixa de texto, tipo **Britta**.  
   
    b. Em Olá **Sobrenome** txtbox, tipo, **Simon**.
   
    c. Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.
   
    d. Em Olá **função** lista, selecione **usuário**.
   
    e. Clique em **Avançar**.

7. Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.
   
    ![O que é o Azure AD Connect][105]  

8. Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![O que é o Azure AD Connect][106]   
   
    a. Anote o valor Olá Olá **nova senha**.
   
    b. Clique em **Concluído**.   

### <a name="creating-a-sciquest-spend-director-test-user"></a>Criação de um usuário de teste do SciQuest Spend Director
Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no SciQuest diretor de gastos.

Necessário toocontact sua equipe de suporte SciQuest diretor de gastos e fornecer detalhes de saudação sobre seu tooget de conta de teste criado por ele.

Como alternativa, você também pode usar o provisionamento just-in-time, um recurso de logon único com suporte do SciQuest Spend Director.  
Se o provisionamento Just-In-Time estiver habilitado, os usuários serão automaticamente criados pelo SciQuest Spend Director durante uma tentativa de logon único, caso não existam. Este recurso elimina a necessidade de saudação toomanually criar equivalente de logon único de usuários.

provisionamento do tooget just-in-time habilitada, é necessário toocontact estiver sua equipe de suporte SciQuest diretor de gastos.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure
Olá objetivo desta seção é tooenabling Britta Simon toouse logon único do Azure concedendo tooSciQuest seu acesso diretor de gastos.

![O que é o Azure AD Connect][200]

**tooassign Britta Simon tooSciQuest diretor de gastos, execute Olá etapas a seguir:**

1. No hello Azure portal clássico, exibição de aplicativos tooopen hello, no modo de exibição de diretório hello, clique em **aplicativos** no menu superior hello.
   
    ![O que é o Azure AD Connect][201]

2. Na lista de aplicativos hello, selecione **SciQuest gastar Director**.
   
    ![O que é o Azure AD Connect][202]

3. No menu de saudação na parte superior de saudação, clique em **usuários**.
   
    ![O que é o Azure AD Connect][203]

4. Na lista de usuários hello, selecione **Britta Simon**.
   
    ![O que é o Azure AD Connect][204]

5. Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.
   
    ![O que é o Azure AD Connect][205]

### <a name="testing-single-sign-on"></a>Teste do logon único
Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.  
Quando você clica em bloco SciQuest gastar Director Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour SciQuest gastar Director aplicativo.

## <a name="additional-resources"></a>Recursos adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

