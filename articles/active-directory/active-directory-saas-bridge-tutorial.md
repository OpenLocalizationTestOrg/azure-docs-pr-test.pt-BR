---
title: "Tutorial: Integração do Azure Active Directory ao Bridge | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ponte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dbb6499-80c1-4d00-a0b4-e0ad5522cf0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 85e1917de63356a86aa87a0f82621391733ab2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bridge"></a><span data-ttu-id="91dc4-103">Tutorial: Integração do Azure Active Directory ao Bridge</span><span class="sxs-lookup"><span data-stu-id="91dc4-103">Tutorial: Azure Active Directory integration with Bridge</span></span>

<span data-ttu-id="91dc4-104">Neste tutorial, você aprenderá como toointegrate acabar com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="91dc4-104">In this tutorial, you learn how toointegrate Bridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91dc4-105">Integrando ponte do Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="91dc4-105">Integrating Bridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="91dc4-106">Você pode controlar no AD do Azure que tenha acesso tooBridge</span><span class="sxs-lookup"><span data-stu-id="91dc4-106">You can control in Azure AD who has access tooBridge</span></span>
- <span data-ttu-id="91dc4-107">Você pode habilitar seu usuários tooautomatically get conectado tooBridge (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91dc4-107">You can enable your users tooautomatically get signed-on tooBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91dc4-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="91dc4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="91dc4-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="91dc4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91dc4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="91dc4-110">Prerequisites</span></span>

<span data-ttu-id="91dc4-111">tooconfigure integração do AD do Azure com ponte, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="91dc4-111">tooconfigure Azure AD integration with Bridge, you need hello following items:</span></span>

- <span data-ttu-id="91dc4-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91dc4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91dc4-113">Uma assinatura habilitada para logon único do Bridge</span><span class="sxs-lookup"><span data-stu-id="91dc4-113">A Bridge single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91dc4-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="91dc4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91dc4-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="91dc4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91dc4-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="91dc4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91dc4-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91dc4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91dc4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="91dc4-118">Scenario description</span></span>
<span data-ttu-id="91dc4-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="91dc4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91dc4-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="91dc4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91dc4-121">Adicionando a ponte da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="91dc4-121">Adding Bridge from hello gallery</span></span>
2. <span data-ttu-id="91dc4-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91dc4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bridge-from-hello-gallery"></a><span data-ttu-id="91dc4-123">Adicionando a ponte da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="91dc4-123">Adding Bridge from hello gallery</span></span>
<span data-ttu-id="91dc4-124">integração de saudação tooconfigure da ponte no AD do Azure, você precisa tooadd ponte na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="91dc4-124">tooconfigure hello integration of Bridge into Azure AD, you need tooadd Bridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="91dc4-125">**Ponte tooadd da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="91dc4-125">**tooadd Bridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="91dc4-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="91dc4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="91dc4-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="91dc4-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="91dc4-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="91dc4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="91dc4-133">Na caixa de pesquisa hello, digite **ponte**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-133">In hello search box, type **Bridge**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_search.png)

5. <span data-ttu-id="91dc4-135">No painel de resultados de saudação, selecione **ponte**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="91dc4-135">In hello results panel, select **Bridge**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91dc4-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91dc4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91dc4-138">Nesta seção, você configura e testa o logon único do Azure AD com o Bridge, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="91dc4-138">In this section, you configure and test Azure AD single sign-on with Bridge based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="91dc4-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário equivalente de saudação na ponte é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="91dc4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bridge is tooa user in Azure AD.</span></span> <span data-ttu-id="91dc4-140">Em outras palavras, uma relação entre um usuário do AD do Azure e o usuário relacionado de saudação na ponte de link deve toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="91dc4-140">In other words, a link relationship between an Azure AD user and hello related user in Bridge needs toobe established.</span></span>

<span data-ttu-id="91dc4-141">Na ponte, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="91dc4-141">In Bridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="91dc4-142">tooconfigure e teste de logon único do AD do Azure com ponte, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="91dc4-142">tooconfigure and test Azure AD single sign-on with Bridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="91dc4-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="91dc4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="91dc4-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91dc4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91dc4-145">**[Criar um usuário de teste de ponte](#creating-a-bridge-test-user)**  -toohave um equivalente do Britta Simon na ponte que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="91dc4-145">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - toohave a counterpart of Britta Simon in Bridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="91dc4-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="91dc4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91dc4-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="91dc4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91dc4-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="91dc4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91dc4-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de ponte.</span><span class="sxs-lookup"><span data-stu-id="91dc4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bridge application.</span></span>

<span data-ttu-id="91dc4-150">**tooconfigure AD do Azure-logon único com ponte, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="91dc4-150">**tooconfigure Azure AD single sign-on with Bridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="91dc4-151">Em Olá portal do Azure, Olá **ponte** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-151">In hello Azure portal, on hello **Bridge** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="91dc4-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="91dc4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_samlbase.png)

3. <span data-ttu-id="91dc4-155">Em Olá **domínio ponte e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="91dc4-155">On hello **Bridge Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_url.png)

    <span data-ttu-id="91dc4-157">a.</span><span class="sxs-lookup"><span data-stu-id="91dc4-157">a.</span></span> <span data-ttu-id="91dc4-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="91dc4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.bridgeapp.com`</span></span>

    <span data-ttu-id="91dc4-159">b.</span><span class="sxs-lookup"><span data-stu-id="91dc4-159">b.</span></span> <span data-ttu-id="91dc4-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="91dc4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.bridgeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91dc4-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="91dc4-161">These values are not real.</span></span> <span data-ttu-id="91dc4-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="91dc4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="91dc4-163">Entre em contato com [equipe de suporte do cliente de ponte](https://community.bridgeapp.com/community/help) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="91dc4-163">Contact [Bridge Client support team](https://community.bridgeapp.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="91dc4-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="91dc4-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_certificate.png) 

5. <span data-ttu-id="91dc4-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="91dc4-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91dc4-168">Em Olá **configuração da ponte** seção, clique em **configurar ponte** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="91dc4-168">On hello **Bridge Configuration** section, click **Configure Bridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="91dc4-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="91dc4-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_configure.png) 

7. <span data-ttu-id="91dc4-171">tooconfigure logon único no **ponte** lado, você precisa toosend Olá baixado **Certificate(Raw)** e **ID da entidade SAML, SAML Single Sign-On URL do serviço e a URL de logout**muito[equipe de suporte de ponte](https://community.bridgeapp.com/community/help).</span><span class="sxs-lookup"><span data-stu-id="91dc4-171">tooconfigure single sign-on on **Bridge** side, you need toosend hello downloaded **Certificate(Raw)** and **SAML Entity ID, SAML Single Sign-On Service URL, and Sign-Out URL** too[Bridge support team](https://community.bridgeapp.com/community/help).</span></span> 

> [!TIP]
> <span data-ttu-id="91dc4-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="91dc4-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="91dc4-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="91dc4-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="91dc4-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91dc4-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91dc4-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91dc4-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="91dc4-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="91dc4-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="91dc4-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="91dc4-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="91dc4-179">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="91dc4-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91dc4-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91dc4-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="91dc4-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91dc4-185">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="91dc4-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91dc4-187">a.</span><span class="sxs-lookup"><span data-stu-id="91dc4-187">a.</span></span> <span data-ttu-id="91dc4-188">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91dc4-189">b.</span><span class="sxs-lookup"><span data-stu-id="91dc4-189">b.</span></span> <span data-ttu-id="91dc4-190">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="91dc4-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91dc4-191">c.</span><span class="sxs-lookup"><span data-stu-id="91dc4-191">c.</span></span> <span data-ttu-id="91dc4-192">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="91dc4-193">d.</span><span class="sxs-lookup"><span data-stu-id="91dc4-193">d.</span></span> <span data-ttu-id="91dc4-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-194">Click **Create**.</span></span>
 
### <a name="creating-a-bridge-test-user"></a><span data-ttu-id="91dc4-195">Criando um usuário de teste do Bridge</span><span class="sxs-lookup"><span data-stu-id="91dc4-195">Creating a Bridge test user</span></span>

<span data-ttu-id="91dc4-196">Nesta seção, você cria um usuário chamado Brenda Fernandes no Bridge.</span><span class="sxs-lookup"><span data-stu-id="91dc4-196">In this section, you create a user called Britta Simon in Bridge.</span></span> <span data-ttu-id="91dc4-197">Trabalhar com [equipe de suporte do cliente de ponte](https://community.bridgeapp.com/community/help) toocreate um usuário na plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="91dc4-197">Work with [Bridge Client support team](https://community.bridgeapp.com/community/help) toocreate a user in hello platform.</span></span> <span data-ttu-id="91dc4-198">Você pode gerar um tíquete de suporte de saudação com ponte de <a href="https://community.bridgeapp.com/community/help">aqui</a> tooadd usuários de saudação na plataforma de ponte de saudação.</span><span class="sxs-lookup"><span data-stu-id="91dc4-198">You can raise hello support ticket with Bridge from <a href="https://community.bridgeapp.com/community/help">here</a> tooadd hello users in hello Bridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="91dc4-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91dc4-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="91dc4-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBridge.</span><span class="sxs-lookup"><span data-stu-id="91dc4-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBridge.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="91dc4-202">**tooassign Britta Simon tooBridge, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="91dc4-202">**tooassign Britta Simon tooBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="91dc4-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="91dc4-205">Na lista de aplicativos hello, selecione **ponte**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-205">In hello applications list, select **Bridge**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_app.png) 

3. <span data-ttu-id="91dc4-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="91dc4-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="91dc4-209">Click **Add** button.</span></span> <span data-ttu-id="91dc4-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="91dc4-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="91dc4-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="91dc4-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="91dc4-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="91dc4-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91dc4-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="91dc4-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91dc4-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="91dc4-215">Testing single sign-on</span></span>

<span data-ttu-id="91dc4-216">Nesta seção, você deve testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="91dc4-216">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="91dc4-217">Quando você clica em um bloco de ponte Olá Olá painel de acesso, você deve obter automaticamente conectado no aplicativo de ponte tooyour.</span><span class="sxs-lookup"><span data-stu-id="91dc4-217">When you click hello Bridge tile in hello Access Panel, you should get automatically signed-on tooyour Bridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91dc4-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="91dc4-218">Additional resources</span></span>

* [<span data-ttu-id="91dc4-219">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="91dc4-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91dc4-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91dc4-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_203.png

