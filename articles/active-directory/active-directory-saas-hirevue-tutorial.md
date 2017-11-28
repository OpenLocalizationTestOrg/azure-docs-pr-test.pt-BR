---
title: "Tutorial: integração do Azure Active Directory ao HireVue | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e HireVue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f890633ee4f13919c32a43d7b6cf30f2270ef6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="eed54-103">Tutorial: Integração do Azure Active Directory com o HireVue</span><span class="sxs-lookup"><span data-stu-id="eed54-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="eed54-104">Neste tutorial, você aprenderá como toointegrate HireVue com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="eed54-104">In this tutorial, you learn how toointegrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eed54-105">Integrando HireVue com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="eed54-105">Integrating HireVue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eed54-106">Você pode controlar no AD do Azure que tenha acesso tooHireVue</span><span class="sxs-lookup"><span data-stu-id="eed54-106">You can control in Azure AD who has access tooHireVue</span></span>
- <span data-ttu-id="eed54-107">Você pode habilitar seu usuários tooautomatically get conectado tooHireVue (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eed54-107">You can enable your users tooautomatically get signed-on tooHireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eed54-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="eed54-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eed54-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eed54-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eed54-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eed54-110">Prerequisites</span></span>

<span data-ttu-id="eed54-111">tooconfigure integração do AD do Azure com HireVue, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="eed54-111">tooconfigure Azure AD integration with HireVue, you need hello following items:</span></span>

- <span data-ttu-id="eed54-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eed54-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eed54-113">Uma assinatura habilitada para logon único do HireVue</span><span class="sxs-lookup"><span data-stu-id="eed54-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eed54-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="eed54-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eed54-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="eed54-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eed54-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="eed54-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eed54-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eed54-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eed54-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="eed54-118">Scenario description</span></span>
<span data-ttu-id="eed54-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="eed54-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eed54-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="eed54-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eed54-121">Adicionando HireVue da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="eed54-121">Adding HireVue from hello gallery</span></span>
2. <span data-ttu-id="eed54-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eed54-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-hello-gallery"></a><span data-ttu-id="eed54-123">Adicionando HireVue da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="eed54-123">Adding HireVue from hello gallery</span></span>
<span data-ttu-id="eed54-124">integração de saudação tooconfigure de HireVue no AD do Azure, você precisa tooadd HireVue da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="eed54-124">tooconfigure hello integration of HireVue into Azure AD, you need tooadd HireVue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eed54-125">**tooadd HireVue da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eed54-125">**tooadd HireVue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eed54-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="eed54-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eed54-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="eed54-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eed54-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="eed54-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="eed54-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eed54-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="eed54-133">Na caixa de pesquisa hello, digite **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="eed54-133">In hello search box, type **HireVue**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="eed54-135">No painel de resultados de saudação, selecione **HireVue**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="eed54-135">In hello results panel, select **HireVue**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eed54-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eed54-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eed54-138">Nesta seção, você configurará e testará o logon único do Azure AD com o HireVue, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="eed54-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eed54-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em HireVue é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="eed54-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HireVue is tooa user in Azure AD.</span></span> <span data-ttu-id="eed54-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em HireVue precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="eed54-140">In other words, a link relationship between an Azure AD user and hello related user in HireVue needs toobe established.</span></span>

<span data-ttu-id="eed54-141">HireVue, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="eed54-141">In HireVue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eed54-142">tooconfigure e teste de logon único do AD do Azure com HireVue, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="eed54-142">tooconfigure and test Azure AD single sign-on with HireVue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eed54-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="eed54-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eed54-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eed54-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eed54-145">**[Criar um usuário de teste HireVue](#creating-a-hirevue-test-user)**  -toohave um equivalente do Britta Simon em HireVue é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="eed54-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - toohave a counterpart of Britta Simon in HireVue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eed54-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="eed54-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eed54-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="eed54-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eed54-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="eed54-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eed54-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo HireVue.</span><span class="sxs-lookup"><span data-stu-id="eed54-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="eed54-150">**tooconfigure AD do Azure-logon único com HireVue, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eed54-150">**tooconfigure Azure AD single sign-on with HireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="eed54-151">Em Olá portal do Azure, Olá **HireVue** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="eed54-151">In hello Azure portal, on hello **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="eed54-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="eed54-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="eed54-155">Em Olá **HireVue domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="eed54-155">On hello **HireVue Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="eed54-157">a.</span><span class="sxs-lookup"><span data-stu-id="eed54-157">a.</span></span> <span data-ttu-id="eed54-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="eed54-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>

    | <span data-ttu-id="eed54-159">Ambiente</span><span class="sxs-lookup"><span data-stu-id="eed54-159">Environment</span></span> | <span data-ttu-id="eed54-160">URL</span><span class="sxs-lookup"><span data-stu-id="eed54-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="eed54-161">Produção</span><span class="sxs-lookup"><span data-stu-id="eed54-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="eed54-162">Staging</span><span class="sxs-lookup"><span data-stu-id="eed54-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="eed54-163">b.</span><span class="sxs-lookup"><span data-stu-id="eed54-163">b.</span></span> <span data-ttu-id="eed54-164">Em Olá **identificador** caixa de texto, digite um URL como:</span><span class="sxs-lookup"><span data-stu-id="eed54-164">In hello **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="eed54-165">Ambiente</span><span class="sxs-lookup"><span data-stu-id="eed54-165">Environment</span></span> | <span data-ttu-id="eed54-166">URN</span><span class="sxs-lookup"><span data-stu-id="eed54-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="eed54-167">Produção</span><span class="sxs-lookup"><span data-stu-id="eed54-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="eed54-168">Staging</span><span class="sxs-lookup"><span data-stu-id="eed54-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="eed54-169">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="eed54-169">These values are not real.</span></span> <span data-ttu-id="eed54-170">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="eed54-170">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eed54-171">Entre em contato com [equipe de suporte do cliente HireVue](mailto:samlsupport@hirevue.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="eed54-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="eed54-172">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="eed54-172">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="eed54-174">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="eed54-174">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eed54-176">Em Olá **HireVue configuração** seção, clique em **configurar HireVue** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="eed54-176">On hello **HireVue Configuration** section, click **Configure HireVue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eed54-177">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="eed54-177">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="eed54-179">tooconfigure logon único no **HireVue** lado, você precisa toosend Olá baixado **Certificate(Base64)** e **URL de logout, ID de entidade de SAML e SAML Single Sign-On URL do serviço** muito[a equipe de suporte HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="eed54-179">tooconfigure single sign-on on **HireVue** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="eed54-180">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="eed54-180">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="eed54-181">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="eed54-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eed54-182">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="eed54-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eed54-183">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eed54-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eed54-184">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eed54-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="eed54-185">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eed54-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="eed54-187">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eed54-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eed54-188">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="eed54-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eed54-190">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="eed54-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eed54-192">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="eed54-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eed54-194">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="eed54-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eed54-196">a.</span><span class="sxs-lookup"><span data-stu-id="eed54-196">a.</span></span> <span data-ttu-id="eed54-197">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eed54-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eed54-198">b.</span><span class="sxs-lookup"><span data-stu-id="eed54-198">b.</span></span> <span data-ttu-id="eed54-199">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eed54-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eed54-200">c.</span><span class="sxs-lookup"><span data-stu-id="eed54-200">c.</span></span> <span data-ttu-id="eed54-201">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="eed54-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eed54-202">d.</span><span class="sxs-lookup"><span data-stu-id="eed54-202">d.</span></span> <span data-ttu-id="eed54-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="eed54-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="eed54-204">Como criar um usuário de teste do HireVue</span><span class="sxs-lookup"><span data-stu-id="eed54-204">Creating a HireVue test user</span></span>

<span data-ttu-id="eed54-205">Nesta seção, você criará uma usuária chamada Brenda Fernandes no HireVue.</span><span class="sxs-lookup"><span data-stu-id="eed54-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="eed54-206">Trabalhe com [HireVue a equipe de suporte](mailto:samlsupport@hirevue.com) tooadd usuários de saudação na plataforma de HireVue hello.</span><span class="sxs-lookup"><span data-stu-id="eed54-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) tooadd hello users in hello HireVue platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eed54-207">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eed54-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eed54-208">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHireVue.</span><span class="sxs-lookup"><span data-stu-id="eed54-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHireVue.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="eed54-210">**tooassign Britta Simon tooHireVue, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eed54-210">**tooassign Britta Simon tooHireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="eed54-211">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="eed54-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="eed54-213">Na lista de aplicativos hello, selecione **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="eed54-213">In hello applications list, select **HireVue**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="eed54-215">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="eed54-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="eed54-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="eed54-217">Click **Add** button.</span></span> <span data-ttu-id="eed54-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eed54-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="eed54-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="eed54-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eed54-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eed54-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eed54-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eed54-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eed54-223">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="eed54-223">Testing single sign-on</span></span>

<span data-ttu-id="eed54-224">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="eed54-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eed54-225">Quando você clica em bloco HireVue Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour HireVue aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eed54-225">When you click hello HireVue tile in hello Access Panel, you should get automatically signed-on tooyour HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eed54-226">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="eed54-226">Additional resources</span></span>

* [<span data-ttu-id="eed54-227">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="eed54-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eed54-228">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eed54-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png

