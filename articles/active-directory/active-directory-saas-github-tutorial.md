---
title: "Tutorial: Integração do Azure Active Directory ao GitHub | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="ffcda-103">Tutorial: Integração do Azure Active Directory ao GitHub</span><span class="sxs-lookup"><span data-stu-id="ffcda-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="ffcda-104">Neste tutorial, você aprenderá como toointegrate GitHub com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="ffcda-104">In this tutorial, you learn how toointegrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ffcda-105">Integração do GitHub com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffcda-105">Integrating GitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ffcda-106">Você pode controlar no AD do Azure que tenha acesso tooGitHub</span><span class="sxs-lookup"><span data-stu-id="ffcda-106">You can control in Azure AD who has access tooGitHub</span></span>
- <span data-ttu-id="ffcda-107">Você pode habilitar seu usuários tooautomatically get conectado tooGitHub (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffcda-107">You can enable your users tooautomatically get signed-on tooGitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ffcda-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="ffcda-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="ffcda-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ffcda-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffcda-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ffcda-110">Prerequisites</span></span>

<span data-ttu-id="ffcda-111">tooconfigure integração do AD do Azure com GitHub, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffcda-111">tooconfigure Azure AD integration with GitHub, you need hello following items:</span></span>

- <span data-ttu-id="ffcda-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffcda-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ffcda-113">Uma assinatura do GitHub habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="ffcda-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="ffcda-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ffcda-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="ffcda-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ffcda-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ffcda-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ffcda-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ffcda-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ffcda-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="ffcda-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ffcda-118">Scenario description</span></span>
<span data-ttu-id="ffcda-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ffcda-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ffcda-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="ffcda-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ffcda-121">Adicionando GitHub da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ffcda-121">Adding GitHub from hello gallery</span></span>
2. <span data-ttu-id="ffcda-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffcda-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-hello-gallery"></a><span data-ttu-id="ffcda-123">Adicionando GitHub da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ffcda-123">Adding GitHub from hello gallery</span></span>
<span data-ttu-id="ffcda-124">integração de saudação tooconfigure do GitHub no AD do Azure, você precisa tooadd GitHub na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ffcda-124">tooconfigure hello integration of GitHub into Azure AD, you need tooadd GitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ffcda-125">**tooadd GitHub da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ffcda-125">**tooadd GitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffcda-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ffcda-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ffcda-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ffcda-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ffcda-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffcda-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ffcda-133">Na caixa de pesquisa hello, digite **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-133">In hello search box, type **GitHub.com**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="ffcda-135">No painel de resultados de saudação, selecione **GitHub**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ffcda-135">In hello results panel, select **GitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ffcda-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffcda-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ffcda-138">Nesta seção, você configurará e testará o logon único do Azure AD com o GitHub, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ffcda-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ffcda-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no GitHub é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffcda-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="ffcda-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no GitHub precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ffcda-140">In other words, a link relationship between an Azure AD user and hello related user in GitHub needs toobe established.</span></span>

<span data-ttu-id="ffcda-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no GitHub.</span><span class="sxs-lookup"><span data-stu-id="ffcda-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in GitHub.</span></span>

<span data-ttu-id="ffcda-142">tooconfigure e teste de logon único do AD do Azure com GitHub, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffcda-142">tooconfigure and test Azure AD single sign-on with GitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ffcda-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ffcda-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ffcda-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffcda-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ffcda-145">**[Criar um usuário de teste do GitHub](#creating-a-GitHub-test-user)**  -toohave um equivalente do Britta Simon no GitHub é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="ffcda-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - toohave a counterpart of Britta Simon in GitHub that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="ffcda-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ffcda-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ffcda-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ffcda-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ffcda-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffcda-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ffcda-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único em seu aplicativo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="ffcda-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="ffcda-150">**tooconfigure AD do Azure-logon único com GitHub, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ffcda-150">**tooconfigure Azure AD single sign-on with GitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffcda-151">No portal de gerenciamento do Azure do hello, no hello **GitHub** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-151">In hello Azure Management portal, on hello **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ffcda-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="ffcda-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="ffcda-155">Em Olá **domínio GitHub e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffcda-155">On hello **GitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="ffcda-157">a.</span><span class="sxs-lookup"><span data-stu-id="ffcda-157">a.</span></span> <span data-ttu-id="ffcda-158">Em Olá **URL de logon** texto, o valor do tipo hello como:`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="ffcda-158">In hello **Sign-on URL** textbox, type hello value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="ffcda-159">b.</span><span class="sxs-lookup"><span data-stu-id="ffcda-159">b.</span></span> <span data-ttu-id="ffcda-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="ffcda-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ffcda-161">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffcda-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="ffcda-162">Você tem tooupdate esses valores com URL de logon real hello e identificador.</span><span class="sxs-lookup"><span data-stu-id="ffcda-162">You have tooupdate these values with hello actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="ffcda-163">Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffcda-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="ffcda-164">Vá tooGitHub Admin seção tooretrieve esses valores.</span><span class="sxs-lookup"><span data-stu-id="ffcda-164">Go tooGitHub Admin section tooretrieve these values.</span></span> 

4. <span data-ttu-id="ffcda-165">Em Olá **atributos de usuário** seção, selecione **identificador de usuário** como user.mail.</span><span class="sxs-lookup"><span data-stu-id="ffcda-165">On hello **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="ffcda-167">Em Olá **o certificado de autenticação SAML** seção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-167">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="ffcda-169">Em Olá **criar um novo certificado** caixa de diálogo, clique o ícone de calendário hello e selecione um **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-169">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="ffcda-170">Em seguida, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-170">Then click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="ffcda-172">Em Olá **o certificado de autenticação SAML** seção, selecione **ativar o novo certificado** e clique em **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="ffcda-172">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="ffcda-174">Na janela pop-up de saudação **certificado de substituição** janela, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-174">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="ffcda-176">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ffcda-176">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="ffcda-178">Em Olá **GitHub configuração** seção, clique em **configurar o GitHub** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="ffcda-178">On hello **GitHub Configuration** section, click **Configure GitHub** tooopen **Configure sign-on** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configurar o logon único](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="ffcda-181">Em outra janela do navegador da Web, faça logon em seu site de organização do GitHub como administrador.</span><span class="sxs-lookup"><span data-stu-id="ffcda-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="ffcda-182">Navegue muito**configurações** e clique em **segurança**</span><span class="sxs-lookup"><span data-stu-id="ffcda-182">Navigate too**Settings** and click **Security**</span></span>

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="ffcda-184">Verificar Olá **habilitar autenticação SAML** caixa, revelar os campos de Olá logon único na configuração.</span><span class="sxs-lookup"><span data-stu-id="ffcda-184">Check hello **Enable SAML authentication** box, revealing hello Single Sign-on configuration fields.</span></span> <span data-ttu-id="ffcda-185">Em seguida, use Olá único logon URL valor tooupdate Olá única URL de logon na configuração do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffcda-185">Then, use hello single sign-on URL value tooupdate hello Single sign-on URL on Azure AD configuration.</span></span>

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="ffcda-187">Configure Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffcda-187">Configure hello following fields:</span></span>

    <span data-ttu-id="ffcda-188">a.</span><span class="sxs-lookup"><span data-stu-id="ffcda-188">a.</span></span> <span data-ttu-id="ffcda-189">**URL de logon**: insira **SAML logon único na URL do serviço** de saudação **configurar o GitHub** seção no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffcda-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="ffcda-190">b.</span><span class="sxs-lookup"><span data-stu-id="ffcda-190">b.</span></span> <span data-ttu-id="ffcda-191">**Emissor**: insira **ID da entidade SAML** de saudação **configurar o GitHub** seção no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffcda-191">**Issuer**: Enter **SAML Entity ID** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="ffcda-192">c.</span><span class="sxs-lookup"><span data-stu-id="ffcda-192">c.</span></span> <span data-ttu-id="ffcda-193">**Certificado público**: Olá abrir baixado o certificado do Azure AD em um bloco de notas e copie Olá de conteúdo incluindo "Iniciar certificado" e "END"</span><span class="sxs-lookup"><span data-stu-id="ffcda-193">**Public Certificate**: Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="ffcda-195">Clique em **configuração SAML do teste** tooconfirm que não há falhas de validação ou erros durante o SSO.</span><span class="sxs-lookup"><span data-stu-id="ffcda-195">Click on **Test SAML configuration** tooconfirm that no validation failures or errors during SSO.</span></span>

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="ffcda-197">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="ffcda-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ffcda-198">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffcda-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="ffcda-199">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffcda-199">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ffcda-201">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ffcda-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffcda-202">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ffcda-202">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ffcda-204">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="ffcda-204">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ffcda-206">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ffcda-206">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ffcda-208">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffcda-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ffcda-210">a.</span><span class="sxs-lookup"><span data-stu-id="ffcda-210">a.</span></span> <span data-ttu-id="ffcda-211">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ffcda-212">b.</span><span class="sxs-lookup"><span data-stu-id="ffcda-212">b.</span></span> <span data-ttu-id="ffcda-213">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ffcda-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ffcda-214">c.</span><span class="sxs-lookup"><span data-stu-id="ffcda-214">c.</span></span> <span data-ttu-id="ffcda-215">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ffcda-216">d.</span><span class="sxs-lookup"><span data-stu-id="ffcda-216">d.</span></span> <span data-ttu-id="ffcda-217">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="ffcda-218">Criar um usuário de teste do GitHub</span><span class="sxs-lookup"><span data-stu-id="ffcda-218">Creating a GitHub test user</span></span>

<span data-ttu-id="ffcda-219">Em ordem tooenable AD do Azure usuários toolog no GitHub, eles devem ser provisionados no GitHub.</span><span class="sxs-lookup"><span data-stu-id="ffcda-219">In order tooenable Azure AD users toolog into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="ffcda-220">No caso de saudação do GitHub, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="ffcda-220">In hello case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="ffcda-221">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ffcda-221">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffcda-222">Faça logon tooyour site do GitHub da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="ffcda-222">Log in tooyour GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="ffcda-223">Clique em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-223">Click **People**.</span></span>

    <span data-ttu-id="ffcda-224">![Pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="ffcda-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="ffcda-225">Clique em **Convidar membro**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-225">Click **Invite member**.</span></span>

    <span data-ttu-id="ffcda-226">![Convidar Usuários](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Convidar Usuários")</span><span class="sxs-lookup"><span data-stu-id="ffcda-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="ffcda-227">Em Olá **convite membro** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffcda-227">On hello **Invite member** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="ffcda-228">a.</span><span class="sxs-lookup"><span data-stu-id="ffcda-228">a.</span></span> <span data-ttu-id="ffcda-229">Em Olá **Email** caixa de texto, tipo hello endereço de email da conta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffcda-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="ffcda-230">![Convidar Pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="ffcda-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="ffcda-231">b.</span><span class="sxs-lookup"><span data-stu-id="ffcda-231">b.</span></span> <span data-ttu-id="ffcda-232">Clique em **Enviar Convite**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="ffcda-233">![Convidar Pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="ffcda-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="ffcda-234">proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="ffcda-234">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ffcda-235">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffcda-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ffcda-236">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooGitHub seu acesso.</span><span class="sxs-lookup"><span data-stu-id="ffcda-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooGitHub.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ffcda-238">**tooassign Britta Simon tooGitHub, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ffcda-238">**tooassign Britta Simon tooGitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffcda-239">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-239">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ffcda-241">Na lista de aplicativos hello, selecione **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-241">In hello applications list, select **GitHub.com**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="ffcda-243">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ffcda-245">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-245">Click **Add** button.</span></span> <span data-ttu-id="ffcda-246">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ffcda-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ffcda-248">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffcda-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ffcda-249">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ffcda-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ffcda-250">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ffcda-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="ffcda-251">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ffcda-251">Testing single sign-on</span></span>

<span data-ttu-id="ffcda-252">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffcda-252">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ffcda-253">Quando você clica em bloco GitHub Olá Olá painel de acesso, você deve obter tooyour assinado no aplicativo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="ffcda-253">When you click hello GitHub tile in hello Access Panel, you should get signed-on tooyour GitHub application.</span></span> <span data-ttu-id="ffcda-254">Você vai ser logon como uma conta de organização mas toolog necessidade com sua conta pessoal.</span><span class="sxs-lookup"><span data-stu-id="ffcda-254">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ffcda-255">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ffcda-255">Additional resources</span></span>

* [<span data-ttu-id="ffcda-256">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ffcda-256">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ffcda-257">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ffcda-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
