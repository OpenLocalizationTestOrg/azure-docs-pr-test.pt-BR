---
title: "Tutorial: Integração do Azure Active Directory ao Mimecast Personal Portal | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Portal pessoal do Mimecast."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="836bf-103">Tutorial: Integração do Azure Active Directory ao Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="836bf-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="836bf-104">Neste tutorial, você aprenderá como toointegrate Portal pessoal do Mimecast com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="836bf-104">In this tutorial, you learn how toointegrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="836bf-105">Integração do Portal pessoal do Mimecast com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="836bf-105">Integrating Mimecast Personal Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="836bf-106">Você pode controlar no AD do Azure que tenha acesso tooMimecast Portal pessoal</span><span class="sxs-lookup"><span data-stu-id="836bf-106">You can control in Azure AD who has access tooMimecast Personal Portal</span></span>
- <span data-ttu-id="836bf-107">Você pode habilitar seu usuários tooautomatically get conectado tooMimecast Portal pessoal (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="836bf-107">You can enable your users tooautomatically get signed-on tooMimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="836bf-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="836bf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="836bf-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="836bf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="836bf-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="836bf-110">Prerequisites</span></span>

<span data-ttu-id="836bf-111">tooconfigure integração do AD do Azure com o Portal pessoal do Mimecast, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="836bf-111">tooconfigure Azure AD integration with Mimecast Personal Portal, you need hello following items:</span></span>

- <span data-ttu-id="836bf-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="836bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="836bf-113">Uma assinatura do Mimecast Personal Portal com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="836bf-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="836bf-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="836bf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="836bf-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="836bf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="836bf-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="836bf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="836bf-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="836bf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="836bf-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="836bf-118">Scenario description</span></span>
<span data-ttu-id="836bf-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="836bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="836bf-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="836bf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="836bf-121">Adicionar Portal pessoal do Mimecast da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="836bf-121">Adding Mimecast Personal Portal from hello gallery</span></span>
2. <span data-ttu-id="836bf-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="836bf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a><span data-ttu-id="836bf-123">Adicionar Portal pessoal do Mimecast da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="836bf-123">Adding Mimecast Personal Portal from hello gallery</span></span>
<span data-ttu-id="836bf-124">integração de saudação tooconfigure do Portal pessoal do Mimecast no AD do Azure, você precisa tooadd Portal pessoal do Mimecast da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="836bf-124">tooconfigure hello integration of Mimecast Personal Portal into Azure AD, you need tooadd Mimecast Personal Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="836bf-125">**tooadd Portal pessoal do Mimecast da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="836bf-125">**tooadd Mimecast Personal Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="836bf-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="836bf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="836bf-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="836bf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="836bf-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="836bf-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="836bf-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="836bf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="836bf-133">Na caixa de pesquisa hello, digite **Portal pessoal do Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="836bf-133">In hello search box, type **Mimecast Personal Portal**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="836bf-135">No painel de resultados de saudação, selecione **Portal pessoal do Mimecast**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="836bf-135">In hello results panel, select **Mimecast Personal Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="836bf-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="836bf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="836bf-138">Nesta seção, você configura e testa o logon único do Azure AD com o Mimecast Personal Portal, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="836bf-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="836bf-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Portal pessoal do Mimecast é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="836bf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Personal Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="836bf-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Portal pessoal do Mimecast precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="836bf-140">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Personal Portal needs toobe established.</span></span>

<span data-ttu-id="836bf-141">No Portal pessoal do Mimecast, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="836bf-141">In Mimecast Personal Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="836bf-142">tooconfigure e teste de logon único do AD do Azure com o Portal pessoal do Mimecast, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="836bf-142">tooconfigure and test Azure AD single sign-on with Mimecast Personal Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="836bf-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="836bf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="836bf-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="836bf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="836bf-145">**[Criar um usuário de teste do Portal pessoal do Mimecast](#creating-a-mimecast-personal-portal-test-user)**  -toohave um equivalente do Britta Simon no Portal pessoal do Mimecast que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="836bf-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - toohave a counterpart of Britta Simon in Mimecast Personal Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="836bf-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="836bf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="836bf-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="836bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="836bf-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="836bf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="836bf-149">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de Portal pessoal do Mimecast.</span><span class="sxs-lookup"><span data-stu-id="836bf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="836bf-150">**tooconfigure logon único do AD do Azure com o Portal pessoal do Mimecast, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="836bf-150">**tooconfigure Azure AD single sign-on with Mimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="836bf-151">Em Olá portal do Azure, Olá **Portal pessoal do Mimecast** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="836bf-151">In hello Azure portal, on hello **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="836bf-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="836bf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="836bf-155">Em Olá **URLs e domínio de Portal pessoal do Mimecast** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="836bf-155">On hello **Mimecast Personal Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="836bf-157">a.</span><span class="sxs-lookup"><span data-stu-id="836bf-157">a.</span></span> <span data-ttu-id="836bf-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="836bf-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="836bf-159">b.</span><span class="sxs-lookup"><span data-stu-id="836bf-159">b.</span></span> <span data-ttu-id="836bf-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="836bf-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="836bf-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="836bf-161">These values are not real.</span></span> <span data-ttu-id="836bf-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="836bf-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="836bf-163">Entre em contato com [equipe de suporte do cliente de Portal pessoal do Mimecast](https://www.mimecast.com/customer-success/technical-support/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="836bf-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) tooget these values.</span></span> 
 


4. <span data-ttu-id="836bf-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="836bf-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="836bf-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="836bf-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="836bf-168">Em Olá **configuração de Portal pessoal do Mimecast** seção, clique em **configurar Portal pessoal do Mimecast** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="836bf-168">On hello **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="836bf-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="836bf-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="836bf-171">Em outra janela do navegador da Web, faça logon em seu Mimecast Personal Portal como um administrador.</span><span class="sxs-lookup"><span data-stu-id="836bf-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="836bf-172">Vá muito**serviços \> aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="836bf-172">Go too**Services \> Applications**.</span></span>
   
    <span data-ttu-id="836bf-173">![Aplicativos](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="836bf-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="836bf-174">Clique em **Perfis de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="836bf-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="836bf-175">![Perfis de Autenticação](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Perfis de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="836bf-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="836bf-176">Clique em **Novo Perfil de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="836bf-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="836bf-177">![Novo Perfil de Autenticação](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "Novo Perfil de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="836bf-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="836bf-178">Em Olá **o perfil de autenticação** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="836bf-178">In hello **Authentication Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="836bf-179">![Perfil de Autenticação](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Perfil de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="836bf-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="836bf-180">a.</span><span class="sxs-lookup"><span data-stu-id="836bf-180">a.</span></span> <span data-ttu-id="836bf-181">Em Olá **descrição** caixa de texto, digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="836bf-181">In hello **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="836bf-182">b.</span><span class="sxs-lookup"><span data-stu-id="836bf-182">b.</span></span> <span data-ttu-id="836bf-183">Selecione **Impor Autenticação SAML para o Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="836bf-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="836bf-184">c.</span><span class="sxs-lookup"><span data-stu-id="836bf-184">c.</span></span> <span data-ttu-id="836bf-185">Como **Provedor**, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="836bf-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="836bf-186">d.</span><span class="sxs-lookup"><span data-stu-id="836bf-186">d.</span></span> <span data-ttu-id="836bf-187">Em **URL do emissor** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="836bf-187">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="836bf-188">e.</span><span class="sxs-lookup"><span data-stu-id="836bf-188">e.</span></span> <span data-ttu-id="836bf-189">Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="836bf-189">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="836bf-190">f.</span><span class="sxs-lookup"><span data-stu-id="836bf-190">f.</span></span> <span data-ttu-id="836bf-191">Em **URL de Logout** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="836bf-191">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="836bf-192">g.</span><span class="sxs-lookup"><span data-stu-id="836bf-192">g.</span></span> <span data-ttu-id="836bf-193">Abra o **base 64** codificado certificado baixado do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência, o bloco de notas e, em seguida, cole-o toohello **certificado do provedor de identidade (metadados)** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="836bf-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="836bf-194">h.</span><span class="sxs-lookup"><span data-stu-id="836bf-194">h.</span></span> <span data-ttu-id="836bf-195">Selecione **Permitir Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="836bf-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="836bf-196">i.</span><span class="sxs-lookup"><span data-stu-id="836bf-196">i.</span></span> <span data-ttu-id="836bf-197">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="836bf-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="836bf-198">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="836bf-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="836bf-199">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="836bf-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="836bf-200">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="836bf-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="836bf-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="836bf-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="836bf-202">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="836bf-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="836bf-204">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="836bf-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="836bf-205">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="836bf-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="836bf-207">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="836bf-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="836bf-209">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="836bf-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="836bf-211">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="836bf-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="836bf-213">a.</span><span class="sxs-lookup"><span data-stu-id="836bf-213">a.</span></span> <span data-ttu-id="836bf-214">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="836bf-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="836bf-215">b.</span><span class="sxs-lookup"><span data-stu-id="836bf-215">b.</span></span> <span data-ttu-id="836bf-216">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="836bf-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="836bf-217">c.</span><span class="sxs-lookup"><span data-stu-id="836bf-217">c.</span></span> <span data-ttu-id="836bf-218">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="836bf-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="836bf-219">d.</span><span class="sxs-lookup"><span data-stu-id="836bf-219">d.</span></span> <span data-ttu-id="836bf-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="836bf-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="836bf-221">Criando um usuário de teste do Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="836bf-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="836bf-222">Em ordem tooenable AD do Azure toolog usuários no Portal pessoal do Mimecast, eles devem ser provisionados no Portal pessoal do Mimecast.</span><span class="sxs-lookup"><span data-stu-id="836bf-222">In order tooenable Azure AD users toolog into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="836bf-223">No caso de saudação do Portal pessoal do Mimecast, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="836bf-223">In hello case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="836bf-224">Antes de criar os usuários, você precisa tooregister um domínio.</span><span class="sxs-lookup"><span data-stu-id="836bf-224">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="836bf-225">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="836bf-225">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="836bf-226">Logon tooyour **Portal pessoal do Mimecast** como administrador.</span><span class="sxs-lookup"><span data-stu-id="836bf-226">Sign on tooyour **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="836bf-227">Vá muito**diretórios \> interno**.</span><span class="sxs-lookup"><span data-stu-id="836bf-227">Go too**Directories \> Internal**.</span></span>
   
    <span data-ttu-id="836bf-228">![Diretórios](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Diretórios")</span><span class="sxs-lookup"><span data-stu-id="836bf-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="836bf-229">Clique em **Registrar Novo Domínio**.</span><span class="sxs-lookup"><span data-stu-id="836bf-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="836bf-230">![Registrar Novo Domínio](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Registrar Novo Domínio")</span><span class="sxs-lookup"><span data-stu-id="836bf-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="836bf-231">Depois de criar o novo domínio, clique em **Novo Endereço**.</span><span class="sxs-lookup"><span data-stu-id="836bf-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="836bf-232">![Novo Endereço](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "Novo Endereço")</span><span class="sxs-lookup"><span data-stu-id="836bf-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="836bf-233">Na caixa de diálogo Olá de novo endereço, executar Olá seguindo as etapas de uma válida do Azure você deseja tooprovision de conta do AD:</span><span class="sxs-lookup"><span data-stu-id="836bf-233">In hello new address dialog, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="836bf-234">![Salvar](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Salvar")</span><span class="sxs-lookup"><span data-stu-id="836bf-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="836bf-235">a.</span><span class="sxs-lookup"><span data-stu-id="836bf-235">a.</span></span> <span data-ttu-id="836bf-236">Em Olá **endereço de Email** caixa de texto, tipo **endereço de Email** do usuário hello como  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="836bf-236">In hello **Email Address** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="836bf-237">b.</span><span class="sxs-lookup"><span data-stu-id="836bf-237">b.</span></span> <span data-ttu-id="836bf-238">Em Olá **nome Global** caixa de texto, Olá tipo **username** como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="836bf-238">In hello **Global Name** textbox, type hello **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="836bf-239">c.</span><span class="sxs-lookup"><span data-stu-id="836bf-239">c.</span></span> <span data-ttu-id="836bf-240">Em Olá **senha**, e **Confirmar senha** caixas de texto, Olá tipo **senha** do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="836bf-240">In hello **Password**, and **Confirm Password** textboxes, type hello **Password** of hello user.</span></span>
   
    <span data-ttu-id="836bf-241">b.</span><span class="sxs-lookup"><span data-stu-id="836bf-241">b.</span></span> <span data-ttu-id="836bf-242">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="836bf-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="836bf-243">Você pode usar qualquer outra ferramenta de criação de conta de usuário do Portal pessoal do Mimecast ou APIs fornecidos pelo Portal pessoal do Mimecast tooprovision contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="836bf-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="836bf-244">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="836bf-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="836bf-245">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMimecast Portal pessoal.</span><span class="sxs-lookup"><span data-stu-id="836bf-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Personal Portal.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="836bf-247">**tooassign Britta Simon tooMimecast Portal pessoal, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="836bf-247">**tooassign Britta Simon tooMimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="836bf-248">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="836bf-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="836bf-250">Na lista de aplicativos hello, selecione **Portal pessoal do Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="836bf-250">In hello applications list, select **Mimecast Personal Portal**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="836bf-252">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="836bf-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="836bf-254">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="836bf-254">Click **Add** button.</span></span> <span data-ttu-id="836bf-255">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="836bf-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="836bf-257">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="836bf-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="836bf-258">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="836bf-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="836bf-259">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="836bf-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="836bf-260">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="836bf-260">Testing single sign-on</span></span>
<span data-ttu-id="836bf-261">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="836bf-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="836bf-262">Quando você clica em bloco Portal pessoal do Mimecast Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Portal pessoal do Mimecast.</span><span class="sxs-lookup"><span data-stu-id="836bf-262">When you click hello Mimecast Personal Portal tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Personal Portal application.</span></span> <span data-ttu-id="836bf-263">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="836bf-263">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="836bf-264">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="836bf-264">Additional resources</span></span>

* [<span data-ttu-id="836bf-265">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="836bf-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="836bf-266">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="836bf-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

