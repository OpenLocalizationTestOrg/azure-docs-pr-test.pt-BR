---
title: "Tutorial: Integração do Azure Active Directory ao Optimizely | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Optimizely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a>Tutorial: Integração do Azure Active Directory ao Optimizely

Neste tutorial, você aprenderá como toointegrate Optimizely com o Azure Active Directory (AD do Azure).

Integrando Optimizely com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooOptimizely
- Você pode habilitar seu usuários tooautomatically get conectado tooOptimizely (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Optimizely, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Optimizely

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Optimizely da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-optimizely-from-hello-gallery"></a>Adicionando Optimizely da Galeria de saudação
integração de saudação tooconfigure de Optimizely no AD do Azure, você precisa tooadd Optimizely da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Optimizely da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Optimizely**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. No painel de resultados de saudação, selecione **Optimizely**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você vai configurar e testar o logon único do Azure AD com o Optimizely, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Optimizely é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Optimizely precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Optimizely.

tooconfigure e teste de logon único do AD do Azure com Optimizely, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Optimizely](#creating-an-optimizely-test-user)**  -toohave um equivalente do Britta Simon em Optimizely é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Optimizely.

**tooconfigure AD do Azure-logon único com Optimizely, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Optimizely** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. Em Olá **Optimizely domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://app.optimizely.net/<instance name>`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`urn:auth0:optimizely:contoso`

    > [!NOTE] 
    > Esses valores não são Olá real. Você atualizará o valor de saudação com URL de logon real hello e o identificador que é explicada posteriormente no tutorial de saudação. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. Em Olá **Optimizely configuração** seção, clique em **configurar Optimizely** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. tooconfigure logon único no **Optimizely** lado, entre em contato com seu gerente de conta Optimizely e fornecer Olá baixado **certificado (Base64)**, e **Single Sign-On URL do serviço SAML** . 

8. No email de tooyour de resposta, Optimizely fornece Olá URL de logon (SSO iniciado por SP) e hello valores do identificador (ID de entidade do provedor de serviço).

    a. Saudação de cópia **URL do SSO iniciado por SP** fornecido por Optimizely e cole no hello **URL de logon** textbox em **Optimizely domínio e URLs** seção no portal do Azure 

    b. Saudação de cópia **ID de entidade do provedor de serviço** fornecido por Optimizely e cole no hello **identificador** textbox em **Optimizely domínio e URLs** seção no portal do Azure 

9. Em uma janela de navegador diferente, logon tooyour Optimizely aplicativo.

10. Clique em nome na parte superior da saudação da conta canto direito e, em seguida, **configurações de conta**.
   
    ![Logon Único do AD do Azure](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. Na guia da conta hello, marque a caixa de saudação **habilitar SSO** em logon único no hello **visão geral** seção.
   
    ![Logon Único do AD do Azure](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. Clique em **Salvar**

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-optimizely-test-user"></a>Criando um usuário de teste do Optimizely

Nesta seção, você cria um usuário chamado Brenda Fernandes no Optimizely.

1. Na home page do hello, selecione **colaboradores** guia.

2. novo projeto de toohello de Colaborador tooadd, clique em **novo parceiro**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. Preencha o endereço de email hello e atribuir uma função. Clique em **Convidar**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. Eles receberão um convite por email. Usando o endereço de email hello, eles têm toolog no tooOptimizely.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooOptimizely.

![Atribuir usuário][200] 

**tooassign Britta Simon tooOptimizely, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Optimizely**.

    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Optimizely Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Optimizely aplicativo. 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

