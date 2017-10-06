---
title: "Tutorial: Integração do Azure Active Directory ao BambooHR | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do BambooHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: f9083f846beb3a4bf4cebbf18b42aba2dfef2472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="736ec-103">Tutorial: Integração do Azure Active Directory ao BambooHR</span><span class="sxs-lookup"><span data-stu-id="736ec-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="736ec-104">Neste tutorial, você aprenderá como toointegrate BambooHR com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="736ec-104">In this tutorial, you learn how toointegrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="736ec-105">Integrando o BambooHR com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="736ec-105">Integrating BambooHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="736ec-106">Você pode controlar no AD do Azure que tenha acesso tooBambooHR</span><span class="sxs-lookup"><span data-stu-id="736ec-106">You can control in Azure AD who has access tooBambooHR</span></span>
- <span data-ttu-id="736ec-107">Você pode habilitar seu usuários tooautomatically get conectado tooBambooHR (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="736ec-107">You can enable your users tooautomatically get signed-on tooBambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="736ec-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="736ec-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="736ec-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="736ec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="736ec-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="736ec-110">Prerequisites</span></span>

<span data-ttu-id="736ec-111">tooconfigure integração do AD do Azure com BambooHR, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="736ec-111">tooconfigure Azure AD integration with BambooHR, you need hello following items:</span></span>

- <span data-ttu-id="736ec-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="736ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="736ec-113">Uma assinatura habilitada para logon único do BambooHR</span><span class="sxs-lookup"><span data-stu-id="736ec-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="736ec-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="736ec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="736ec-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="736ec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="736ec-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="736ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="736ec-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="736ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="736ec-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="736ec-118">Scenario description</span></span>
<span data-ttu-id="736ec-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="736ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="736ec-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="736ec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="736ec-121">Adicionando BambooHR da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="736ec-121">Adding BambooHR from hello gallery</span></span>
2. <span data-ttu-id="736ec-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="736ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-hello-gallery"></a><span data-ttu-id="736ec-123">Adicionando BambooHR da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="736ec-123">Adding BambooHR from hello gallery</span></span>
<span data-ttu-id="736ec-124">integração de saudação tooconfigure do BambooHR no AD do Azure, você precisa tooadd BambooHR da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="736ec-124">tooconfigure hello integration of BambooHR into Azure AD, you need tooadd BambooHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="736ec-125">**tooadd BambooHR da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="736ec-125">**tooadd BambooHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="736ec-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="736ec-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="736ec-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="736ec-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="736ec-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="736ec-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="736ec-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="736ec-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="736ec-133">Na caixa de pesquisa hello, digite **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="736ec-133">In hello search box, type **BambooHR**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="736ec-135">No painel de resultados de saudação, selecione **BambooHR**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="736ec-135">In hello results panel, select **BambooHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="736ec-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="736ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="736ec-138">Nesta seção, você configura e testa o logon único do Azure AD com o BambooHR, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="736ec-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="736ec-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no BambooHR é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="736ec-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BambooHR is tooa user in Azure AD.</span></span> <span data-ttu-id="736ec-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no BambooHR precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="736ec-140">In other words, a link relationship between an Azure AD user and hello related user in BambooHR needs toobe established.</span></span>

<span data-ttu-id="736ec-141">No BambooHR, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="736ec-141">In BambooHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="736ec-142">tooconfigure e teste de logon único do AD do Azure com BambooHR, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="736ec-142">tooconfigure and test Azure AD single sign-on with BambooHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="736ec-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="736ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="736ec-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="736ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="736ec-145">**[Criar um usuário de teste do BambooHR](#creating-a-bamboohr-test-user)**  -toohave um equivalente do Britta Simon no BambooHR é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="736ec-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - toohave a counterpart of Britta Simon in BambooHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="736ec-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="736ec-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="736ec-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="736ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="736ec-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="736ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="736ec-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo BambooHR.</span><span class="sxs-lookup"><span data-stu-id="736ec-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="736ec-150">**tooconfigure AD do Azure-logon único com BambooHR, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="736ec-150">**tooconfigure Azure AD single sign-on with BambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="736ec-151">Em Olá portal do Azure, Olá **BambooHR** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="736ec-151">In hello Azure portal, on hello **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="736ec-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="736ec-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="736ec-155">Em Olá **BambooHR domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="736ec-155">On hello **BambooHR Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="736ec-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="736ec-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="736ec-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="736ec-158">This value is not real.</span></span> <span data-ttu-id="736ec-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="736ec-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="736ec-160">Entre em contato com [equipe de suporte do cliente do BambooHR](https://www.bamboohr.com/contact.php) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="736ec-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) tooget this value.</span></span> 
 
4. <span data-ttu-id="736ec-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="736ec-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="736ec-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="736ec-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="736ec-165">Em Olá **BambooHR configuração** seção, clique em **configurar BambooHR** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="736ec-165">On hello **BambooHR Configuration** section, click **Configure BambooHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="736ec-166">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="736ec-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="736ec-168">Em outra janela do navegador da Web, faça logon em seu site de empresa BambooHR como um administrador.</span><span class="sxs-lookup"><span data-stu-id="736ec-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="736ec-169">Na home page Olá, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="736ec-169">On hello homepage, perform hello following steps:</span></span>
   
    <span data-ttu-id="736ec-170">![Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="736ec-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="736ec-171">a.</span><span class="sxs-lookup"><span data-stu-id="736ec-171">a.</span></span> <span data-ttu-id="736ec-172">Clique em **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="736ec-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="736ec-173">b.</span><span class="sxs-lookup"><span data-stu-id="736ec-173">b.</span></span> <span data-ttu-id="736ec-174">No menu de aplicativos Olá Olá esquerda, clique em **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="736ec-174">In hello apps menu on hello left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="736ec-175">c.</span><span class="sxs-lookup"><span data-stu-id="736ec-175">c.</span></span> <span data-ttu-id="736ec-176">Clique em **Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="736ec-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="736ec-177">Em Olá **logon único SAML** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="736ec-177">In hello **SAML Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="736ec-178">![Logon Único do SAML](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="736ec-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="736ec-179">a.</span><span class="sxs-lookup"><span data-stu-id="736ec-179">a.</span></span> <span data-ttu-id="736ec-180">Saudação de colar **Single Sign-On URL do serviço SAML** valor em Olá **Url de logon SSO** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="736ec-180">Paste hello **SAML Single Sign-On Service URL** value into hello **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="736ec-181">b.</span><span class="sxs-lookup"><span data-stu-id="736ec-181">b.</span></span> <span data-ttu-id="736ec-182">Abra o certificado codificado em base 64, baixado do portal do Azure no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto</span><span class="sxs-lookup"><span data-stu-id="736ec-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="736ec-183">c.</span><span class="sxs-lookup"><span data-stu-id="736ec-183">c.</span></span> <span data-ttu-id="736ec-184">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="736ec-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="736ec-185">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="736ec-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="736ec-186">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="736ec-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="736ec-187">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="736ec-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="736ec-188">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="736ec-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="736ec-189">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="736ec-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="736ec-191">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="736ec-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="736ec-192">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="736ec-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="736ec-194">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="736ec-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="736ec-196">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="736ec-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="736ec-198">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="736ec-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="736ec-200">a.</span><span class="sxs-lookup"><span data-stu-id="736ec-200">a.</span></span> <span data-ttu-id="736ec-201">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="736ec-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="736ec-202">b.</span><span class="sxs-lookup"><span data-stu-id="736ec-202">b.</span></span> <span data-ttu-id="736ec-203">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="736ec-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="736ec-204">c.</span><span class="sxs-lookup"><span data-stu-id="736ec-204">c.</span></span> <span data-ttu-id="736ec-205">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="736ec-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="736ec-206">d.</span><span class="sxs-lookup"><span data-stu-id="736ec-206">d.</span></span> <span data-ttu-id="736ec-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="736ec-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="736ec-208">Criando um usuário de teste do BambooHR</span><span class="sxs-lookup"><span data-stu-id="736ec-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="736ec-209">tooenable AD do Azure usuários toolog em tooBambooHR, eles devem ser provisionados no BambooHR.</span><span class="sxs-lookup"><span data-stu-id="736ec-209">tooenable Azure AD users toolog in tooBambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="736ec-210">No caso de saudação do BambooHR, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="736ec-210">In hello case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="736ec-211">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="736ec-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="736ec-212">Faça logon no tooyour **BambooHR** site como administrador.</span><span class="sxs-lookup"><span data-stu-id="736ec-212">Log in tooyour **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="736ec-213">Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="736ec-213">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="736ec-214">![Configuração](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="736ec-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="736ec-215">Clique em **Visão Geral**.</span><span class="sxs-lookup"><span data-stu-id="736ec-215">Click **Overview**.</span></span>

4. <span data-ttu-id="736ec-216">No painel de navegação esquerdo hello, vá muito**segurança \> usuários**.</span><span class="sxs-lookup"><span data-stu-id="736ec-216">In hello left navigation pane, go too**Security \> Users**.</span></span>

5. <span data-ttu-id="736ec-217">Nome de usuário do tipo hello, senha e endereço de email de uma conta válida do AAD que você deseja tooprovision em Olá relacionam caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="736ec-217">Type hello user name, password, and email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

6. <span data-ttu-id="736ec-218">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="736ec-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="736ec-219">Você pode usar qualquer ferramenta de criação outros BambooHR usuário conta ou APIs fornecidas pelo BambooHR tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="736ec-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="736ec-220">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="736ec-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="736ec-221">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBambooHR.</span><span class="sxs-lookup"><span data-stu-id="736ec-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBambooHR.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="736ec-223">**tooassign Britta Simon tooBambooHR, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="736ec-223">**tooassign Britta Simon tooBambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="736ec-224">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="736ec-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="736ec-226">Na lista de aplicativos hello, selecione **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="736ec-226">In hello applications list, select **BambooHR**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="736ec-228">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="736ec-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="736ec-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="736ec-230">Click **Add** button.</span></span> <span data-ttu-id="736ec-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="736ec-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="736ec-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="736ec-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="736ec-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="736ec-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="736ec-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="736ec-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="736ec-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="736ec-236">Testing single sign-on</span></span>

<span data-ttu-id="736ec-237">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="736ec-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="736ec-238">Quando você clica em bloco BambooHR Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour BambooHR aplicativo.</span><span class="sxs-lookup"><span data-stu-id="736ec-238">When you click hello BambooHR tile in hello Access Panel, you should get automatically signed-on tooyour BambooHR application.</span></span>
<span data-ttu-id="736ec-239">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="736ec-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="736ec-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="736ec-240">Additional resources</span></span>

* [<span data-ttu-id="736ec-241">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="736ec-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="736ec-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="736ec-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

