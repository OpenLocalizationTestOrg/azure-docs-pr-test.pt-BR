---
title: "Tutorial: Integração do Azure Active Directory com o Neota Logic Studio | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Neota lógica Studio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: a479ee49618de8275132dbc2c21a8ef723d92d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="f1a32-103">Tutorial: Integração do Azure Active Directory com o Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="f1a32-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="f1a32-104">Neste tutorial, você aprenderá como toointegrate Neota lógica Studio com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f1a32-104">In this tutorial, you learn how toointegrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1a32-105">Integrando Neota lógica Studio com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1a32-105">Integrating Neota Logic Studio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1a32-106">Você pode controlar no AD do Azure que tenha acesso tooNeota Studio lógica</span><span class="sxs-lookup"><span data-stu-id="f1a32-106">You can control in Azure AD who has access tooNeota Logic Studio</span></span>
- <span data-ttu-id="f1a32-107">Você pode habilitar seu usuários tooautomatically get conectado tooNeota Studio lógica (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a32-107">You can enable your users tooautomatically get signed-on tooNeota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1a32-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a32-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f1a32-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte.</span><span class="sxs-lookup"><span data-stu-id="f1a32-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="f1a32-110">[O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1a32-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1a32-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f1a32-111">Prerequisites</span></span>

<span data-ttu-id="f1a32-112">tooconfigure integração do AD do Azure com Neota lógica Studio, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1a32-112">tooconfigure Azure AD integration with Neota Logic Studio, you need hello following items:</span></span>

- <span data-ttu-id="f1a32-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a32-113">An Azure AD subscription</span></span>
- <span data-ttu-id="f1a32-114">Uma assinatura do Neota Logic Studio habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="f1a32-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1a32-115">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f1a32-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1a32-116">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f1a32-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1a32-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f1a32-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1a32-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1a32-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1a32-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f1a32-119">Scenario description</span></span>

<span data-ttu-id="f1a32-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f1a32-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1a32-121">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="f1a32-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1a32-122">Adicionando Neota lógica Studio da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f1a32-122">Adding Neota Logic Studio from hello gallery</span></span>
2. <span data-ttu-id="f1a32-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a32-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-hello-gallery"></a><span data-ttu-id="f1a32-124">Adicionando Neota lógica Studio da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f1a32-124">Adding Neota Logic Studio from hello gallery</span></span>

<span data-ttu-id="f1a32-125">integração de saudação tooconfigure do Studio de lógica de Neota no AD do Azure, você precisa tooadd Neota lógica Studio na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f1a32-125">tooconfigure hello integration of Neota Logic Studio into Azure AD, you need tooadd Neota Logic Studio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1a32-126">**tooadd Neota lógica Studio da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f1a32-126">**tooadd Neota Logic Studio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1a32-127">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f1a32-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1a32-129">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f1a32-130">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-130">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f1a32-132">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1a32-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f1a32-134">Na caixa de pesquisa hello, digite **Neota lógica Studio**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-134">In hello search box, type **Neota Logic Studio**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="f1a32-136">No painel de resultados de saudação, selecione **Neota lógica Studio**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f1a32-136">In hello results panel, select **Neota Logic Studio**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1a32-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a32-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="f1a32-139">Nesta seção, você configurará e testará o logon único do Azure AD com o Neota Logic Studio, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="f1a32-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f1a32-140">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Studio de lógica de Neota é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a32-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Neota Logic Studio is tooa user in Azure AD.</span></span> <span data-ttu-id="f1a32-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Studio de lógica de Neota precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f1a32-141">In other words, a link relationship between an Azure AD user and hello related user in Neota Logic Studio needs toobe established.</span></span>

<span data-ttu-id="f1a32-142">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Studio de lógica de Neota.</span><span class="sxs-lookup"><span data-stu-id="f1a32-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="f1a32-143">tooconfigure e teste de logon único do AD do Azure com Neota lógica Studio, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1a32-143">tooconfigure and test Azure AD single sign-on with Neota Logic Studio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1a32-144">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f1a32-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1a32-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1a32-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1a32-146">**[Criar um usuário de teste Neota lógica Studio](#creating-a-neota-logic-studio-test-user)**  -toohave um equivalente do Britta Simon no Studio de lógica de Neota é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f1a32-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - toohave a counterpart of Britta Simon in Neota Logic Studio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1a32-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="f1a32-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1a32-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="f1a32-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1a32-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1a32-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1a32-150">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Neota lógica Studio.</span><span class="sxs-lookup"><span data-stu-id="f1a32-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="f1a32-151">**tooconfigure logon único do AD do Azure com Neota lógica Studio, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f1a32-151">**tooconfigure Azure AD single sign-on with Neota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1a32-152">Em Olá portal do Azure, Olá **Neota lógica Studio** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-152">In hello Azure portal, on hello **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f1a32-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="f1a32-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="f1a32-156">Em Olá **Neota lógica Studio domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1a32-156">On hello **Neota Logic Studio Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="f1a32-158">a.</span><span class="sxs-lookup"><span data-stu-id="f1a32-158">a.</span></span> <span data-ttu-id="f1a32-159">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="f1a32-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="f1a32-160">b.</span><span class="sxs-lookup"><span data-stu-id="f1a32-160">b.</span></span> <span data-ttu-id="f1a32-161">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="f1a32-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1a32-162">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="f1a32-162">These values are not hello real.</span></span> <span data-ttu-id="f1a32-163">Atualizar esses valores com hello real & identificador de URL de logon.</span><span class="sxs-lookup"><span data-stu-id="f1a32-163">Update these values with hello actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="f1a32-164">Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a32-164">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="f1a32-165">Entre em contato com [equipe de suporte do cliente do Studio lógica Neota](https://www.neotalogic.com/contact-us/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="f1a32-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="f1a32-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f1a32-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="f1a32-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f1a32-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f1a32-170">tooget SSO configurado para o seu aplicativo, entre em contato com [suporte Neota lógica Studio](https://www.neotalogic.com/contact-us/) da equipe e fornecê-los com baixado **Metadata XML** arquivo.</span><span class="sxs-lookup"><span data-stu-id="f1a32-170">tooget SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="f1a32-171">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="f1a32-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f1a32-172">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a32-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f1a32-173">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1a32-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1a32-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a32-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1a32-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a32-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f1a32-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f1a32-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1a32-178">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f1a32-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1a32-180">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1a32-182">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a32-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1a32-184">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1a32-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1a32-186">a.</span><span class="sxs-lookup"><span data-stu-id="f1a32-186">a.</span></span> <span data-ttu-id="f1a32-187">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1a32-188">b.</span><span class="sxs-lookup"><span data-stu-id="f1a32-188">b.</span></span> <span data-ttu-id="f1a32-189">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1a32-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1a32-190">c.</span><span class="sxs-lookup"><span data-stu-id="f1a32-190">c.</span></span> <span data-ttu-id="f1a32-191">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f1a32-192">d.</span><span class="sxs-lookup"><span data-stu-id="f1a32-192">d.</span></span> <span data-ttu-id="f1a32-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="f1a32-194">Criar um usuário de teste do Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="f1a32-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="f1a32-195">Nesta seção, você criará um usuário chamado Brenda Fernandes no Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="f1a32-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="f1a32-196">trabalhar com [a equipe de suporte Neota lógica Studio cliente](https://www.neotalogic.com/contact-us/) para adicionar usuários de saudação na plataforma de Neota lógica Studio hello.</span><span class="sxs-lookup"><span data-stu-id="f1a32-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add hello users in hello Neota Logic Studio platform.</span></span> <span data-ttu-id="f1a32-197">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="f1a32-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f1a32-198">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a32-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f1a32-199">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooNeota Studio lógica.</span><span class="sxs-lookup"><span data-stu-id="f1a32-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNeota Logic Studio.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f1a32-201">**tooassign Britta Simon tooNeota Studio lógica, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f1a32-201">**tooassign Britta Simon tooNeota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1a32-202">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f1a32-204">Na lista de aplicativos hello, selecione **Neota lógica Studio**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-204">In hello applications list, select **Neota Logic Studio**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="f1a32-206">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f1a32-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f1a32-208">Click **Add** button.</span></span> <span data-ttu-id="f1a32-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1a32-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f1a32-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a32-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f1a32-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1a32-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1a32-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1a32-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1a32-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f1a32-214">Testing single sign-on</span></span>

<span data-ttu-id="f1a32-215">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a32-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f1a32-216">Clique em bloco de Neota lógica Studio Olá Olá painel de acesso, será redirecionado tooOrganization logon na página.</span><span class="sxs-lookup"><span data-stu-id="f1a32-216">Click hello Neota Logic Studio tile in hello Access Panel, you will be redirected tooOrganization sign-on page.</span></span> <span data-ttu-id="f1a32-217">Após o logon bem-sucedido, você será conectado tooyour aplicativo Neota lógica Studio.</span><span class="sxs-lookup"><span data-stu-id="f1a32-217">After successful login, you will be signed-on tooyour Neota Logic Studio application.</span></span> <span data-ttu-id="f1a32-218">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="f1a32-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="f1a32-219">Para obter mais informações sobre Olá painel de acesso, consulte [Introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="f1a32-219">For more information about hello Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f1a32-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f1a32-220">Additional resources</span></span>

* [<span data-ttu-id="f1a32-221">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a32-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1a32-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1a32-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

