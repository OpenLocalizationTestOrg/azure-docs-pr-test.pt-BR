---
title: "Tutorial: Integração do Active Directory do Azure ao Aha! | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Aha!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="0066a-104">Tutorial: Integração do Active Directory do Azure ao Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="0066a-105">Neste tutorial, você aprenderá como toointegrate Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-105">In this tutorial, you learn how toointegrate Aha!</span></span> <span data-ttu-id="0066a-106">ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0066a-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0066a-107">A integração do Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-107">Integrating Aha!</span></span> <span data-ttu-id="0066a-108">com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="0066a-108">with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0066a-109">Você pode controlar no AD do Azure que tenha acesso tooAha!</span><span class="sxs-lookup"><span data-stu-id="0066a-109">You can control in Azure AD who has access tooAha!</span></span>
- <span data-ttu-id="0066a-110">Você pode habilitar seu usuários tooautomatically get conectado tooAha!</span><span class="sxs-lookup"><span data-stu-id="0066a-110">You can enable your users tooautomatically get signed-on tooAha!</span></span> <span data-ttu-id="0066a-111">(Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0066a-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0066a-112">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0066a-112">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0066a-113">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0066a-113">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0066a-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0066a-114">Prerequisites</span></span>

<span data-ttu-id="0066a-115">tooconfigure integração do AD do Azure com o Aha!, é necessário Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="0066a-115">tooconfigure Azure AD integration with Aha!, you need hello following items:</span></span>

- <span data-ttu-id="0066a-116">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0066a-116">An Azure AD subscription</span></span>
- <span data-ttu-id="0066a-117">Uma assinatura da Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-117">An Aha!</span></span> <span data-ttu-id="0066a-118">Uma assinatura habilitada para logon único do Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0066a-119">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0066a-119">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0066a-120">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0066a-120">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0066a-121">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0066a-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0066a-122">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0066a-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0066a-123">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0066a-123">Scenario description</span></span>
<span data-ttu-id="0066a-124">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0066a-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0066a-125">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="0066a-125">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0066a-126">Adicionando o Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-126">Adding Aha!</span></span> <span data-ttu-id="0066a-127">da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0066a-127">from hello gallery</span></span>
2. <span data-ttu-id="0066a-128">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0066a-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-hello-gallery"></a><span data-ttu-id="0066a-129">Adicionando o Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-129">Adding Aha!</span></span> <span data-ttu-id="0066a-130">da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0066a-130">from hello gallery</span></span>
<span data-ttu-id="0066a-131">integração de saudação do tooconfigure do Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-131">tooconfigure hello integration of Aha!</span></span> <span data-ttu-id="0066a-132">no AD do Azure, você precisa tooadd Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-132">into Azure AD, you need tooadd Aha!</span></span> <span data-ttu-id="0066a-133">na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0066a-133">from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0066a-134">**tooadd Aha! na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0066a-134">**tooadd Aha! from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0066a-135">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0066a-135">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0066a-137">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0066a-137">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0066a-138">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0066a-138">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0066a-140">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0066a-140">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0066a-142">Na caixa de pesquisa hello, digite **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="0066a-142">In hello search box, type **Aha!**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="0066a-144">No painel de resultados de saudação, selecione **Aha!**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0066a-144">In hello results panel, select **Aha!**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0066a-146">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0066a-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0066a-147">Nesta seção, configura e testa o logon único do Azure AD com o Aha!,</span><span class="sxs-lookup"><span data-stu-id="0066a-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="0066a-148">com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="0066a-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0066a-149">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aha!</span></span> <span data-ttu-id="0066a-150">é o usuário tooa no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0066a-150">is tooa user in Azure AD.</span></span> <span data-ttu-id="0066a-151">Em outras palavras, uma relação de link entre um usuário do AD do Azure e hello relacionados ao usuário no Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-151">In other words, a link relationship between an Azure AD user and hello related user in Aha!</span></span> <span data-ttu-id="0066a-152">precisa de toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0066a-152">needs toobe established.</span></span>

<span data-ttu-id="0066a-153">No Aha!, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="0066a-153">In Aha!, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0066a-154">tooconfigure e teste do AD do Azure, logon único com o Aha!, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="0066a-154">tooconfigure and test Azure AD single sign-on with Aha!, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0066a-155">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0066a-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0066a-156">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0066a-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0066a-157">**[Criando um Aha! usuário de teste](#creating-an-aha-test-user)**  -toohave um equivalente do Britta Simon no Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - toohave a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="0066a-158">que é vinculado toohello representação do AD do Azure do usuário.</span><span class="sxs-lookup"><span data-stu-id="0066a-158">that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0066a-159">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="0066a-159">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0066a-160">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="0066a-160">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0066a-161">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0066a-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0066a-162">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-162">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="0066a-163">.</span><span class="sxs-lookup"><span data-stu-id="0066a-163">application.</span></span>

<span data-ttu-id="0066a-164">**tooconfigure logon único do AD do Azure com o Aha!, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0066a-164">**tooconfigure Azure AD single sign-on with Aha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="0066a-165">Em Olá portal do Azure, Olá **Aha!**</span><span class="sxs-lookup"><span data-stu-id="0066a-165">In hello Azure portal, on hello **Aha!**</span></span> <span data-ttu-id="0066a-166">clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="0066a-166">application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0066a-168">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="0066a-168">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="0066a-170">Em Olá **Aha! Domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0066a-170">On hello **Aha! Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="0066a-172">a.</span><span class="sxs-lookup"><span data-stu-id="0066a-172">a.</span></span> <span data-ttu-id="0066a-173">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="0066a-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="0066a-174">b.</span><span class="sxs-lookup"><span data-stu-id="0066a-174">b.</span></span> <span data-ttu-id="0066a-175">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="0066a-175">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0066a-176">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="0066a-176">These values are not real.</span></span> <span data-ttu-id="0066a-177">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="0066a-177">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0066a-178">Contate a [equipe de suporte ao Cliente do Equipe de suporte do cliente](https://www.aha.io/company/contact) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="0066a-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="0066a-179">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0066a-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="0066a-181">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0066a-181">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0066a-183">Em uma janela de navegador web diferente, faça logon no tooyour Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-183">In a different web browser window, log in tooyour Aha!</span></span> <span data-ttu-id="0066a-184">como um administrador.</span><span class="sxs-lookup"><span data-stu-id="0066a-184">company site as an administrator.</span></span>

7. <span data-ttu-id="0066a-185">No menu de saudação na parte superior de saudação, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="0066a-185">In hello menu on hello top, click **Settings**.</span></span>

    <span data-ttu-id="0066a-186">![Configurações](./media/active-directory-saas-aha-tutorial/IC798950.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="0066a-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="0066a-187">Clique em **Conta**.</span><span class="sxs-lookup"><span data-stu-id="0066a-187">Click **Account**.</span></span>
   
    <span data-ttu-id="0066a-188">![Perfil](./media/active-directory-saas-aha-tutorial/IC798951.png "Perfil")</span><span class="sxs-lookup"><span data-stu-id="0066a-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="0066a-189">Clique em **Segurança e logon único**.</span><span class="sxs-lookup"><span data-stu-id="0066a-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="0066a-190">![Segurança e logon único](./media/active-directory-saas-aha-tutorial/IC798952.png "Segurança e logon único")</span><span class="sxs-lookup"><span data-stu-id="0066a-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="0066a-191">Na seção **Logon Único**, como **Provedor de Identidade**, selecione **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="0066a-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="0066a-192">![Segurança e logon único](./media/active-directory-saas-aha-tutorial/IC798953.png "Segurança e logon único")</span><span class="sxs-lookup"><span data-stu-id="0066a-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="0066a-193">Em Olá **Single Sign-On** configuração de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0066a-193">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
    
    <span data-ttu-id="0066a-194">![Logon Único](./media/active-directory-saas-aha-tutorial/IC798954.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="0066a-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="0066a-195">a.</span><span class="sxs-lookup"><span data-stu-id="0066a-195">a.</span></span> <span data-ttu-id="0066a-196">Em Olá **nome** caixa de texto, digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="0066a-196">In hello **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="0066a-197">b.</span><span class="sxs-lookup"><span data-stu-id="0066a-197">b.</span></span> <span data-ttu-id="0066a-198">Para **Configurar usando**, selecione **Arquivo de Metadados**.</span><span class="sxs-lookup"><span data-stu-id="0066a-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="0066a-199">c.</span><span class="sxs-lookup"><span data-stu-id="0066a-199">c.</span></span> <span data-ttu-id="0066a-200">tooupload seu arquivo de metadados baixado, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="0066a-200">tooupload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="0066a-201">d.</span><span class="sxs-lookup"><span data-stu-id="0066a-201">d.</span></span> <span data-ttu-id="0066a-202">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="0066a-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="0066a-203">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="0066a-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0066a-204">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="0066a-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0066a-205">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0066a-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0066a-206">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0066a-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="0066a-207">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0066a-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0066a-209">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0066a-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0066a-210">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0066a-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0066a-212">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="0066a-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0066a-214">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0066a-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0066a-216">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0066a-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0066a-218">a.</span><span class="sxs-lookup"><span data-stu-id="0066a-218">a.</span></span> <span data-ttu-id="0066a-219">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0066a-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0066a-220">b.</span><span class="sxs-lookup"><span data-stu-id="0066a-220">b.</span></span> <span data-ttu-id="0066a-221">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0066a-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0066a-222">c.</span><span class="sxs-lookup"><span data-stu-id="0066a-222">c.</span></span> <span data-ttu-id="0066a-223">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="0066a-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0066a-224">d.</span><span class="sxs-lookup"><span data-stu-id="0066a-224">d.</span></span> <span data-ttu-id="0066a-225">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0066a-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="0066a-226">Criando um usuário de teste</span><span class="sxs-lookup"><span data-stu-id="0066a-226">Creating an Aha!</span></span> <span data-ttu-id="0066a-227">do Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-227">test user</span></span>

<span data-ttu-id="0066a-228">toolog de usuários tooenable AD do Azure no tooAha!, eles devem ser provisionados no Aha!.</span><span class="sxs-lookup"><span data-stu-id="0066a-228">tooenable Azure AD users toolog in tooAha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="0066a-229">No caso de saudação do Aha!, o provisionamento é uma tarefa automatizada.</span><span class="sxs-lookup"><span data-stu-id="0066a-229">In hello case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="0066a-230">Não há nenhum item de ação para você.</span><span class="sxs-lookup"><span data-stu-id="0066a-230">There is no action item for you.</span></span>

<span data-ttu-id="0066a-231">Os usuários são criados automaticamente se necessário durante a saudação primeiro único tentativa de logon.</span><span class="sxs-lookup"><span data-stu-id="0066a-231">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="0066a-232">É possível usar qualquer outra ferramenta de criação da conta de usuário do Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-232">You can use any other Aha!</span></span> <span data-ttu-id="0066a-233">ou as APIs fornecidas pelo Aha!</span><span class="sxs-lookup"><span data-stu-id="0066a-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="0066a-234">contas de usuário do AAD tooprovision.</span><span class="sxs-lookup"><span data-stu-id="0066a-234">tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0066a-235">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0066a-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0066a-236">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAha!.</span><span class="sxs-lookup"><span data-stu-id="0066a-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAha!.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0066a-238">**tooassign tooAha Britta Simon!, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0066a-238">**tooassign Britta Simon tooAha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="0066a-239">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0066a-239">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0066a-241">Na lista de aplicativos hello, selecione **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="0066a-241">In hello applications list, select **Aha!**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="0066a-243">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0066a-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0066a-245">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0066a-245">Click **Add** button.</span></span> <span data-ttu-id="0066a-246">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0066a-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0066a-248">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="0066a-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0066a-249">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0066a-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0066a-250">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0066a-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0066a-251">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0066a-251">Testing single sign-on</span></span>

<span data-ttu-id="0066a-252">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="0066a-252">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="0066a-253">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0066a-253">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0066a-254">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0066a-254">Additional resources</span></span>

* [<span data-ttu-id="0066a-255">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0066a-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0066a-256">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0066a-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

