---
title: "Tutorial: integração do Azure Active Directory com o Adaptive Suite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o pacote adaptável."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a>Tutorial: Integração do Active Directory do Azure ao Adaptive Suite

Neste tutorial, você aprenderá como toointegrate pacote adaptável com o Azure Active Directory (AD do Azure).

Pacote adaptável integrando o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooAdaptive Suite
- Você pode habilitar seu usuários tooautomatically get conectado tooAdaptive Suite (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o pacote adaptável, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Adaptive Suite

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando pacote adaptável da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-adaptive-suite-from-hello-gallery"></a>Adicionando pacote adaptável da Galeria de saudação
integração de saudação tooconfigure do pacote adaptável no AD do Azure, você precisa tooadd pacote adaptável de lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd pacote adaptável da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **pacote adaptável**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. No painel de resultados de saudação, selecione **pacote adaptável**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Adaptive Suite, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no pacote adaptável é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no pacote adaptável precisa toobe estabelecida.

Pacote adaptável, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o pacote adaptável, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do pacote adaptável](#creating-an-adaptive-suite-test-user)**  -toohave um equivalente do Britta Simon no pacote adaptável que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de pacote adaptável.

**tooconfigure AD do Azure-logon único com o pacote adaptável, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **pacote adaptável** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. Em Olá **domínio adaptável de pacote e as URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`

    >[!NOTE]
    > Você pode obter esse valor de saudação pacote adaptável **configurações de SSO do SAML** página.
    >  

4. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. Em Olá **adaptável configuração do conjunto** seção, clique em **configurar pacote adaptável** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. Em uma janela de navegador web diferente, faça logon no site da empresa tooyour pacote adaptável como um administrador.

8. Vá muito**Admin**.
   
    ![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")

9. Em Olá **usuários e funções** seção, clique em **gerenciar configurações de SSO de SAML**.
   
    ![Gerenciar Configurações de SSO do SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Gerenciar Configurações de SSO do SAML")

10. Em Olá **configurações de SSO do SAML** página, execute Olá etapas a seguir:
   
    ![Configurações de SSO do SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "Configurações de SSO do SAML")

    a. Em Olá **nome do provedor de identidade** caixa de texto, digite um nome para a sua configuração.
    
    b. Saudação de colar **ID da entidade SAML** valor copiado do portal do Azure para Olá **ID da entidade do provedor de identidade** caixa de texto.
  
    c. Saudação de colar **Single Sign-On URL do serviço SAML** valor copiado do portal do Azure para Olá **URL do SSO do provedor de identidade** caixa de texto.
  
    d. Saudação de colar **Single Sign-On URL do serviço SAML** valor copiado do portal do Azure para Olá **URL personalizada do logout** caixa de texto.
  
    e. tooupload seu certificado baixado, clique em **Escolher arquivo**.
  
    f. Selecione o seguinte hello, para:
    * **ID de usuário do SAML**, selecione **Nome de usuário do Adaptive Insights do Usuário**.
    * **Local da ID de usuário do SAML**, selecione **ID de usuário em NameID da Entidade**.
    * **Formato de NameID do SAML**, selecione **Endereço de email**.
    * **Habilitar SAML**, selecione **Permitir SSO do SAML e direcionar logon do Adaptive Insights**.
    
    g. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-adaptive-suite-test-user"></a>Criando de um usuário de teste do Adaptive Suite

tooenable AD do Azure usuários toolog em tooAdaptive Suite, eles devem ser provisionados no pacote adaptável.  

* No caso de saudação do pacote adaptável, o provisionamento é uma tarefa manual.

**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:** 

1. Faça logon no tooyour **pacote adaptável** site da empresa como um administrador.
2. Vá muito**Admin**.
   
   ![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")
3. Em Olá **usuários e funções** seção, clique em **adicionar usuário**.
   
   ![Adicionar Usuário](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Adicionar Usuário")
4. Em Olá **novo usuário** , execute Olá etapas a seguir:
   
   ![Enviar](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Enviar")   

   a. Saudação de tipo **nome**, **Login**, **Email**, **senha** de um usuário válido do Active Directory do Azure que você deseja tooprovision em Olá relacionado caixas de texto.
  
   b. Selecione uma **Função**.
  
   c. Clique em **Enviar**.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outro pacote adaptável usuário conta ou APIs fornecidas pelo pacote adaptável tooprovision contas de usuário do AAD.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAdaptive Suite.

![Atribuir usuário][200] 

**tooassign Britta Simon tooAdaptive Suite, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **pacote adaptável**.

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Olá o objetivo desta seção é tootest seu AD do Microsoft Azure Single Sign-On configuração usando Olá painel de acesso.

Quando você clica em um bloco de pacote adaptável Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de pacote adaptável.


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

