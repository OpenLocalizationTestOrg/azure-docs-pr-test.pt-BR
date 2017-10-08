---
title: "Tutorial: Integração do Azure Active Directory com o SSO do SAML para Jira da Resolution GmbH | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SSO do SAML para Jira resolução GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="7f146-103">Tutorial: Integração do Azure Active Directory com o SSO do SAML para Jira da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="7f146-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="7f146-104">Neste tutorial, você aprenderá como toointegrate SSO do SAML para Jira resolução GmbH com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7f146-104">In this tutorial, you learn how toointegrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f146-105">Integração de SSO do SAML para Jira resolução GmbH com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f146-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7f146-106">Você pode controlar no AD do Azure que tenha tooSAML acesso SSO para Jira resolução GmbH</span><span class="sxs-lookup"><span data-stu-id="7f146-106">You can control in Azure AD who has access tooSAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="7f146-107">Você pode habilitar seu usuários tooautomatically get conectado tooSAML SSO para Jira resolução GmbH (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f146-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7f146-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7f146-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7f146-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f146-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f146-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7f146-110">Prerequisites</span></span>

<span data-ttu-id="7f146-111">tooconfigure integração do AD do Azure com o SSO do SAML para Jira resolução GmbH, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f146-111">tooconfigure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="7f146-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f146-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f146-113">Uma assinatura habilitada para logon único do SSO do SAML para Jira da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="7f146-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f146-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7f146-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f146-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7f146-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f146-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7f146-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f146-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f146-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f146-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7f146-118">Scenario description</span></span>
<span data-ttu-id="7f146-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7f146-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f146-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="7f146-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f146-121">Adicionando o SSO do SAML para Jira resolução GmbH da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7f146-121">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="7f146-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f146-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="7f146-123">Adicionando o SSO do SAML para Jira resolução GmbH da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7f146-123">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
<span data-ttu-id="7f146-124">tooconfigure Olá integração do SSO do SAML para Jira resolução GmbH no AD do Azure, você precisa tooadd SSO do SAML para Jira resolução GmbH na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7f146-124">tooconfigure hello integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need tooadd SAML SSO for Jira by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7f146-125">**tooadd SSO do SAML para Jira resolução GmbH da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7f146-125">**tooadd SAML SSO for Jira by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f146-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7f146-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7f146-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7f146-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7f146-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7f146-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7f146-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7f146-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7f146-133">Na caixa de pesquisa hello, digite **SSO do SAML para Jira resolução GmbH**.</span><span class="sxs-lookup"><span data-stu-id="7f146-133">In hello search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="7f146-135">No painel de resultados de saudação, selecione **SSO do SAML para Jira resolução GmbH**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7f146-135">In hello results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7f146-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f146-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7f146-138">Nesta seção, você configura e testa o logon único do Azure AD com o SSO de SAML para Jira da Resolution GmbH com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="7f146-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7f146-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SSO do SAML para Jira resolução GmbH é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f146-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Jira by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="7f146-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado Olá no SSO do SAML para Jira resolução GmbH precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7f146-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Jira by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="7f146-141">SSO do SAML para Jira resolução GmbH, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f146-141">In SAML SSO for Jira by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7f146-142">tooconfigure e testar logon único do AD do Azure com o SSO do SAML Jira resolução GmbH, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f146-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7f146-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7f146-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7f146-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f146-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f146-145">**[Criando um SSO do SAML para Jira pelo usuário de teste GmbH resolução](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave um equivalente do Britta Simon no SSO do SAML para Jira resolução GmbH é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7f146-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f146-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="7f146-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f146-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7f146-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7f146-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f146-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7f146-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu SSO do SAML para Jira resolução GmbH aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f146-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="7f146-150">**tooconfigure logon único do AD do Azure com o SSO do SAML para Jira resolução GmbH, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7f146-150">**tooconfigure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f146-151">Em Olá portal do Azure, Olá **SSO do SAML para Jira resolução GmbH** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="7f146-151">In hello Azure portal, on hello **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7f146-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="7f146-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="7f146-155">Em Olá **SSO do SAML para URLs e Jira resolução GmbH domínio** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="7f146-155">On hello **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="7f146-157">a.</span><span class="sxs-lookup"><span data-stu-id="7f146-157">a.</span></span> <span data-ttu-id="7f146-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="7f146-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="7f146-159">b.</span><span class="sxs-lookup"><span data-stu-id="7f146-159">b.</span></span> <span data-ttu-id="7f146-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="7f146-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="7f146-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="7f146-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="7f146-162">Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="7f146-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="7f146-164">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="7f146-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7f146-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="7f146-165">These values are not real.</span></span> <span data-ttu-id="7f146-166">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="7f146-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7f146-167">Entre em contato com [equipe de suporte do SSO do SAML para Jira resolução GmbH cliente](https://www.resolution.de/go/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="7f146-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="7f146-168">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7f146-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="7f146-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7f146-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="7f146-172">Em uma janela do navegador web diferente, faça logon no tooyour **SSO do SAML para Jira pelo portal de administração de GmbH resolução** como um administrador.</span><span class="sxs-lookup"><span data-stu-id="7f146-172">In a different web browser window, log in tooyour **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="7f146-173">Passe o mouse sobre engrenagem e clique em Olá **complementos**.</span><span class="sxs-lookup"><span data-stu-id="7f146-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="7f146-175">Você é redirecionado tooAdministrator página de acesso.</span><span class="sxs-lookup"><span data-stu-id="7f146-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="7f146-176">Digite hello **senha** e clique em **confirmar** botão.</span><span class="sxs-lookup"><span data-stu-id="7f146-176">Enter hello **Password** and click **Confirm** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="7f146-178">Na seção da guia Complementos, clique em **Localizar novos complementos**.</span><span class="sxs-lookup"><span data-stu-id="7f146-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="7f146-179">Pesquisa **SAML logon único (SSO) para JIRA** e clique em **instalar** tooinstall botão Olá novo plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="7f146-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="7f146-181">instalação do plug-in de saudação será iniciado.</span><span class="sxs-lookup"><span data-stu-id="7f146-181">hello plugin installation will start.</span></span> <span data-ttu-id="7f146-182">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="7f146-182">Click **Close**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="7f146-185">Clique em **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="7f146-185">Click **Manage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="7f146-187">Clique em **configurar** tooconfigure Olá novo plug-in.</span><span class="sxs-lookup"><span data-stu-id="7f146-187">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="7f146-189">Em **configuração de plug-in de logon único do SAML** , clique em **Adicionar provedor de identidade adicional** botão tooconfigure configurações de saudação do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="7f146-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="7f146-191">Execute as seguintes etapas nesta página:</span><span class="sxs-lookup"><span data-stu-id="7f146-191">Perform following steps on this page:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="7f146-193">a.</span><span class="sxs-lookup"><span data-stu-id="7f146-193">a.</span></span> <span data-ttu-id="7f146-194">Adicionar **nome** da saudação (por exemplo, o AD do Azure) do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="7f146-194">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="7f146-195">b.</span><span class="sxs-lookup"><span data-stu-id="7f146-195">b.</span></span> <span data-ttu-id="7f146-196">Adicionar **descrição** da saudação (por exemplo, o AD do Azure) do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="7f146-196">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="7f146-197">c.</span><span class="sxs-lookup"><span data-stu-id="7f146-197">c.</span></span> <span data-ttu-id="7f146-198">Clique em **XML** e selecione hello **metadados** arquivo que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f146-198">Click **XML** and select hello **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="7f146-199">d.</span><span class="sxs-lookup"><span data-stu-id="7f146-199">d.</span></span> <span data-ttu-id="7f146-200">Clique no botão **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="7f146-200">Click **Load** button.</span></span>

    <span data-ttu-id="7f146-201">e.</span><span class="sxs-lookup"><span data-stu-id="7f146-201">e.</span></span> <span data-ttu-id="7f146-202">Ele lê Olá IdP metadados e preenche os campos de saudação conforme realçado na captura de tela de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f146-202">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   

