---
title: "Tutorial: integração do Azure Active Directory ao FreshDesk | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a>Tutorial: integração do Azure Active Directory ao FreshDesk

Neste tutorial, você aprenderá como toointegrate FreshDesk com o Azure Active Directory (AD do Azure).

Integrando o FreshDesk com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooFreshDesk
- Você pode habilitar seu usuários tooautomatically get conectado tooFreshDesk (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o FreshDesk, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do FreshDesk com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando FreshDesk da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-freshdesk-from-hello-gallery"></a>Adicionando FreshDesk da Galeria de saudação
integração de saudação tooconfigure do FreshDesk no AD do Azure, você precisa tooadd FreshDesk da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd FreshDesk da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **FreshDesk**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. No painel de resultados de saudação, selecione **FreshDesk**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o FreshDesk, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no FreshDesk é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no FreshDesk precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no FreshDesk.

tooconfigure e teste de logon único do AD do Azure com o FreshDesk, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do FreshDesk](#creating-a-freshdesk-test-user)**  -toohave um equivalente do Britta Simon no FreshDesk é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo do Freshservice.

**tooconfigure AD do Azure-logon único com o FreshDesk, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **FreshDesk** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. Em Olá **FreshDesk domínio e URLs** seção, digite Olá **URL de logon** como: `https://<tenant-name>.freshdesk.com` ou qualquer outro valor Freshdesk sugeriu.

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > Observe que esse não é o valor real. Você precisa atualizar o valor com a URL de Entrada real. Para obter esse valor, entre em contato com a [equipe de suporte do cliente FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg).  

4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado** e, em seguida, salve o certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. Em Olá **FreshDesk configuração** seção, clique em **FreshDesk configurar** tooopen configurar o logon na janela. Copiar hello SAML Single Sign-On URL do serviço e a URL de logout de saudação **referência rápida** seção.

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Freshdesk como administrador.

8. No menu de saudação na parte superior de saudação, clique em **Admin**.
   
   ![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")

9. Em Olá **configurações gerais** , clique em **segurança**.
   
   ![Segurança](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Segurança")

10. Em Olá **segurança** , execute Olá etapas a seguir:
   
    ![Logon Único](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Logon Único")
   
    a. Para **SSO (Logon Único)**, selecione **Ativado**.

    b. Selecione **SSO do SAML**.

    c. Saudação de tipo **Single Sign-On URL do serviço SAML** você copiou do portal do Azure para Olá **URL de logon** caixa de texto.

    d. Saudação de tipo **URL de logout** você copiou do portal do Azure para Olá **URL de Logout** caixa de texto.

    e. Saudação de cópia **impressão digital** valor de certificado Olá baixado do portal do Azure e cole-a saudação **impressão digital do certificado de segurança** caixa de texto.  
 
    >[!TIP]
    >Para obter mais detalhes, consulte [como tooretrieve o valor de impressão digital do certificado](http://youtu.be/YKQF266SAxI). 
    
    f. Clique em **Salvar**.


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-freshdesk-test-user"></a>Criar um usuário de teste FreshDesk

Ordem tooenable AD do Azure usuários toolog no FreshDesk, eles devem ser provisionados no FreshDesk.  
No caso de saudação do FreshDesk, o provisionamento é uma tarefa manual.

**tooprovision contas de usuário, executar Olá seguintes etapas:**

1. Faça logon no tooyour **Freshdesk** locatário.
2. No menu de saudação na parte superior de saudação, clique em **Admin**.
   
   ![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")

3. Em Olá **configurações gerais** , clique em **agentes**.
   
   ![Agentes](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agentes")

4. Clique em **Novo Agente**.
   
    ![Novo Agente](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "Novo Agente")

5. Na caixa de diálogo de informações de agentes hello, execute Olá etapas a seguir:
   
   ![Informações de Agente](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Informações de Agente")
   
   a. Em Olá **nome completo** caixa de texto, nome de saudação do tipo da conta de saudação do AD do Azure que você deseja tooprovision.

   b. Em Olá **Email** caixa de texto, Olá tipo AD do Azure endereço de email da conta de saudação do AD do Azure que você deseja tooprovision.

   c. Em Olá **título** caixa de texto, digite o título da saudação da conta de saudação do AD do Azure que você deseja tooprovision.

   d. Selecione **Função de agentes** e clique em **Atribuir**.
       
   e. Clique em **Salvar**.     
   
    >[!NOTE]
    >proprietário de conta do AD do Azure Olá receberá um email que inclui uma conta de saudação do link tooconfirm antes que ele seja ativado. 
    > 
    
    >[!NOTE]
    >Você pode usar qualquer ferramenta de criação outros Freshdesk usuário conta ou APIs fornecidas pelo Freshdesk tooprovision contas de usuário do AAD. tooFreshDesk.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooBox seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooFreshDesk, execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **FreshDesk**.

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco FreshDesk Olá Olá painel de acesso, você deve obter logon página tooget conectado tooyour FreshDesk aplicativo.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

