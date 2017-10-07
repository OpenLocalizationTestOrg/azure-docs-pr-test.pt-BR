---
title: "Tutorial: integração do Azure Active Directory com o xMatters OnDemand | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e xMatters OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a>Tutorial: integração do Azure Active Directory com o xMatters OnDemand

Neste tutorial, você aprenderá como toointegrate xMatters OnDemand com o Azure Active Directory (AD do Azure).

Integrando xMatters OnDemand com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooxMatters sob demanda
- Você pode habilitar seus usuários tooautomatically get conectado tooxMatters OnDemand (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o xMatters OnDemand, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do xMatters OnDemand habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando xMatters OnDemand da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a>Adicionando xMatters OnDemand da Galeria de saudação
integração de saudação tooconfigure do xMatters OnDemand no AD do Azure, você precisa tooadd xMatters OnDemand na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd xMatters OnDemand da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **xMatters OnDemand**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. No painel de resultados de saudação, selecione **xMatters OnDemand**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o xMatters OnDemand com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, AD do Azure precisa tooknow quais Olá usuário correspondente no xMatters OnDemand é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no xMatters OnDemand precisa toobe estabelecida.

No xMatters OnDemand, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o xMatters OnDemand, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)**  -toohave um equivalente do Britta Simon no xMatters OnDemand é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu xMatters OnDemand aplicativo.

**tooconfigure AD do Azure-logon único com o xMatters OnDemand, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **xMatters OnDemand** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. Em Olá **xMatters OnDemand domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com URL de resposta e o identificador de real de saudação. Entre em contato com [equipe de suporte do xMatters OnDemand](https://www.xmatters.com/company/contact-us/) tooget esses valores.

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado do hello localmente como **c:\\XMatters OnDemand.cer**.

    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > Você precisa tooforward Olá certificado toohello [equipe de suporte do xMatters OnDemand](https://www.xmatters.com/company/contact-us/). certificado Olá precisa toobe carregado pela equipe de suporte de xMatters Olá antes de finalizar a configuração de logon único hello. 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. Em Olá **xMatters OnDemand configuração** seção, clique em **configurar xMatters OnDemand** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. Em uma janela do navegador web diferente, faça logon no tooyour site da empresa XMatters OnDemand como um administrador.

8. Na barra de ferramentas de saudação na parte superior do hello, clique em **Admin**e, em seguida, clique em **detalhes da empresa** na barra de navegação Olá Olá lado esquerdo.
   
    ![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")

9. Em Olá **configuração SAML** página, execute Olá etapas a seguir:
   
    ![Configuração SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Configuração SAML")
   
    a. Selecione **Habilitar SAML**.
   
    b. Colar **ID da entidade SAML**, que você copiou de saudação portal do Azure em hello **ID do provedor de identidade** caixa de texto.
   
    c. Colar **Single Sign-On URL do serviço SAML**, que você copiou de saudação portal do Azure em hello **URL de logon único** caixa de texto.
   
    d. Colar **URL de logout**, que você copiou de saudação portal do Azure em hello **URL de Logout único** caixa de texto.
   
    e. Na página de detalhes da empresa hello, na parte superior da saudação, clique em **salvar alterações**.
    
    ![Detalhes da empresa](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Detalhes da empresa")

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-xmatters-ondemand-test-user"></a>Criação de um usuário de teste do xMatters OnDemand

Em ordem tooenable AD do Azure usuários toolog em tooXMatters OnDemand, eles devem ser provisionados no XMatters OnDemand. No caso de saudação do XMatters OnDemand, o provisionamento é uma tarefa manual.

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a>tooprovision contas de usuário, executar Olá seguintes etapas:
1. Faça logon no tooyour **XMatters OnDemand** locatário.

2.  Clique em **usuários** na guia e clique **adicionar usuário**.
  
    ![Usuários](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Usuários")

3. Em Olá **adicionar um usuário** , execute Olá etapas a seguir:
   
    ![Adicionar um Usuário](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Adicionar um Usuário")

    a. Selecione **Ativo**.

    b. Em Olá **ID de usuário** caixa de texto, id de usuário do tipo saudação do usuário como Brittasimon@contoso.com.
   
    c. Em Olá **nome** caixa de texto Nome do primeiro tipo de usuário hello como Britta.

    d. Em Olá **Sobrenome** caixa de texto, digite sobrenome do usuário hello como Simon.
    
    e. Em Olá **Site** caixa de texto, digite site válido do hello de um válida do Azure você deseja tooprovision de conta do AD.
    
    f. Clique em **Salvar**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooxMatters sob demanda.

![Atribuir usuário][200] 

**tooassign Britta Simon tooxMatters OnDemand, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **xMatters OnDemand**.

    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá xMatters OnDemand lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour xMatters OnDemand aplicativo.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

