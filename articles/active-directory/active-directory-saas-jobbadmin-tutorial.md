---
title: "Tutorial: Integração do Azure Active Directory ao Jobbadmin | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Jobbadmin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c5208b0d-66a3-49ed-9aad-70d21f54aee0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0796abd2934c0f94648b2c11e7fdf69304f835c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobbadmin"></a><span data-ttu-id="95b86-103">Tutorial: Integração do Azure Active Directory com o Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="95b86-103">Tutorial: Azure Active Directory integration with Jobbadmin</span></span>

<span data-ttu-id="95b86-104">Neste tutorial, você aprenderá como toointegrate Jobbadmin com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="95b86-104">In this tutorial, you learn how toointegrate Jobbadmin with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95b86-105">Integrando Jobbadmin com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="95b86-105">Integrating Jobbadmin with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="95b86-106">Você pode controlar no AD do Azure que tenha acesso tooJobbadmin</span><span class="sxs-lookup"><span data-stu-id="95b86-106">You can control in Azure AD who has access tooJobbadmin</span></span>
- <span data-ttu-id="95b86-107">Você pode habilitar seu usuários tooautomatically get conectado tooJobbadmin (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95b86-107">You can enable your users tooautomatically get signed-on tooJobbadmin (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="95b86-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="95b86-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="95b86-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="95b86-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95b86-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="95b86-110">Prerequisites</span></span>

<span data-ttu-id="95b86-111">tooconfigure integração do AD do Azure com Jobbadmin, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="95b86-111">tooconfigure Azure AD integration with Jobbadmin, you need hello following items:</span></span>

- <span data-ttu-id="95b86-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95b86-112">An Azure AD subscription</span></span>
- <span data-ttu-id="95b86-113">Uma assinatura do Jobbadmin com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="95b86-113">A Jobbadmin single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="95b86-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="95b86-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="95b86-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="95b86-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="95b86-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="95b86-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="95b86-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95b86-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95b86-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="95b86-118">Scenario description</span></span>
<span data-ttu-id="95b86-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="95b86-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95b86-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="95b86-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95b86-121">Adicionando Jobbadmin da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="95b86-121">Adding Jobbadmin from hello gallery</span></span>
2. <span data-ttu-id="95b86-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95b86-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobbadmin-from-hello-gallery"></a><span data-ttu-id="95b86-123">Adicionando Jobbadmin da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="95b86-123">Adding Jobbadmin from hello gallery</span></span>
<span data-ttu-id="95b86-124">integração de saudação tooconfigure de Jobbadmin no AD do Azure, você precisa tooadd Jobbadmin da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="95b86-124">tooconfigure hello integration of Jobbadmin into Azure AD, you need tooadd Jobbadmin from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="95b86-125">**tooadd Jobbadmin da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95b86-125">**tooadd Jobbadmin from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="95b86-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="95b86-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="95b86-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="95b86-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="95b86-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="95b86-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="95b86-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95b86-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="95b86-133">Na caixa de pesquisa hello, digite **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="95b86-133">In hello search box, type **Jobbadmin**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_search.png)

5. <span data-ttu-id="95b86-135">No painel de resultados de saudação, selecione **Jobbadmin**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="95b86-135">In hello results panel, select **Jobbadmin**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="95b86-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95b86-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="95b86-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Jobbadmin com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="95b86-138">In this section, you configure and test Azure AD single sign-on with Jobbadmin based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="95b86-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Jobbadmin é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="95b86-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobbadmin is tooa user in Azure AD.</span></span> <span data-ttu-id="95b86-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Jobbadmin precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="95b86-140">In other words, a link relationship between an Azure AD user and hello related user in Jobbadmin needs toobe established.</span></span>

<span data-ttu-id="95b86-141">Jobbadmin, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b86-141">In Jobbadmin, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="95b86-142">tooconfigure e teste de logon único do AD do Azure com Jobbadmin, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="95b86-142">tooconfigure and test Azure AD single sign-on with Jobbadmin, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="95b86-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="95b86-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="95b86-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95b86-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="95b86-145">**[Criar um usuário de teste Jobbadmin](#creating-a-jobbadmin-test-user)**  -toohave um equivalente do Britta Simon em Jobbadmin é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="95b86-145">**[Creating a Jobbadmin test user](#creating-a-jobbadmin-test-user)** - toohave a counterpart of Britta Simon in Jobbadmin that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="95b86-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="95b86-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="95b86-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="95b86-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="95b86-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="95b86-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="95b86-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="95b86-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobbadmin application.</span></span>

<span data-ttu-id="95b86-150">**tooconfigure AD do Azure-logon único com Jobbadmin, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95b86-150">**tooconfigure Azure AD single sign-on with Jobbadmin, perform hello following steps:**</span></span>

1. <span data-ttu-id="95b86-151">Em Olá portal do Azure, Olá **Jobbadmin** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="95b86-151">In hello Azure portal, on hello **Jobbadmin** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="95b86-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="95b86-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_samlbase.png)

