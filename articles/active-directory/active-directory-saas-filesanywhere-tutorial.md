---
title: "Tutorial: integração do Azure Active Directory com o FilesAnywhere | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e FilesAnywhere."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a>Tutorial: Integração do Azure Active Directory com o FilesAnywhere

Neste tutorial, você aprenderá como toointegrate FilesAnywhere com o Azure Active Directory (AD do Azure).

Integrando FilesAnywhere com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooFilesAnywhere
- Você pode habilitar seu usuários tooautomatically get conectado tooFilesAnywhere (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com FilesAnywhere, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do FilesAnywhere habilitada para logon único


> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.


tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando FilesAnywhere da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure


## <a name="adding-filesanywhere-from-hello-gallery"></a>Adicionando FilesAnywhere da Galeria de saudação
integração de saudação tooconfigure de FilesAnywhere no AD do Azure, você precisa tooadd FilesAnywhere da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd FilesAnywhere da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **FilesAnywhere**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. No painel de resultados de saudação, selecione **FilesAnywhere**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o FilesAnywhere, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em FilesAnywhere é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em FilesAnywhere precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em FilesAnywhere.

tooconfigure e teste de logon único do AD do Azure com FilesAnywhere, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave um equivalente do Britta Simon em FilesAnywhere é a representação toohello vinculado do Azure AD dela.
3. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
4. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo FilesAnywhere.

**tooconfigure AD do Azure-logon único com FilesAnywhere, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **FilesAnywhere** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. Em Olá **FilesAnywhere domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**:

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    a. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`
> [!NOTE]
> Observe que esse valor Olá **215** é um **clientid** e é apenas um exemplo. Você precisa tooreplace com o valor do hello clientid real.

4. Em Olá **FilesAnywhere domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:
    
    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    a. Clique em Olá **Mostrar configurações de URL avançadas** opção

    b. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<sub domain>.filesanywhere.com/`

    > [!NOTE] 
    > Observe que esses não são valores reais de saudação. Você tem tooupdate esses valores com a URL real Olá URL de logon e de resposta. Entre em contato com [FilesAnywhere a equipe de suporte](mailto:support@FilesAnywhere.com) tooget esses valores. 

5. Aplicativo de FilesAnywhere Software espera as asserções de SAML de saudação em um formato específico. Configure Olá declarações para esse aplicativo a seguir. Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo. Olá captura de tela a seguir mostra um exemplo.
    
    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    Olá quando os usuários inscreve-se com FilesAnywhere recebem o valor de saudação do **clientid** de atributo de [FilesAnywhere equipe](mailto:support@FilesAnywhere.com). Você tem o atributo de "Id do cliente" hello tooadd com valor exclusivo de saudação fornecido pela FilesAnywhere. Todos esses atributos mostrados acima são necessários.
    > [!NOTE] 
    > Observe que esse valor Olá **2331** de **clientid** é apenas um exemplo. É necessário o valor real do tooprovide hello.


6. Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:
    
    | Nome do atributo | Valor do atributo |
    | ---------------| --------------- |    
    | clientid | *"uniquevalue"* |

    a. Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    b. Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    c. De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.
    
    d. Clique em **Ok**

7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. Em Olá **FilesAnywhere configuração** seção, clique em **configurar FilesAnywhere** tooopen **configurar o logon** janela.

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. configuração de SSO de tooget concluída para o seu aplicativo FilesAnywhere final, entre em contato com [FilesAnywhere a equipe de suporte](mailto:support@FilesAnywhere.com) e fornecê-los a URL de logon único (SSO) e de certificado de assinatura de token SAML Olá baixado.

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**. 



### <a name="creating-a-filesanywhere-test-user"></a>Criando um usuário de teste do FilesAnywhere

Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação serão criados no aplicativo hello automaticamente. 


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooFilesAnywhere seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooFilesAnywhere, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **FilesAnywhere**.

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    


### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco FilesAnywhere Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour FilesAnywhere aplicativo.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
