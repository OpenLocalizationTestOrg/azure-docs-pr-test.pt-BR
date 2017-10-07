---
title: "Tutorial: Integração do Azure Active Directory ao ServiceNow | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ServiceNow e ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>Tutorial: Integração do Active Directory do Azure com o ServiceNow
Neste tutorial, você aprenderá como toointegrate ServiceNow e ServiceNow Express com o Azure Active Directory (AD do Azure).

Integração do ServiceNow e ServiceNow Express com o AD do Azure fornece Olá benefícios a seguir:

* Você pode controlar no AD do Azure que tenha acesso tooServiceNow e Express do ServiceNow
* Você pode habilitar seus usuários tooautomatically get conectado tooServiceNow e ServiceNow Express (logon único) com suas contas do AD do Azure
* Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure

Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
tooconfigure integração do Azure AD com ServiceNow e ServiceNow Express, você precisa Olá itens a seguir:

* Uma assinatura do AD do Azure
* Para o ServiceNow, uma instância ou um locatário do ServiceNow, versão Calgary ou superior
* Para o ServiceNow Express, uma instância do ServiceNow Express, versão Helsinki ou superior
* locatário de ServiceNow Olá deve ter Olá [vários provedor única entrada no plug-in](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) habilitado. Isso pode ser feito [enviando uma solicitação de serviço](https://hi.service-now.com). 

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.
> 
> 

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

* Não use o ambiente de produção, a menos que seja necessário.
* Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. cenário de saudação descrito neste tutorial consiste em dois elementos básicos:

1. Adicionando ServiceNow da Galeria de saudação
2. Configurando e testando o logon único do Azure AD para o ServiceNow ou para o ServiceNow Express

## <a name="adding-servicenow-from-hello-gallery"></a>Adicionando ServiceNow da Galeria de saudação
integração de saudação tooconfigure do ServiceNow ou ServiceNow Express no AD do Azure, você precisa tooadd ServiceNow, na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados. 

**tooadd ServiceNow da Galeria hello, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**. 
   
    ![Active Directory][1]
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Aplicativos][2]
4. Clique em **adicionar** final Olá Olá página.
   
    ![Aplicativos][3]
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Aplicativos][4]
6. Na caixa de pesquisa hello, digite **ServiceNow**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. No painel de resultados de saudação, selecione **ServiceNow**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o ServiceNow ou o ServiceNow Express, com base em um usuário de teste chamado “Brenda Fernandes”.

Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ServiceNow é tooa usuário no AD do Azure. Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no ServiceNow precisa toobe estabelecida.
Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no ServiceNow. tooconfigure e teste de logon único do Azure AD com ServiceNow, é necessário Olá toocomplete blocos de construção a seguir:

