---
title: "Tutorial: Integração do Azure Active Directory ao Trakopolis | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Trakopolis."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 73d67c3e-4b4b-4d3b-aa58-6699ea1ccea3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 00f9b21c0a837d1d9fbbd9135367fae4b02db934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakopolis"></a><span data-ttu-id="fa6e5-103">Tutorial: Integração do Azure Active Directory ao Trakopolis</span><span class="sxs-lookup"><span data-stu-id="fa6e5-103">Tutorial: Azure Active Directory integration with Trakopolis</span></span>

<span data-ttu-id="fa6e5-104">Neste tutorial, você aprenderá como toointegrate Trakopolis com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="fa6e5-104">In this tutorial, you learn how toointegrate Trakopolis with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fa6e5-105">Integrando Trakopolis com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa6e5-105">Integrating Trakopolis with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fa6e5-106">Você pode controlar no AD do Azure que tenha acesso tooTrakopolis</span><span class="sxs-lookup"><span data-stu-id="fa6e5-106">You can control in Azure AD who has access tooTrakopolis</span></span>
- <span data-ttu-id="fa6e5-107">Você pode habilitar seus usuários tooautomatically get conectado tooTrakopolis (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fa6e5-107">You can enable your users tooautomatically get signed-on tooTrakopolis (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fa6e5-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fa6e5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fa6e5-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fa6e5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa6e5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fa6e5-110">Prerequisites</span></span>

<span data-ttu-id="fa6e5-111">tooconfigure integração do AD do Azure com Trakopolis, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa6e5-111">tooconfigure Azure AD integration with Trakopolis, you need hello following items:</span></span>

- <span data-ttu-id="fa6e5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fa6e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fa6e5-113">Uma assinatura do Trakopolis habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="fa6e5-113">A Trakopolis single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fa6e5-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fa6e5-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="fa6e5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fa6e5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fa6e5-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fa6e5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fa6e5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="fa6e5-118">Scenario description</span></span>
<span data-ttu-id="fa6e5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fa6e5-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="fa6e5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fa6e5-121">Adicionando Trakopolis da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="fa6e5-121">Adding Trakopolis from hello gallery</span></span>
2. <span data-ttu-id="fa6e5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fa6e5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakopolis-from-hello-gallery"></a><span data-ttu-id="fa6e5-123">Adicionando Trakopolis da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="fa6e5-123">Adding Trakopolis from hello gallery</span></span>
<span data-ttu-id="fa6e5-124">integração de saudação tooconfigure de Trakopolis no AD do Azure, você precisa tooadd Trakopolis da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-124">tooconfigure hello integration of Trakopolis into Azure AD, you need tooadd Trakopolis from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fa6e5-125">**tooadd Trakopolis da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fa6e5-125">**tooadd Trakopolis from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa6e5-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fa6e5-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fa6e5-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="fa6e5-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="fa6e5-133">Na caixa de pesquisa hello, digite **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-133">In hello search box, type **Trakopolis**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_search.png)

5. <span data-ttu-id="fa6e5-135">No painel de resultados de saudação, selecione **Trakopolis**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-135">In hello results panel, select **Trakopolis**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fa6e5-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fa6e5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fa6e5-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Trakopolis com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="fa6e5-138">In this section, you configure and test Azure AD single sign-on with Trakopolis based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fa6e5-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Trakopolis é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trakopolis is tooa user in Azure AD.</span></span> <span data-ttu-id="fa6e5-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Trakopolis precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-140">In other words, a link relationship between an Azure AD user and hello related user in Trakopolis needs toobe established.</span></span>

<span data-ttu-id="fa6e5-141">Trakopolis, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-141">In Trakopolis, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fa6e5-142">tooconfigure e teste de logon único do AD do Azure com Trakopolis, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa6e5-142">tooconfigure and test Azure AD single sign-on with Trakopolis, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fa6e5-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fa6e5-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fa6e5-145">**[Criar um usuário de teste Trakopolis](#creating-a-trakopolis-test-user)**  -toohave um equivalente do Britta Simon em Trakopolis é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-145">**[Creating a Trakopolis test user](#creating-a-trakopolis-test-user)** - toohave a counterpart of Britta Simon in Trakopolis that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fa6e5-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fa6e5-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fa6e5-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa6e5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fa6e5-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trakopolis application.</span></span>

<span data-ttu-id="fa6e5-150">**tooconfigure AD do Azure-logon único com Trakopolis, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fa6e5-150">**tooconfigure Azure AD single sign-on with Trakopolis, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa6e5-151">Em Olá portal do Azure, Olá **Trakopolis** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-151">In hello Azure portal, on hello **Trakopolis** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="fa6e5-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_samlbase.png)

3. <span data-ttu-id="fa6e5-155">Em Olá **Trakopolis domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa6e5-155">On hello **Trakopolis Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_url.png)

    <span data-ttu-id="fa6e5-157">a.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-157">a.</span></span> <span data-ttu-id="fa6e5-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.trakopolis.com/`</span><span class="sxs-lookup"><span data-stu-id="fa6e5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.trakopolis.com/`</span></span>

    <span data-ttu-id="fa6e5-159">b.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-159">b.</span></span> <span data-ttu-id="fa6e5-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.trakopolis.com`</span><span class="sxs-lookup"><span data-stu-id="fa6e5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.trakopolis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fa6e5-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-161">These values are not real.</span></span> <span data-ttu-id="fa6e5-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fa6e5-163">Entre em contato com [equipe de suporte do cliente Trakopolis](mailto:support@cantelematics.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-163">Contact [Trakopolis Client support team](mailto:support@cantelematics.com) tooget these values.</span></span> 

4. <span data-ttu-id="fa6e5-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_certificate.png) 

5. <span data-ttu-id="fa6e5-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="fa6e5-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakopolis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fa6e5-168">Em Olá **Trakopolis configuração** seção, clique em **configurar Trakopolis** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-168">On hello **Trakopolis Configuration** section, click **Configure Trakopolis** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fa6e5-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="fa6e5-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_configure.png) 

7. <span data-ttu-id="fa6e5-171">tooconfigure logon único no **Trakopolis** lado, você precisa toosend Olá baixado **Metadata XML, URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** muito[Trakopolis equipe de suporte](mailto:support@cantelematics.com).</span><span class="sxs-lookup"><span data-stu-id="fa6e5-171">tooconfigure single sign-on on **Trakopolis** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Trakopolis support team](mailto:support@cantelematics.com).</span></span> <span data-ttu-id="fa6e5-172">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fa6e5-173">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="fa6e5-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fa6e5-174">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fa6e5-175">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fa6e5-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fa6e5-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fa6e5-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="fa6e5-177">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="fa6e5-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fa6e5-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa6e5-180">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fa6e5-182">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fa6e5-184">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fa6e5-186">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa6e5-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fa6e5-188">a.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-188">a.</span></span> <span data-ttu-id="fa6e5-189">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fa6e5-190">b.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-190">b.</span></span> <span data-ttu-id="fa6e5-191">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fa6e5-192">c.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-192">c.</span></span> <span data-ttu-id="fa6e5-193">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fa6e5-194">d.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-194">d.</span></span> <span data-ttu-id="fa6e5-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-195">Click **Create**.</span></span>
 
### <a name="creating-a-trakopolis-test-user"></a><span data-ttu-id="fa6e5-196">Criação de um usuário de teste do Trakopolis</span><span class="sxs-lookup"><span data-stu-id="fa6e5-196">Creating a Trakopolis test user</span></span>

<span data-ttu-id="fa6e5-197">Nesta seção, você criará um usuário chamado Brenda Fernandes no Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-197">In this section, you create a user called Britta Simon in Trakopolis.</span></span> <span data-ttu-id="fa6e5-198">Trabalhar com [Trakopolis equipe de suporte](mailto:support@cantelematics.com) para adicionar usuários de saudação na plataforma de Trakopolis hello.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-198">Work with [Trakopolis support team](mailto:support@cantelematics.com) to add hello users in hello Trakopolis platform.</span></span> <span data-ttu-id="fa6e5-199">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fa6e5-200">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fa6e5-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fa6e5-201">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTrakopolis.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrakopolis.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="fa6e5-203">**tooassign Britta Simon tooTrakopolis, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fa6e5-203">**tooassign Britta Simon tooTrakopolis, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa6e5-204">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="fa6e5-206">Na lista de aplicativos hello, selecione **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-206">In hello applications list, select **Trakopolis**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_app.png) 

3. <span data-ttu-id="fa6e5-208">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="fa6e5-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-210">Click **Add** button.</span></span> <span data-ttu-id="fa6e5-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="fa6e5-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fa6e5-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fa6e5-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fa6e5-216">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="fa6e5-216">Testing single sign-on</span></span>

<span data-ttu-id="fa6e5-217">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="fa6e5-218">Quando você clica em Olá Trakopolis bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Trakopolis aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fa6e5-218">When you click hello Trakopolis tile in hello Access Panel, you should get automatically signed-on tooyour Trakopolis application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fa6e5-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fa6e5-219">Additional resources</span></span>

* [<span data-ttu-id="fa6e5-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="fa6e5-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fa6e5-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fa6e5-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_203.png

