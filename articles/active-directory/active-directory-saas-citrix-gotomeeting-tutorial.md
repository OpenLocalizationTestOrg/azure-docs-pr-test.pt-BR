---
title: "Tutorial: integração do Azure Active Directory ao Citrix GoToMeeting | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 46a5da7504806202a5ec29f73c504e772c61bc2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a>Tutorial: integração do Active Directory do Azure ao Citrix GoToMeeting

Neste tutorial, você aprenderá como toointegrate Citrix GoToMeeting com o Azure Active Directory (AD do Azure).

Integração do Citrix GoToMeeting com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooCitrix GoToMeeting
- Você pode habilitar seu usuários tooautomatically get conectado tooCitrix GoToMeeting (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do Azure AD com Citrix GoToMeeting, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Citrix GoToMeeting habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Citrix GoToMeeting da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-citrix-gotomeeting-from-hello-gallery"></a>Adicionando Citrix GoToMeeting da Galeria de saudação
integração de saudação tooconfigure do Citrix GoToMeeting no AD do Azure, você precisa tooadd Citrix GoToMeeting da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Citrix GoToMeeting da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Citrix GoToMeeting**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. No painel de resultados de saudação, selecione **Citrix GoToMeeting**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Citrix GoToMeeting com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Citrix GoToMeeting é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Citrix GoToMeeting precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Citrix GoToMeeting.

tooconfigure e teste de logon único do Azure AD com Citrix GoToMeeting, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)**  -toohave um equivalente do Britta Simon no Citrix GoToMeeting que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Citrix GoToMeeting.

**tooconfigure AD do Azure-logon único com o Citrix GoToMeeting, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Citrix GoToMeeting** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. Em Olá **URLs e Citrix GoToMeeting domínio** seção tooperform sem necessidade de todas as etapas.

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. No hello seção de configuração da Citrix GoToMeeting SAML, clique em Configurar SAML do Citrix GoToMeeting tooopen configurar logon na janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

6. Em uma janela de navegador diferente, faça logon no tooyour [Citrix organização Center](https://account.citrixonline.com/organization/administration/).

7. Clique em Olá **provedor de identidade** guia e, em seguida, executar Olá etapas a seguir:  
   
    ![Instalação do SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Instalação do SAML")
   
    a. Selecione **Manual**

    b. Em Olá portal do Azure, Olá **configurar logon único no Citrix GoToMeeting** página de diálogo, Olá cópia **Single Sign-On URL do serviço SAML** valor e, em seguida, cole-o em Olá **na página de entrada URL** caixa de texto. 

    c. Em Olá portal do Azure, Olá **configurar logon único no Citrix GoToMeeting** página de diálogo, Olá cópia **URL de logout** valor e, em seguida, cole-o em Olá **URL da página de logout**caixa de texto.

    d. Em Olá portal do Azure, Olá **configurar logon único no Citrix GoToMeeting** página de diálogo, Olá cópia **ID da entidade SAML** valor e, em seguida, cole-Olá **ID de entidade do provedor de identidade**  caixa de texto.

    e. tooupload seu certificado baixado, clique em **carregar certificado**.

    f. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a>Criando um usuário de teste do Citrix GoToMeeting

Nesta seção, é criado um usuário chamado Brenda Fernandes no Citrix GoToMeeting. O Citrix GoToMeeting dá suporte ao provisionamento just-in-time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Se um usuário não existir no Citrix GoToMeeting, um novo é criado quando você tenta tooaccess Citrix GoToMeeting.

>[!Note]
>Se você precisar toocreate um usuário manualmente, entre em contato com [equipe de suporte do Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting) 


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCitrix GoToMeeting.

![Atribuir usuário][200] 

**tooassign tooCitrix Britta Simon GoToMeeting, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Citrix GoToMeeting**.

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso. Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Provisionamento de Usuário](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

