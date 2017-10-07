---
title: "Tutorial: integração do Azure Active Directory com o BlueJeans | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure com BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a>Tutorial: Integração do Azure Active Directory ao BlueJeans

Neste tutorial, você aprenderá como toointegrate BlueJeans com o Azure Active Directory (AD do Azure).

Integrando BlueJeans com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooBlueJeans
- Você pode habilitar seus usuários tooautomatically get conectado tooBlueJeans (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com BlueJeans, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do BlueJeans

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando BlueJeans da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-bluejeans-from-hello-gallery"></a>Adicionando BlueJeans da Galeria de saudação
integração de saudação tooconfigure do BlueJeans no AD do Azure, você precisa tooadd BlueJeans da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd BlueJeans da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **BlueJeans**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. No painel de resultados de saudação, selecione **BlueJeans**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o BlueJeans, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no BlueJeans é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no BlueJeans precisa toobe estabelecida.

No BlueJeans, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com BlueJeans, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do BlueJeans](#creating-a-bluejeans-test-user)**  -toohave um equivalente do Britta Simon no BlueJeans que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo BlueJeans.

**tooconfigure AD do Azure-logon único com BlueJeans, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **BlueJeans** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. Em Olá **BlueJeans domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.BlueJeans.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.BlueJeans.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente BlueJeans](https://support.bluejeans.com/contact) tooget esses valores. 
 
4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. Em Olá **BlueJeans configuração** seção, clique em **configurar BlueJeans** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout, alterar a URL da senha e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. Em uma janela do navegador web diferente, faça logon no tooyour **BlueJeans** site da empresa como um administrador.

8. Vá muito**ADMIN \> as configurações de grupo \> segurança**.
   
   ![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")

9. Em Olá **segurança** , execute Olá etapas a seguir:
   
   ![Logon Único do SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Logon Único do SAML")   
   
   a. Selecione **Logon Único do SAML**.
  
   b. Selecione **Habilitar provisionamento automático**.

10. Passar por hello etapas a seguir:

    ![Caminho de Certificado](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Caminho de Certificado")
    
    a. Clique em **Escolher arquivo**e, em seguida, carregue o certificado de saudação baixado.
   
    b. Colar **Single Sign-On URL do serviço SAML** em Olá **URL de logon** caixa de texto.
   
    c. Colar **alterar a URL da senha** em Olá **alterar a URL da senha** caixa de texto.
   
    d. Colar **URL de logout** em Olá **URL de Logout** caixa de texto.

11. Passar por hello etapas a seguir:
    
    ![Salvar Alterações](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Salvar Alterações")
    
    a. Em Olá **id de usuário** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
   
    b. Em Olá **Email** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
   
    c. Clique em **Salvar Alterações**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-bluejeans-test-user"></a>Criando um usuário de teste do BlueJeans

tooenable AD do Azure usuários toolog em tooBlueJeans, eles devem ser provisionados no BlueJeans.  

No caso do BlueJeans, o provisionamento é uma tarefa manual.

**tooprovision contas de usuário, executar Olá seguintes etapas:**

1. Faça logon no tooyour **BlueJeans** site da empresa como um administrador.

2. Vá muito**ADMIN \> gerenciar usuários \> adicionar usuário**.
   
   ![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")
   
   >[!IMPORTANT]
   >Olá **adicionar usuário** guia está disponível somente se, no hello **guia Segurança**, **habilitar o provisionamento automático** está desmarcada. 
   
3. Em Olá **adicionar usuário** , execute Olá etapas a seguir:

    ![Adicionar Usuário](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Adicionar Usuário")
    
    a. Digite um **nome de usuário do BlueJeans**, uma **endereço de Email**, um **ID de reunião BlueJeans**, um **senha de moderador**, um **nome completo** , Olá **empresa** de uma conta válida do AAD você deseja tooprovision em Olá relacionados caixas de texto.
    
    b. Clique em **Adicionar Usuário**.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros BlueJeans usuário conta ou APIs fornecidas pelo BlueJeans tooprovision contas de usuário do AAD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBlueJeans.

![Atribuir usuário][200] 

**tooassign Britta Simon tooBlueJeans, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **BlueJeans**.

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá BlueJeans bloco no painel de acesso de saudação, você deve obter a página de logon do aplicativo BlueJeans.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

