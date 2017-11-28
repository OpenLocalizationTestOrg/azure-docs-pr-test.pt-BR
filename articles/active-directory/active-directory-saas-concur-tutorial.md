---
title: "Tutorial: integração do Azure Active Directory ao Concur | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1012bf8c6f036306d0ca90689415d5e22e449989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="87020-103">Tutorial: integração do Active Directory do Azure ao Concur</span><span class="sxs-lookup"><span data-stu-id="87020-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="87020-104">Neste tutorial, você aprenderá como toointegrate de acordo com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="87020-104">In this tutorial, you learn how toointegrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87020-105">Integrando o Concur com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="87020-105">Integrating Concur with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="87020-106">Você pode controlar no AD do Azure que tenha acesso tooConcur</span><span class="sxs-lookup"><span data-stu-id="87020-106">You can control in Azure AD who has access tooConcur</span></span>
- <span data-ttu-id="87020-107">Você pode habilitar seu usuários tooautomatically get conectado tooConcur (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87020-107">You can enable your users tooautomatically get signed-on tooConcur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="87020-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="87020-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="87020-109">Se você quiser tooknow para obter mais informações sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="87020-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87020-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="87020-110">Prerequisites</span></span>

<span data-ttu-id="87020-111">tooconfigure integração do AD do Azure com o Concur, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="87020-111">tooconfigure Azure AD integration with Concur, you need hello following items:</span></span>

- <span data-ttu-id="87020-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87020-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87020-113">Uma assinatura habilitada para logon único do Concur</span><span class="sxs-lookup"><span data-stu-id="87020-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87020-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="87020-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87020-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="87020-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87020-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="87020-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87020-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87020-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87020-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="87020-118">Scenario description</span></span>
<span data-ttu-id="87020-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="87020-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87020-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="87020-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87020-121">Adicionando Concur da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="87020-121">Adding Concur from hello gallery</span></span>
2. <span data-ttu-id="87020-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87020-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="87020-123">configuração de saudação da sua assinatura Concur para SSO federado por meio de SAML é uma tarefa separada, você deverá contatar [equipe de suporte de cliente concorrente](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="87020-123">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 

## <a name="adding-concur-from-hello-gallery"></a><span data-ttu-id="87020-124">Adicionando Concur da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="87020-124">Adding Concur from hello gallery</span></span>
<span data-ttu-id="87020-125">integração de saudação tooconfigure do Concur no AD do Azure, você precisa tooadd Concur da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="87020-125">tooconfigure hello integration of Concur into Azure AD, you need tooadd Concur from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="87020-126">**tooadd Concur da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="87020-126">**tooadd Concur from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="87020-127">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="87020-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="87020-129">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="87020-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="87020-130">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="87020-130">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="87020-132">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="87020-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="87020-134">Na caixa de pesquisa hello, digite **Concur**.</span><span class="sxs-lookup"><span data-stu-id="87020-134">In hello search box, type **Concur**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="87020-136">No painel de resultados de saudação, selecione **Concur**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="87020-136">In hello results panel, select **Concur**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="87020-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87020-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="87020-139">Nesta seção, você configurará e testará o logon único do Azure AD com o Concur, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="87020-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="87020-140">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Concur é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="87020-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Concur is tooa user in Azure AD.</span></span> <span data-ttu-id="87020-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Concur precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="87020-141">In other words, a link relationship between an Azure AD user and hello related user in Concur needs toobe established.</span></span>

<span data-ttu-id="87020-142">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Concur.</span><span class="sxs-lookup"><span data-stu-id="87020-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Concur.</span></span>

<span data-ttu-id="87020-143">tooconfigure e teste de logon único do AD do Azure com o Concur, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="87020-143">tooconfigure and test Azure AD single sign-on with Concur, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="87020-144">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="87020-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="87020-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87020-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87020-146">**[Criar um usuário de teste do Concur](#creating-a-concur-test-user)**  -toohave um equivalente do Britta Simon no Concur que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="87020-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - toohave a counterpart of Britta Simon in Concur that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="87020-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="87020-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87020-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="87020-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="87020-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="87020-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="87020-150">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Concur.</span><span class="sxs-lookup"><span data-stu-id="87020-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="87020-151">**tooconfigure AD do Azure-logon único com o Concur, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="87020-151">**tooconfigure Azure AD single sign-on with Concur, perform hello following steps:**</span></span>

1. <span data-ttu-id="87020-152">Em Olá portal do Azure, Olá **Concur** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="87020-152">In hello Azure portal, on hello **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="87020-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="87020-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="87020-156">Em Olá **domínio concorrente e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="87020-156">On hello **Concur Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="87020-158">a.</span><span class="sxs-lookup"><span data-stu-id="87020-158">a.</span></span> <span data-ttu-id="87020-159">Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="87020-159">In hello **Sign on URL** textbox, type hello value using hello following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="87020-160">b.</span><span class="sxs-lookup"><span data-stu-id="87020-160">b.</span></span> <span data-ttu-id="87020-161">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="87020-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="87020-162">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="87020-162">These values are not hello real.</span></span> <span data-ttu-id="87020-163">Entrassem esses valores com hello real na URL e o identificador de atualização.</span><span class="sxs-lookup"><span data-stu-id="87020-163">Update these values with hello actual Sign on URL and Identifier.</span></span> <span data-ttu-id="87020-164">Entre em contato com [equipe de suporte de cliente concorrente](https://www.concur.co.in/contact) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="87020-164">Contact [Concur Client support team](https://www.concur.co.in/contact) tooget these values.</span></span> 

4. <span data-ttu-id="87020-165">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="87020-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="87020-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="87020-167">Click **Save** button.</span></span>

    <span data-ttu-id="87020-168">![Configurar Logon Único](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="87020-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="87020-169">tooconfigure logon único no **Concur** lado, você precisa toosend Olá baixado **Metadata XML** tooConcur suporte.</span><span class="sxs-lookup"><span data-stu-id="87020-169">tooconfigure single sign-on on **Concur** side, you need toosend hello downloaded **Metadata XML** tooConcur support.</span></span> <span data-ttu-id="87020-170">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="87020-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="87020-171">configuração de saudação da sua assinatura Concur para SSO federado por meio de SAML é uma tarefa separada, você deverá contatar [equipe de suporte de cliente concorrente](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="87020-171">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="87020-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="87020-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="87020-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="87020-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="87020-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="87020-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="87020-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87020-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="87020-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="87020-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="87020-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="87020-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="87020-179">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="87020-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="87020-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="87020-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="87020-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="87020-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="87020-185">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="87020-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="87020-187">a.</span><span class="sxs-lookup"><span data-stu-id="87020-187">a.</span></span> <span data-ttu-id="87020-188">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87020-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87020-189">b.</span><span class="sxs-lookup"><span data-stu-id="87020-189">b.</span></span> <span data-ttu-id="87020-190">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="87020-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="87020-191">c.</span><span class="sxs-lookup"><span data-stu-id="87020-191">c.</span></span> <span data-ttu-id="87020-192">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="87020-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="87020-193">d.</span><span class="sxs-lookup"><span data-stu-id="87020-193">d.</span></span> <span data-ttu-id="87020-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="87020-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="87020-195">Criação de um usuário de teste do Concur</span><span class="sxs-lookup"><span data-stu-id="87020-195">Creating a Concur test user</span></span>

<span data-ttu-id="87020-196">Aplicativo dá suporte a saudação apenas durante o provisionamento do usuário e depois que os usuários de autenticação são criados automaticamente no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="87020-196">Application supports hello Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="87020-197">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87020-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="87020-198">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooConcur.</span><span class="sxs-lookup"><span data-stu-id="87020-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConcur.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="87020-200">**tooassign Britta Simon tooConcur, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="87020-200">**tooassign Britta Simon tooConcur, perform hello following steps:**</span></span>

1. <span data-ttu-id="87020-201">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="87020-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="87020-203">Na lista de aplicativos hello, selecione **Concur**.</span><span class="sxs-lookup"><span data-stu-id="87020-203">In hello applications list, select **Concur**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="87020-205">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="87020-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="87020-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="87020-207">Click **Add** button.</span></span> <span data-ttu-id="87020-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="87020-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="87020-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="87020-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="87020-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="87020-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="87020-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="87020-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="87020-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="87020-213">Testing single sign-on</span></span>

<span data-ttu-id="87020-214">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="87020-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="87020-215">Quando você clica em bloco Concur Olá Olá painel de acesso, você deve obter a página de logon do aplicativo do Concur.</span><span class="sxs-lookup"><span data-stu-id="87020-215">When you click hello Concur tile in hello Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="87020-216">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="87020-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="87020-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="87020-217">Additional resources</span></span>

* [<span data-ttu-id="87020-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="87020-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87020-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87020-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="87020-220">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="87020-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