1. **[Configurando o Azure AD logon único para ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable toouse seus usuários esse recurso.
2. **[Configurando o Azure AD logon único para ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable toouse seus usuários esse recurso.
3. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.
4. **[Criar um usuário de teste do ServiceNow](#creating-a-servicenow-test-user)**  -toohave um equivalente do Britta Simon no ServiceNow é a representação toohello vinculado do Azure AD dela.
5. **[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.
6. **[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.

> [!NOTE]
> Se você quiser tooconfigure ServiceNow pular a etapa 2. Da mesma forma, se você quiser tooconfigure ServiceNow Express pular a etapa 1.
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a>Configuração do logon único do Azure AD para o ServiceNow
1. No portal clássico de saudação do AD do Azure, em Olá **ServiceNow** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo .
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar logon único")

2. Em Olá **como você gostaria usuários toosign em tooServiceNow** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar logon único")

3. Em Olá **definir configurações de aplicativo** página, execute Olá etapas a seguir:
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar URL do Aplicativo")
   
    a. em Olá **ServiceNow URL de logon** caixa de texto, digite a URL usada pelo seu aplicativo de ServiceNow tooyour toosign em usuários seguindo saudação padrão: `https://<instance-name>.service-now.com`.
   
    b. Em Olá **identificador** caixa de texto, digite a URL usada pelo seu aplicativo de ServiceNow tooyour toosign em usuários seguindo saudação padrão: `https://<instance-name>.service-now.com`.
   
    c. Clique em **Avançar**

4. toohave AD do Azure automaticamente configurar ServiceNow para autenticação SAML, digite o nome da instância do ServiceNow, nome de usuário administrador e senha do administrador no hello **configurar automaticamente o logon único** formulário e clique em  *Configurar*. Observe que esse nome de usuário de administrador Olá fornecido deve ter Olá **security_admin** função atribuída no ServiceNow para este toowork. Caso contrário, toomanually configurar ServiceNow toouse AD do Azure como um provedor de identidade SAML, clique em **configurar manualmente o aplicativo hello para logon único**, em seguida, clique em **próximo** e hello concluída as etapas a seguir.
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar URL do Aplicativo")

5. Em hello **configurar logon único em ServiceNow** , clique em **Download certificado**, salvar arquivo de certificado Olá localmente no seu computador.
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar logon único")

6. Logon tooyour ServiceNow aplicativo como um administrador.

7. Ativar Olá *integração - vários provedor Single Sign-On instalador* plug-in seguindo Olá próximas etapas:
   
    a. No painel de navegação Olá no lado esquerdo do hello, vá muito**definição sistema** seção e, em seguida, clique em **plug-ins**.
   
    ![Configurar URL do aplicativo](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Ativar o plug-in")
   
    b. Procure *Integração - Instalador de Logon Único de Vários Provedores*.
   
    ![Configurar URL do aplicativo](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Ativar o plug-in")
   
    c. Selecione Olá plug-in. Clique com o botão direito do mouse e selecione **Ativar/Atualizar**.
   
    d. Clique em Olá **ativar** botão.

8. No painel de navegação Olá no lado esquerdo do hello, clique em **propriedades**.  
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurar URL do Aplicativo")

9. Em Olá **várias propriedades do provedor de SSO** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurar URL do Aplicativo")
   
    a. Como **Habilitar vários provedores SSO**, selecione **Sim**.
   
    b. Como **Habilitar log de depuração tem Olá provedor múltiplo integração SSO**, selecione **Sim**.
   
    c. No **campo Olá no usuário de saudação de tabela que...**  caixa de texto, tipo **user_name**.
   
    d. Clique em **Salvar**.

10. No painel de navegação Olá no lado esquerdo do hello, clique em **certificados x509**.
    
     ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurar logon único")

11. Em Olá **certificados x. 509** caixa de diálogo, clique em **novo**.
    
     ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurar logon único")

12. Em Olá **certificados x. 509** caixa de diálogo, executar Olá etapas a seguir:
    
     ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar logon único")
    
     a. Clique em **Novo**.
    
     b. Em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: **TestSAML2.0**).
    
     c. Selecione **Ativo**.
    
     d. Para **Formato**, selecione **PEM**.
    
     e. Como **Tipo**, selecione **Confiar nos Certificados do Repositório**.
    
     f. Abra seu certificado codificado na Base64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado PEM** caixa de texto.
    
     g. Clique em **Atualizar**.

13. No painel de navegação Olá no lado esquerdo do hello, clique em **provedores de identidade**.
    
     ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurar logon único")

14. Em Olá **provedores de identidade** caixa de diálogo, clique em **novo**:
    
     ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurar logon único")

15. Em Olá **provedores de identidade** caixa de diálogo, clique em **SAML2 Update1?**:
    
     ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurar logon único")

16. Na caixa de diálogo de propriedades de Update1 SAML2 hello, execute Olá etapas a seguir:
    
     ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurar logon único")

    a. em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: **SAML 2.0**).

    b. Em Olá **campo usuário** caixa de texto, tipo **email** ou **user_name**, dependendo de qual campo é usado toouniquely identificar os usuários de sua implantação do ServiceNow. 

    > [!NOTE] 
    > Você pode tooemit de configuração do AD do Azure ou ID de usuário de saudação do AD do Azure (nome principal do usuário) ou Olá endereço de email como Olá identificador exclusivo no token SAML Olá por vai toohello **ServiceNow > atributos > Single Sign-On** seção Olá portal clássico do Azure e mapeamento Olá desejado campo toohello **nameidentifier** atributo. valor Olá armazenado para o atributo selecionado Olá no AD do Azure (por exemplo, nome) deve corresponder o valor de saudação armazenado no ServiceNow para o campo de saudação inserido (por exemplo, user_name)

    c. No portal clássico de saudação do AD do Azure, copie Olá **ID do provedor de identidade** valor e, em seguida, cole-o em Olá **URL do provedor de identidade** caixa de texto.

    d. No portal clássico de saudação do AD do Azure, copie Olá **URL de solicitação de autenticação** valor e, em seguida, cole-o em Olá **AuthnRequest do provedor de identidade** caixa de texto.

    e. No portal clássico de saudação do AD do Azure, copie Olá **URL do serviço de logon único** valor e, em seguida, cole-o em Olá **SingleLogoutRequest do provedor de identidade** caixa de texto.

    f. Em Olá **ServiceNow Homepage** caixa de texto, digite a URL de saudação da instância ServiceNow home page.

    > [!NOTE] 
    > página inicial da instância de ServiceNow Olá é uma concatenação do seu **URL do locatário ServieNow** e **/navpage.do** (por exemplo:`https://fabrikam.service-now.com/navpage.do`).

    g. Em Olá **ID da entidade / emissor** caixa de texto, digite a URL de saudação do seu locatário ServiceNow.

    h. Em Olá **URL público** caixa de texto, digite a URL de saudação do seu locatário ServiceNow. 

    i. Em Olá **protocolo de associação de saudação do IDP SingleLogoutRequest** caixa de texto, tipo **urn: oasis: nomes: tc: SAML:2.0:bindings:HTTP-redirecionar**.

    j. Em Olá política NameID caixa de texto, digite **urn: oasis: nomes: tc: SAML: 1.1 nameid-format: não especificado**.

    k. Desmarque **Criar um AuthnContextClass**.

    l. Em Olá **método AuthnContextClassRef**, tipo `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`. Isso só será necessário se você for uma organização que esteja somente na nuvem. Se você estiver usando o ADFS ou o MFA local para autenticação, não deverá configurar esse valor. 

    m. Na caixa de texto **Distorção do Relógio**, digite **60**.

    n. Como **Script de Logon Único**, selecione **MultiSSO_SAML2_Update1**.

    o. Como **x509 certificado**, selecione certificado Olá que você criou na etapa anterior hello.

    p. Clique em **Enviar**. 

1. No portal clássico de saudação do AD do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**. 
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar logon único")

2. Em Olá **único logon confirmação** , clique em **concluir**.
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar logon único")

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a>Configuração do logon único do Azure AD para o ServiceNow Express
1. No portal clássico de saudação do AD do Azure, em Olá **ServiceNow** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo .
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar logon único")

2. Em Olá **como você gostaria usuários toosign em tooServiceNow** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar logon único")

3. Em Olá **definir configurações de aplicativo** página, execute Olá etapas a seguir:
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar URL do Aplicativo")
   
    a. em Olá **ServiceNow URL de logon** caixa de texto, digite a URL usada pelo seu aplicativo de ServiceNow tooyour toosign em usuários seguindo saudação padrão: `https://<instance-name>.service-now.com`.
   
    b. Em Olá **URL do emissor** caixa de texto, digite a URL usada pelo seu aplicativo de ServiceNow tooyour toosign em usuários seguindo saudação padrão `https://<instance-name>.service-now.com`.
   
    c. Clique em **Avançar**

4. Clique em **configurar manualmente o aplicativo hello para logon único**, em seguida, clique em **próximo** e Olá completo seguindo as etapas.
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar URL do Aplicativo")

5. Em Olá **configurar logon único em ServiceNow** , clique em **Download certificado**, salvar o arquivo de certificado Olá localmente no seu computador e, em seguida, clique em **próximo**.
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar logon único")

6. Logon tooyour aplicativo ServiceNow expresso como um administrador.

7. No painel de navegação Olá no lado esquerdo do hello, clique em **Single Sign-On**.  
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurar URL do Aplicativo")

8. Em Olá **Single Sign-On** caixa de diálogo, clique Olá configuração ícone superior de saudação à direita e defina hello propriedades a seguir:
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurar URL do Aplicativo")
   
    a. Ativar/desativar **Habilitar provedor múltiplo SSO** toohello direita.
   
    b. Ativar/desativar **depuração habilitar registro em log para Olá provedor múltiplo integração SSO** toohello direita.
   
    c. No **campo Olá no usuário de saudação de tabela que...**  caixa de texto, tipo **user_name**.
9. Em Olá **Single Sign-On** caixa de diálogo, clique em **adicionar novo certificado**.
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurar logon único")
10. Em Olá **certificados x. 509** caixa de diálogo, executar Olá etapas a seguir:
    
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar logon único")
    
    a. Em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: **TestSAML2.0**).
    
    b. Selecione **Ativo**.
    
    c. Para **Formato**, selecione **PEM**.
    
    d. Como **Tipo**, selecione **Confiar nos Certificados do Repositório**.
    
    e. Crie um arquivo codificado em Base64 usando o certificado baixado.
    
    > [!NOTE]
    > Para obter mais detalhes, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o).
    > 
    > 
    
    f. Abra seu certificado codificado na Base64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado PEM** caixa de texto.
    
    g. Clique em **Atualizar**.
11. Em Olá **Single Sign-On** caixa de diálogo, clique em **adicionar novo IdP**.
    
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurar logon único")
12. Em Olá **adicionar novo provedor de identidade** caixa de diálogo, em **configurar o provedor de identidade**, executar Olá etapas a seguir:
    
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurar logon único")

    a. em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: **SAML 2.0**).

    b. No portal clássico de saudação do AD do Azure, copie Olá **ID do provedor de identidade** valor e, em seguida, cole-o em Olá **URL do provedor de identidade** caixa de texto.

    c. No portal clássico de saudação do AD do Azure, copie Olá **URL de solicitação de autenticação** valor e, em seguida, cole-o em Olá **AuthnRequest do provedor de identidade** caixa de texto.

    d. No portal clássico de saudação do AD do Azure, copie Olá **URL do serviço de logon único** valor e, em seguida, cole-o em Olá **SingleLogoutRequest do provedor de identidade** caixa de texto.

    e. Como **certificado do provedor de identidade**, selecione certificado Olá que você criou na etapa anterior hello.


1. Clique em **configurações avançadas**e, em **propriedades adicionais do provedor de identidade**, executar Olá etapas a seguir:
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurar logon único")
   
    a. Em Olá **protocolo de associação de saudação do IDP SingleLogoutRequest** caixa de texto, tipo **urn: oasis: nomes: tc: SAML:2.0:bindings:HTTP-redirecionar**.
   
    b. Em hello **política NameID** caixa de texto, tipo **urn: oasis: nomes: tc: SAML: 1.1 nameid-format: não especificado**.    
   
    c. Em Olá **método AuthnContextClassRef**, tipo **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.
   
    d. Desmarque **Criar um AuthnContextClass**.

2. Em **propriedades adicionais do provedor de serviço**, executar Olá etapas a seguir:
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurar logon único")
   
    a. Em Olá **ServiceNow Homepage** caixa de texto, digite a URL de saudação da instância ServiceNow home page.
   
    > [!NOTE]
    > página inicial da instância de ServiceNow Olá é uma concatenação do seu **URL do locatário ServieNow** e **/navpage.do** (por exemplo: `https://fabrikam.service-now.com/navpage.do`).
    > 
    > 
   
    b. Em Olá **ID da entidade / emissor** caixa de texto, digite a URL de saudação do seu locatário ServiceNow.
   
    c. Em Olá **URI de audiência** caixa de texto, digite a URL de saudação do seu locatário ServiceNow. 
   
    d. Na caixa de texto **Distorção do Relógio**, digite **60**.
   
    e. Em Olá **campo usuário** caixa de texto, tipo **email** ou **user_name**, dependendo de qual campo é usado toouniquely identificar os usuários de sua implantação do ServiceNow.
   
    > [!NOTE]
    > Você pode tooemit de configuração do AD do Azure ou ID de usuário de saudação do AD do Azure (nome principal do usuário) ou Olá endereço de email como Olá identificador exclusivo no token SAML Olá por vai toohello **ServiceNow > atributos > Single Sign-On** seção Olá portal clássico do Azure e mapeamento Olá desejado campo toohello **nameidentifier** atributo. valor Olá armazenado para o atributo selecionado Olá no AD do Azure (por exemplo, nome) deve corresponder o valor de saudação armazenado no ServiceNow para o campo de saudação inserido (por exemplo, user_name)
    > 
    > 
   
    f. Clique em **Salvar**. 

3. No portal clássico de saudação do AD do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**. 
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar logon único")

4. Em Olá **único logon confirmação** , clique em **concluir**.
   
    ![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar logon único")

## <a name="configuring-user-provisioning"></a>Configurando o provisionamento de usuários
Olá o objetivo desta seção é toooutline como tooenable o provisionamento de usuário do usuário do Active Directory contas tooServiceNow.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure provisionamento de usuário, execute Olá etapas a seguir:
1. No portal clássico do hello gerenciamento do Azure, em Olá **ServiceNow** página de integração de aplicativos, clique em **configurar provisionamento de usuário**. 
   
    ![Provisionamento do usuário](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Provisionamento do usuário")

2. Em Olá **insira seu ServiceNow credenciais tooenable provisionamento automático de usuário** , forneça Olá definições de configuração a seguir:
   
     a. Em Olá **nome da instância ServiceNow** caixa de texto, nome da instância do tipo hello ServiceNow.
   
     b. Em Olá **nome de usuário administrador ServiceNow** caixa de texto Nome do tipo hello de saudação conta de administrador do ServiceNow.
   
     c. Em Olá **senha do administrador do ServiceNow** caixa de texto, digite a senha Olá para esta conta.
   
     d. Clique em **validar** tooverify sua configuração.
   
     e. Clique em Olá **próximo** saudação do botão tooopen **próximas etapas** página.
   
     f. Se você desejar tooprovision todos os usuários toothis de aplicativos, selecione "**provisionar automaticamente todas as contas de usuário no aplicativo do hello diretório toothis**". 
   
    ![Próximas etapas](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Próximas etapas")
   
     g. Em Olá **próximas etapas** , clique em **concluir** toosave sua configuração.

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
Nesta seção, você pode criar um usuário de teste no portal clássico do hello chamado Britta Simon.

![Criar um usuário do AD do Azure][20]

**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**

1. Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.

3. lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    a. Em Tipo de Usuário, selecione Novo usuário na organização.
   
    b. Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.
   
    c. Clique em **Avançar**.

6. Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   a. Em Olá **nome** caixa de texto, tipo **Britta**.  
   
   b. Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.
   
   c. Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.
   
   d. Em Olá **função** lista, selecione **usuário**.
   
   e. Clique em **Avançar**.

7. Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    a. Anote o valor Olá Olá **nova senha**.
   
    b. Clique em **Concluído**.   

### <a name="creating-a-servicenow-test-user"></a>Criar um usuário de teste do ServiceNow
Nesta seção, você criará uma usuária chamada Brenda Fernandes no ServiceNow. Nesta seção, você criará uma usuária chamada Brenda Fernandes no ServiceNow. Se você não souber como tooadd a um usuário no ServiceNow ou ServiceNow Express conta, contate a equipe de suporte do ServiceNow.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir um usuário de teste de saudação do AD do Azure
Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooServiceNow seu acesso.

![Atribuir usuário][200] 

**tooassign Britta Simon tooServiceNow, execute Olá etapas a seguir:**

1. No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.
   
    ![Atribuir usuário][201] 

2. Na lista de aplicativos hello, selecione **ServiceNow**.
   
    ![Configurar Logon Único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. No menu de saudação na parte superior de saudação, clique em **usuários**.
   
    ![Atribuir usuário][203] 

4. Na lista de todos os usuários hello, selecione **Britta Simon**.

5. Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.
   
    ![Atribuir usuário][205]

### <a name="testing-single-sign-on"></a>Teste do logon único
Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.

Quando você clica em bloco ServiceNow Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour ServiceNow aplicativo.

## <a name="additional-resources"></a>Recursos adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
