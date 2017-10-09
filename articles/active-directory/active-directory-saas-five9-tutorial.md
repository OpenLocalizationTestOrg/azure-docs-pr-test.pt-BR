---
title: "Tutorial: Integração do Azure Active Directory ao Five9 Plus Adapter (CTI, Contact Center Agents) | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Five9 mais adaptador (CTI, entre em contato com os agentes Center)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a>Tutorial: Integração do Azure Active Directory ao Five9 Plus Adapter (CTI, Contact Center Agents)

Neste tutorial, você aprenderá como toointegrate Five9 Plus adaptador (CTI, entre em contato com os agentes Center) com o Azure Active Directory (AD do Azure).

Integrar Five9 Plus adaptador (CTI, entre em contato com os agentes Center) com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooFive9 mais adaptador (CTI, entre em contato com os agentes Center)
- Você pode habilitar seus usuários tooautomatically get conectado tooFive9 mais adaptador (CTI, entre em contato com Center agentes) (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração de tooconfigure AD do Azure com Five9 Plus adaptador (CTI, contato Center agentes), você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Five9 Plus Adapter (CTI, Contact Center Agents)

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Five9 Plus adaptador (CTI, entre em contato com os agentes Center) da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a>Adicionando Five9 Plus adaptador (CTI, entre em contato com os agentes Center) da Galeria de saudação
integração de saudação tooconfigure do Five9 mais adaptador (CTI, entre em contato com os agentes Center) no AD do Azure, você precisa tooadd Five9 Plus adaptador (CTI, entre em contato com os agentes Center) na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Five9 Plus adaptador (CTI, entre em contato com os agentes Center) da Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Five9 Plus adaptador (CTI, entre em contato com os agentes Center)**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. No painel de resultados de saudação, selecione **Five9 Plus adaptador (CTI, entre em contato com os agentes Center)**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Five9 Plus Adapter (CTI, Contact Center Agents), com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá Five9 Plus adaptador (CTI, entre em contato com os agentes Center) é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação Five9 Plus adaptador (CTI, entre em contato com Center agentes) deve toobe estabelecida.

Five9 mais adaptador (CTI, entre em contato com os agentes Center), atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com Five9 Plus adaptador (CTI, contato Center agentes), precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Five9 Plus adaptador (CTI, entre em contato com os agentes Center)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave um equivalente de Britta Simon Five9 Plus adaptador (CTI, entre em contato com os agentes Center) que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Five9 Plus adaptador (CTI, entre em contato com os agentes Center).

**tooconfigure logon único do AD do Azure com Five9 Plus adaptador (CTI, entre em contato com os agentes Center), execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Five9 Plus adaptador (CTI, entre em contato com os agentes Center)** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. Em Olá **Five9 Plus adaptador (CTI, entre em contato com os agentes Center) de domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    a. Em Olá **identificador** caixa de texto, digite uma URL usando Olá seguintes padrões:

    |    Ambiente      |       URL      |
    | :-- | :-- |
    | Para o “Five9 Plus Adapter for Microsoft Dynamics CRM” | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | Para o “Five9 Plus Adapter for Zendesk” | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | Para o “Five9 Plus Adapter for Agent Desktop Toolkit” | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:

    |      Ambiente     |      URL      |
    | :--                  | :--           |
    | Para o “Five9 Plus Adapter for Microsoft Dynamics CRM” | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | Para o “Five9 Plus Adapter for Zendesk” | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | Para o “Five9 Plus Adapter for Agent Desktop Toolkit” | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. Em Olá **Five9 Plus adaptador (CTI, entre em contato com os agentes Center) configuração** seção, clique em **configurar Five9 Plus adaptador (CTI, entre em contato com os agentes Center)** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. tooconfigure logon único no **Five9 Plus adaptador (CTI, entre em contato com os agentes Center)** lado, você precisa toosend Olá baixado **Certificate(Base64), URL de logout, ID de entidade de SAML e SAML Single Sign-On URL do serviço** muito[Five9 Plus (CTI, entre em contato com os agentes Center) suporte adaptadoras](https://www.five9.com/about/contact). Também Além disso, para configurar SSO adicional, siga Olá etapas de acordo com o adaptador de toohello abaixo:

    a. Guia do Administrador do “Five9 Plus Adapter for Agent Desktop Toolkit”: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)
    
    b. Guia do Administrador do “Five9 Plus Adapter for Microsoft Dynamics CRM”: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)
    
    c. Guia do Administrador do “Five9 Plus Adapter for Zendesk”: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)


> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a>Criando um usuário de teste do Five9 Plus Adapter (CTI, Contact Center Agents)

Nesta seção, você cria um usuário chamado Brenda Fernandes no Five9 Plus Adapter (CTI, Contact Center Agents). Trabalhar com [Five9 Plus (CTI, entre em contato com os agentes Center) suporte adaptadoras](https://www.five9.com/about/contact) para adicionar usuários de saudação na plataforma do hello Five9 Plus adaptador (CTI, entre em contato com os agentes Center). Os usuários devem ser criados e ativados antes de usar o logon único.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooFive9 além do adaptador (CTI, entre em contato com os agentes Center).

![Atribuir usuário][200] 

**tooassign Britta Simon tooFive9 Plus adaptador (CTI, entre em contato com os agentes Center), execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Five9 Plus adaptador (CTI, entre em contato com os agentes Center)**.

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Five9 Plus adaptador (CTI, entre em contato com os agentes Center) Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Five9 mais adaptador (CTI, entre em contato com os agentes Center).
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

