---
title: "Tutorial: Integração do Azure Active Directory com o Convercent | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Convercent."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: e6d09d7de52779dcf05e80215df9369ebc2ed06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="6d383-103">Tutorial: Integração do Azure Active Directory ao Convercent</span><span class="sxs-lookup"><span data-stu-id="6d383-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="6d383-104">Neste tutorial, você aprenderá como toointegrate Convercent com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="6d383-104">In this tutorial, you learn how toointegrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d383-105">Integrando Convercent com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d383-105">Integrating Convercent with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6d383-106">Você pode controlar no AD do Azure que tenha acesso tooConvercent</span><span class="sxs-lookup"><span data-stu-id="6d383-106">You can control in Azure AD who has access tooConvercent</span></span>
- <span data-ttu-id="6d383-107">Você pode habilitar seu usuários tooautomatically get conectado tooConvercent (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d383-107">You can enable your users tooautomatically get signed-on tooConvercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6d383-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6d383-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6d383-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d383-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d383-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6d383-110">Prerequisites</span></span>

<span data-ttu-id="6d383-111">tooconfigure integração do AD do Azure com Convercent, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d383-111">tooconfigure Azure AD integration with Convercent, you need hello following items:</span></span>

- <span data-ttu-id="6d383-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d383-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d383-113">Uma assinatura habilitada para logon único do Convercent</span><span class="sxs-lookup"><span data-stu-id="6d383-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6d383-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6d383-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d383-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6d383-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d383-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6d383-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d383-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d383-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d383-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6d383-118">Scenario description</span></span>
<span data-ttu-id="6d383-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6d383-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d383-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="6d383-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d383-121">Adicionando Convercent da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="6d383-121">Adding Convercent from hello gallery</span></span>
2. <span data-ttu-id="6d383-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d383-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-hello-gallery"></a><span data-ttu-id="6d383-123">Adicionando Convercent da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="6d383-123">Adding Convercent from hello gallery</span></span>
<span data-ttu-id="6d383-124">integração de saudação tooconfigure de Convercent no AD do Azure, você precisa tooadd Convercent da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6d383-124">tooconfigure hello integration of Convercent into Azure AD, you need tooadd Convercent from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6d383-125">**tooadd Convercent da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6d383-125">**tooadd Convercent from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d383-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="6d383-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6d383-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6d383-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6d383-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6d383-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="6d383-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d383-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="6d383-133">Na caixa de pesquisa hello, digite **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="6d383-133">In hello search box, type **Convercent**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="6d383-135">No painel de resultados de saudação, selecione **Convercent**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6d383-135">In hello results panel, select **Convercent**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6d383-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d383-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6d383-138">Nesta seção, você configura e testa o logon único do Azure AD com o Convercent com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="6d383-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6d383-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Convercent é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d383-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Convercent is tooa user in Azure AD.</span></span> <span data-ttu-id="6d383-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Convercent precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="6d383-140">In other words, a link relationship between an Azure AD user and hello related user in Convercent needs toobe established.</span></span>

<span data-ttu-id="6d383-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Convercent.</span><span class="sxs-lookup"><span data-stu-id="6d383-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Convercent.</span></span>

<span data-ttu-id="6d383-142">tooconfigure e teste de logon único do AD do Azure com Convercent, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d383-142">tooconfigure and test Azure AD single sign-on with Convercent, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6d383-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6d383-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6d383-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d383-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d383-145">**[Criar um usuário de teste Convercent](#creating-a-convercent-test-user)**  -toohave um equivalente do Britta Simon em Convercent é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="6d383-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - toohave a counterpart of Britta Simon in Convercent that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6d383-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="6d383-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d383-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="6d383-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6d383-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d383-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6d383-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Convercent.</span><span class="sxs-lookup"><span data-stu-id="6d383-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="6d383-150">**tooconfigure AD do Azure-logon único com Convercent, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6d383-150">**tooconfigure Azure AD single sign-on with Convercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d383-151">Em Olá portal do Azure, Olá **Convercent** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="6d383-151">In hello Azure portal, on hello **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="6d383-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="6d383-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="6d383-155">Em Olá **Convercent domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**, executar Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d383-155">On hello **Convercent Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="6d383-157">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="6d383-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="6d383-158">Se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, em Olá **Convercent domínio e URLs** seção executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d383-158">If you wish tooconfigure hello application in **SP initiated mode**, on hello **Convercent Domain and URLs** section perform hello following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="6d383-160">a.</span><span class="sxs-lookup"><span data-stu-id="6d383-160">a.</span></span> <span data-ttu-id="6d383-161">Clique em **"Mostrar configurações de URL avançadas"**.</span><span class="sxs-lookup"><span data-stu-id="6d383-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="6d383-162">b.</span><span class="sxs-lookup"><span data-stu-id="6d383-162">b.</span></span> <span data-ttu-id="6d383-163">Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="6d383-163">In hello **Sign On URL** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="6d383-164">c.</span><span class="sxs-lookup"><span data-stu-id="6d383-164">c.</span></span> <span data-ttu-id="6d383-165">Em Olá **estado de retransmissão** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="6d383-165">In hello **Relay State** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6d383-166">Esses valores não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d383-166">These values are not hello real values.</span></span> <span data-ttu-id="6d383-167">Atualizar esses valores com hello real identificador, o URL de logon e o estado de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="6d383-167">Update these values with hello actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="6d383-168">Entre em contato com [equipe de suporte do cliente Convercent](http://support.convercent.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="6d383-168">Contact [Convercent Client support team](http://support.convercent.com) tooget these values.</span></span>

5. <span data-ttu-id="6d383-169">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="6d383-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="6d383-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6d383-171">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6d383-173">tooget SSO configurado para o seu aplicativo, entre em contato com [a equipe de suporte Convercent](mailto:support@convercent.com) e fornecê-los com hello baixado **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="6d383-173">tooget SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with hello downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="6d383-174">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="6d383-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6d383-175">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="6d383-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6d383-176">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6d383-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6d383-177">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d383-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="6d383-178">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d383-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="6d383-180">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6d383-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d383-181">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="6d383-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6d383-183">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="6d383-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6d383-185">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d383-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6d383-187">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d383-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6d383-189">a.</span><span class="sxs-lookup"><span data-stu-id="6d383-189">a.</span></span> <span data-ttu-id="6d383-190">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6d383-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d383-191">b.</span><span class="sxs-lookup"><span data-stu-id="6d383-191">b.</span></span> <span data-ttu-id="6d383-192">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6d383-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6d383-193">c.</span><span class="sxs-lookup"><span data-stu-id="6d383-193">c.</span></span> <span data-ttu-id="6d383-194">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="6d383-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6d383-195">d.</span><span class="sxs-lookup"><span data-stu-id="6d383-195">d.</span></span> <span data-ttu-id="6d383-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6d383-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="6d383-197">Criando um usuário de teste do Convercent</span><span class="sxs-lookup"><span data-stu-id="6d383-197">Creating a Convercent test user</span></span>

<span data-ttu-id="6d383-198">Trabalhar com [Convercent a equipe de suporte](mailto:support@convercent.com) tooadd usuários de saudação na plataforma de Convercent hello.</span><span class="sxs-lookup"><span data-stu-id="6d383-198">Work with [Convercent support team](mailto:support@convercent.com) tooadd hello users in hello Convercent platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6d383-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d383-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6d383-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooConvercent.</span><span class="sxs-lookup"><span data-stu-id="6d383-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConvercent.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="6d383-202">**tooassign Britta Simon tooConvercent, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6d383-202">**tooassign Britta Simon tooConvercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d383-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6d383-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="6d383-205">Na lista de aplicativos hello, selecione **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="6d383-205">In hello applications list, select **Convercent**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="6d383-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6d383-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="6d383-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d383-209">Click **Add** button.</span></span> <span data-ttu-id="6d383-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d383-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="6d383-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d383-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6d383-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d383-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d383-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d383-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6d383-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="6d383-215">Testing single sign-on</span></span>

<span data-ttu-id="6d383-216">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d383-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6d383-217">Quando você clica em bloco Convercent Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Convercent aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6d383-217">When you click hello Convercent tile in hello Access Panel, you should get automatically signed-on tooyour Convercent application.</span></span>
<span data-ttu-id="6d383-218">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6d383-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6d383-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6d383-219">Additional resources</span></span>

* [<span data-ttu-id="6d383-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6d383-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d383-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6d383-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

