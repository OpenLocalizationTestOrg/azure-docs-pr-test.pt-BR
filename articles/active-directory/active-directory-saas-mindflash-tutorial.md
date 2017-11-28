---
title: "Tutorial: Integração do Azure Active Directory ao Mindflash | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Mindflash."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a1bc327ea3867287103acbb64d30f0a8d7d4c5e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="57403-103">Tutorial: Integração do Active Directory do Azure com o Mindflash</span><span class="sxs-lookup"><span data-stu-id="57403-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="57403-104">Neste tutorial, você aprenderá como toointegrate Mindflash com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="57403-104">In this tutorial, you learn how toointegrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57403-105">Integrando o Mindflash com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="57403-105">Integrating Mindflash with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="57403-106">Você pode controlar no AD do Azure que tenha acesso tooMindflash</span><span class="sxs-lookup"><span data-stu-id="57403-106">You can control in Azure AD who has access tooMindflash</span></span>
- <span data-ttu-id="57403-107">Você pode habilitar seu usuários tooautomatically get conectado tooMindflash (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="57403-107">You can enable your users tooautomatically get signed-on tooMindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57403-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="57403-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="57403-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57403-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57403-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="57403-110">Prerequisites</span></span>

<span data-ttu-id="57403-111">tooconfigure integração do AD do Azure com o Mindflash, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="57403-111">tooconfigure Azure AD integration with Mindflash, you need hello following items:</span></span>

- <span data-ttu-id="57403-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="57403-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57403-113">Uma assinatura habilitada para logon único do Mindflash</span><span class="sxs-lookup"><span data-stu-id="57403-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57403-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="57403-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57403-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="57403-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57403-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="57403-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57403-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57403-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57403-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="57403-118">Scenario description</span></span>
<span data-ttu-id="57403-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="57403-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57403-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="57403-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57403-121">Adicionando Mindflash da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="57403-121">Adding Mindflash from hello gallery</span></span>
2. <span data-ttu-id="57403-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="57403-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-hello-gallery"></a><span data-ttu-id="57403-123">Adicionando Mindflash da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="57403-123">Adding Mindflash from hello gallery</span></span>
<span data-ttu-id="57403-124">integração de saudação tooconfigure do Mindflash no AD do Azure, você precisa tooadd Mindflash da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="57403-124">tooconfigure hello integration of Mindflash into Azure AD, you need tooadd Mindflash from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="57403-125">**tooadd Mindflash da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="57403-125">**tooadd Mindflash from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="57403-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="57403-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57403-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="57403-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="57403-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="57403-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="57403-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="57403-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="57403-133">Na caixa de pesquisa hello, digite **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="57403-133">In hello search box, type **Mindflash**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="57403-135">No painel de resultados de saudação, selecione **Mindflash**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="57403-135">In hello results panel, select **Mindflash**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57403-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="57403-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57403-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Mindflash, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="57403-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57403-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Mindflash é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="57403-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mindflash is tooa user in Azure AD.</span></span> <span data-ttu-id="57403-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Mindflash precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="57403-140">In other words, a link relationship between an Azure AD user and hello related user in Mindflash needs toobe established.</span></span>

<span data-ttu-id="57403-141">No Mindflash, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="57403-141">In Mindflash, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="57403-142">tooconfigure e teste de logon único do AD do Azure com o Mindflash, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="57403-142">tooconfigure and test Azure AD single sign-on with Mindflash, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="57403-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="57403-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="57403-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57403-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57403-145">**[Criar um usuário de teste do Mindflash](#creating-a-mindflash-test-user)**  -toohave um equivalente do Britta Simon no Mindflash é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="57403-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - toohave a counterpart of Britta Simon in Mindflash that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="57403-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="57403-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57403-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="57403-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57403-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="57403-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57403-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Mindflash.</span><span class="sxs-lookup"><span data-stu-id="57403-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="57403-150">**tooconfigure AD do Azure-logon único com o Mindflash, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="57403-150">**tooconfigure Azure AD single sign-on with Mindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="57403-151">Em Olá portal do Azure, Olá **Mindflash** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="57403-151">In hello Azure portal, on hello **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="57403-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="57403-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="57403-155">Em Olá **Mindflash domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="57403-155">On hello **Mindflash Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="57403-157">a.</span><span class="sxs-lookup"><span data-stu-id="57403-157">a.</span></span> <span data-ttu-id="57403-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="57403-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="57403-159">b.</span><span class="sxs-lookup"><span data-stu-id="57403-159">b.</span></span> <span data-ttu-id="57403-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="57403-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="57403-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="57403-161">These values are not real.</span></span> <span data-ttu-id="57403-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="57403-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="57403-163">Entre em contato com [equipe de suporte do Mindflash cliente](https://www.mindflash.com/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="57403-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="57403-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="57403-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="57403-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="57403-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="57403-168">tooconfigure logon único no **Mindflash** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do Mindflash](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="57403-168">tooconfigure single sign-on on **Mindflash** side, you need toosend hello downloaded **Metadata XML** too[Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="57403-169">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="57403-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="57403-170">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="57403-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="57403-171">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57403-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57403-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="57403-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="57403-173">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="57403-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="57403-175">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="57403-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="57403-176">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="57403-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57403-178">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="57403-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57403-180">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="57403-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57403-182">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="57403-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57403-184">a.</span><span class="sxs-lookup"><span data-stu-id="57403-184">a.</span></span> <span data-ttu-id="57403-185">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57403-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57403-186">b.</span><span class="sxs-lookup"><span data-stu-id="57403-186">b.</span></span> <span data-ttu-id="57403-187">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="57403-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57403-188">c.</span><span class="sxs-lookup"><span data-stu-id="57403-188">c.</span></span> <span data-ttu-id="57403-189">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="57403-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="57403-190">d.</span><span class="sxs-lookup"><span data-stu-id="57403-190">d.</span></span> <span data-ttu-id="57403-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="57403-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="57403-192">Criação de um usuário de teste do Mindflash</span><span class="sxs-lookup"><span data-stu-id="57403-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="57403-193">Ordem tooenable AD do Azure usuários toolog no Mindflash, eles devem ser provisionados no Mindflash.</span><span class="sxs-lookup"><span data-stu-id="57403-193">In order tooenable Azure AD users toolog into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="57403-194">No caso de saudação do Mindflash, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="57403-194">In hello case of Mindflash, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="57403-195">tooprovision contas de usuário, executar Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="57403-195">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="57403-196">Faça logon no tooyour **Mindflash** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="57403-196">Log in tooyour **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="57403-197">Vá muito**gerenciar usuários**.</span><span class="sxs-lookup"><span data-stu-id="57403-197">Go too**Manage Users**.</span></span>
   
    <span data-ttu-id="57403-198">![Gerenciar Usuários](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="57403-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="57403-199">Clique em Olá **adicionar usuários**e, em seguida, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="57403-199">Click hello **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="57403-200">Em Olá **adicionar novos usuários** , execute Olá seguindo as etapas de uma válida do Azure você deseja tooprovision de conta do AD:</span><span class="sxs-lookup"><span data-stu-id="57403-200">In hello **Add New Users** section, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="57403-201">![Adicionar Novos Usuários](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Adicionar Novos Usuários")</span><span class="sxs-lookup"><span data-stu-id="57403-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="57403-202">a.</span><span class="sxs-lookup"><span data-stu-id="57403-202">a.</span></span> <span data-ttu-id="57403-203">Em Olá **nome** caixa de texto, tipo **nome** do usuário hello como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="57403-203">In hello **First name** textbox, type **First name** of hello user as **Britta**.</span></span>

    <span data-ttu-id="57403-204">b.</span><span class="sxs-lookup"><span data-stu-id="57403-204">b.</span></span> <span data-ttu-id="57403-205">Em Olá **Sobrenome** caixa de texto, tipo **Sobrenome** do usuário hello como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="57403-205">In hello **Last name** textbox, type **Last name** of hello user as **Simon**.</span></span>
    
    <span data-ttu-id="57403-206">c.</span><span class="sxs-lookup"><span data-stu-id="57403-206">c.</span></span> <span data-ttu-id="57403-207">Em Olá **Email** caixa de texto, tipo **endereço de Email** do usuário hello como  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="57403-207">In hello **Email** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="57403-208">b.</span><span class="sxs-lookup"><span data-stu-id="57403-208">b.</span></span> <span data-ttu-id="57403-209">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="57403-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="57403-210">Você pode usar qualquer ferramenta de criação outros Mindflash usuário conta ou APIs fornecidas pelo Mindflash tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="57403-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="57403-211">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="57403-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="57403-212">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMindflash.</span><span class="sxs-lookup"><span data-stu-id="57403-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMindflash.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="57403-214">**tooassign Britta Simon tooMindflash, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="57403-214">**tooassign Britta Simon tooMindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="57403-215">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="57403-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="57403-217">Na lista de aplicativos hello, selecione **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="57403-217">In hello applications list, select **Mindflash**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="57403-219">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="57403-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="57403-221">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="57403-221">Click **Add** button.</span></span> <span data-ttu-id="57403-222">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="57403-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="57403-224">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="57403-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="57403-225">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="57403-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57403-226">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="57403-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57403-227">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="57403-227">Testing single sign-on</span></span>

<span data-ttu-id="57403-228">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="57403-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="57403-229">Quando você clica em bloco Mindflash Olá Olá painel de acesso, você deve obter a página de logon do aplicativo do Mindflash.</span><span class="sxs-lookup"><span data-stu-id="57403-229">When you click hello Mindflash tile in hello Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="57403-230">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="57403-230">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57403-231">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="57403-231">Additional resources</span></span>

* [<span data-ttu-id="57403-232">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="57403-232">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57403-233">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="57403-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

