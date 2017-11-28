---
title: "Tutorial: integração do Azure Active Directory com a Área Restrita do Salesforce | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e a área restrita do Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="86a14-103">Tutorial: Integração do Active Directory do Azure com a Área Restrita Salesforce</span><span class="sxs-lookup"><span data-stu-id="86a14-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="86a14-104">Neste tutorial, você aprenderá como toointegrate área restrita do Salesforce com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="86a14-104">In this tutorial, you learn how toointegrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86a14-105">Integração de área restrita do Salesforce com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="86a14-105">Integrating Salesforce Sandbox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="86a14-106">Você pode controlar no AD do Azure que tenha acesso tooSalesforce área restrita</span><span class="sxs-lookup"><span data-stu-id="86a14-106">You can control in Azure AD who has access tooSalesforce Sandbox</span></span>
- <span data-ttu-id="86a14-107">Você pode habilitar seu usuários tooautomatically get conectado tooSalesforce seguro (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="86a14-107">You can enable your users tooautomatically get signed-on tooSalesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86a14-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="86a14-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="86a14-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86a14-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86a14-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="86a14-110">Prerequisites</span></span>

<span data-ttu-id="86a14-111">tooconfigure integração do AD do Azure com área restrita do Salesforce, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="86a14-111">tooconfigure Azure AD integration with Salesforce Sandbox, you need hello following items:</span></span>

- <span data-ttu-id="86a14-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="86a14-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86a14-113">Uma assinatura habilitada para logon único do Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="86a14-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86a14-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="86a14-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86a14-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="86a14-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86a14-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="86a14-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86a14-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86a14-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86a14-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="86a14-118">Scenario description</span></span>
<span data-ttu-id="86a14-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="86a14-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86a14-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="86a14-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86a14-121">Adicionando a área restrita do Salesforce da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="86a14-121">Adding Salesforce Sandbox from hello gallery</span></span>
2. <span data-ttu-id="86a14-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="86a14-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a><span data-ttu-id="86a14-123">Adicionando a área restrita do Salesforce da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="86a14-123">Adding Salesforce Sandbox from hello gallery</span></span>
<span data-ttu-id="86a14-124">integração de Olá tooconfigure da área restrita do Salesforce no AD do Azure, você precisa tooadd área restrita do Salesforce, na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="86a14-124">tooconfigure hello integration of Salesforce Sandbox into Azure AD, you need tooadd Salesforce Sandbox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="86a14-125">**tooadd área restrita do Salesforce da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="86a14-125">**tooadd Salesforce Sandbox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a14-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="86a14-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="86a14-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="86a14-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="86a14-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="86a14-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="86a14-131">Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="86a14-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="86a14-133">Na caixa de pesquisa hello, digite **área restrita do Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="86a14-133">In hello search box, type **Salesforce Sandbox**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="86a14-135">No painel de resultados de saudação, selecione **área restrita do Salesforce**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="86a14-135">In hello results panel, select **Salesforce Sandbox**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="86a14-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="86a14-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="86a14-138">Nesta seção, você configura e testa o logon único do Azure AD com o Salesforce Sandbox, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="86a14-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="86a14-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em área restrita do Salesforce é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="86a14-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce Sandbox is tooa user in Azure AD.</span></span> <span data-ttu-id="86a14-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em área restrita do Salesforce deve toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="86a14-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce Sandbox needs toobe established.</span></span>

<span data-ttu-id="86a14-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em área restrita do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="86a14-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="86a14-142">tooconfigure e teste de logon único do AD do Azure com área restrita do Salesforce, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="86a14-142">tooconfigure and test Azure AD single sign-on with Salesforce Sandbox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="86a14-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="86a14-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="86a14-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86a14-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86a14-145">**[Criar um usuário de teste de área restrita do Salesforce](#creating-a-salesforce-sandbox-test-user)**  -toohave um equivalente do Britta Simon em área restrita do Salesforce que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="86a14-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - toohave a counterpart of Britta Simon in Salesforce Sandbox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="86a14-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="86a14-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86a14-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="86a14-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="86a14-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a14-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="86a14-149">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de área restrita do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="86a14-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="86a14-150">**tooconfigure AD do Azure-logon único com área restrita do Salesforce, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="86a14-150">**tooconfigure Azure AD single sign-on with Salesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a14-151">Em Olá portal do Azure, Olá **área restrita do Salesforce** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="86a14-151">In hello Azure portal, on hello **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="86a14-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="86a14-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="86a14-155">Em Olá **URLs e domínio de área restrita do Salesforce** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="86a14-155">On hello **Salesforce Sandbox Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="86a14-157">Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="86a14-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="86a14-158">Esse valor não é hello real.</span><span class="sxs-lookup"><span data-stu-id="86a14-158">This value is not hello real.</span></span> <span data-ttu-id="86a14-159">Atualize esse valor com a URL de logon real hello. Entre em contato com [equipe de suporte do cliente de área restrita do Salesforce](https://help.salesforce.com/support) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="86a14-159">Update this value with hello actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) tooget this value.</span></span>


4. <span data-ttu-id="86a14-160">Se você já tiver configurado logon único para outra instância de área restrita do Salesforce em seu diretório, você também deve configurar Olá **identificador** toohave Olá mesmo valor Olá **URL de entrada**.</span><span class="sxs-lookup"><span data-stu-id="86a14-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="86a14-161">Olá **identificador** campo pode ser encontrado verificando Olá **Mostrar configurações avançadas** caixa de seleção na Olá **configurar URL do aplicativo** página da caixa de diálogo Olá</span><span class="sxs-lookup"><span data-stu-id="86a14-161">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog</span></span> 


5. <span data-ttu-id="86a14-162">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="86a14-162">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="86a14-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="86a14-164">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="86a14-166">Em Olá **configuração da área restrita Salesforce** seção, clique em **configurar área restrita do Salesforce** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="86a14-166">On hello **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="86a14-167">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="86a14-167">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="86a14-168">![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="86a14-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="86a14-169">Abra uma nova guia no seu navegador e faça logon tooyour conta de administrador da área restrita do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="86a14-169">Open a new tab in your browser and log in tooyour Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="86a14-170">No menu de saudação na parte superior de saudação, clique em **instalação**.</span><span class="sxs-lookup"><span data-stu-id="86a14-170">In hello menu on hello top, click **Setup**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="86a14-172">No painel de navegação Olá Olá esquerda, clique em **controles de segurança**e, em seguida, clique em **configurações de logon único**.</span><span class="sxs-lookup"><span data-stu-id="86a14-172">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="86a14-174">Na seção configurações de logon único do hello, executar Olá etapas a seguir: ![configurar logon único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="86a14-174">On hello Single Sign-On Settings section, perform hello following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="86a14-175">a.</span><span class="sxs-lookup"><span data-stu-id="86a14-175">a.</span></span>  <span data-ttu-id="86a14-176">Selecione **SAML Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="86a14-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="86a14-177">b.</span><span class="sxs-lookup"><span data-stu-id="86a14-177">b.</span></span>  <span data-ttu-id="86a14-178">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="86a14-178">Click **New**.</span></span>

12. <span data-ttu-id="86a14-179">Na seção configurações de logon único SAML do hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="86a14-179">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="86a14-181">a.In Olá de texto Nome, digite o nome de saudação da configuração de saudação (por exemplo: *SPSSOWAAD\_teste*).</span><span class="sxs-lookup"><span data-stu-id="86a14-181">a.In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="86a14-182">b.</span><span class="sxs-lookup"><span data-stu-id="86a14-182">b.</span></span> <span data-ttu-id="86a14-183">Colar **ID da entidade Small** valor em Olá **emissor** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="86a14-183">Paste **SMAL Entity ID** value into hello **Issuer** textbox.</span></span>

    <span data-ttu-id="86a14-184">c.</span><span class="sxs-lookup"><span data-stu-id="86a14-184">c.</span></span> <span data-ttu-id="86a14-185">Em Olá **Id da entidade** caixa de texto, tipo **https://test.salesforce.com** se for Olá a primeira instância de área restrita do Salesforce que você está adicionando tooyour directory.</span><span class="sxs-lookup"><span data-stu-id="86a14-185">In hello **Entity Id** textbox, type **https://test.salesforce.com** if it is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="86a14-186">Se você já tiver adicionado uma instância de área restrita do Salesforce, em seguida, para Olá **ID da entidade** tipo no hello **URL de logon**, que deveriam estar neste formato:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="86a14-186">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="86a14-187">d.</span><span class="sxs-lookup"><span data-stu-id="86a14-187">d.</span></span> <span data-ttu-id="86a14-188">Clique em **procurar** Olá tooupload baixado o certificado.</span><span class="sxs-lookup"><span data-stu-id="86a14-188">Click **Browse** tooupload hello downloaded certificate.</span></span>  

    <span data-ttu-id="86a14-189">e.</span><span class="sxs-lookup"><span data-stu-id="86a14-189">e.</span></span> <span data-ttu-id="86a14-190">Como **tipo de identidade SAML**, selecione **asserção contém Olá ID de Federação do objeto de usuário Olá**.</span><span class="sxs-lookup"><span data-stu-id="86a14-190">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
 
    <span data-ttu-id="86a14-191">f.</span><span class="sxs-lookup"><span data-stu-id="86a14-191">f.</span></span> <span data-ttu-id="86a14-192">Como **local da identidade do SAML**, selecione **identidade está no elemento NameIdentifier Olá Olá declaração assunto**.</span><span class="sxs-lookup"><span data-stu-id="86a14-192">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="86a14-193">g.</span><span class="sxs-lookup"><span data-stu-id="86a14-193">g.</span></span> <span data-ttu-id="86a14-194">Colar **o URL de serviço de logon único** em Olá **URL de logon do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="86a14-194">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="86a14-195">h.</span><span class="sxs-lookup"><span data-stu-id="86a14-195">h.</span></span> <span data-ttu-id="86a14-196">O SFDC não dá suporte a logout SAML.</span><span class="sxs-lookup"><span data-stu-id="86a14-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="86a14-197">Como alternativa, cole 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0'-o na Olá **URL de Logout do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="86a14-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="86a14-198">i.</span><span class="sxs-lookup"><span data-stu-id="86a14-198">i.</span></span> <span data-ttu-id="86a14-199">Para **Associação de Solicitação Iniciada pelo Provedor de Serviços**, selecione **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="86a14-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="86a14-200">j.</span><span class="sxs-lookup"><span data-stu-id="86a14-200">j.</span></span> <span data-ttu-id="86a14-201">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="86a14-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="86a14-202">Habilitar seu domínio</span><span class="sxs-lookup"><span data-stu-id="86a14-202">Enable your domain</span></span>
<span data-ttu-id="86a14-203">Esta seção pressupõe que você já tenha criado um domínio.</span><span class="sxs-lookup"><span data-stu-id="86a14-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="86a14-204">Para obter mais informações, consulte [Definindo o nome de domínio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="86a14-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="86a14-205">**tooenable seu domínio, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="86a14-205">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a14-206">No painel de navegação esquerdo hello, clique em **gerenciamento de domínio**e, em seguida, clique em **meu domínio.**</span><span class="sxs-lookup"><span data-stu-id="86a14-206">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="86a14-208">Verifique se o domínio foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="86a14-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="86a14-209">Em Olá **configurações de página de logon** seção, clique em **editar**, em seguida, como **serviço de autenticação**, selecione nome de saudação do hello configuração de logon único SAML de saudação anterior seção e, finalmente, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="86a14-209">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="86a14-211">Assim que você tiver um domínio configurado, seus usuários devem usar a área restrita do Salesforce Olá domínio URL toologin toohello.</span><span class="sxs-lookup"><span data-stu-id="86a14-211">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="86a14-212">valor tooget Olá Olá URL, clique em perfil Olá SSO que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="86a14-212">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="86a14-213">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="86a14-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="86a14-214">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="86a14-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="86a14-215">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86a14-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="86a14-216">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="86a14-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="86a14-217">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="86a14-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="86a14-219">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="86a14-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a14-220">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="86a14-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86a14-222">lista de saudação toodisplay de usuários ir muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="86a14-222">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86a14-224">Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="86a14-224">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86a14-226">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="86a14-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86a14-228">a.</span><span class="sxs-lookup"><span data-stu-id="86a14-228">a.</span></span> <span data-ttu-id="86a14-229">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86a14-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86a14-230">b.</span><span class="sxs-lookup"><span data-stu-id="86a14-230">b.</span></span> <span data-ttu-id="86a14-231">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="86a14-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86a14-232">c.</span><span class="sxs-lookup"><span data-stu-id="86a14-232">c.</span></span> <span data-ttu-id="86a14-233">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="86a14-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="86a14-234">d.</span><span class="sxs-lookup"><span data-stu-id="86a14-234">d.</span></span> <span data-ttu-id="86a14-235">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="86a14-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="86a14-236">Criando um usuário de teste do Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="86a14-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="86a14-237">Nesta seção, um usuário chamado Brenda Fernandes é criado no Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="86a14-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="86a14-238">O Salesforce Sandbox dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="86a14-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="86a14-239">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="86a14-239">There is no action item for you in this section.</span></span> <span data-ttu-id="86a14-240">Se um usuário ainda não existir na área restrita do Salesforce, um novo será criado quando você tenta tooaccess área restrita do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="86a14-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt tooaccess Salesforce Sandbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="86a14-241">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="86a14-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="86a14-242">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSalesforce área restrita.</span><span class="sxs-lookup"><span data-stu-id="86a14-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce Sandbox.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="86a14-244">**tooassign Britta Simon tooSalesforce área restrita, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="86a14-244">**tooassign Britta Simon tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a14-245">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="86a14-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="86a14-247">Na lista de aplicativos hello, selecione **área restrita do Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="86a14-247">In hello applications list, select **Salesforce Sandbox**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="86a14-249">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="86a14-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="86a14-251">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86a14-251">Click **Add** button.</span></span> <span data-ttu-id="86a14-252">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="86a14-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="86a14-254">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="86a14-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="86a14-255">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="86a14-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86a14-256">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="86a14-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="86a14-257">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="86a14-257">Testing single sign-on</span></span>

<span data-ttu-id="86a14-258">Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="86a14-258">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="86a14-259">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="86a14-259">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86a14-260">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="86a14-260">Additional resources</span></span>

* [<span data-ttu-id="86a14-261">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="86a14-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86a14-262">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="86a14-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="86a14-263">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="86a14-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

