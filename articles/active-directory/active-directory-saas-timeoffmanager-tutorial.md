---
title: "Tutorial: integração do Azure Active Directory ao TimeOffManager | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a>Tutorial: Integração do Active Directory do Azure ao TimeOffManager

Neste tutorial, você aprenderá como toointegrate TimeOffManager com o Azure Active Directory (AD do Azure).

Integrando o TimeOffManager com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooTimeOffManager
- Você pode habilitar seu usuários tooautomatically get conectado tooTimeOffManager (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o TimeOffManager, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do TimeOffManager

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionar TimeOffManager da Galeria de saudação
2. Configurar e testar logon único do Azure AD

## <a name="add-timeoffmanager-from-hello-gallery"></a>Adicionar TimeOffManager da Galeria de saudação
integração de saudação tooconfigure do TimeOffManager no AD do Azure, você precisa tooadd TimeOffManager na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd TimeOffManager da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **TimeOffManager**, selecione **TimeOffManager** do painel de resultados e clique **adicionar** botão aplicativo hello de tooadd.

    ![Adicionar da galeria](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD
Nesta seção, você configurará e testará o logon único do Azure AD com o TimeOffManager, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no TimeOffManager é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no TimeOffManager precisa toobe estabelecida.

No TimeOffManager, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o TimeOffManager, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave um equivalente do Britta Simon no TimeOffManager é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do TimeOffManager.

**tooconfigure AD do Azure-logon único com o TimeOffManager, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **TimeOffManager** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Logon baseado em SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. Em Olá **TimeOffManager domínio e URLs** , execute o seguinte hello:

     ![Seção Domínio e URLs do TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`

    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com hello URL de resposta real. Você pode obter esse valor de **página Configurações de logon único** que é explicado posteriormente no tutorial de saudação ou entre em contato com [equipe de suporte do TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooTimeOffManger com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.
    
    Seu aplicativo TimeOffManger espera as asserções de SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML. Olá captura de tela a seguir mostra um exemplo.

    ![Atributos de Token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "Atributos de Token SAML")
    
    | Nome do atributo | Valor do atributo |
    | --- | --- |
    | Firstname |User.givenname |
    | Sobrenome |User.surname |
    | Email |User.mail |
    
    a.  Para cada linha de dados na tabela de saudação acima, clique em **Adicionar atributo de usuário**.
    
    ![Atributos de Token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "Atributos de Token SAML")
    
    ![Atributos de Token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "Atributos de Token SAML")
    
    b.  Em Olá **nome do atributo** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
    
    c.  Em Olá **o valor do atributo** texto, o valor do atributo select Olá mostrado para aquela linha.
    
    d.  Clique em **OK**.
    
6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. Em Olá **TimeOffManager configuração** seção, clique em **configurar TimeOffManager** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Seção de configuração do TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. Em outra janela do navegador da Web, faça logon em seu site de empresa TimeOffManager como um administrador.

9. Vá muito**conta \> opções de conta \> configurações de logon único**.
   
   ![Configurações de Logon Único](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Configurações de Logon Único")
7. Em Olá **configurações de logon único** , execute Olá etapas a seguir:
   
   ![Configurações de Logon Único](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Configurações de Logon Único")
   
   a. Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e cole Olá certificado inteiro na **certificado x. 509** caixa de texto.
   
   b. Em **emissor Idp** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.
   
   c. Em **URL de ponto de extremidade IdP** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.
   
   d. Para **Impor SAML**, selecione **Não**.
   
   e. Para **Criação Automática de Usuários**, selecione **Sim**.
   
   f. Em **URL de Logout** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.
   
   g. Clique em **Salvar Alterações**.

11. Em **configurações de logon único** página cópia Olá valor **URL do serviço de consumidor de declaração** e cole-o no hello **URL de resposta** caixa de texto em **TimeOffManager Domínio e URLs** seção no portal do Azure. 

      ![Configurações de Logon Único](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Configurações de Logon Único")

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Usuários e grupos --> Todos os usuários](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Botão Adicionar](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Página da caixa de diálogo do usuário](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-timeoffmanager-test-user"></a>Criar um usuário de teste do TimeOffManager

Ordem tooenable AD do Azure usuários toolog no TimeOffManager, elas devem ser provisionado tooTimeOffManager.  

O TimeOffManager dá suporte ao provisionamento de usuário just in time. Não há nenhum item de ação para você.  

usuários de saudação são adicionados automaticamente durante o primeiro logon de saudação usando o logon único.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros TimeOffManager usuário conta ou APIs fornecidas pelo TimeOffManager tooprovision contas de usuário do AD do Azure.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTimeOffManager.

![Atribuir usuário][200] 

**tooassign Britta Simon tooTimeOffManager, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **TimeOffManager**.

    ![TimeOffManager na lista de aplicativos](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco TimeOffManager Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour TimeOffManager aplicativo. Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

