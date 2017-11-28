---
title: "Tutorial: integração do Azure Active Directory ao T&E Express | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e T & E Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="0c8ee-103">Tutorial: integração do Azure Active Directory com o T&E Express</span><span class="sxs-lookup"><span data-stu-id="0c8ee-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="0c8ee-104">Neste tutorial, você aprenderá como toointegrate T & E Express com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="0c8ee-104">In this tutorial, you learn how toointegrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0c8ee-105">Integrando T & E Express com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c8ee-105">Integrating T&E Express with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0c8ee-106">Você pode controlar no AD do Azure que tenha tooT acesso & E Express</span><span class="sxs-lookup"><span data-stu-id="0c8ee-106">You can control in Azure AD who has access tooT&E Express</span></span>
- <span data-ttu-id="0c8ee-107">Você pode habilitar seus usuários tooautomatically get conectado tooT & E Express (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0c8ee-107">You can enable your users tooautomatically get signed-on tooT&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0c8ee-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="0c8ee-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="0c8ee-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0c8ee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c8ee-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0c8ee-110">Prerequisites</span></span>

<span data-ttu-id="0c8ee-111">tooconfigure integração do AD do Azure com T & E Express, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c8ee-111">tooconfigure Azure AD integration with T&E Express, you need hello following items:</span></span>

- <span data-ttu-id="0c8ee-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0c8ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0c8ee-113">Uma assinatura habilitada para logon único do T&E Express</span><span class="sxs-lookup"><span data-stu-id="0c8ee-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0c8ee-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0c8ee-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0c8ee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0c8ee-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0c8ee-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c8ee-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0c8ee-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0c8ee-118">Scenario description</span></span>
<span data-ttu-id="0c8ee-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0c8ee-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="0c8ee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0c8ee-121">Adicionando T & E Express da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0c8ee-121">Adding T&E Express from hello gallery</span></span>
2. <span data-ttu-id="0c8ee-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0c8ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-hello-gallery"></a><span data-ttu-id="0c8ee-123">Adicionando T & E Express da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0c8ee-123">Adding T&E Express from hello gallery</span></span>
<span data-ttu-id="0c8ee-124">integração de saudação tooconfigure de T & E Express no AD do Azure, você precisa tooadd T & E Express na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-124">tooconfigure hello integration of T&E Express into Azure AD, you need tooadd T&E Express from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0c8ee-125">**tooadd T & E Express da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0c8ee-125">**tooadd T&E Express from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c8ee-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0c8ee-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0c8ee-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0c8ee-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0c8ee-133">Na caixa de pesquisa hello, digite **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-133">In hello search box, type **T&E Express**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="0c8ee-135">No painel de resultados de saudação, selecione **T & E Express**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-135">In hello results panel, select **T&E Express**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0c8ee-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0c8ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0c8ee-138">Nesta seção, você configurará e testará o logon único do Azure AD com o T&E Express, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0c8ee-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá T & E Express é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in T&E Express is tooa user in Azure AD.</span></span> <span data-ttu-id="0c8ee-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em T & E Express toobe necessidades estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-140">In other words, a link relationship between an Azure AD user and hello related user in T&E Express needs toobe established.</span></span>

<span data-ttu-id="0c8ee-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em T & E Express.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in T&E Express.</span></span>

<span data-ttu-id="0c8ee-142">tooconfigure e teste de logon único do AD do Azure com T & E Express, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c8ee-142">tooconfigure and test Azure AD single sign-on with T&E Express, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0c8ee-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0c8ee-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0c8ee-145">**[Criar um usuário de teste T & E Express](#creating-a-te-express-test-user)**  -toohave um equivalente do Britta Simon T & E Express que é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - toohave a counterpart of Britta Simon in T&E Express that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="0c8ee-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0c8ee-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0c8ee-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c8ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0c8ee-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único em seu aplicativo T & E Express.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="0c8ee-150">**tooconfigure logon único do AD do Azure com T & E Express, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0c8ee-150">**tooconfigure Azure AD single sign-on with T&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c8ee-151">No portal de gerenciamento do Azure do hello, no hello **T & E Express** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-151">In hello Azure Management portal, on hello **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0c8ee-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="0c8ee-155">Em Olá **T & E Express domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c8ee-155">On hello **T&E Express Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="0c8ee-157">a.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-157">a.</span></span> <span data-ttu-id="0c8ee-158">Em Olá **identificador** texto, o valor do tipo hello como:`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="0c8ee-158">In hello **Identifier** textbox, type hello value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="0c8ee-159">b.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-159">b.</span></span> <span data-ttu-id="0c8ee-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="0c8ee-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0c8ee-161">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="0c8ee-162">Você tem tooupdate esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="0c8ee-163">Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="0c8ee-164">Entre em contato com [equipe de suporte de T & E Express](http://www.tyeexpress.com/contacto.aspx) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) tooget these values.</span></span>

5. <span data-ttu-id="0c8ee-165">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="0c8ee-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0c8ee-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0c8ee-169">tooconfigure logon único no **T & E Express** lado, logon toohello T & aplicativo express E sem SAML único logon usando credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-169">tooconfigure single sign-on on **T&E Express** side, login toohello T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="0c8ee-170">Em Olá **Admin** guia, clique em **domínio SAML** página de configurações do tooOpen Olá SAML.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-170">Under hello **Admin** Tab, Click on **SAML domain** tooOpen hello SAML settings page.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="0c8ee-172">Selecione Olá **Activar(Activate)** opção **não** muito**SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-172">Select hello **Activar(Activate)** option from **No** too**SI(Yes)**.</span></span> <span data-ttu-id="0c8ee-173">Em Olá **metadados do provedor de identidade** caixa de texto, colar Olá metadados XML que você tiver donwloaded do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-173">In hello **Identity Provider Metadata** textbox, paste hello metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="0c8ee-175">Clique em Olá **Guardar(Save)** botão Configurações de saudação toosave.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-175">Click on hello **Guardar(Save)** button toosave hello settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0c8ee-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0c8ee-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="0c8ee-177">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0c8ee-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0c8ee-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c8ee-180">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0c8ee-182">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0c8ee-184">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0c8ee-186">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c8ee-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0c8ee-188">a.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-188">a.</span></span> <span data-ttu-id="0c8ee-189">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0c8ee-190">b.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-190">b.</span></span> <span data-ttu-id="0c8ee-191">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0c8ee-192">c.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-192">c.</span></span> <span data-ttu-id="0c8ee-193">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0c8ee-194">d.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-194">d.</span></span> <span data-ttu-id="0c8ee-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="0c8ee-196">Criar um usuário de teste do T&E Express</span><span class="sxs-lookup"><span data-stu-id="0c8ee-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="0c8ee-197">Em ordem tooenable AD do Azure usuários toolog em T & E Express, eles devem ser provisionados no T & E Express.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-197">In order tooenable Azure AD users toolog into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="0c8ee-198">No caso do T&E Express, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="0c8ee-199">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0c8ee-199">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c8ee-200">Faça logon tooyour T & E Express site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-200">Log in tooyour T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="0c8ee-201">Na marca de administração, clique em página mestra a usuários tooopen Olá para os usuários.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-201">Under Admin tag, click on Users tooopen hello Users master page.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="0c8ee-203">Na home page do hello, clique em  **+**  tooadd usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-203">On hello home page, click on **+** tooadd hello users.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="0c8ee-205">Insira todos os detalhes de obrigatório Olá conforme solicitado no formulário hello e clique em Olá Salvar botão toosave Olá detalhes.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-205">Enter all hello mandatory details as asked in hello form and click hello save button toosave hello details.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0c8ee-208">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0c8ee-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0c8ee-209">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure concedendo sua tooT acesso & E Express.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooT&E Express.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0c8ee-211">**tooassign tooT Britta Simon & E Express, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0c8ee-211">**tooassign Britta Simon tooT&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c8ee-212">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-212">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0c8ee-214">Na lista de aplicativos hello, selecione **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-214">In hello applications list, select **T&E Express**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="0c8ee-216">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0c8ee-218">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-218">Click **Add** button.</span></span> <span data-ttu-id="0c8ee-219">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0c8ee-221">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0c8ee-222">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0c8ee-223">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0c8ee-224">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0c8ee-224">Testing single sign-on</span></span>

<span data-ttu-id="0c8ee-225">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0c8ee-226">Quando você clica em Olá T & E Express lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour T & Express E aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0c8ee-226">When you click hello T&E Express tile in hello Access Panel, you should get automatically signed-on tooyour T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0c8ee-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0c8ee-227">Additional resources</span></span>

* [<span data-ttu-id="0c8ee-228">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0c8ee-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0c8ee-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0c8ee-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

