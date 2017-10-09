---
title: "Tutorial: integração do Azure Active Directory com o SmarterU | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SmarterU."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: a3b81b557c47e31f09e61bcf75dd23f370e642e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="c8abb-103">Tutorial: integração do Azure Active Directory com o SmarterU</span><span class="sxs-lookup"><span data-stu-id="c8abb-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="c8abb-104">Neste tutorial, você aprenderá como toointegrate SmarterU com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c8abb-104">In this tutorial, you learn how toointegrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c8abb-105">Integrando o SmarterU com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8abb-105">Integrating SmarterU with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c8abb-106">Você pode controlar no AD do Azure que tenha acesso tooSmarterU</span><span class="sxs-lookup"><span data-stu-id="c8abb-106">You can control in Azure AD who has access tooSmarterU</span></span>
- <span data-ttu-id="c8abb-107">Você pode habilitar seu usuários tooautomatically get conectado tooSmarterU (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8abb-107">You can enable your users tooautomatically get signed-on tooSmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c8abb-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c8abb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c8abb-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8abb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8abb-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c8abb-110">Prerequisites</span></span>

<span data-ttu-id="c8abb-111">tooconfigure integração do AD do Azure com SmarterU, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8abb-111">tooconfigure Azure AD integration with SmarterU, you need hello following items:</span></span>

- <span data-ttu-id="c8abb-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8abb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c8abb-113">Uma assinatura habilitada para logon único do SmarterU</span><span class="sxs-lookup"><span data-stu-id="c8abb-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c8abb-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c8abb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c8abb-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c8abb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c8abb-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c8abb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c8abb-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8abb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c8abb-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c8abb-118">Scenario description</span></span>
<span data-ttu-id="c8abb-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c8abb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8abb-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c8abb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c8abb-121">Adicionando SmarterU da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c8abb-121">Adding SmarterU from hello gallery</span></span>
2. <span data-ttu-id="c8abb-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8abb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-hello-gallery"></a><span data-ttu-id="c8abb-123">Adicionando SmarterU da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c8abb-123">Adding SmarterU from hello gallery</span></span>
<span data-ttu-id="c8abb-124">integração de saudação tooconfigure do SmarterU no AD do Azure, você precisa tooadd SmarterU da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c8abb-124">tooconfigure hello integration of SmarterU into Azure AD, you need tooadd SmarterU from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c8abb-125">**tooadd SmarterU da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8abb-125">**tooadd SmarterU from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8abb-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c8abb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c8abb-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c8abb-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c8abb-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8abb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c8abb-133">Na caixa de pesquisa hello, digite **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-133">In hello search box, type **SmarterU**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="c8abb-135">No painel de resultados de saudação, selecione **SmarterU**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c8abb-135">In hello results panel, select **SmarterU**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c8abb-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8abb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c8abb-138">Nesta seção, você configurará e testará o logon único do Azure AD com o SmarterU, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c8abb-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c8abb-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SmarterU é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8abb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SmarterU is tooa user in Azure AD.</span></span> <span data-ttu-id="c8abb-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no SmarterU precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c8abb-140">In other words, a link relationship between an Azure AD user and hello related user in SmarterU needs toobe established.</span></span>

<span data-ttu-id="c8abb-141">No SmarterU, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8abb-141">In SmarterU, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c8abb-142">tooconfigure e teste de logon único do AD do Azure com SmarterU, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8abb-142">tooconfigure and test Azure AD single sign-on with SmarterU, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c8abb-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c8abb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c8abb-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8abb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8abb-145">**[Criar um usuário de teste do SmarterU](#creating-a-smarteru-test-user)**  -toohave um equivalente do Britta Simon no SmarterU é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c8abb-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - toohave a counterpart of Britta Simon in SmarterU that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c8abb-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c8abb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8abb-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c8abb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c8abb-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8abb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c8abb-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo SmarterU.</span><span class="sxs-lookup"><span data-stu-id="c8abb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="c8abb-150">**tooconfigure AD do Azure-logon único com o SmarterU, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8abb-150">**tooconfigure Azure AD single sign-on with SmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8abb-151">Em Olá portal do Azure, Olá **SmarterU** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-151">In hello Azure portal, on hello **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c8abb-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c8abb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="c8abb-155">Em Olá **SmarterU domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8abb-155">On hello **SmarterU Domain and URLs** section, perform hello following steps:</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="c8abb-157">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="c8abb-157">In hello **Identifier** textbox, type hello URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="c8abb-158">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c8abb-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="c8abb-160">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c8abb-160">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c8abb-162">Em uma janela de navegador web diferente, faça logon no site da empresa SmarterU tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c8abb-162">In a different web browser window, log in tooyour SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="c8abb-163">Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações de conta**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-163">In hello toolbar on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="c8abb-164">![Configurações de Conta](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Configurações de Conta")</span><span class="sxs-lookup"><span data-stu-id="c8abb-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="c8abb-165">Na página de configuração de conta hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8abb-165">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="c8abb-166">![Autorização Externa](./media/active-directory-saas-smarteru-tutorial/IC777327.png "Autorização Externa")</span><span class="sxs-lookup"><span data-stu-id="c8abb-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="c8abb-167">a.</span><span class="sxs-lookup"><span data-stu-id="c8abb-167">a.</span></span> <span data-ttu-id="c8abb-168">Selecione **Habilitar Autorização Externa**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="c8abb-169">b.</span><span class="sxs-lookup"><span data-stu-id="c8abb-169">b.</span></span> <span data-ttu-id="c8abb-170">Em Olá **controle de logon mestre** seção, selecione Olá **SmarterU** guia.</span><span class="sxs-lookup"><span data-stu-id="c8abb-170">In hello **Master Login Control** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="c8abb-171">c.</span><span class="sxs-lookup"><span data-stu-id="c8abb-171">c.</span></span> <span data-ttu-id="c8abb-172">Em Olá **logon padrão do usuário** seção, selecione Olá **SmarterU** guia.</span><span class="sxs-lookup"><span data-stu-id="c8abb-172">In hello **User Default Login** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="c8abb-173">d.</span><span class="sxs-lookup"><span data-stu-id="c8abb-173">d.</span></span> <span data-ttu-id="c8abb-174">Selecione **Habilitar Okta**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="c8abb-175">e.</span><span class="sxs-lookup"><span data-stu-id="c8abb-175">e.</span></span> <span data-ttu-id="c8abb-176">Copiar o conteúdo de saudação do arquivo de metadados baixado hello e, em seguida, cole-Olá **Okta Metadata** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="c8abb-176">Copy hello content of hello downloaded metadata file, and then paste it into hello **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="c8abb-177">f.</span><span class="sxs-lookup"><span data-stu-id="c8abb-177">f.</span></span> <span data-ttu-id="c8abb-178">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c8abb-179">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c8abb-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c8abb-180">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c8abb-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c8abb-181">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c8abb-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c8abb-182">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8abb-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="c8abb-183">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8abb-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c8abb-185">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8abb-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8abb-186">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c8abb-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c8abb-188">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c8abb-190">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8abb-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c8abb-192">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8abb-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c8abb-194">a.</span><span class="sxs-lookup"><span data-stu-id="c8abb-194">a.</span></span> <span data-ttu-id="c8abb-195">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8abb-196">b.</span><span class="sxs-lookup"><span data-stu-id="c8abb-196">b.</span></span> <span data-ttu-id="c8abb-197">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c8abb-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c8abb-198">c.</span><span class="sxs-lookup"><span data-stu-id="c8abb-198">c.</span></span> <span data-ttu-id="c8abb-199">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c8abb-200">d.</span><span class="sxs-lookup"><span data-stu-id="c8abb-200">d.</span></span> <span data-ttu-id="c8abb-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="c8abb-202">Criar um usuário de teste do SmarterU</span><span class="sxs-lookup"><span data-stu-id="c8abb-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="c8abb-203">tooenable AD do Azure usuários toolog em tooSmarterU, eles devem ser provisionados no SmarterU.</span><span class="sxs-lookup"><span data-stu-id="c8abb-203">tooenable Azure AD users toolog in tooSmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="c8abb-204">No caso do SmarterU, o provisionamento será uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="c8abb-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="c8abb-205">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8abb-205">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8abb-206">Faça logon no tooyour **SmarterU** locatário.</span><span class="sxs-lookup"><span data-stu-id="c8abb-206">Log in tooyour **SmarterU** tenant.</span></span>

2. <span data-ttu-id="c8abb-207">Vá muito**usuários**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-207">Go too**Users**.</span></span>

3. <span data-ttu-id="c8abb-208">Na seção de usuário hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8abb-208">In hello user section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c8abb-209">![Novo Usuário](./media/active-directory-saas-smarteru-tutorial/IC777329.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="c8abb-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="c8abb-210">a.</span><span class="sxs-lookup"><span data-stu-id="c8abb-210">a.</span></span> <span data-ttu-id="c8abb-211">Clique em **+Usuário**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-211">Click **+User**.</span></span>
    
    <span data-ttu-id="c8abb-212">b.</span><span class="sxs-lookup"><span data-stu-id="c8abb-212">b.</span></span> <span data-ttu-id="c8abb-213">Saudação de tipo relacionados a valores de atributo de conta de usuário de saudação do AD do Azure em Olá caixas de texto a seguir: **Email primário**, **ID de funcionário**, **senha**,  **Verificar senha**, **nome**, **Sobrenome**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-213">Type hello related attribute values of hello Azure AD user account into hello following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="c8abb-214">c.</span><span class="sxs-lookup"><span data-stu-id="c8abb-214">c.</span></span> <span data-ttu-id="c8abb-215">Clique em **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="c8abb-216">d.</span><span class="sxs-lookup"><span data-stu-id="c8abb-216">d.</span></span> <span data-ttu-id="c8abb-217">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="c8abb-218">Você pode usar qualquer ferramenta de criação outros SmarterU usuário conta ou APIs fornecidas pelo SmarterU tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="c8abb-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c8abb-219">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8abb-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c8abb-220">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSmarterU.</span><span class="sxs-lookup"><span data-stu-id="c8abb-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmarterU.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c8abb-222">**tooassign Britta Simon tooSmarterU, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8abb-222">**tooassign Britta Simon tooSmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8abb-223">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c8abb-225">Na lista de aplicativos hello, selecione **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-225">In hello applications list, select **SmarterU**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="c8abb-227">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c8abb-229">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c8abb-229">Click **Add** button.</span></span> <span data-ttu-id="c8abb-230">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8abb-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c8abb-232">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8abb-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c8abb-233">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8abb-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c8abb-234">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8abb-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c8abb-235">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c8abb-235">Testing single sign-on</span></span>

<span data-ttu-id="c8abb-236">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8abb-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="c8abb-237">Quando você clica em bloco SmarterU Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour SmarterU aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c8abb-237">When you click hello SmarterU tile in hello Access Panel, you should get automatically signed-on tooyour SmarterU application.</span></span>
<span data-ttu-id="c8abb-238">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8abb-238">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="c8abb-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c8abb-239">Additional resources</span></span>

* [<span data-ttu-id="c8abb-240">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c8abb-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8abb-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c8abb-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

