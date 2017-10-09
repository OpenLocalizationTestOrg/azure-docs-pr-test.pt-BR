---
title: "Tutorial: Integração do Azure Active Directory com o Wikispaces | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Wikispaces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: eb5b72e60b415cb657b70ba530df731ae14b0425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="1b9ea-103">Tutorial: Integração do Active Directory do Azure com o Wikispaces</span><span class="sxs-lookup"><span data-stu-id="1b9ea-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="1b9ea-104">Neste tutorial, você aprenderá como toointegrate Wikispaces com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="1b9ea-104">In this tutorial, you learn how toointegrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b9ea-105">Integrando o Wikispaces com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b9ea-105">Integrating Wikispaces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1b9ea-106">Você pode controlar no AD do Azure que tenha acesso tooWikispaces</span><span class="sxs-lookup"><span data-stu-id="1b9ea-106">You can control in Azure AD who has access tooWikispaces</span></span>
- <span data-ttu-id="1b9ea-107">Você pode habilitar seus usuários tooautomatically get conectado tooWikispaces (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b9ea-107">You can enable your users tooautomatically get signed-on tooWikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1b9ea-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1b9ea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1b9ea-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1b9ea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b9ea-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1b9ea-110">Prerequisites</span></span>

<span data-ttu-id="1b9ea-111">tooconfigure integração do AD do Azure com o Wikispaces, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b9ea-111">tooconfigure Azure AD integration with Wikispaces, you need hello following items:</span></span>

- <span data-ttu-id="1b9ea-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b9ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b9ea-113">Uma assinatura do Wikispaces habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="1b9ea-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b9ea-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b9ea-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1b9ea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b9ea-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b9ea-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b9ea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b9ea-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1b9ea-118">Scenario description</span></span>
<span data-ttu-id="1b9ea-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b9ea-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="1b9ea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b9ea-121">Adicionando Wikispaces da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1b9ea-121">Adding Wikispaces from hello gallery</span></span>
2. <span data-ttu-id="1b9ea-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b9ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-hello-gallery"></a><span data-ttu-id="1b9ea-123">Adicionando Wikispaces da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1b9ea-123">Adding Wikispaces from hello gallery</span></span>
<span data-ttu-id="1b9ea-124">integração de saudação tooconfigure do Wikispaces no AD do Azure, você precisa tooadd Wikispaces da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-124">tooconfigure hello integration of Wikispaces into Azure AD, you need tooadd Wikispaces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1b9ea-125">**tooadd Wikispaces da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1b9ea-125">**tooadd Wikispaces from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b9ea-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1b9ea-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1b9ea-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1b9ea-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1b9ea-133">Na caixa de pesquisa hello, digite **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-133">In hello search box, type **Wikispaces**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="1b9ea-135">No painel de resultados de saudação, selecione **Wikispaces**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-135">In hello results panel, select **Wikispaces**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1b9ea-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b9ea-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1b9ea-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Wikispaces com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b9ea-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Wikispaces é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wikispaces is tooa user in Azure AD.</span></span> <span data-ttu-id="1b9ea-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Wikispaces precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-140">In other words, a link relationship between an Azure AD user and hello related user in Wikispaces needs toobe established.</span></span>

<span data-ttu-id="1b9ea-141">No Wikispaces, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-141">In Wikispaces, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1b9ea-142">tooconfigure e teste de logon único do AD do Azure com o Wikispaces, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b9ea-142">tooconfigure and test Azure AD single sign-on with Wikispaces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1b9ea-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1b9ea-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b9ea-145">**[Criar um usuário de teste do Wikispaces](#creating-a-wikispaces-test-user)**  -toohave um equivalente do Britta Simon no Wikispaces é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - toohave a counterpart of Britta Simon in Wikispaces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1b9ea-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b9ea-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1b9ea-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b9ea-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1b9ea-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="1b9ea-150">**tooconfigure AD do Azure-logon único com o Wikispaces, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1b9ea-150">**tooconfigure Azure AD single sign-on with Wikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b9ea-151">Em Olá portal do Azure, Olá **Wikispaces** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-151">In hello Azure portal, on hello **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1b9ea-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="1b9ea-155">Em Olá **Wikispaces domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b9ea-155">On hello **Wikispaces Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="1b9ea-157">a.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-157">a.</span></span> <span data-ttu-id="1b9ea-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="1b9ea-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="1b9ea-159">b.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-159">b.</span></span> <span data-ttu-id="1b9ea-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1b9ea-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1b9ea-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-161">These values are not real.</span></span> <span data-ttu-id="1b9ea-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1b9ea-163">Entre em contato com [equipe de suporte do Wikispaces cliente](https://www.wikispaces.com/site/help) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) tooget these values.</span></span> 

4. <span data-ttu-id="1b9ea-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="1b9ea-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1b9ea-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1b9ea-168">tooconfigure logon único no **Wikispaces** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do Wikispaces](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="1b9ea-168">tooconfigure single sign-on on **Wikispaces** side, you need toosend hello downloaded **Metadata XML** too[Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="1b9ea-169">Você receberá uma notificação assim Olá configuração foi concluída.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-169">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="1b9ea-170">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="1b9ea-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1b9ea-171">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1b9ea-172">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1b9ea-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1b9ea-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b9ea-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="1b9ea-174">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1b9ea-176">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1b9ea-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b9ea-177">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1b9ea-179">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1b9ea-181">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1b9ea-183">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b9ea-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1b9ea-185">a.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-185">a.</span></span> <span data-ttu-id="1b9ea-186">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b9ea-187">b.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-187">b.</span></span> <span data-ttu-id="1b9ea-188">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1b9ea-189">c.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-189">c.</span></span> <span data-ttu-id="1b9ea-190">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1b9ea-191">d.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-191">d.</span></span> <span data-ttu-id="1b9ea-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="1b9ea-193">Criação de um usuário de teste do Wikispaces</span><span class="sxs-lookup"><span data-stu-id="1b9ea-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="1b9ea-194">Ordem tooenable AD do Azure usuários toolog em tooWikispaces, eles devem ser provisionados no Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-194">In order tooenable Azure AD users toolog in tooWikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="1b9ea-195">No caso de saudação do Wikispaces, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-195">In hello case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="1b9ea-196">tooprovision contas de usuário, executar Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1b9ea-196">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="1b9ea-197">Faça logon no tooyour **Wikispaces** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-197">Log in tooyour **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="1b9ea-198">Vá muito**membros**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-198">Go too**Members**.</span></span>
   
    <span data-ttu-id="1b9ea-199">![Membros](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Membros")</span><span class="sxs-lookup"><span data-stu-id="1b9ea-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="1b9ea-200">Clique em Olá **convidar pessoas**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-200">Click hello **Invite People**.</span></span>
   
    <span data-ttu-id="1b9ea-201">![Convidar Pessoas](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="1b9ea-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="1b9ea-202">Em Olá **convidar pessoas** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b9ea-202">In hello **Invite People** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1b9ea-203">![Convidar Pessoas](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="1b9ea-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="1b9ea-204">a.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-204">a.</span></span> <span data-ttu-id="1b9ea-205">Saudação de tipo **nomes de usuário ou endereço de Email** de uma conta válida do AAD você deseja tooprovision em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-205">Type hello **Usernames or Email Address** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="1b9ea-206">b.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-206">b.</span></span> <span data-ttu-id="1b9ea-207">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="1b9ea-208">proprietário de conta do Active Directory do Azure Olá recebe um email com uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-208">hello Azure Active Directory account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="1b9ea-209">Você pode usar qualquer ferramenta de criação outros Wikispaces usuário conta ou APIs fornecidas pelo Wikispaces tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1b9ea-210">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b9ea-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1b9ea-211">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWikispaces.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWikispaces.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1b9ea-213">**tooassign Britta Simon tooWikispaces, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1b9ea-213">**tooassign Britta Simon tooWikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b9ea-214">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1b9ea-216">Na lista de aplicativos hello, selecione **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-216">In hello applications list, select **Wikispaces**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="1b9ea-218">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1b9ea-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-220">Click **Add** button.</span></span> <span data-ttu-id="1b9ea-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1b9ea-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1b9ea-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b9ea-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1b9ea-226">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1b9ea-226">Testing single sign-on</span></span>

<span data-ttu-id="1b9ea-227">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1b9ea-228">Quando você clica em Olá Wikispaces bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo do Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="1b9ea-228">When you click hello Wikispaces tile in hello Access Panel, you should get automatically signed-on tooyour Wikispaces application.</span></span>
<span data-ttu-id="1b9ea-229">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1b9ea-229">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b9ea-230">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1b9ea-230">Additional resources</span></span>

* [<span data-ttu-id="1b9ea-231">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1b9ea-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b9ea-232">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b9ea-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

