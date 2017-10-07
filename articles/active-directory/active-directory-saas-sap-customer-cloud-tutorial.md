---
title: "Tutorial: integração do Azure Active Directory ao SAP Cloud for Customer | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e a nuvem do SAP para o cliente."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a>Tutorial: integração do Azure Active Directory ao SAP Cloud for Customer

Neste tutorial, você aprenderá como toointegrate SAP nuvem para o cliente com o Azure Active Directory (AD do Azure).

Integração de nuvem do SAP para o cliente com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooSAP nuvem para o cliente
- Você pode habilitar seu usuários tooautomatically get conectado tooSAP nuvem para o cliente (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com a nuvem do SAP para o cliente, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do SAP Cloud for Customer

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando nuvem SAP para o cliente da Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a>Adicionando nuvem SAP para o cliente da Galeria de saudação
integração de saudação tooconfigure da nuvem do SAP para o cliente no AD do Azure, você precisa tooadd nuvem SAP para cliente da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd nuvem SAP para o cliente da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **nuvem SAP para o cliente**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. No painel de resultados de saudação, selecione **nuvem SAP para o cliente**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o SAP Cloud for Customer, com base em uma usuária de teste chamada "Brenda Fernandes".

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na nuvem do SAP para o cliente é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na nuvem do SAP para o cliente precisa toobe estabelecida.

Na nuvem do SAP para o cliente, atribua o valor de saudação de Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com a nuvem do SAP para o cliente, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
3. **[Criando uma nuvem do SAP para o usuário de teste do cliente](#creating-a-sap-cloud-for-customer-test-user)**  -toohave um equivalente do Britta Simon na nuvem do SAP para o cliente que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em sua nuvem do SAP para o aplicativo cliente.

**tooconfigure logon único do AD do Azure com a nuvem do SAP para o cliente, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **nuvem SAP para o cliente** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. Em Olá **nuvem SAP para o domínio de cliente e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server name>.crm.ondemand.com`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server name>.crm.ondemand.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real URL de logon e o identificador. Entre em contato com [SAP nuvem para a equipe de suporte do cliente do cliente](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget esses valores. 

4. Em Olá **atributos de usuário** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    a. Em **identificador de usuário** lista, selecione Olá **ExtractMailPrefix()** função.

    b. De saudação **Mail** lista, selecione Olá usuário atributo que toouse para sua implementação.
    Por exemplo, se você quiser toouse Olá EmployeeID como identificador exclusivo do usuário e você armazenou o valor de atributo Olá Olá ExtensionAttribute2, selecione user.extensionattribute2.  

5. Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. Em Olá **nuvem SAP para configuração de cliente** seção, clique em **configurar nuvem do SAP para o cliente** tooopen **configurar o logon** janela. Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. tooget SSO configurado, execute Olá etapas a seguir:
   
    a. Faça logon no portal do SAP Cloud for Customer com direitos de administrador.
   
    b. Navegue toohello **aplicativo e tarefas comuns de gerenciamento de usuário** e clique em Olá **provedor de identidade** guia.
   
    c. Clique em **novo provedor de identidade** e um arquivo XML de metadados Olá select que baixou do portal do Azure de saudação. Importando metadados hello, sistema Olá carrega automaticamente certificados de assinatura necessária hello e certificado de criptografia.
   
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    d. Active Directory do Azure requer URL do serviço de consumidor de declaração de elemento de saudação na solicitação SAML hello, então selecione Olá **URL do serviço de consumidor asserção incluem** caixa de seleção.
   
    e. Clique em **Ativar Logon Único**.
   
    f. Salve suas alterações.
   
    g. Clique em Olá **meu sistema** guia.
   
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    h. Na caixa de texto **URL de Logon do Azure AD**, cole a **URL do Serviço de Logon Único SAML** copiada do portal do Azure.
   
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    i. Especificar se o funcionário Olá manualmente pode escolher entre fazer logon com a ID de usuário e senha ou SSO selecionando Olá **seleção de provedor de identidade Manual**.
   
    j. Em Olá **URL SSO** seção, especificar URL de saudação que deve ser usada por seu toosign funcionários no sistema toohello. 
    Em Olá **tooEmployee URL enviado** lista, você pode escolher entre hello as opções a seguir:
   
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

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a>Criando um usuário de teste do SAP Cloud for Customer

Nesta seção, você criará uma usuária chamada Brenda Fernandes no SAP Cloud for Customer. Trabalhe com [SAP nuvem para a equipe de suporte do cliente](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd usuários Olá Olá SAP nuvem para a plataforma de cliente. 

> [!NOTE]
> Certifique-se de que o valor de NameID deve corresponder com campo de nome de usuário Olá Olá SAP nuvem para a plataforma de cliente.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSAP nuvem para o cliente.

![Atribuir usuário][200] 

**tooassign Britta Simon tooSAP nuvem para o cliente, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **nuvem SAP para o cliente**.

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em hello nuvem SAP para o bloco de cliente no painel de acesso de saudação, você deve obter tooyour automaticamente conectado em nuvem do SAP para o aplicativo cliente.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

