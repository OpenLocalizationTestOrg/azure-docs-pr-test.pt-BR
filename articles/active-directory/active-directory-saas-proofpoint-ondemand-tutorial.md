---
title: "Tutorial: integração do Azure Active Directory com o Proofpoint on Demand | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Proofpoint sob demanda."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0f9472ddc01f2c18ffc9e8d2b59a17b3b595515e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a>Tutorial: integração do Azure Active Directory ao Proofpoint on Demand

Neste tutorial, você aprenderá como toointegrate Proofpoint sob demanda com o Azure Active Directory (AD do Azure).

Integrando Proofpoint sob demanda com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooProofpoint sob demanda
- Você pode habilitar seu usuários tooautomatically get conectado tooProofpoint sob demanda (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do AD do Azure de tooconfigure com Proofpoint sob demanda, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura de logon único do Proofpoint on Demand habilitada

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Proofpoint sob demanda da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-proofpoint-on-demand-from-hello-gallery"></a>Adicionando Proofpoint sob demanda da Galeria de saudação
integração de saudação tooconfigure do Proofpoint sob demanda no Azure AD, é necessário tooadd Proofpoint sob demanda na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Proofpoint sob demanda da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Proofpoint sob demanda**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. No painel de resultados de saudação, selecione **Proofpoint sob demanda**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Proofpoint on Demand com base em uma usuária de teste chamada “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Proofpoint sob demanda é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Proofpoint sob demanda precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Proofpoint sob demanda.

teste do AD do Azure e tooconfigure o logon único com Proofpoint sob demanda, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criando um Proofpoint no usuário de teste de demanda](#creating-a-proofpoint-on-demand-test-user)**  -toohave um equivalente do Britta Simon em Proofpoint sob demanda que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu Proofpoint no aplicativo de demanda.

**tooconfigure AD do Azure-logon único com Proofpoint sob demanda, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Proofpoint sob demanda** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
  
    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. Em Olá **Proofpoint no domínio de demanda e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    Olá a.In **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<hostname>.pphosted.com/ppssamlsp_hostname`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<hostname>.pphosted.com/ppssamlsp`

    c.  Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`
     
    > [!NOTE] 
    > Esses valores não são Olá real. Atualizar esses valores com hello real identificador, a URL de resposta e a URL de logon. Entre em contato com [Proofpoint da equipe de suporte de cliente de demanda](https://www.proofpoint.com/us/support-services) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. Em Olá **Proofpoint na configuração de demanda** seção, clique em **Proofpoint configurar sob demanda** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. tooconfigure logon único no **Proofpoint sob demanda** lado, você precisa toosend Olá baixado **Certificate(Base64)**,**ID da entidade SAML**, e **SAML URL do serviço de logon em um único** muito[Proofpoint da equipe de suporte de cliente de demanda](https://www.proofpoint.com/us/support-services).

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. Esses valores não são Olá real. Atualizar esses valores com hello real
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **Britta Simon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a>Criar um usuário de teste do Proofpoint on Demand

Nesta seção, você cria uma usuária chamada Brenda Fernandes no Proofpoint on Demand. Trabalhar com [Proofpoint da equipe de suporte de cliente de demanda](https://www.proofpoint.com/us/support-services) tooadd usuários Olá Proofpoint na plataforma de demanda.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooProofpoint sob demanda.

![Atribuir usuário][200] 

**tooassign tooProofpoint Britta Simon sob demanda, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Proofpoint sob demanda**.

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá **Proofpoint sob demanda** bloco Olá painel de acesso, você deve ser conectado automaticamente em tooyour Proofpoint no aplicativo de demanda.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).  

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

