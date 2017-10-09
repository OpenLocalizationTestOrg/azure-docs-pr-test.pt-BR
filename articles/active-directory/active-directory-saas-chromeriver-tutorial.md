---
title: "Tutorial: integração do Azure Active Directory com o Chromeriver | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Chromeriver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 445c5600-e340-4724-a9cb-3cfaf5770b70
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 7cf0e36fb6407bf3915e26717a2a997ac13110e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-chromeriver"></a><span data-ttu-id="e3bd5-103">Tutorial: Integração do Active Directory do Azure ao Chromeriver</span><span class="sxs-lookup"><span data-stu-id="e3bd5-103">Tutorial: Azure Active Directory integration with Chromeriver</span></span>

<span data-ttu-id="e3bd5-104">Neste tutorial, você aprenderá como toointegrate Chromeriver com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="e3bd5-104">In this tutorial, you learn how toointegrate Chromeriver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e3bd5-105">Integrando o Chromeriver com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3bd5-105">Integrating Chromeriver with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e3bd5-106">Você pode controlar no AD do Azure que tenha acesso tooChromeriver</span><span class="sxs-lookup"><span data-stu-id="e3bd5-106">You can control in Azure AD who has access tooChromeriver</span></span>
- <span data-ttu-id="e3bd5-107">Você pode habilitar seu usuários tooautomatically get conectado tooChromeriver (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd5-107">You can enable your users tooautomatically get signed-on tooChromeriver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e3bd5-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e3bd5-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e3bd5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3bd5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3bd5-110">Prerequisites</span></span>

<span data-ttu-id="e3bd5-111">tooconfigure integração do AD do Azure com o Chromeriver, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3bd5-111">tooconfigure Azure AD integration with Chromeriver, you need hello following items:</span></span>

- <span data-ttu-id="e3bd5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e3bd5-113">Uma assinatura habilitada para logon único do Chromeriver</span><span class="sxs-lookup"><span data-stu-id="e3bd5-113">A Chromeriver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3bd5-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e3bd5-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e3bd5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e3bd5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e3bd5-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3bd5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e3bd5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e3bd5-118">Scenario description</span></span>
<span data-ttu-id="e3bd5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3bd5-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="e3bd5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e3bd5-121">Adicionando Chromeriver da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e3bd5-121">Adding Chromeriver from hello gallery</span></span>
2. <span data-ttu-id="e3bd5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-chromeriver-from-hello-gallery"></a><span data-ttu-id="e3bd5-123">Adicionando Chromeriver da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e3bd5-123">Adding Chromeriver from hello gallery</span></span>
<span data-ttu-id="e3bd5-124">integração de saudação tooconfigure do Chromeriver no AD do Azure, você precisa tooadd Chromeriver da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-124">tooconfigure hello integration of Chromeriver into Azure AD, you need tooadd Chromeriver from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e3bd5-125">**tooadd Chromeriver da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e3bd5-125">**tooadd Chromeriver from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3bd5-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e3bd5-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e3bd5-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e3bd5-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e3bd5-133">Na caixa de pesquisa hello, digite **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-133">In hello search box, type **Chromeriver**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_search.png)

5. <span data-ttu-id="e3bd5-135">No painel de resultados de saudação, selecione **Chromeriver**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-135">In hello results panel, select **Chromeriver**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e3bd5-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e3bd5-138">Nesta seção, você configura e testa o logon único do Azure AD com o Chromeriver, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-138">In this section, you configure and test Azure AD single sign-on with Chromeriver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e3bd5-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Chromeriver é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Chromeriver is tooa user in Azure AD.</span></span> <span data-ttu-id="e3bd5-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Chromeriver precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-140">In other words, a link relationship between an Azure AD user and hello related user in Chromeriver needs toobe established.</span></span>

<span data-ttu-id="e3bd5-141">No Chromeriver, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-141">In Chromeriver, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e3bd5-142">tooconfigure e teste de logon único do AD do Azure com o Chromeriver, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3bd5-142">tooconfigure and test Azure AD single sign-on with Chromeriver, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e3bd5-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e3bd5-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3bd5-145">**[Criar um usuário de teste do Chromeriver](#creating-a-chromeriver-test-user)**  -toohave um equivalente do Britta Simon no Chromeriver é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-145">**[Creating a Chromeriver test user](#creating-a-chromeriver-test-user)** - toohave a counterpart of Britta Simon in Chromeriver that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e3bd5-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3bd5-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e3bd5-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3bd5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e3bd5-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Chromeriver application.</span></span>

<span data-ttu-id="e3bd5-150">**tooconfigure AD do Azure-logon único com o Chromeriver, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e3bd5-150">**tooconfigure Azure AD single sign-on with Chromeriver, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3bd5-151">Em Olá portal do Azure, Olá **Chromeriver** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-151">In hello Azure portal, on hello **Chromeriver** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e3bd5-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_samlbase.png)

3. <span data-ttu-id="e3bd5-155">Em Olá **Chromeriver domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3bd5-155">On hello **Chromeriver Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_url.png)

    <span data-ttu-id="e3bd5-157">a.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-157">a.</span></span> <span data-ttu-id="e3bd5-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.chromeriver.com`</span><span class="sxs-lookup"><span data-stu-id="e3bd5-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.chromeriver.com`</span></span>

    <span data-ttu-id="e3bd5-159">b.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-159">b.</span></span> <span data-ttu-id="e3bd5-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="e3bd5-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e3bd5-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-161">These values are not real.</span></span> <span data-ttu-id="e3bd5-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="e3bd5-163">Entre em contato com [equipe de suporte do Chromeriver](https://www.chromeriver.com/services/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-163">Contact [Chromeriver support team](https://www.chromeriver.com/services/support) tooget these values.</span></span>
 


4. <span data-ttu-id="e3bd5-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_certificate.png) 

5. <span data-ttu-id="e3bd5-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e3bd5-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-chromeriver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e3bd5-168">tooconfigure logon único no **Chromeriver** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do Chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="e3bd5-168">tooconfigure single sign-on on **Chromeriver** side, you need toosend hello downloaded **Metadata XML** too[Chromeriver support team](https://www.chromeriver.com/services/support).</span></span> <span data-ttu-id="e3bd5-169">Você receberá uma notificação quando o SSO tiver sido habilitado para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-169">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="e3bd5-170">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="e3bd5-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e3bd5-171">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e3bd5-172">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e3bd5-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e3bd5-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd5-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="e3bd5-174">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e3bd5-176">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e3bd5-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3bd5-177">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e3bd5-179">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e3bd5-181">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e3bd5-183">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3bd5-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e3bd5-185">a.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-185">a.</span></span> <span data-ttu-id="e3bd5-186">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3bd5-187">b.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-187">b.</span></span> <span data-ttu-id="e3bd5-188">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e3bd5-189">c.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-189">c.</span></span> <span data-ttu-id="e3bd5-190">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e3bd5-191">d.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-191">d.</span></span> <span data-ttu-id="e3bd5-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-192">Click **Create**.</span></span>
 
### <a name="creating-a-chromeriver-test-user"></a><span data-ttu-id="e3bd5-193">Criando um usuário de teste do Chromeriver</span><span class="sxs-lookup"><span data-stu-id="e3bd5-193">Creating a Chromeriver test user</span></span>

<span data-ttu-id="e3bd5-194">tooenable AD do Azure usuários toolog em tooChromeriver, eles devem ser provisionados no Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-194">tooenable Azure AD users toolog in tooChromeriver, they must be provisioned into Chromeriver.</span></span>  

<span data-ttu-id="e3bd5-195">Em caso de saudação do Chromeriver, contas de usuário de saudação necessário toobe criado por seu [equipe de suporte do Chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="e3bd5-195">In hello case of Chromeriver, hello user accounts need toobe created by your [Chromeriver support team](https://www.chromeriver.com/services/support).</span></span>

>[!NOTE]
><span data-ttu-id="e3bd5-196">Você pode usar qualquer ferramenta de criação outros Chromeriver usuário conta ou APIs fornecidas pelo Chromeriver tooprovision Azure Active Directory as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-196">You can use any other Chromeriver user account creation tools or APIs provided by Chromeriver tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e3bd5-197">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd5-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e3bd5-198">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooChromeriver.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooChromeriver.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e3bd5-200">**tooassign Britta Simon tooChromeriver, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e3bd5-200">**tooassign Britta Simon tooChromeriver, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3bd5-201">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e3bd5-203">Na lista de aplicativos hello, selecione **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-203">In hello applications list, select **Chromeriver**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_app.png) 

3. <span data-ttu-id="e3bd5-205">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e3bd5-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-207">Click **Add** button.</span></span> <span data-ttu-id="e3bd5-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e3bd5-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e3bd5-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e3bd5-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e3bd5-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e3bd5-213">Testing single sign-on</span></span>

<span data-ttu-id="e3bd5-214">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e3bd5-215">Quando você clica em bloco Chromeriver Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Chromeriver aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3bd5-215">When you click hello Chromeriver tile in hello Access Panel, you should get automatically signed-on tooyour Chromeriver application.</span></span> <span data-ttu-id="e3bd5-216">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e3bd5-216">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3bd5-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e3bd5-217">Additional resources</span></span>

* [<span data-ttu-id="e3bd5-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd5-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3bd5-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e3bd5-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_203.png

