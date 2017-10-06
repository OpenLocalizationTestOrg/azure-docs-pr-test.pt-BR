---
title: "Tutorial: Integração do Azure Active Directory ao Velpic SAML | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Velpic SAML."
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
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a>Tutorial: Integração do Azure Active Directory ao Velpic SAML

Neste tutorial, você aprenderá como toointegrate Velpic SAML com o Azure Active Directory (AD do Azure).

Integrando Velpic SAML com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooVelpic SAML
- Você pode habilitar seu usuários tooautomatically get conectado tooVelpic SAML (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Velpic SAML, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Velpic SAML habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Velpic SAML da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-velpic-saml-from-hello-gallery"></a>Adicionando Velpic SAML da Galeria de saudação
integração de saudação tooconfigure do Velpic SAML no AD do Azure, você precisa tooadd Velpic SAML na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Velpic SAML da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Velpic SAML**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. No painel de resultados de saudação, selecione **Velpic SAML**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Velpic SAML, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Velpic SAML é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Velpic SAML precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Velpic SAML.

tooconfigure e teste de logon único do AD do Azure com Velpic SAML, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave um equivalente do Britta Simon no Velpic SAML que é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Velpic SAML.

**tooconfigure AD do Azure-logon único com SAML Velpic, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **Velpic SAML** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. Insira os detalhes de saudação em Olá **Velpic SAML domínio e URLs** seção -

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    a. Em Olá **URL de logon** texto, o valor do tipo hello como:`https://<sub-domain>.velpicsaml.net`

    b. Em Olá **identificador** caixa de texto, colar Olá **'URL do logon único'** valor`https://auth.velpic.com/saml/v2/<entity-id>/login`
    
    > [!NOTE]
    > Observe que Olá URL de logon será fornecida pelo Olá team Velpic SAML e o valor de identificador estarão disponível quando você configura Olá plug-in do SSO no lado Velpic SAML. É necessário toocopy que o valor da página de aplicativo Velpic SAML e cole-o aqui.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. No hello seção de configuração de SAML Velpic, clique em Configurar Velpic SAML tooopen configurar logon na janela. Copie Olá SAML ID da entidade de saudação seção de referência rápida.

7. Em uma janela diferente do navegador da Web, faça logon no site do Velpic SAML na sua empresa como administrador.

8. Clique em **gerenciar** guia e vá muito**integração** seção onde você precisa de tooclick em **plug-ins** botão toocreate novo plug-in para entrar.

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. Clique em Olá **'Adicionar plug-in'** botão.
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. Clique em Olá **SAML** lado a lado na página de adicionar plug-in de saudação.
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. Insira nome de saudação do hello novo SAML plug-in e clique em Olá **'Add'** botão.

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. Insira os detalhes de saudação da seguinte maneira:

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    a. Em Olá **nome** caixa de texto Nome do tipo saudação do plug-in SAML.

    b. Em hello **URL do emissor** textbox, colar Olá **ID da entidade SAML** você copiou da saudação **configurar o logon** janela de saudação portal do Azure.

    c. Em Olá **configuração do provedor de metadados** carregar Olá arquivo Metadata XML que você baixou do portal do Azure.

    d. Você também pode escolher tooenable SAML apenas durante o provisionamento, permitindo Olá **'Criação automática de novos usuários'** caixa de seleção. Se um usuário não existe no Velpic e esse sinalizador não estiver habilitado, o logon de saudação do Azure falhará. Se o sinalizador Olá será habilitado Olá usuário automaticamente ser provisionados no Velpic no tempo de saudação do logon. 

    e. Saudação de cópia **URL do logon único** da caixa de texto de saudação e colar no hello portal do Azure.
    
    f. Clique em **Salvar**.

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-velpic-saml-test-user"></a>Criando um usuário de teste no Velpic SAML

Esta etapa geralmente não é necessária como aplicativo hello dá suporte apenas durante o provisionamento do usuário. Se o provisionamento de usuário automático de saudação não estiver habilitado, em seguida, criação manual do usuário pode ser feita conforme descrito abaixo.

Entre no site da empresa do seu Velpic SAML como um administrador e execute as seguintes etapas:
    
1. Clique na guia gerenciar e vá tooUsers seção, clique no novo usuários tooadd de botão.

    ![adicionar usuário](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. Em Olá **"Criar novo usuário"** caixa de diálogo de página, execute Olá etapas a seguir.

    ![usuário](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    a. Em Olá **nome** caixa de texto, tipo hello nome Britta Simon.

    b. Em Olá **Sobrenome** caixa de texto, digite Olá sobrenome do Britta Simon.

    c. Em Olá **nome de usuário** caixa de texto, nome de usuário do tipo saudação do Britta Simon.

    d. Em Olá **Email** caixa de texto, tipo hello endereço de email da conta de Britta Simon.

    e. O restante das informações de saudação é opcional, que você pode preenchê-lo se necessário.
    
    f. Clique em **SALVAR**.  

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooVelpic seu acesso SAML.

![Atribuir usuário][200] 

**tooassign Britta Simon tooVelpic SAML, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Velpic SAML**.

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

1. Quando você clica em Olá Velpic SAML bloco no painel de acesso de saudação, você deve obter a página de logon do aplicativo Velpic SAML. Você deve ver Olá **'Fazer logon com o AD do Azure'** botão na página de entrada hello.

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. Clique em Olá **'Fazer logon com o AD do Azure'** botão toolog em tooVelpic usando sua conta do AD do Azure.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

