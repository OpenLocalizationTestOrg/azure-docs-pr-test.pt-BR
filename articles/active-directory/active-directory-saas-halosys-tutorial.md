---
title: "Tutorial: integração do Azure Active Directory com o Halosys | Microsoft Docs"
description: "Saiba como toouse Halosys com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>Tutorial: integração do Azure Active Directory com o Halosys

Neste tutorial, você aprenderá como toointegrate Halosys com o Azure Active Directory (AD do Azure).

Integrando Halosys com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooHalosys
- Você pode habilitar seus usuários tooautomatically get conectado tooHalosys (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Halosys, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Halosys habilitada para logon único


> [!NOTE] 
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.


tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.

cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Halosys da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure


## <a name="adding-halosys-from-hello-gallery"></a>Adicionando Halosys da Galeria de saudação
integração de saudação tooconfigure de Halosys no AD do Azure, você precisa tooadd Halosys da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Halosys da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.

    ![Active Directory][1]
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.

    ![Aplicativos][2]

4. Clique em **adicionar** final Olá Olá página.

    ![Aplicativos][3]

5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.

    ![Aplicativos][4]

6. Na caixa de pesquisa hello, digite **Halosys**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. No painel de resultados de saudação, selecione **Halosys**e, em seguida, clique em **concluir** aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Halosys, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Halosys é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Halosys precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Halosys.

tooconfigure e teste de logon único do AD do Azure com Halosys, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Halosys](#creating-a-halosys-test-user)**  -toohave um equivalente do Britta Simon em Halosys é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal clássico do hello e configurar o logon único no aplicativo Halosys.


**tooconfigure AD do Azure-logon único com Halosys, execute Olá etapas a seguir:**

1. No portal clássico hello, em Olá **Halosys** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.
     
    ![Configurar Logon Único][6] 

2. Em Olá **como você gostaria usuários toosign em tooHalosys** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.

    ![Configurar Logon Único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    a. Em Olá **URL de logon** caixa de texto, digite a URL do hello usada pelo seu aplicativo de Halosys tooyour toosign em usuários usando o saudação padrão a seguir: `https://<company-name>.Halosys.com/client-api/api`.

    Olá b.In **URL de identificador** caixa de texto, digite a URL de saudação em saudação padrão a seguir: `https://<company-name>.Halosys.com`. 
         
4. Em Olá **configurar logon único no Halosys** , clique em **baixar metadados**e, em seguida, salve o arquivo de saudação em seu computador:

    ![Configurar Logon Único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. tooget SSO configurado para o seu aplicativo, entre em contato com a equipe de suporte Halosys e fornecê-los com os seguintes hello:

    • Olá baixado **arquivo de metadados**
    
    • Olá **URL SSO SAML**
    

6. No portal clássico do hello, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.
    
    ![Logon Único do AD do Azure][10]

7. Em Olá **único logon confirmação** , clique em **concluir**.  
 
    ![Logon Único do AD do Azure][11]


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Nesta seção, você pode criar um usuário de teste no portal clássico do hello chamado Britta Simon.


![Criar um usuário do AD do Azure][20]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir: ![criando um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    a. Em Tipo de Usuário, selecione Novo usuário na organização.

    b. Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.

    c. Clique em **Avançar**.

6.  Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir: ![criando um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    a. Em Olá **nome** caixa de texto, tipo **Britta**.  

    b. Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.

    c. Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.

    d. Em Olá **função** lista, selecione **usuário**.

    e. Clique em **Avançar**.

7. Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    a. Anote o valor Olá Olá **nova senha**.

    b. Clique em **Concluído**.   



### <a name="creating-a-halosys-test-user"></a>Criando um usuário de teste do Halosys

Nesta seção, você criará um usuário chamado Brenda Fernandes no Halosys. Trabalhe com Halosys suporte team tooadd Olá usuários na plataforma de Halosys hello.


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooHalosys seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooHalosys, execute Olá etapas a seguir:**

1. No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Halosys**.

    ![Configurar Logon Único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. No menu de saudação na parte superior de saudação, clique em **usuários**.

    ![Atribuir usuário][203]

4. Na lista de usuários hello, selecione **Britta Simon**.

5. Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.

    ![Atribuir usuário][205]


### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá Halosys bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Halosys aplicativo.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