3. <span data-ttu-id="95b86-155">Em Olá **Jobbadmin domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95b86-155">On hello **Jobbadmin Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_url.png)

    <span data-ttu-id="95b86-157">a.</span><span class="sxs-lookup"><span data-stu-id="95b86-157">a.</span></span> <span data-ttu-id="95b86-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span><span class="sxs-lookup"><span data-stu-id="95b86-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    <span data-ttu-id="95b86-159">b.</span><span class="sxs-lookup"><span data-stu-id="95b86-159">b.</span></span> <span data-ttu-id="95b86-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.jobnorge.no`</span><span class="sxs-lookup"><span data-stu-id="95b86-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.jobnorge.no`</span></span>

    <span data-ttu-id="95b86-161">c.</span><span class="sxs-lookup"><span data-stu-id="95b86-161">c.</span></span> <span data-ttu-id="95b86-162">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span><span class="sxs-lookup"><span data-stu-id="95b86-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="95b86-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="95b86-163">These values are not real.</span></span> <span data-ttu-id="95b86-164">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="95b86-164">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="95b86-165">Entre em contato com [equipe de suporte do cliente Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="95b86-165">Contact [Jobbadmin Client support team](https://www.jobbnorge.no/om-oss/kontakt-oss) tooget these values.</span></span> 
 


4. <span data-ttu-id="95b86-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="95b86-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_certificate.png) 

5. <span data-ttu-id="95b86-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="95b86-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="95b86-170">tooconfigure logon único no **Jobbadmin** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss).</span><span class="sxs-lookup"><span data-stu-id="95b86-170">tooconfigure single sign-on on **Jobbadmin** side, you need toosend hello downloaded **Metadata XML** too[Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss).</span></span> <span data-ttu-id="95b86-171">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="95b86-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="95b86-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="95b86-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="95b86-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="95b86-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="95b86-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="95b86-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="95b86-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95b86-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="95b86-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="95b86-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="95b86-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95b86-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="95b86-179">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="95b86-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="95b86-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="95b86-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="95b86-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b86-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="95b86-185">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95b86-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="95b86-187">a.</span><span class="sxs-lookup"><span data-stu-id="95b86-187">a.</span></span> <span data-ttu-id="95b86-188">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="95b86-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="95b86-189">b.</span><span class="sxs-lookup"><span data-stu-id="95b86-189">b.</span></span> <span data-ttu-id="95b86-190">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="95b86-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="95b86-191">c.</span><span class="sxs-lookup"><span data-stu-id="95b86-191">c.</span></span> <span data-ttu-id="95b86-192">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="95b86-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="95b86-193">d.</span><span class="sxs-lookup"><span data-stu-id="95b86-193">d.</span></span> <span data-ttu-id="95b86-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="95b86-194">Click **Create**.</span></span>
 
### <a name="creating-a-jobbadmin-test-user"></a><span data-ttu-id="95b86-195">Criar um usuário de teste do Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="95b86-195">Creating a Jobbadmin test user</span></span>

<span data-ttu-id="95b86-196">tooenable AD do Azure usuários toolog em tooJobbadmin, eles devem ser provisionados no Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="95b86-196">tooenable Azure AD users toolog in tooJobbadmin, they must be provisioned into Jobbadmin.</span></span>
 
<span data-ttu-id="95b86-197">Entre em contato com [Jobbadmin a equipe de suporte](https://www.jobbnorge.no/om-oss/kontakt-oss) usuários de saudação tooget adicionados no seu lado.</span><span class="sxs-lookup"><span data-stu-id="95b86-197">Please contact [Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss) tooget hello users added on their side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="95b86-198">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95b86-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="95b86-199">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooJobbadmin.</span><span class="sxs-lookup"><span data-stu-id="95b86-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobbadmin.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="95b86-201">**tooassign Britta Simon tooJobbadmin, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95b86-201">**tooassign Britta Simon tooJobbadmin, perform hello following steps:**</span></span>

1. <span data-ttu-id="95b86-202">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="95b86-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="95b86-204">Na lista de aplicativos hello, selecione **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="95b86-204">In hello applications list, select **Jobbadmin**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_app.png) 

3. <span data-ttu-id="95b86-206">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="95b86-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="95b86-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="95b86-208">Click **Add** button.</span></span> <span data-ttu-id="95b86-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95b86-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="95b86-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b86-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="95b86-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95b86-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="95b86-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95b86-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="95b86-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="95b86-214">Testing single sign-on</span></span>

<span data-ttu-id="95b86-215">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b86-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="95b86-216">Quando você clica em bloco Jobbadmin Olá Olá painel de acesso, você deve obter a página de logon do aplicativo Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="95b86-216">When you click hello Jobbadmin tile in hello Access Panel, you should get login page of Jobbadmin application.</span></span>
<span data-ttu-id="95b86-217">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="95b86-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="95b86-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="95b86-218">Additional resources</span></span>

* [<span data-ttu-id="95b86-219">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="95b86-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95b86-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="95b86-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_203.png

