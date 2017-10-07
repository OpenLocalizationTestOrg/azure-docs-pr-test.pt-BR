---
title: "Tutorial: Integração do Azure Active Directory ao SSO do SAML para o JIRA da Microsoft | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SSO do SAML JIRA pela Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a>Tutorial: Integração do Azure Active Directory ao SSO do SAML para o JIRA da Microsoft

Neste tutorial, você aprenderá como toointegrate JIRA SSO do SAML pela Microsoft no Azure Active Directory (AD do Azure).

Integração de SSO do SAML JIRA pela Microsoft com o Azure AD oferece Olá benefícios a seguir:

- Você pode controlar no AD do Azure que tenha acesso tooJIRA SSO do SAML pela Microsoft
- Você pode habilitar seu usuários tooautomatically get conectado tooJIRA SSO do SAML pela Microsoft (logon único) com suas contas do AD do Azure
- Você pode gerenciar suas contas em um local central - Olá portal do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o SSO do SAML JIRA pela Microsoft, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Aplicativo de servidor JIRA instalado em um servidor do Windows de 64 bits (no local ou na nuvem Olá infraestrutura IaaS)
- O servidor do JIRA é habilitado para HTTPS
- Observação Olá suporte para versões JIRA plug-in são mencionadas na seção abaixo.
- Servidor JIRA está acessível na internet particularmente tooAzure página de logon do AD para autenticação e deve tooreceive capaz de Olá token do AD do Azure
- As credenciais do administrador são configuradas no JIRA
- O WebSudo está desabilitado no JIRA
- Testar usuário criado na Olá aplicativo de servidor JIRA

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção de JIRA. Teste a integração de saudação primeiro em desenvolvimento ou ambiente de aplicativo hello e, em seguida, ambiente de produção de hello do uso de preparo.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="supported-versions-of-jira"></a>Versões com suporte do JIRA 

A partir de agora, há suporte para as seguintes versões do JIRA:

- JIRA Core e Software: too7.2.0 6.0
- JIRA suporte técnico: too3.2 3.0

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando o SSO do SAML JIRA pela Microsoft na Galeria de saudação
2. Configurar e testar o logon único do AD do Azure

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a>Adicionando o SSO do SAML JIRA pela Microsoft na Galeria de saudação
integração de saudação tooconfigure do SSO do SAML JIRA pela Microsoft no Azure AD, é necessário tooadd JIRA SSO do SAML pela Microsoft na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.

**tooadd JIRA SSO do SAML pela Microsoft na Galeria de hello, execute Olá etapas a seguir:**

1. Em Olá ** [portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone. 

    ![Active Directory][1]

2. Navegue muito**aplicativos empresariais**. Em seguida, acesse muito**todos os aplicativos**.

    ![Aplicativos][2]
    
3. tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.

    ![Aplicativos][3]

4. Na caixa de pesquisa hello, digite **JIRA SSO do SAML pela Microsoft**.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. No painel de resultados de saudação, selecione **JIRA SSO do SAML pela Microsoft**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configura e testa o logon único do Azure AD com o SSO do SAML para o JIRA da Microsoft, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SSO do SAML JIRA pela Microsoft é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em SSO do SAML JIRA pela Microsoft precisa toobe estabelecida.

SSO do SAML JIRA pela Microsoft, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.

tooconfigure e teste de logon único do AD do Azure com o SSO do SAML JIRA pela Microsoft, você precisa Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable toouse seus usuários esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user) ** -tootest AD do Azure-logon único com Britta Simon.
3. **[Criando um SSO do SAML JIRA pelo usuário de teste do Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user) ** -toohave um equivalente do Britta Simon no SSO do SAML JIRA pela Microsoft que é vinculado toohello AD do Azure representação do usuário.
4. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse AD do Azure-logon único.
5. **[Teste o logon único](#testing-single-sign-on) ** -tooverify Olá se os trabalhos de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu SSO do SAML JIRA pelo aplicativo Microsoft.

**tooconfigure logon único do AD do Azure com o SSO do SAML JIRA pela Microsoft, execute Olá etapas a seguir:**

1. Em Olá portal do Azure, Olá **JIRA SSO do SAML pela Microsoft** página de integração de aplicativos, clique em **o logon único**.

    ![Configurar Logon Único][4]

2. Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.
 
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. Em Olá **SSO do SAML JIRA Domain da Microsoft e URLs** , execute Olá etapas a seguir:

    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    a. Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<domain:port>/plugins/servlet/saml/auth`

    b. Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<domain:port>/`

    c. Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE] 
    > Esses valores não são reais. Atualizar esses valores com hello real identificador, URL de resposta e URL de logon. A porta é opcional, caso seja uma URL nomeada. Esses valores são recebidos durante a configuração de saudação do plugin Jira, que é explicada posteriormente no tutorial de saudação.
 
