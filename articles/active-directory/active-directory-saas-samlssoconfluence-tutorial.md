---
title: "Tutorial: Integração do Azure Active Directory com o SSO do SAML para Confluence da Resolution GmbH | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SSO do SAML para confluência resolução GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: fe50636709857ec49023e24bdc8c6cd8c58e3c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="64103-103">Tutorial: Integração do Azure Active Directory com o SSO do SAML para Confluence da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="64103-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="64103-104">Neste tutorial, você aprenderá como toointegrate SSO do SAML para confluência resolução GmbH com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="64103-104">In this tutorial, you learn how toointegrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64103-105">Integração de SSO do SAML para confluência resolução GmbH com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="64103-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="64103-106">Você pode controlar no AD do Azure que tenha tooSAML acesso SSO para confluência resolução GmbH</span><span class="sxs-lookup"><span data-stu-id="64103-106">You can control in Azure AD who has access tooSAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="64103-107">Você pode habilitar seu usuários tooautomatically get conectado tooSAML SSO para confluência resolução GmbH (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64103-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="64103-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="64103-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="64103-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64103-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64103-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="64103-110">Prerequisites</span></span>

<span data-ttu-id="64103-111">tooconfigure integração do AD do Azure com o SSO do SAML para confluência resolução GmbH, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="64103-111">tooconfigure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="64103-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64103-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64103-113">Uma assinatura habilitada para logon único do SSO do SAML para Confluence da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="64103-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64103-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="64103-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64103-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="64103-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64103-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="64103-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64103-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64103-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64103-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="64103-118">Scenario description</span></span>
<span data-ttu-id="64103-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="64103-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64103-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="64103-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64103-121">Adicionando o SSO do SAML para confluência resolução GmbH da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="64103-121">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="64103-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64103-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="64103-123">Adicionando o SSO do SAML para confluência resolução GmbH da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="64103-123">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>

<span data-ttu-id="64103-124">tooconfigure Olá integração do SSO do SAML para confluência resolução GmbH no AD do Azure, você precisa tooadd SSO do SAML para confluência resolução GmbH na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="64103-124">tooconfigure hello integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need tooadd SAML SSO for Confluence by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="64103-125">**tooadd SSO do SAML para confluência resolução GmbH da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64103-125">**tooadd SAML SSO for Confluence by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="64103-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="64103-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="64103-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="64103-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="64103-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="64103-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="64103-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64103-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="64103-133">Na caixa de pesquisa hello, digite **SSO do SAML para confluência resolução GmbH**.</span><span class="sxs-lookup"><span data-stu-id="64103-133">In hello search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. <span data-ttu-id="64103-135">No painel de resultados de saudação, selecione **SSO do SAML para confluência resolução GmbH**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="64103-135">In hello results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="64103-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64103-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="64103-138">Nesta seção, você configura e testa o logon único do Azure AD com o SSO de SAML para Confluence da Resolution GmbH com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="64103-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="64103-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SSO do SAML para confluência resolução GmbH é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="64103-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Confluence by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="64103-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado Olá no SSO do SAML para confluência resolução GmbH precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="64103-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Confluence by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="64103-141">SSO do SAML para confluência resolução GmbH, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="64103-141">In SAML SSO for Confluence by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="64103-142">tooconfigure e testar logon único do AD do Azure com o SSO do SAML confluência resolução GmbH, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="64103-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="64103-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="64103-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="64103-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64103-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64103-145">**[Criando um SSO do SAML para confluência pelo usuário de teste GmbH resolução](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  -toohave um equivalente do Britta Simon no SSO do SAML para confluência resolução GmbH é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="64103-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="64103-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="64103-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64103-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="64103-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="64103-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="64103-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="64103-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu SSO do SAML para confluência resolução GmbH aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64103-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="64103-150">**tooconfigure logon único do AD do Azure com o SSO do SAML para confluência resolução GmbH, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64103-150">**tooconfigure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="64103-151">Em Olá portal do Azure, Olá **SSO do SAML para confluência resolução GmbH** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="64103-151">In hello Azure portal, on hello **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="64103-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="64103-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. <span data-ttu-id="64103-155">Em Olá **SSO do SAML para URLs e confluência resolução GmbH domínio** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="64103-155">On hello **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="64103-157">a.</span><span class="sxs-lookup"><span data-stu-id="64103-157">a.</span></span> <span data-ttu-id="64103-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="64103-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="64103-159">b.</span><span class="sxs-lookup"><span data-stu-id="64103-159">b.</span></span> <span data-ttu-id="64103-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="64103-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="64103-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="64103-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="64103-162">Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="64103-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="64103-164">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="64103-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="64103-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="64103-165">These values are not real.</span></span> <span data-ttu-id="64103-166">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="64103-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="64103-167">Entre em contato com [equipe de suporte do SSO do SAML para confluência resolução GmbH cliente](https://www.resolution.de/go/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="64103-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="64103-168">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="64103-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. <span data-ttu-id="64103-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="64103-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. <span data-ttu-id="64103-172">Em uma janela do navegador web diferente, faça logon no tooyour **SSO do SAML para confluência pelo portal de administração de GmbH resolução** como um administrador.</span><span class="sxs-lookup"><span data-stu-id="64103-172">In a different web browser window, log in tooyour **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="64103-173">Passe o mouse sobre engrenagem e clique em Olá **complementos**.</span><span class="sxs-lookup"><span data-stu-id="64103-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. <span data-ttu-id="64103-175">Você é redirecionado tooAdministrator página de acesso.</span><span class="sxs-lookup"><span data-stu-id="64103-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="64103-176">Insira a senha de saudação e clique em **confirmar** botão.</span><span class="sxs-lookup"><span data-stu-id="64103-176">Enter hello password and click **Confirm** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. <span data-ttu-id="64103-178">Na guia **ATLASSIAN MARKETPLACE**, clique em **Localizar novos complementos**.</span><span class="sxs-lookup"><span data-stu-id="64103-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. <span data-ttu-id="64103-180">Pesquisa **SAML logon único (SSO) para confluência** e clique em **instalar** tooinstall botão Olá novo plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="64103-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. <span data-ttu-id="64103-182">instalação do plug-in de saudação será iniciado.</span><span class="sxs-lookup"><span data-stu-id="64103-182">hello plugin installation will start.</span></span> <span data-ttu-id="64103-183">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="64103-183">Click **Close**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. <span data-ttu-id="64103-186">Clique em **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="64103-186">Click **Manage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. <span data-ttu-id="64103-188">Clique em **configurar** tooconfigure Olá novo plug-in.</span><span class="sxs-lookup"><span data-stu-id="64103-188">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. <span data-ttu-id="64103-190">Este novo plug-in também pode ser encontrado na guia **USUÁRIOS E SEGURANÇA**.</span><span class="sxs-lookup"><span data-stu-id="64103-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. <span data-ttu-id="64103-192">Em **configuração de plug-in de logon único do SAML** , clique em **Adicionar provedor de identidade adicional** botão tooconfigure configurações de saudação do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="64103-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. <span data-ttu-id="64103-194">Execute as seguintes etapas nesta página:</span><span class="sxs-lookup"><span data-stu-id="64103-194">Perform following steps on this page:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    <span data-ttu-id="64103-196">a.</span><span class="sxs-lookup"><span data-stu-id="64103-196">a.</span></span> <span data-ttu-id="64103-197">Adicionar **nome** da saudação (por exemplo, o AD do Azure) do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="64103-197">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="64103-198">b.</span><span class="sxs-lookup"><span data-stu-id="64103-198">b.</span></span> <span data-ttu-id="64103-199">Adicionar **descrição** da saudação (por exemplo, o AD do Azure) do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="64103-199">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="64103-200">c.</span><span class="sxs-lookup"><span data-stu-id="64103-200">c.</span></span> <span data-ttu-id="64103-201">Clique em **XML** e selecione hello **metadados** arquivo que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64103-201">Click **XML** and select hello **Metadata** file that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="64103-202">d.</span><span class="sxs-lookup"><span data-stu-id="64103-202">d.</span></span> <span data-ttu-id="64103-203">Clique no botão **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="64103-203">Click **Load** button.</span></span>

    <span data-ttu-id="64103-204">e.</span><span class="sxs-lookup"><span data-stu-id="64103-204">e.</span></span> <span data-ttu-id="64103-205">Ele lê Olá IdP metadados e preenche os campos de saudação conforme realçado na captura de tela de saudação.</span><span class="sxs-lookup"><span data-stu-id="64103-205">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   
18. <span data-ttu-id="64103-206">Clique em **salvar configurações** botão Configurações de saudação toosave.</span><span class="sxs-lookup"><span data-stu-id="64103-206">Click **Save settings** button toosave hello settings.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="64103-208">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="64103-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="64103-209">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="64103-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="64103-210">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="64103-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="64103-211">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64103-211">Creating an Azure AD test user</span></span>
<span data-ttu-id="64103-212">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64103-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="64103-214">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64103-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="64103-215">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="64103-215">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="64103-217">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="64103-217">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="64103-219">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="64103-219">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64103-221">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="64103-221">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="64103-223">a.</span><span class="sxs-lookup"><span data-stu-id="64103-223">a.</span></span> <span data-ttu-id="64103-224">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64103-224">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64103-225">b.</span><span class="sxs-lookup"><span data-stu-id="64103-225">b.</span></span> <span data-ttu-id="64103-226">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="64103-226">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="64103-227">c.</span><span class="sxs-lookup"><span data-stu-id="64103-227">c.</span></span> <span data-ttu-id="64103-228">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="64103-228">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="64103-229">d.</span><span class="sxs-lookup"><span data-stu-id="64103-229">d.</span></span> <span data-ttu-id="64103-230">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="64103-230">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="64103-231">Criando um usuário de teste do SSO do SAML para Confluence da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="64103-231">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="64103-232">tooenable AD do Azure usuários toolog em tooSAML SSO para confluência resolução GmbH, eles devem ser provisionados no SSO do SAML para confluência resolução GmbH.</span><span class="sxs-lookup"><span data-stu-id="64103-232">tooenable Azure AD users toolog in tooSAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="64103-233">No SSO do SAML para Confluence da Resolution GmbH, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="64103-233">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="64103-234">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64103-234">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="64103-235">Faça logon no tooyour SSO do SAML para confluência pelo site da empresa GmbH resolução como um administrador.</span><span class="sxs-lookup"><span data-stu-id="64103-235">Log in tooyour SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="64103-236">Passe o mouse sobre engrenagem e clique em Olá **gerenciamento de usuário**.</span><span class="sxs-lookup"><span data-stu-id="64103-236">Hover on cog and click hello **User management**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. <span data-ttu-id="64103-238">Na seção usuários, clique na guia **Adicionar usuários**. Em Olá **"Adicionar um usuário"** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="64103-238">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="64103-240">a.</span><span class="sxs-lookup"><span data-stu-id="64103-240">a.</span></span> <span data-ttu-id="64103-241">Em Olá **Username** caixa de texto, tipo hello email do usuário como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64103-241">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="64103-242">b.</span><span class="sxs-lookup"><span data-stu-id="64103-242">b.</span></span> <span data-ttu-id="64103-243">Em Olá **nome completo** caixa de texto, nome completo do tipo saudação do usuário como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64103-243">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="64103-244">c.</span><span class="sxs-lookup"><span data-stu-id="64103-244">c.</span></span> <span data-ttu-id="64103-245">Em Olá **Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="64103-245">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="64103-246">d.</span><span class="sxs-lookup"><span data-stu-id="64103-246">d.</span></span> <span data-ttu-id="64103-247">Em Olá **senha** caixa de texto, digite a senha para Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="64103-247">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="64103-248">e.</span><span class="sxs-lookup"><span data-stu-id="64103-248">e.</span></span> <span data-ttu-id="64103-249">Clique em **Confirmar senha** Redigite a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="64103-249">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="64103-250">f.</span><span class="sxs-lookup"><span data-stu-id="64103-250">f.</span></span> <span data-ttu-id="64103-251">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="64103-251">Click **Add** button.</span></span>    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="64103-252">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64103-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="64103-253">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSAML SSO para confluência resolução GmbH.</span><span class="sxs-lookup"><span data-stu-id="64103-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Confluence by resolution GmbH.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="64103-255">**tooassign Britta Simon tooSAML SSO para confluência resolução GmbH, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64103-255">**tooassign Britta Simon tooSAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="64103-256">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="64103-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="64103-258">Na lista de aplicativos hello, selecione **SSO do SAML para confluência resolução GmbH**.</span><span class="sxs-lookup"><span data-stu-id="64103-258">In hello applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. <span data-ttu-id="64103-260">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="64103-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="64103-262">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="64103-262">Click **Add** button.</span></span> <span data-ttu-id="64103-263">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64103-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="64103-265">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="64103-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="64103-266">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64103-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64103-267">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64103-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="64103-268">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="64103-268">Testing single sign-on</span></span>

<span data-ttu-id="64103-269">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="64103-269">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="64103-270">Quando você clica em Olá SSO do SAML para confluência pelo bloco GmbH resolução Olá painel de acesso, você deve obter automaticamente assinado em tooyour SSO do SAML confluência resolução GmbH aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64103-270">When you click hello SAML SSO for Confluence by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="64103-271">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="64103-271">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="64103-272">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="64103-272">Additional resources</span></span>

* [<span data-ttu-id="64103-273">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="64103-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64103-274">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="64103-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

