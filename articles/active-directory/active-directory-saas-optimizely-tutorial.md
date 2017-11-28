---
title: "Tutorial: Integração do Azure Active Directory ao Optimizely | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Optimizely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="823dc-103">Tutorial: Integração do Azure Active Directory ao Optimizely</span><span class="sxs-lookup"><span data-stu-id="823dc-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="823dc-104">Neste tutorial, você aprenderá como toointegrate Optimizely com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="823dc-104">In this tutorial, you learn how toointegrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="823dc-105">Integrando Optimizely com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="823dc-105">Integrating Optimizely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="823dc-106">Você pode controlar no AD do Azure que tenha acesso tooOptimizely</span><span class="sxs-lookup"><span data-stu-id="823dc-106">You can control in Azure AD who has access tooOptimizely</span></span>
- <span data-ttu-id="823dc-107">Você pode habilitar seu usuários tooautomatically get conectado tooOptimizely (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="823dc-107">You can enable your users tooautomatically get signed-on tooOptimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="823dc-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="823dc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="823dc-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="823dc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="823dc-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="823dc-110">Prerequisites</span></span>

<span data-ttu-id="823dc-111">tooconfigure integração do AD do Azure com Optimizely, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="823dc-111">tooconfigure Azure AD integration with Optimizely, you need hello following items:</span></span>

- <span data-ttu-id="823dc-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="823dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="823dc-113">Uma assinatura habilitada para logon único do Optimizely</span><span class="sxs-lookup"><span data-stu-id="823dc-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="823dc-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="823dc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="823dc-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="823dc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="823dc-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="823dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="823dc-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="823dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="823dc-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="823dc-118">Scenario description</span></span>
<span data-ttu-id="823dc-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="823dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="823dc-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="823dc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="823dc-121">Adicionando Optimizely da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="823dc-121">Adding Optimizely from hello gallery</span></span>
2. <span data-ttu-id="823dc-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="823dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-hello-gallery"></a><span data-ttu-id="823dc-123">Adicionando Optimizely da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="823dc-123">Adding Optimizely from hello gallery</span></span>
<span data-ttu-id="823dc-124">integração de saudação tooconfigure de Optimizely no AD do Azure, você precisa tooadd Optimizely da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="823dc-124">tooconfigure hello integration of Optimizely into Azure AD, you need tooadd Optimizely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="823dc-125">**tooadd Optimizely da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="823dc-125">**tooadd Optimizely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="823dc-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="823dc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="823dc-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="823dc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="823dc-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="823dc-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="823dc-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="823dc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="823dc-133">Na caixa de pesquisa hello, digite **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="823dc-133">In hello search box, type **Optimizely**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="823dc-135">No painel de resultados de saudação, selecione **Optimizely**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="823dc-135">In hello results panel, select **Optimizely**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="823dc-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="823dc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="823dc-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o Optimizely, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="823dc-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="823dc-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Optimizely é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="823dc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Optimizely is tooa user in Azure AD.</span></span> <span data-ttu-id="823dc-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Optimizely precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="823dc-140">In other words, a link relationship between an Azure AD user and hello related user in Optimizely needs toobe established.</span></span>

<span data-ttu-id="823dc-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Optimizely.</span><span class="sxs-lookup"><span data-stu-id="823dc-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Optimizely.</span></span>

<span data-ttu-id="823dc-142">tooconfigure e teste de logon único do AD do Azure com Optimizely, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="823dc-142">tooconfigure and test Azure AD single sign-on with Optimizely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="823dc-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="823dc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="823dc-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="823dc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="823dc-145">**[Criar um usuário de teste Optimizely](#creating-an-optimizely-test-user)**  -toohave um equivalente do Britta Simon em Optimizely é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="823dc-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - toohave a counterpart of Britta Simon in Optimizely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="823dc-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="823dc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="823dc-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="823dc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="823dc-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="823dc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="823dc-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Optimizely.</span><span class="sxs-lookup"><span data-stu-id="823dc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="823dc-150">**tooconfigure AD do Azure-logon único com Optimizely, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="823dc-150">**tooconfigure Azure AD single sign-on with Optimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="823dc-151">Em Olá portal do Azure, Olá **Optimizely** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="823dc-151">In hello Azure portal, on hello **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="823dc-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="823dc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="823dc-155">Em Olá **Optimizely domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="823dc-155">On hello **Optimizely Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="823dc-157">a.</span><span class="sxs-lookup"><span data-stu-id="823dc-157">a.</span></span> <span data-ttu-id="823dc-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="823dc-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="823dc-159">b.</span><span class="sxs-lookup"><span data-stu-id="823dc-159">b.</span></span> <span data-ttu-id="823dc-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="823dc-160">In hello **Identifier** textbox, type a URL using hello following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="823dc-161">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="823dc-161">These values are not hello real.</span></span> <span data-ttu-id="823dc-162">Você atualizará o valor de saudação com URL de logon real hello e o identificador que é explicada posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="823dc-162">You will update hello value with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="823dc-163">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="823dc-163">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="823dc-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="823dc-165">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="823dc-167">Em Olá **Optimizely configuração** seção, clique em **configurar Optimizely** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="823dc-167">On hello **Optimizely Configuration** section, click **Configure Optimizely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="823dc-168">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="823dc-168">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="823dc-170">tooconfigure logon único no **Optimizely** lado, entre em contato com seu gerente de conta Optimizely e fornecer Olá baixado **certificado (Base64)**, e **Single Sign-On URL do serviço SAML** .</span><span class="sxs-lookup"><span data-stu-id="823dc-170">tooconfigure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide hello downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="823dc-171">No email de tooyour de resposta, Optimizely fornece Olá URL de logon (SSO iniciado por SP) e hello valores do identificador (ID de entidade do provedor de serviço).</span><span class="sxs-lookup"><span data-stu-id="823dc-171">In response tooyour email, Optimizely provides you with hello Sign On URL (SP-initiated SSO) and hello Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="823dc-172">a.</span><span class="sxs-lookup"><span data-stu-id="823dc-172">a.</span></span> <span data-ttu-id="823dc-173">Saudação de cópia **URL do SSO iniciado por SP** fornecido por Optimizely e cole no hello **URL de logon** textbox em **Optimizely domínio e URLs** seção no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="823dc-173">Copy hello **SP-initiated SSO URL** provided by Optimizely, and paste into hello **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="823dc-174">b.</span><span class="sxs-lookup"><span data-stu-id="823dc-174">b.</span></span> <span data-ttu-id="823dc-175">Saudação de cópia **ID de entidade do provedor de serviço** fornecido por Optimizely e cole no hello **identificador** textbox em **Optimizely domínio e URLs** seção no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="823dc-175">Copy hello **Service Provider Entity ID** provided by Optimizely, and paste into hello **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="823dc-176">Em uma janela de navegador diferente, logon tooyour Optimizely aplicativo.</span><span class="sxs-lookup"><span data-stu-id="823dc-176">In a different browser window, sign-on tooyour Optimizely application.</span></span>

10. <span data-ttu-id="823dc-177">Clique em nome na parte superior da saudação da conta canto direito e, em seguida, **configurações de conta**.</span><span class="sxs-lookup"><span data-stu-id="823dc-177">Click you account name in hello top right corner and then **Account Settings**.</span></span>
   
    ![Logon Único do AD do Azure](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="823dc-179">Na guia da conta hello, marque a caixa de saudação **habilitar SSO** em logon único no hello **visão geral** seção.</span><span class="sxs-lookup"><span data-stu-id="823dc-179">In hello Account tab, check hello box **Enable SSO** under Single Sign On in hello **Overview** section.</span></span>
   
    ![Logon Único do AD do Azure](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="823dc-181">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="823dc-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="823dc-182">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="823dc-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="823dc-183">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="823dc-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="823dc-184">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="823dc-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="823dc-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="823dc-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="823dc-186">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="823dc-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="823dc-188">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="823dc-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="823dc-189">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="823dc-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="823dc-191">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="823dc-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="823dc-193">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="823dc-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="823dc-195">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="823dc-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="823dc-197">a.</span><span class="sxs-lookup"><span data-stu-id="823dc-197">a.</span></span> <span data-ttu-id="823dc-198">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="823dc-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="823dc-199">b.</span><span class="sxs-lookup"><span data-stu-id="823dc-199">b.</span></span> <span data-ttu-id="823dc-200">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="823dc-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="823dc-201">c.</span><span class="sxs-lookup"><span data-stu-id="823dc-201">c.</span></span> <span data-ttu-id="823dc-202">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="823dc-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="823dc-203">d.</span><span class="sxs-lookup"><span data-stu-id="823dc-203">d.</span></span> <span data-ttu-id="823dc-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="823dc-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="823dc-205">Criando um usuário de teste do Optimizely</span><span class="sxs-lookup"><span data-stu-id="823dc-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="823dc-206">Nesta seção, você cria um usuário chamado Brenda Fernandes no Optimizely.</span><span class="sxs-lookup"><span data-stu-id="823dc-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="823dc-207">Na home page do hello, selecione **colaboradores** guia.</span><span class="sxs-lookup"><span data-stu-id="823dc-207">On hello home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="823dc-208">novo projeto de toohello de Colaborador tooadd, clique em **novo parceiro**.</span><span class="sxs-lookup"><span data-stu-id="823dc-208">tooadd new collaborator toohello project, click **New Collaborator**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="823dc-210">Preencha o endereço de email hello e atribuir uma função.</span><span class="sxs-lookup"><span data-stu-id="823dc-210">Fill in hello email address and assign them a role.</span></span> <span data-ttu-id="823dc-211">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="823dc-211">Click **Invite**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="823dc-213">Eles receberão um convite por email.</span><span class="sxs-lookup"><span data-stu-id="823dc-213">They receive an email invite.</span></span> <span data-ttu-id="823dc-214">Usando o endereço de email hello, eles têm toolog no tooOptimizely.</span><span class="sxs-lookup"><span data-stu-id="823dc-214">Using hello email address, they have toolog in tooOptimizely.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="823dc-215">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="823dc-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="823dc-216">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooOptimizely.</span><span class="sxs-lookup"><span data-stu-id="823dc-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOptimizely.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="823dc-218">**tooassign Britta Simon tooOptimizely, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="823dc-218">**tooassign Britta Simon tooOptimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="823dc-219">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="823dc-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="823dc-221">Na lista de aplicativos hello, selecione **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="823dc-221">In hello applications list, select **Optimizely**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="823dc-223">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="823dc-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="823dc-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="823dc-225">Click **Add** button.</span></span> <span data-ttu-id="823dc-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="823dc-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="823dc-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="823dc-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="823dc-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="823dc-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="823dc-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="823dc-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="823dc-231">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="823dc-231">Testing single sign-on</span></span>

<span data-ttu-id="823dc-232">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="823dc-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="823dc-233">Quando você clica em bloco Optimizely Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Optimizely aplicativo.</span><span class="sxs-lookup"><span data-stu-id="823dc-233">When you click hello Optimizely tile in hello Access Panel, you should get automatically signed-on tooyour Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="823dc-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="823dc-234">Additional resources</span></span>

* [<span data-ttu-id="823dc-235">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="823dc-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="823dc-236">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="823dc-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

