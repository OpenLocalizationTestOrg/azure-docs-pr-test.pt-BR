---
title: "Tutorial: integração do Azure Active Directory com o ZPA (Zscaler Private Access) | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e acesso privado do Zscaler (ZPA)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a>Tutorial: integração do Azure Active Directory com o ZPA (Zscaler Private Access)

Neste tutorial, você aprenderá como toointegrate Zscaler privada acesso (ZPA) com o Azure Active Directory (AD do Azure).

Integrando Zscaler privada acesso (ZPA) com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooZscaler acesso privado (ZPA)
- Você pode habilitar seu usuários tooautomatically get conectado tooZscaler privada acesso (ZPA) (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Zscaler privada acesso (ZPA), você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura com logon único do ZPA (Zscaler Private Access) habilitado


> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.


tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar acesso privado do Zscaler (ZPA) da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a>Adicionar acesso privado do Zscaler (ZPA) da Galeria de saudação
integração de saudação do tooconfigure do Zscaler privada acesso (ZPA) no AD do Azure, você precisa tooadd acesso privado do Zscaler (ZPA) na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Zscaler privada acesso (ZPA) da Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Zscaler privada acesso (ZPA)**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. No painel de resultados de saudação, selecione **Zscaler privada acesso (ZPA)**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o ZPA (Zscaler Private Access), com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que o usuário de contraparte Olá no Zscaler privada acesso (ZPA) é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado da saudação no Zscaler privada acesso (ZPA) precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Zscaler privada acesso (ZPA).

tooconfigure e teste de logon único do AD do Azure com o Zscaler privada acesso (ZPA), você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Zscaler privada acesso (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)**  -toohave um equivalente do Britta Simon no Zscaler privada acesso (ZPA) que é a representação toohello vinculado do Azure AD dela.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Zscaler privada acesso (ZPA).

**tooconfigure logon único do AD do Azure com o Zscaler privada acesso (ZPA), execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure do hello, no hello **Zscaler privada acesso (ZPA)** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. Em Olá **Zscaler privada acesso (ZPA) de domínio e URLs** , execute Olá etapas a seguir:
    
    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`

    b. Em Olá **identificador** caixa de texto, tipo:`https://samlsp.private.zscaler.com/auth/metadata`

    > [!NOTE] 
    > Observe que esses não são valores reais de saudação. Você tem tooupdate entrassem esses valores com hello real na URL e o identificador. Aqui, sugerimos você toouse Olá valor exclusivo de URL em Olá identificador. Entre em contato com [equipe de suporte do Zscaler privada acesso (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooget esses valores.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **criar novo certificado**.

    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. Em Olá **criar um novo certificado** caixa de diálogo, clique o ícone de calendário hello e selecione um **data de expiração**. Em seguida, clique no botão **Salvar**.

    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. Em Olá **o certificado de autenticação SAML** seção, selecione **ativar o novo certificado** e clique em **salvar** botão.

    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. Na janela pop-up de saudação **certificado de substituição** janela, clique em **Okey**.

    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. Em uma janela diferente do navegador da Web, faça logon no site ZPA (Zscaler Private Access) da sua empresa como administrador.

10. Navegue muito**administrador** e, em seguida, clique em **Idp configuração**.

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. Em Olá **Idp configuração** seção, clique em **adicionar nova configuração IDP**.

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. Em Olá **nova configuração IDP** , execute Olá etapas a seguir:

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    a. Clique em **Selecionar Arquivo** e carregue o arquivo de metadados baixado.

    b. Clique no botão **Salvar** .
    


### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**. 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a>Criar um usuário de teste do ZPA (Zscaler Private Access)

Nesta seção, você deve criar uma usuária chamada Brenda Fernandes no ZPA (Zscaler Private Access). Trabalhe com [equipe de suporte do Zscaler privada acesso (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooadd usuários de saudação na plataforma do hello Zscaler privada acesso (ZPA).


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooZscaler seu acesso acesso privado (ZPA).

![Atribuir usuário][200] 

**tooassign Britta Simon tooZscaler acesso privado (ZPA), execute Olá etapas a seguir:**

1. No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Zscaler privada acesso (ZPA)**.

    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    


### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Zscaler privada acesso (ZPA) Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Zscaler privada acesso (ZPA).


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png