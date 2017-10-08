---
title: "Tutorial: Integração do Azure Active Directory ao SAP Business ByDesign | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a>Tutorial: integração do Azure Active Directory ao SAP Business ByDesign

Neste tutorial, você aprenderá como toointegrate SAP Business ByDesign com o Azure Active Directory (AD do Azure).

Integração do SAP Business ByDesign com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSAP ByDesign de negócios.
- Você pode habilitar seu usuários tooautomatically get conectado tooSAP ByDesign de negócios (logon único) com suas contas do AD do Azure.
- Você pode gerenciar suas contas em um local central - Olá portal do Azure.

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o SAP Business ByDesign, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do SAP Business ByDesign habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando SAP Business ByDesign da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a>Adicionando SAP Business ByDesign da Galeria de saudação
integração de saudação tooconfigure do SAP Business ByDesign no AD do Azure, você precisa tooadd SAP Business ByDesign da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd SAP Business ByDesign da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![botão de Active Directory do Azure Olá][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![folha de aplicativos de empresa Olá][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Novo botão de aplicativo Hello][3]

4. Na caixa de pesquisa hello, digite **SAP Business ByDesign**, selecione **SAP Business ByDesign** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.

    ![SAP Business ByDesign na lista de resultados de saudação](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o SAP Business ByDesign, com base em uma usuária de teste chamada "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SAP Business ByDesign é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no SAP Business ByDesign precisa toobe estabelecida.

No SAP Business ByDesign, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o SAP Business ByDesign, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criar um usuário de teste do SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  -toohave um equivalente do Britta Simon no SAP Business ByDesign que é vinculado toohello AD do Azure representação do usuário.
4. **[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo SAP Business ByDesign.

**tooconfigure logon único do AD do Azure com o SAP Business ByDesign, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **SAP Business ByDesign** página de integração de aplicativos, clique em **o logon único**.

    ![Link Configurar logon único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. Em Olá **URLs e domínio do SAP Business ByDesign** , execute Olá etapas a seguir:

    ![Informações de logon único de Domínio e URLs do SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<servername>.sapbydesign.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<servername>.sapbydesign.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [equipe de suporte do cliente do SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) tooget esses valores.

4. Em Olá **atributos de usuário** , execute Olá etapas a seguir:

    ![Seção Atributo do SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    a. Em **identificador de usuário** lista, selecione Olá **ExtractMailPrefix()** função.
    
    b. De saudação **Mail** lista, selecione Olá usuário atributo que toouse para sua implementação. Por exemplo, se você quiser toouse Olá EmployeeID como identificador exclusivo do usuário e você armazenou o valor de atributo Olá Olá ExtensionAttribute2, selecione user.extensionattribute2.   

5. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![link de download de certificado Olá](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. Em Olá **configuração do SAP Business ByDesign** seção, clique em **configurar o SAP Business ByDesign** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configuração do SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. tooget SSO configurado para o seu aplicativo executar Olá etapas a seguir:
   
    a. Faça logon no portal do SAP Business ByDesign tooyour com direitos de administrador.
   
    b. Navegue muito**aplicativo e tarefas comuns de gerenciamento de usuário** e clique em Olá **provedor de identidade** guia.
   
    c. Clique em **novo provedor de identidade** e selecione Olá metadados XML que você baixou do portal do Azure de saudação. Importando metadados hello, sistema Olá carrega automaticamente certificados de assinatura necessária hello e certificado de criptografia.
   
    ![Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    d. Olá tooinclude **URL do serviço de consumidor de declaração** na solicitação SAML hello, selecione **incluem URL de serviço de consumidor de declaração**.
   
    e. Clique em **Ativar Logon Único**.
   
    f. Salve suas alterações.
   
    g. Clique em Olá **meu sistema** guia.
   
    ![Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    h. Colar **Single Sign-On URL do serviço SAML**, que você tiver copiado da saudação portal do Azure para Olá **na URL de logon do AD do Azure** caixa de texto.
   
    ![Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    i. Especificar se o funcionário Olá manualmente pode escolher entre fazer logon com a ID de usuário e senha ou SSO selecionando **seleção de provedor de identidade Manual**.
   
    j. Em Olá **URL SSO** seção, especificar URL Olá que deve ser usado pelo sistema do hello funcionário toologon toohello. 
    Olá URL enviado tooEmployee lista suspensa, você pode escolher entre Olá as opções a seguir:
   
    **URL não SSO**
   
    sistema de saudação envia somente saudação normal do sistema URL toohello funcionário. Olá funcionário não pode fazer logon usando o SSO e deve usar senha ou certificado em vez disso.
   
    **URL de SSO** 
   
    sistema de saudação envia somente Olá URL SSO toohello funcionário. funcionário Olá pode fazer logon usando o SSO. Solicitação de autenticação é redirecionada por meio de saudação IdP.
   
    **Seleção Automática**
   
    Se SSO não estiver ativo, o sistema de saudação envia funcionário de toohello de URL saudação normal do sistema. Se o SSO estiver ativo, o sistema de Olá verifica se o funcionário Olá tem uma senha. Se uma senha estiver disponível, a URL do SSO e URL do SSO não são enviadas toohello funcionário. No entanto, se funcionário Olá não tem senha, Olá URL SSO é enviada toohello funcionário.
   
    k. Salve suas alterações.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

   ![Criar um usuário de teste do Azure AD][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.

    ![botão Adicionar de saudação](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    a. Em Olá **nome** , digite **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.

    c. Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.

    d. Clique em **Criar**.
 
### <a name="create-an-sap-business-bydesign-test-user"></a>Criar um usuário de teste do SAP Business ByDesign

Nesta seção, você criará uma usuária chamada Brenda Fernandes no SAP Business ByDesign. Trabalhe com [equipe de suporte do cliente do SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) tooadd usuários de saudação na plataforma do SAP Business ByDesign hello. 

> [!NOTE]
> Certifique-se de que o valor de NameID deve corresponder com o campo de nome de usuário de saudação na plataforma do SAP Business ByDesign hello.

### <a name="assign-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSAP ByDesign de negócios.

![Atribuir função de usuário Olá][200] 

**tooassign Britta Simon tooSAP ByDesign Business, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **SAP Business ByDesign**.

    ![link do SAP Business ByDesign Olá na lista de aplicativos Olá](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![link de "Usuários e grupos" Hello][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição adicionar Olá][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em bloco SAP Business ByDesign Olá Olá painel de acesso, você deve obter aplicativos do SAP Business ByDesign automaticamente assinado em tooyour.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