16. <span data-ttu-id="7f146-203">Clique em **salvar configurações** botão Configurações de saudação toosave.</span><span class="sxs-lookup"><span data-stu-id="7f146-203">Click **Save settings** button toosave hello settings.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="7f146-205">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="7f146-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7f146-206">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="7f146-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7f146-207">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7f146-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7f146-208">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f146-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="7f146-209">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f146-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7f146-211">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7f146-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f146-212">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7f146-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7f146-214">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7f146-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7f146-216">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f146-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7f146-218">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f146-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f146-220">a.</span><span class="sxs-lookup"><span data-stu-id="7f146-220">a.</span></span> <span data-ttu-id="7f146-221">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f146-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f146-222">b.</span><span class="sxs-lookup"><span data-stu-id="7f146-222">b.</span></span> <span data-ttu-id="7f146-223">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7f146-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f146-224">c.</span><span class="sxs-lookup"><span data-stu-id="7f146-224">c.</span></span> <span data-ttu-id="7f146-225">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="7f146-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7f146-226">d.</span><span class="sxs-lookup"><span data-stu-id="7f146-226">d.</span></span> <span data-ttu-id="7f146-227">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7f146-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="7f146-228">Criando um usuário de teste do SSO do SAML para Jira da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="7f146-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="7f146-229">tooenable AD do Azure usuários toolog em tooSAML SSO para Jira resolução GmbH, eles devem ser provisionados no SSO do SAML para Jira resolução GmbH.</span><span class="sxs-lookup"><span data-stu-id="7f146-229">tooenable Azure AD users toolog in tooSAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="7f146-230">No SSO do SAML para Jira da Resolution GmbH, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="7f146-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="7f146-231">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7f146-231">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f146-232">Faça logon no tooyour SSO do SAML para Jira pelo site da empresa GmbH resolução como um administrador.</span><span class="sxs-lookup"><span data-stu-id="7f146-232">Log in tooyour SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="7f146-233">Passe o mouse sobre engrenagem e clique em Olá **gerenciamento de usuário**.</span><span class="sxs-lookup"><span data-stu-id="7f146-233">Hover on cog and click hello **User management**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="7f146-235">São redirecionadas tooAdministrator acesso página tooenter **senha** e clique em **confirmar** botão.</span><span class="sxs-lookup"><span data-stu-id="7f146-235">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="7f146-237">Na seção da guia **Gerenciamento de usuário**, clique em **criar usuário**.</span><span class="sxs-lookup"><span data-stu-id="7f146-237">Under **User management** tab section, click **create user**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="7f146-239">Em Olá **"Criar novo usuário"** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f146-239">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="7f146-241">a.</span><span class="sxs-lookup"><span data-stu-id="7f146-241">a.</span></span> <span data-ttu-id="7f146-242">Em Olá **endereço de Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7f146-242">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="7f146-243">b.</span><span class="sxs-lookup"><span data-stu-id="7f146-243">b.</span></span> <span data-ttu-id="7f146-244">Em Olá **nome completo** caixa de texto, nome completo do tipo de usuário hello como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f146-244">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="7f146-245">c.</span><span class="sxs-lookup"><span data-stu-id="7f146-245">c.</span></span> <span data-ttu-id="7f146-246">Em Olá **Username** caixa de texto, como o email de saudação do tipo de usuário Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7f146-246">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="7f146-247">d.</span><span class="sxs-lookup"><span data-stu-id="7f146-247">d.</span></span> <span data-ttu-id="7f146-248">Em Olá **senha** caixa de texto, digite a senha de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7f146-248">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="7f146-249">e.</span><span class="sxs-lookup"><span data-stu-id="7f146-249">e.</span></span> <span data-ttu-id="7f146-250">Clique em **Criar usuário**.</span><span class="sxs-lookup"><span data-stu-id="7f146-250">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7f146-251">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f146-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7f146-252">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSAML SSO para Jira resolução GmbH.</span><span class="sxs-lookup"><span data-stu-id="7f146-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Jira by resolution GmbH.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7f146-254">**tooassign Britta Simon tooSAML SSO para Jira resolução GmbH, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7f146-254">**tooassign Britta Simon tooSAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f146-255">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7f146-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7f146-257">Na lista de aplicativos hello, selecione **SSO do SAML para Jira resolução GmbH**.</span><span class="sxs-lookup"><span data-stu-id="7f146-257">In hello applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="7f146-259">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7f146-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7f146-261">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7f146-261">Click **Add** button.</span></span> <span data-ttu-id="7f146-262">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7f146-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7f146-264">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f146-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7f146-265">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7f146-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f146-266">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7f146-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7f146-267">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7f146-267">Testing single sign-on</span></span>

<span data-ttu-id="7f146-268">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f146-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7f146-269">Quando você clica em Olá SSO do SAML para Jira pelo bloco GmbH resolução Olá painel de acesso, você deve obter automaticamente assinado em tooyour SSO do SAML Jira resolução GmbH aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f146-269">When you click hello SAML SSO for Jira by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="7f146-270">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7f146-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7f146-271">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7f146-271">Additional resources</span></span>

* [<span data-ttu-id="7f146-272">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7f146-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f146-273">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f146-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

