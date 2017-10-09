---
title: "Tutorial: integração do Azure Active Directory com o Igloo Software | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a>Tutorial: integração do Active Directory do Azure ao Igloo Software

Neste tutorial, você aprenderá como toointegrate Igloo Software com o Azure Active Directory (AD do Azure).

Integrando o Igloo Software com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooIgloo Software
- Você pode habilitar seu usuários tooautomatically get conectado tooIgloo Software (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o Igloo Software, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Igloo Software habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Igloo Software da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-igloo-software-from-hello-gallery"></a>Adicionando Igloo Software da Galeria de saudação
integração de saudação tooconfigure do Igloo Software no AD do Azure, você precisa tooadd Igloo Software na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Igloo Software da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Igloo Software**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. No painel de resultados de saudação, selecione **Igloo Software**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o Igloo Software com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Igloo Software é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Igloo Software precisa toobe estabelecida.

No Igloo Software, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o Igloo Software, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do Igloo Software](#creating-an-igloo-software-test-user)**  -toohave um equivalente do Britta Simon no Igloo Software que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Igloo Software.

**tooconfigure AD do Azure-logon único com o Igloo Software, executar Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Igloo Software** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. Em Olá **Igloo Software domínio e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.igloocommmunities.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.igloocommmunities.com/saml.digest`

    c. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.igloocommmunities.com/saml.digest`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real identificador, URL de resposta e URL de logon. Entre em contato com [equipe de suporte do Igloo Software cliente](https://www.igloosoftware.com/services/support) tooget esses valores. 

4. Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. Em Olá **Igloo Software configuração** seção, clique em **configurar Igloo Software** tooopen **configurar o logon** janela. Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Igloo Software como um administrador.

8. Vá toohello **painel de controle**.
   
     ![Painel de controle](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Painel de controle")

9. Em Olá **associação** , clique em **configurações de entrada**.
   
    ![Configurações de entrada](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Configurações de entrada")

10. No hello seção de configuração do SAML, clique em **configurar autenticação SAML**.
   
    ![Configuração SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "configuração SAML")
   
11. Em Olá **configuração geral** , execute Olá etapas a seguir:
   
    ![Configuração geral](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "Configuração geral")

    a. Em Olá **nome de Conexão** caixa de texto, digite um nome personalizado para sua configuração.
   
    b. Em Olá **URL de logon IdP** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.
   
    c. Em Olá **URL de Logout IdP** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.
    
    d. Selecione **Tipo HTTP de Solicitação e Resposta de Logoff** como **POST**.
   
    e. Abra seu **base 64** codificado certificado baixado do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência, o bloco de notas e, em seguida, cole-o toohello **certificado público** caixa de texto.
    
12. Em Olá **resposta e a configuração de autenticação**, executar Olá etapas a seguir:
    
    ![Configuração de autenticação e resposta](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Configuração de autenticação e resposta")
  
      a. Para **Provedor de Identidade**, selecione **Microsoft ADFS**.
      
      b. Para **Tipo de Identificador**, selecione **Endereço de Email**. 

      c. Em Olá **Email atributo** caixa de texto, tipo **emailaddress**.

      d. Em Olá **atributo de nome** caixa de texto, tipo **givenname**.

      e. Em Olá **último nome de atributo** caixa de texto, tipo **Sobrenome**.

13. Execute Olá configuração de saudação do toocomplete as etapas a seguir:
    
    ![Criação de usuário na entrada](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Criação de usuário na entrada") 

     a. Para **Criação de usuário na Entrada**, selecione **Criar um novo usuário em seu site ao entrar**.

     b. Para **Configurações de Entrada**, selecione **Usar botão do SAML na tela “Entrar”**.

     c. Clique em **Salvar**.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-an-igloo-software-test-user"></a>Como criar um usuário de teste do Igloo Software

Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooIgloo Software.  

Quando um usuário atribuído tenta toolog em tooIgloo Software usando o painel de acesso hello, Igloo Software verifica se o usuário Olá existe.  Se ainda não houver conta de usuário, ela será criada automaticamente pelo Igloo Software.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooIgloo Software.

![Atribuir usuário][200] 

**tooassign Britta Simon tooIgloo Software, executar Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Igloo Software**.

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco Igloo Software Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Igloo Software.
Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

