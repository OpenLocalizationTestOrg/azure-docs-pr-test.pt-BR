---
title: "Tutorial: Integração do Azure Active Directory ao ScaleX Enterprise | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a>Tutorial: Integração do Azure Active Directory ao ScaleX Enterprise

Neste tutorial, você aprenderá como toointegrate ScaleX Enterprise com o Azure Active Directory (AD do Azure).

Integrando ScaleX Enterprise com o AD do Azure fornece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooScaleX Enterprise
- Você pode habilitar seu usuários tooautomatically get conectado tooScaleX Enterprise (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte. O que é o acesso a aplicativos e logon único com o [Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com ScaleX Enterprise, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do ScaleX Enterprise habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando ScaleX Enterprise na Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-scalex-enterprise-from-hello-gallery"></a>Adicionando ScaleX Enterprise na Galeria de saudação
tooconfigure Olá integração do ScaleX Enterprise tooAzure AD, é necessário tooadd ScaleX Enterprise na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd ScaleX Enterprise na Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **ScaleX Enterprise**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. No painel de resultados de saudação, selecione **ScaleX Enterprise**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o ScaleX Enterprise, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá empresa ScaleX é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação ScaleX empresa precisa toobe estabelecida.

Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** ScaleX empresa.

tooconfigure e teste de logon único do AD do Azure com ScaleX Enterprise, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave um equivalente do Britta Simon ScaleX empresa que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ScaleX Enterprise.

**tooconfigure AD do Azure-logon único com ScaleX Enterprise, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **ScaleX Enterprise** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. Em Olá **ScaleX domínio da empresa e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    a. Em Olá **identificador** texto, o valor do tipo hello usando saudação padrão a seguir:`https://platform.rescale.com/saml2/<company id>/`

    b. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://platform.rescale.com/saml2/<company id>/acs/`

4. Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://platform.rescale.com/saml2/<company id>/sso/`
     
    > [!NOTE] 
    > Eles não são valores reais de saudação. Atualize esses valores com hello identificador real, a URL de resposta ou a URL de logon. Entre em contato com [a equipe de suporte ScaleX Enterprise Client](http://info.rescale.com/contact_sales) tooget esses valores. 

5. Seu aplicativo ScaleX espera as asserções de SAML de saudação em um formato específico, o que exige que você toomodify atributo personalizado mapeamentos tooyour atributos de token configuração SAML. Clique em **exibir e editar todos os outros atributos de usuário** configurações de atributos de caixa de seleção tooopen Olá personalizado.

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    a. Clique com botão direito atributo Olá **nome** e clique em Excluir.

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    b. Clique em **emailaddress** janela Editar atributo do atributo tooopen hello. Altere o valor de **user.mail** muito**User** e clique em Okey.

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. Em Olá **ScaleX Enterprise configuração** seção, clique em **configurar ScaleX Enterprise** tooopen **configurar o logon** janela. Saudação de cópia **ID da entidade SAML** e **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. tooconfigure logon único no **ScaleX Enterprise** lado, o site da empresa do logon toohello ScaleX Enterprise como um administrador.

9. Clique em menu Olá Olá superior direito e selecione **Contoso administração**.

    > [!NOTE] 
    > Contoso é apenas um exemplo. Esse deve ser o Nome real de sua Empresa. 

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. Selecione **integrações** no menu superior hello e selecione **Single Sign-On**.

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. Preencha o formulário de saudação da seguinte maneira:

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    a. Selecione **“Criar qualquer usuário que pode se autenticar com o SSO”.**

    b. **Provedor saml**: colar Olá valor ***urn: oasis: nomes: tc: SAML:2.0:nameid-formato: persistente***

    c. **Nome de campo de email do provedor de identidade na resposta do ACS**: colar Olá valor`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

    d. **ID de entidade EntityDescriptor do provedor de identidade:** Olá colar **ID da entidade SAML** valor copiado do hello portal do Azure.

    e. **URL de SingleSignOnService do provedor de identidade:** Olá colar **Single Sign-On URL do serviço SAML** de saudação portal do Azure.

    f. **Certificado público X509 do provedor de identidade:** certificado abra Olá X509 baixado do hello Azure no bloco de notas e cole conteúdo Olá nesta caixa. Certifique-se de que não há que nenhuma linha de quebra em Olá intermediária do conteúdo do certificado de saudação.
    
    g. Verificar Olá caixas de seleção a seguir: **habilitado, criptografar NameID e AuthnRequests de entrada.**

    h. Clique em **configurações de atualização de SSO** toosave configurações de saudação.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-scalex-enterprise-test-user"></a>Criando um usuário de teste do ScaleX Enterprise

tooenable AD do Azure usuários toolog em tooScaleX Enterprise, eles devem ser provisionados no tooScaleX Enterprise. No caso de saudação do ScaleX Enterprise, o provisionamento é uma tarefa automática e nenhuma etapa manual é necessária. Qualquer usuário que pode autenticar com credenciais de SSO será configurado automaticamente Olá ScaleX lado.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure concedendo Enterprise de tooScaleX de acesso do usuário.

![Atribuir usuário][200] 

**tooassign Britta Simon tooScaleX Enterprise, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **ScaleX Enterprise**.

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.

### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Clique em Olá ScaleX Enterprise lado a lado no hello painel de acesso, você receberá automaticamente assinado em tooyour aplicativo empresarial ScaleX. Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](https://msdn.microsoft.com/library/dn308586).


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

