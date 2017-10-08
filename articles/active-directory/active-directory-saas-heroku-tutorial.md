---
title: "Tutorial: Integração do Azure Active Directory com o Heroku | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Heroku."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee11db647fd385140f1dbcab2586dfafffe5d912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="8c5b1-103">Tutorial: Integração do Azure Active Directory ao Heroku</span><span class="sxs-lookup"><span data-stu-id="8c5b1-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="8c5b1-104">Neste tutorial, você aprenderá como toointegrate Heroku com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="8c5b1-104">In this tutorial, you learn how toointegrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c5b1-105">Integrando Heroku com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c5b1-105">Integrating Heroku with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8c5b1-106">Você pode controlar no AD do Azure que tenha acesso tooHeroku</span><span class="sxs-lookup"><span data-stu-id="8c5b1-106">You can control in Azure AD who has access tooHeroku</span></span>
- <span data-ttu-id="8c5b1-107">Você pode habilitar seu usuários tooautomatically get conectado tooHeroku (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8c5b1-107">You can enable your users tooautomatically get signed-on tooHeroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8c5b1-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8c5b1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8c5b1-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c5b1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c5b1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8c5b1-110">Prerequisites</span></span>

<span data-ttu-id="8c5b1-111">tooconfigure integração do AD do Azure com Heroku, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c5b1-111">tooconfigure Azure AD integration with Heroku, you need hello following items:</span></span>

- <span data-ttu-id="8c5b1-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8c5b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c5b1-113">Uma assinatura habilitada para logon único do Heroku</span><span class="sxs-lookup"><span data-stu-id="8c5b1-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8c5b1-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8c5b1-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8c5b1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8c5b1-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8c5b1-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c5b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8c5b1-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8c5b1-118">Scenario description</span></span>
<span data-ttu-id="8c5b1-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8c5b1-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="8c5b1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c5b1-121">Adicionando Heroku da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8c5b1-121">Adding Heroku from hello gallery</span></span>
2. <span data-ttu-id="8c5b1-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8c5b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-hello-gallery"></a><span data-ttu-id="8c5b1-123">Adicionando Heroku da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8c5b1-123">Adding Heroku from hello gallery</span></span>
<span data-ttu-id="8c5b1-124">integração de saudação tooconfigure de Heroku no AD do Azure, você precisa tooadd Heroku da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-124">tooconfigure hello integration of Heroku into Azure AD, you need tooadd Heroku from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8c5b1-125">**tooadd Heroku da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8c5b1-125">**tooadd Heroku from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c5b1-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8c5b1-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8c5b1-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8c5b1-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8c5b1-133">Na caixa de pesquisa hello, digite **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-133">In hello search box, type **Heroku**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="8c5b1-135">No painel de resultados de saudação, selecione **Heroku**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-135">In hello results panel, select **Heroku**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8c5b1-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8c5b1-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="8c5b1-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Heroku, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8c5b1-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Heroku é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Heroku is tooa user in Azure AD.</span></span> <span data-ttu-id="8c5b1-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Heroku precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-140">In other words, a link relationship between an Azure AD user and hello related user in Heroku needs toobe established.</span></span>

<span data-ttu-id="8c5b1-141">Heroku, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-141">In Heroku, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8c5b1-142">tooconfigure e teste de logon único do AD do Azure com Heroku, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c5b1-142">tooconfigure and test Azure AD single sign-on with Heroku, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8c5b1-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8c5b1-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8c5b1-145">**[Criar um usuário de teste Heroku](#creating-a-heroku-test-user)**  -toohave um equivalente do Britta Simon em Heroku é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - toohave a counterpart of Britta Simon in Heroku that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8c5b1-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8c5b1-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8c5b1-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c5b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8c5b1-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Heroku.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="8c5b1-150">**tooconfigure AD do Azure-logon único com Heroku, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8c5b1-150">**tooconfigure Azure AD single sign-on with Heroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c5b1-151">Em Olá portal do Azure, Olá **Heroku** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-151">In hello Azure portal, on hello **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8c5b1-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="8c5b1-155">Em Olá **Heroku domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c5b1-155">On hello **Heroku Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="8c5b1-157">a.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-157">a.</span></span> <span data-ttu-id="8c5b1-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c5b1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="8c5b1-159">b.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-159">b.</span></span> <span data-ttu-id="8c5b1-160">Em Olá **URL de identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c5b1-160">In hello **Identifier URL** textbox, type a URL using hello following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="8c5b1-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-161">These values are not real.</span></span> <span data-ttu-id="8c5b1-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8c5b1-163">Você obtém esses valores da equipe do Heroku, o que é descrito nas próximas seções deste artigo.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="8c5b1-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="8c5b1-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8c5b1-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8c5b1-168">tooenable SSO no Heroku, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c5b1-168">tooenable SSO in Heroku, perform hello following steps:</span></span>
   
    <span data-ttu-id="8c5b1-169">a.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-169">a.</span></span> <span data-ttu-id="8c5b1-170">Faça logon no toohello Heroku conta como um administrador.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-170">Log in toohello Heroku account as an administrator.</span></span>

    <span data-ttu-id="8c5b1-171">b.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-171">b.</span></span> <span data-ttu-id="8c5b1-172">Clique em Olá **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-172">Click hello **Settings** tab.</span></span>

    <span data-ttu-id="8c5b1-173">c.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-173">c.</span></span> <span data-ttu-id="8c5b1-174">Em Olá **logon único na página**, clique em **carregar metadados**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-174">On hello **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="8c5b1-175">d.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-175">d.</span></span> <span data-ttu-id="8c5b1-176">Carregar arquivo de metadados de saudação, que você baixou do portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-176">Upload hello metadata file, which you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="8c5b1-177">e.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-177">e.</span></span> <span data-ttu-id="8c5b1-178">Quando a instalação de saudação for bem-sucedida, os administradores veem uma caixa de diálogo de confirmação e URL de saudação do hello logon de SSO para os usuários finais é exibida.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-178">When hello setup is successful, administrators see a confirmation dialog and hello URL of hello SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="8c5b1-179">f.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-179">f.</span></span> <span data-ttu-id="8c5b1-180">Saudação de cópia **URL de logon Heroku** e **Heroku ID da entidade** valores e vá para fazer muito**Heroku domínio e URLs** seção no portal do Azure e cole esses valores hello **Url de logon** e **identificador** caixas de texto respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-180">Copy hello **Heroku Login URL** and **Heroku Entity ID** values and go back too**Heroku Domain and URLs** section in Azure portal and paste these values into hello **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="8c5b1-182">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="8c5b1-183">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="8c5b1-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8c5b1-184">Depois de adicionar a este aplicativo de saudação **Active Directory corporativo Applications** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-184">After adding this app from hello **Active Directory Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8c5b1-185">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8c5b1-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8c5b1-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8c5b1-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="8c5b1-187">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8c5b1-189">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8c5b1-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c5b1-190">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8c5b1-192">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8c5b1-194">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8c5b1-196">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c5b1-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8c5b1-198">a.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-198">a.</span></span> <span data-ttu-id="8c5b1-199">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c5b1-200">b.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-200">b.</span></span> <span data-ttu-id="8c5b1-201">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8c5b1-202">c.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-202">c.</span></span> <span data-ttu-id="8c5b1-203">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8c5b1-204">d.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-204">d.</span></span> <span data-ttu-id="8c5b1-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="8c5b1-206">Criação de um usuário de teste do Heroku</span><span class="sxs-lookup"><span data-stu-id="8c5b1-206">Creating a Heroku test user</span></span>

<span data-ttu-id="8c5b1-207">Nesta seção, você criará um usuário chamado Brenda Fernandes no Heroku.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="8c5b1-208">O Heroku dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="8c5b1-209">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-209">There is no action item for you in this section.</span></span> <span data-ttu-id="8c5b1-210">Um novo usuário é criado ao acessar Heroku se o usuário Olá ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-210">A new user is created when accessing Heroku if hello user doesn't exist yet.</span></span> <span data-ttu-id="8c5b1-211">Depois de saudação conta é provisionada, Olá final usuário recebe um email de verificação e precisa de link de confirmação de saudação tooclick.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-211">After hello account is provisioned, hello end user receives a verification email and needs tooclick hello acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="8c5b1-212">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [equipe de suporte do cliente Heroku](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="8c5b1-212">If you need toocreate a user manually, you need toocontact hello [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8c5b1-213">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8c5b1-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8c5b1-214">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHeroku.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHeroku.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8c5b1-216">**tooassign Britta Simon tooHeroku, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8c5b1-216">**tooassign Britta Simon tooHeroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c5b1-217">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8c5b1-219">Na lista de aplicativos hello, selecione **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-219">In hello applications list, select **Heroku**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="8c5b1-221">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8c5b1-223">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-223">Click **Add** button.</span></span> <span data-ttu-id="8c5b1-224">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8c5b1-226">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8c5b1-227">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8c5b1-228">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8c5b1-229">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8c5b1-229">Testing single sign-on</span></span>

<span data-ttu-id="8c5b1-230">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8c5b1-231">Quando você clica em bloco Heroku Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Heroku aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8c5b1-231">When you click hello Heroku tile in hello Access Panel, you should get automatically signed-on tooyour Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8c5b1-232">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8c5b1-232">Additional resources</span></span>

* [<span data-ttu-id="8c5b1-233">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8c5b1-233">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c5b1-234">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8c5b1-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