4. Olá toogenerate **metadados** url, executar Olá etapas a seguir:

    a. Clique em **Registros do aplicativo**.
    
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    b. Clique em **pontos de extremidade** tooopen **pontos de extremidade** caixa de diálogo.  
    
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    c. Clique em Olá cópia botão toocopy **documento de METADADOS de Federação** url e cole-o no bloco de notas.
    
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    d. Agora vá toohello a página de propriedades de **JIRA SSO do SAML pela Microsoft** e cópia hello **Id do aplicativo** usando **cópia** botão e cole-o no bloco de notas.
 
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    e. Gerar Olá **URL de metadados** usando saudação padrão a seguir: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` e copie esse valor no bloco de notas, como ele é usado posteriormente para configuração de saudação do plug-in de saudação.

5. Clique no botão **Salvar** .

    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. Entre em contato com [Microsoft](mailto:waadpartners@microsoft.com) com hello informações para o plug-in do hello JIRA a seguir.
    
    *   Nome do cliente:
    *   Nome de domínio primário:
    *   O Azure AD Premium: Sim/não (o plug-in será tooall disponível Prezado cliente gratuito, básico e SKU Premium)
    *   Número de usuários que usarão essa integração:
    *   Versão do JIRA:
    *   Comentários:

7. Em uma janela de navegador web diferente, faça logon na instância JIRA tooyour como um administrador.

8. Passe o mouse sobre engrenagem e clique em Olá **complementos**.
    
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. Na seção da guia Complementos, clique em **Gerenciar complementos**.

    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. Carregar manualmente o plug-in de saudação fornecido pela Microsoft. Depois de instalar o plug-in do hello, ele aparece na **usuário instalado** seção complementos **gerenciar complementos** seção.

11. Clique em **configurar** tooconfigure Olá novo plug-in.

12. Realize as seguintes etapas na página de configuração:

    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    a. Em **URL de metadados** colar Olá **URL de metadados** gerado a partir do AD do Azure e clique em Olá **resolver** botão. Ele lê a URL de metadados IdP hello e preenche todas as informações de campos de saudação.

    > [!Note]
    > O local padrão da ID de Usuário SAML é o Identificador de Nome. Você pode alterar essa opção de atributo tooan e inserir nome do atributo apropriado hello.

    > [!TIP]
    > Certifique-se de que há apenas um certificado mapeado em relação a saudação aplicativo para que não haja nenhum erro na resolução de metadados de saudação. Se houver vários certificados, após a resolução de metadados hello, o administrador recebe um erro.
    
    b. Saudação de cópia **identificador, a URL de resposta e a URL de logon** valores e colá-los em **identificador, a URL de resposta e a URL de logon** caixas de texto em respectivamente **SSO do SAML JIRA Domain da Microsoft e URLs** seção no portal do Azure.

    c. Em **nome do botão de logon** nome do tipo de saudação do botão de sua organização deseja Olá toosee de usuários na tela de logon.

    d. Em **locais de ID de usuário SAML** selecione **ID de usuário está no elemento NameIdentifier Olá Olá declaração assunto** ou **ID de usuário está em um elemento de atributo**.  Essa ID tem a id de usuário do toobe Olá JIRA. Se a id de usuário de saudação não for atendida, sistema não permitirá que usuários toolog no. 
    
    e. Se você selecionar **ID de usuário está em um elemento de atributo** opção, em seguida, em **nome do atributo** caixa de texto nome de saudação do tipo do atributo Olá onde a Id de usuário é esperada. 

    f. Se você estiver usando o domínio federado de saudação (como o ADFS etc) com o AD do Azure, em seguida, clique em Olá **habilitar Home Realm Discovery** opção e configurar Olá **nome de domínio**.
    
    g. Em **nome de domínio** Olá domínio nome do tipo aqui em caso de logon baseada no AD FS do hello.

    h. Verificar **habilitar o logout único** se desejar toolog fora do AD do Azure, quando um usuário faz logoff do JIRA. 

    i. Clique em **salvar** botão Configurações de saudação toosave.

> [!TIP]
> Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!  Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação ** Configuração** seção na parte inferior da saudação. Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.

![Criar um usuário do AD do Azure][100]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    a. Em Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.

    c. Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a>Criando um usuário de teste do SSO do SAML para o JIRA da Microsoft

toolog de usuários tooenable AD do Azure no servidor de local de tooJIRA, eles devem ser provisionados no SSO do SAML JIRA pela Microsoft. Para o SSO do SAML para o JIRA da Microsoft, o provisionamento é uma tarefa manual.

**tooprovision uma conta de usuário, execute Olá etapas a seguir:**

1. Faça logon tooyour servidor de local JIRA como um administrador.

2. Passe o mouse sobre engrenagem e clique em Olá **gerenciamento de usuário**.

    ![Adicionar Funcionário](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. São redirecionadas tooAdministrator acesso página tooenter **senha** e clique em **confirmar** botão.

    ![Adicionar Funcionário](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. Na seção da guia **Gerenciamento de usuário**, clique em **criar usuário**.

    ![Adicionar Funcionário](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. Em Olá **"Criar novo usuário"** caixa de diálogo de página, execute Olá etapas a seguir:

    ![Adicionar Funcionário](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    a. Em Olá **endereço de Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.

    b. Em Olá **nome completo** caixa de texto, nome completo do tipo de usuário hello como Britta Simon.

    c. Em Olá **Username** caixa de texto, como o email de saudação do tipo de usuário Brittasimon@contoso.com.

    d. Em Olá **senha** caixa de texto, digite a senha de saudação do usuário.

    e. Clique em **Criar usuário**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure

Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooJIRA SSO do SAML pela Microsoft.

![Atribuir usuário][200] 

**tooassign Britta Simon tooJIRA SSO do SAML pela Microsoft, execute Olá etapas a seguir:**

1. No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **JIRA SSO do SAML pela Microsoft**.

    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. No menu Olá Olá esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.

Quando você clica em Olá SSO do SAML JIRA pelo bloco Microsoft hello painel de acesso, você deve obter automaticamente assinado em tooyour SSO do SAML JIRA pelo aplicativo da Microsoft.
Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

