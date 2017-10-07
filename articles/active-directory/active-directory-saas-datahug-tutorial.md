---
title: "Tutorial: Integração do Azure Active Directory ao Datahug | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a>Tutorial: integração do Azure Active Directory ao Datahug

Neste tutorial, você aprenderá como toointegrate Datahug com o Azure Active Directory (AD do Azure).

Integrando Datahug com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooDatahug
- Você pode habilitar seu usuários tooautomatically get conectado tooDatahug (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte. [O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com Datahug, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Datahug com logon único habilitado

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando Datahug da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-datahug-from-hello-gallery"></a>Adicionando Datahug da Galeria de saudação
integração de saudação tooconfigure de Datahug no AD do Azure, você precisa tooadd Datahug da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd Datahug da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **Datahug**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. No painel de resultados de saudação, selecione **Datahug**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Datahug, com base em um usuário de teste chamado "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Datahug é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Datahug precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Datahug.

tooconfigure e teste de logon único do AD do Azure com Datahug, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste Datahug](#creating-a-datahug-test-user)**  -toohave um equivalente do Britta Simon em Datahug é toohello vinculado do Azure AD representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Datahug.

**tooconfigure AD do Azure-logon único com Datahug, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **Datahug** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. Em Olá **Datahug domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    a. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://apps.datahug.com/identity/<uniqueID>`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://apps.datahug.com/identity/<uniqueID>/acs`

4. Marque **Mostrar configurações de URL avançadas**. Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    Em Olá **URL de logon** caixa de texto, digite um URL como:`https://apps.datahug.com/`
     
    > [!NOTE] 
    > Esses valores não são Olá real. Atualize esses valores com URL de resposta e o identificador de real de saudação. Aqui, sugerimos você toouse Olá valor exclusivo de cadeia de caracteres em Olá identificador e URL de resposta. Entre em contato com [equipe de suporte do cliente Datahug](http://datahug.com/about/contact-us/) tooget esses valores. 

5. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  Verificar **"Mostrar configurações de assinatura de certificado avançadas"** e executar Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    a. Em **Opção de Assinatura**, selecione **Assinar declaração SAML**.
    
    b. Em **Algoritmo de assinatura**, selecione **SHA1**.
 
7. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. Em Olá **Datahug configuração** seção, clique em **configurar Datahug** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML** e **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. tooconfigure logon único no **Datahug** lado, você precisa toosend Olá baixado **Metadata XML**, **ID da entidade SAML** e **serviço de logon único SAML URL** muito[Datahug suporte](http://datahug.com/about/contact-us/). Eles definidos neste aplicativo backup toohave Olá conexão SSO do SAML definido corretamente em ambos os lados.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-datahug-test-user"></a>Criar um usuário de teste Datahug

tooenable AD do Azure usuários toolog em tooDatahug, eles devem ser provisionados no Datahug.  
Quando se usa o Datahug, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour Datahug site da empresa como um administrador.

2. Passe o mouse sobre Olá **engrenagem** no canto direito superior de saudação e clique em **configurações**
   
   ![Adicionar Funcionário](./media/active-directory-saas-datahug-tutorial/1.png)

3. Escolha **pessoas** e clique em Olá **adicionar usuários** guia

    ![Adicionar Funcionário](./media/active-directory-saas-datahug-tutorial/2.png)

4. Digite hello email da pessoa Olá você gostaria que toocreate uma conta para e clique em **adicionar**.

    ![Adicionar Funcionário](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > Você pode enviar toouser de email de registro selecionando **enviar email de boas-vinda** caixa de seleção.  
    > Se você estiver criando uma conta do Salesforce não enviar email de boas-vindas hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooDatahug.

![Atribuir usuário][200] 

**tooassign Britta Simon tooDatahug, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **Datahug**.

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.
Quando você clica em bloco Datahug Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Datahug aplicativo. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

