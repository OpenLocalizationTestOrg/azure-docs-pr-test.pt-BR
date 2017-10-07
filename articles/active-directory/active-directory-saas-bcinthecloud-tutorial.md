---
title: "Tutorial: Integração do Active Directory do Azure com continuidade de negócios na nuvem de saudação | Microsoft Docs"
description: "Saiba como tooconfigure logon único entre o Active Directory do Azure e continuidade de negócios em Olá nuvem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: e81ffb522b2c96c7e9b2919abd8d3b199c295eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-hello-cloud"></a>Tutorial: Integração do Active Directory do Azure com continuidade de negócios na nuvem de saudação

Neste tutorial, você aprenderá como toointegrate BC em Olá nuvem com o Azure Active Directory (AD do Azure).

Integração de continuidade de negócios em Olá nuvem com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooBC em Olá nuvem
- Você pode habilitar seu usuários tooautomatically get conectado tooBC em Olá nuvem (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com continuidade de negócios na nuvem do hello, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Continuidade de negócios em Olá logon único de nuvem na assinatura habilitada

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando a continuidade de negócios em Olá nuvem da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-bc-in-hello-cloud-from-hello-gallery"></a>Adicionando a continuidade de negócios em Olá nuvem da Galeria de saudação
integração de saudação tooconfigure de continuidade de negócios em Olá nuvem no Azure AD, é necessário tooadd BC em Olá nuvem na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd BC em Olá nuvem da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **adicionar** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **continuidade de negócios na nuvem de saudação**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. No painel de resultados de saudação, selecione **continuidade de negócios na nuvem de saudação**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, configurar e testar o AD do Azure-logon único com BC em Olá baseada em nuvem em um usuário de teste chamado "Britta Simon".

Para toowork de logon único, AD do Azure precisa tooknow quais Olá usuário correspondente na continuidade de negócios na nuvem de saudação é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na continuidade de negócios na nuvem de saudação precisa toobe estabelecida.

Na continuidade de negócios na nuvem do hello, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com continuidade de negócios na nuvem de Olá, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criando uma continuidade de negócios no usuário de teste de nuvem Olá](#creating-a-bc-in-the-cloud-test-user)**  -toohave um equivalente do Britta Simon na continuidade de negócios em Olá nuvem que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único na continuidade de negócios no aplicativo de nuvem hello.

**tooconfigure AD do Azure-logon único com continuidade de negócios na nuvem, de saudação execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **continuidade de negócios na nuvem de saudação** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. Em Olá **BC em hello domínio de nuvem e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://app.bcinthecloud.com/router/loginSaml/<customerid>`

    b. Em Olá **identificador** caixa de texto, digite um URL como:`https://app.bcinthecloud.com`

    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com hello URL de logon real. Entre em contato com [BC na equipe de suporte de cliente de nuvem Olá](https://www.bcinthecloud.com/supportcenter/) tooget esse valor. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. tooconfigure logon único no **continuidade de negócios na nuvem de saudação** lado, você precisa toosend Olá baixado **Metadata XML** muito[BC na equipe de suporte de nuvem Olá](https://www.bcinthecloud.com/supportcenter/).

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-bc-in-hello-cloud-test-user"></a>Criando uma continuidade de negócios no usuário de teste de nuvem Olá

Nesta seção, você deve criar um usuário chamado Britta Simon na continuidade de negócios na nuvem de saudação. Trabalhar com [BC na equipe de suporte de cliente de nuvem Olá](https://www.bcinthecloud.com/supportcenter/) para adicionar usuários Olá Olá BC em Olá aplicativo em nuvem. Os usuários devem ser criados e ativados antes de usar o logon único. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBC em Olá nuvem.

![Atribuir usuário][200] 

**tooassign Britta Simon tooBC em Olá nuvem, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **continuidade de negócios na nuvem de saudação**.

    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

 Quando você clica em Olá BC no bloco de nuvem Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour BC em Olá aplicativo em nuvem. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

