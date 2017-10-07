---
title: "Tutorial: Integração do Azure Active Directory ao Bynder | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>Tutorial: Integração do Azure Active Directory ao Bynder
Olá objetivo deste tutorial é tooshow você como toointegrate Bynder com o Azure Active Directory (AD do Azure).

Integrando Bynder com o AD do Azure fornece Olá benefícios a seguir:

* Você pode controlar no AD do Azure que tenha acesso tooBynder
* Você pode habilitar seu usuários tooautomatically get conectado tooBynder-logon único (SSO) com suas contas do AD do Azure
* Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
tooconfigure integração do AD do Azure com Bynder, você precisa Olá itens a seguir:

* Uma assinatura do AD do Azure
* Uma assinatura habilitada para SSO (logon único) do Bynder

>[!NOTE]
>Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção. 
> 

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

* Não use o ambiente de produção, a menos que seja necessário.
* Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Olá objetivo deste tutorial é tooenable você tootest SSO do Microsoft Azure AD em um ambiente de teste.

cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Bynder da Galeria de saudação
2. Configuração e testes do SSO do Microsoft Azure AD

## <a name="add-bynder-from-hello-gallery"></a>Adicionar Bynder da Galeria de saudação
integração de saudação tooconfigure de Bynder no AD do Azure, você precisa tooadd Bynder da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Bynder da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá **Portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**. 
   
    ![Active Directory][1]
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Aplicativos][2]
4. Clique em **adicionar** final Olá Olá página.
   
    ![Aplicativos][3]
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Aplicativos][4]
6. Na caixa de pesquisa hello, digite **Bynder**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. No painel de resultados de saudação, selecione **Bynder**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
    ![Selecionar aplicativo hello na Galeria de saudação](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Configurar e testar o SSO do Microsoft Azure AD
Olá o objetivo desta seção é tooshow como tooconfigure e Microsoft Azure AD SSO com Bynder de teste com base em um usuário de teste chamado "Britta Simon".

Para SSO toowork, o AD do Azure precisa tooknow que usuário de contraparte Olá Bynder tooan usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Bynder precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Bynder.

tooconfigure e Microsoft Azure AD SSO com Bynder de teste, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurar o logon único do Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Microsoft Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Bynder](#creating-a-bynder-test-user)**  -toohave um equivalente do Britta Simon em Bynder é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable toouse Britta Simon AD do Microsoft Azure Single Sign-On.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-microsoft-azure-ad-sso"></a>Configuração do SSO do Microsoft Azure AD
Nesta seção, habilitar SSO de AD do Microsoft Azure no portal clássico do hello e configurar o SSO em seu aplicativo Bynder.

**tooconfigure Microsoft Azure AD SSO com Bynder, execute Olá etapas a seguir:**

1. No portal clássico hello, em Olá **Bynder** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.
   
    ![Configurar Logon Único][6] 
2. Em Olá **como você gostaria usuários toosign em tooBynder** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. Em Olá **definir configurações de aplicativo** página de diálogo, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**, execute Olá etapas a seguir e clique em **próximo**:
   
    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. Clique em **Avançar**.
4. Se desejar que o aplicativo hello tooconfigure **modo iniciado do SP** em Olá **definir configurações de aplicativo** página de diálogo, em seguida, clique em Olá **"Show advanced configurações (opcional)"**e, em seguida, digite Olá **URL de logon** e clique em **próximo**.

    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.getbynder.com/login/`
  2. Clique em **Avançar**.
  
   >[!NOTE]
   >valor Olá Olá URL de logon neste tutorial é apenas um placeholfer. saudação de tooget valor real para o seu ambiente, entre em contato com Bynder.
   >

5. Em Olá **configurar logon único no Bynder** página, execute Olá etapas a seguir e clique em **próximo**:
   
    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. Clique em **baixar metadados**e, em seguida, salve o arquivo de saudação em seu computador.
  2. Clique em **Avançar**.
6. tooget SSO configurado para o seu aplicativo, entre em contato com sua equipe de suporte de Bynder. Anexar o arquivo de metadados baixado hello e compartilhá-lo com tooset de equipe Bynder o logon único em seu lado.
7. No portal clássico do hello, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.
   
    ![Logon Único do AD do Azure][10]
8. Em Olá **único logon confirmação** , clique em **concluir**.  
   
    ![Logon Único do AD do Azure][11]

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no portal clássico do hello chamado Britta Simon.

![Criar um usuário do AD do Azure][20]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **Portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. Em Tipo de Usuário, selecione Novo usuário na organização.
  2. Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.
  3. Clique em **Avançar**.
6. Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. Em Olá **nome** caixa de texto, tipo **Britta**.  
  2. Em Olá **Sobrenome** caixa de texto, tipo, **Simon**. 
  3. Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.
  4. Em Olá **função** lista, selecione **usuário**.
  5. Clique em **Avançar**.
7. Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Anote o valor Olá Olá **nova senha**.
   2. Clique em **Concluído**.   

### <a name="create-a-bynder-test-user"></a>Criar um usuário de teste do Bynder
Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Bynder. O Bynder dá suporte ao provisionamento just-in-time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Será criado um novo usuário durante uma tentativa tooaccess Bynder se ele ainda não existir.

>[!NOTE]
>Se você precisar toocreate um usuário manualmente, é necessário a equipe de suporte de Bynder toocontact hello. 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure
Olá objetivo desta seção é tooenabling Britta Simon toouse Azure SSO concedendo tooBynder seu acesso.

   ![Atribuir usuário][200]

**tooassign Britta Simon tooBynder, execute Olá etapas a seguir:**

1. No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.
   
    ![Atribuir usuário][201]
2. Na lista de aplicativos hello, selecione **Bynder**.
   
    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. No menu de saudação na parte superior de saudação, clique em **usuários**.
   
    ![Atribuir usuário][203]
4. Na lista de usuários hello, selecione **Britta Simon**.
5. Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.
   
    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a>Testar logon único
Olá o objetivo desta seção é tootest sua configuração de SSO do Microsoft Azure AD usando Olá painel de acesso.

Quando você clica em bloco Bynder Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Bynder aplicativo.

## <a name="additional-resources"></a>Recursos adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
