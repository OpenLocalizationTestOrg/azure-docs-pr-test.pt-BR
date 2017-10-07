---
title: "Tutorial: integração do Azure Active Directory com o People | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e pessoas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: d540c31867c92c4dc09db9c0833f8a8a7c02b371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="251ff-103">Tutorial: Integração do Azure Active Directory ao People</span><span class="sxs-lookup"><span data-stu-id="251ff-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="251ff-104">Neste tutorial, você aprenderá como toointegrate pessoas com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="251ff-104">In this tutorial, you learn how toointegrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="251ff-105">Integração de pessoas com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="251ff-105">Integrating People with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="251ff-106">Você pode controlar no AD do Azure que tenha acesso tooPeople</span><span class="sxs-lookup"><span data-stu-id="251ff-106">You can control in Azure AD who has access tooPeople</span></span>
- <span data-ttu-id="251ff-107">Você pode habilitar seu usuários tooautomatically get conectado tooPeople (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="251ff-107">You can enable your users tooautomatically get signed-on tooPeople (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="251ff-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="251ff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="251ff-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="251ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="251ff-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="251ff-110">Prerequisites</span></span>

<span data-ttu-id="251ff-111">integração do AD do Azure com pessoas de tooconfigure, é necessário Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="251ff-111">tooconfigure Azure AD integration with People, you need hello following items:</span></span>

- <span data-ttu-id="251ff-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="251ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="251ff-113">Uma assinatura habilitada para logon único do People</span><span class="sxs-lookup"><span data-stu-id="251ff-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="251ff-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="251ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="251ff-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="251ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="251ff-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="251ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="251ff-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="251ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="251ff-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="251ff-118">Scenario description</span></span>
<span data-ttu-id="251ff-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="251ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="251ff-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="251ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="251ff-121">Adicionar pessoas da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="251ff-121">Adding People from hello gallery</span></span>
2. <span data-ttu-id="251ff-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="251ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-hello-gallery"></a><span data-ttu-id="251ff-123">Adicionar pessoas da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="251ff-123">Adding People from hello gallery</span></span>
<span data-ttu-id="251ff-124">integração de saudação tooconfigure de pessoas no AD do Azure, você precisa tooadd pessoas na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="251ff-124">tooconfigure hello integration of People into Azure AD, you need tooadd People from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="251ff-125">**tooadd pessoas da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="251ff-125">**tooadd People from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="251ff-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="251ff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="251ff-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="251ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="251ff-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="251ff-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="251ff-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="251ff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="251ff-133">Na caixa de pesquisa hello, digite **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="251ff-133">In hello search box, type **People**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="251ff-135">No painel de resultados de saudação, selecione **pessoas**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="251ff-135">In hello results panel, select **People**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="251ff-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="251ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="251ff-138">Nesta seção, você configurará e testará o logon único do Azure AD com o People, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="251ff-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="251ff-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em pessoas é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="251ff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in People is tooa user in Azure AD.</span></span> <span data-ttu-id="251ff-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em pessoas deve toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="251ff-140">In other words, a link relationship between an Azure AD user and hello related user in People needs toobe established.</span></span>

<span data-ttu-id="251ff-141">Em pessoas, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="251ff-141">In People, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="251ff-142">tooconfigure e teste de logon único do AD do Azure com pessoas, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="251ff-142">tooconfigure and test Azure AD single sign-on with People, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="251ff-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="251ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="251ff-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="251ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="251ff-145">**[Criar um usuário de teste de pessoas](#creating-a-people-test-user)**  -toohave um equivalente do Britta Simon no pessoas que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="251ff-145">**[Creating a People test user](#creating-a-people-test-user)** - toohave a counterpart of Britta Simon in People that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="251ff-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="251ff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="251ff-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="251ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="251ff-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="251ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="251ff-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de pessoas.</span><span class="sxs-lookup"><span data-stu-id="251ff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="251ff-150">**tooconfigure AD do Azure-logon único com pessoas, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="251ff-150">**tooconfigure Azure AD single sign-on with People, perform hello following steps:**</span></span>

1. <span data-ttu-id="251ff-151">Em Olá portal do Azure, Olá **pessoas** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="251ff-151">In hello Azure portal, on hello **People** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="251ff-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="251ff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="251ff-155">Em Olá **URLs e domínio de pessoas** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="251ff-155">On hello **People Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="251ff-157">a.</span><span class="sxs-lookup"><span data-stu-id="251ff-157">a.</span></span> <span data-ttu-id="251ff-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="251ff-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="251ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="251ff-159">b.</span></span> <span data-ttu-id="251ff-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="251ff-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="251ff-161">c.</span><span class="sxs-lookup"><span data-stu-id="251ff-161">c.</span></span> <span data-ttu-id="251ff-162">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="251ff-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="251ff-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="251ff-163">These values are not real.</span></span> <span data-ttu-id="251ff-164">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="251ff-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="251ff-165">Entre em contato com [equipe de suporte do cliente de pessoas](mailto:customerservices@peoplehr.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="251ff-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) tooget these values.</span></span>

5. <span data-ttu-id="251ff-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="251ff-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="251ff-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="251ff-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="251ff-170">tooget SSO configurado para o seu aplicativo, você precisa de locatário de pessoas em toosign tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="251ff-170">tooget SSO configured for your application, you need toosign-on tooyour People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="251ff-171">No menu de saudação no lado esquerdo da saudação, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="251ff-171">In hello menu on hello left side, click **Settings**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="251ff-173">Clique em **Empresa**.</span><span class="sxs-lookup"><span data-stu-id="251ff-173">Click **Company**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="251ff-175">Em Olá **arquivo de metadados de carregamento 'Single Sign On' SAML**, clique em **procurar** Olá tooupload baixou o arquivo de metadados.</span><span class="sxs-lookup"><span data-stu-id="251ff-175">On hello **Upload 'Single Sign On' SAML meta-data file**, click **Browse** tooupload hello downloaded metadata file.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="251ff-177">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="251ff-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="251ff-178">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="251ff-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="251ff-179">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="251ff-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="251ff-180">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="251ff-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="251ff-181">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="251ff-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="251ff-183">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="251ff-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="251ff-184">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="251ff-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="251ff-186">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="251ff-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="251ff-188">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="251ff-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="251ff-190">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="251ff-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="251ff-192">a.</span><span class="sxs-lookup"><span data-stu-id="251ff-192">a.</span></span> <span data-ttu-id="251ff-193">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="251ff-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="251ff-194">b.</span><span class="sxs-lookup"><span data-stu-id="251ff-194">b.</span></span> <span data-ttu-id="251ff-195">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="251ff-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="251ff-196">c.</span><span class="sxs-lookup"><span data-stu-id="251ff-196">c.</span></span> <span data-ttu-id="251ff-197">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="251ff-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="251ff-198">d.</span><span class="sxs-lookup"><span data-stu-id="251ff-198">d.</span></span> <span data-ttu-id="251ff-199">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="251ff-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="251ff-200">Criação de um usuário de teste do People</span><span class="sxs-lookup"><span data-stu-id="251ff-200">Creating a People test user</span></span>

<span data-ttu-id="251ff-201">Nesta seção, você criará um usuário chamado Brenda Fernandes no People.</span><span class="sxs-lookup"><span data-stu-id="251ff-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="251ff-202">Trabalhar com [equipe de suporte do cliente de pessoas](mailto:customerservices@peoplehr.com) para adicionar usuários de saudação na plataforma de pessoas hello.</span><span class="sxs-lookup"><span data-stu-id="251ff-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add hello users in hello People platform.</span></span> <span data-ttu-id="251ff-203">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="251ff-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="251ff-204">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="251ff-204">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="251ff-205">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPeople.</span><span class="sxs-lookup"><span data-stu-id="251ff-205">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeople.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="251ff-207">**tooassign Britta Simon tooPeople, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="251ff-207">**tooassign Britta Simon tooPeople, perform hello following steps:**</span></span>

1. <span data-ttu-id="251ff-208">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="251ff-208">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="251ff-210">Na lista de aplicativos hello, selecione **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="251ff-210">In hello applications list, select **People**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="251ff-212">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="251ff-212">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="251ff-214">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="251ff-214">Click **Add** button.</span></span> <span data-ttu-id="251ff-215">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="251ff-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="251ff-217">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="251ff-217">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="251ff-218">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="251ff-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="251ff-219">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="251ff-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="251ff-220">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="251ff-220">Testing single sign-on</span></span>

<span data-ttu-id="251ff-221">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="251ff-221">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="251ff-222">Quando você clica em Olá pessoas bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de pessoas.</span><span class="sxs-lookup"><span data-stu-id="251ff-222">When you click hello People tile in hello Access Panel, you should get automatically signed-on tooyour People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="251ff-223">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="251ff-223">Additional resources</span></span>

* [<span data-ttu-id="251ff-224">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="251ff-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="251ff-225">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="251ff-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

