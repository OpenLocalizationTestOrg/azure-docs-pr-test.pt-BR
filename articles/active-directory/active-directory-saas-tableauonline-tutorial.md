---
title: "Tutorial: Integração do Azure Active Directory com o Tableau Online | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Tableau Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="2f5fd-103">Tutorial: Integração do Azure Active Directory com o Tableau Online</span><span class="sxs-lookup"><span data-stu-id="2f5fd-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="2f5fd-104">Neste tutorial, você aprenderá como toointegrate Tableau Online com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="2f5fd-104">In this tutorial, you learn how toointegrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f5fd-105">Integrando Tableau Online com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f5fd-105">Integrating Tableau Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2f5fd-106">Você pode controlar no AD do Azure que tenha acesso tooTableau Online</span><span class="sxs-lookup"><span data-stu-id="2f5fd-106">You can control in Azure AD who has access tooTableau Online</span></span>
- <span data-ttu-id="2f5fd-107">Você pode habilitar seu usuários tooautomatically get conectado tooTableau on-line (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f5fd-107">You can enable your users tooautomatically get signed-on tooTableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f5fd-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2f5fd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2f5fd-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f5fd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f5fd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2f5fd-110">Prerequisites</span></span>

<span data-ttu-id="2f5fd-111">tooconfigure integração do AD do Azure com Tableau Online, você precisará Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f5fd-111">tooconfigure Azure AD integration with Tableau Online, you need hello following items:</span></span>

- <span data-ttu-id="2f5fd-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f5fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f5fd-113">Uma assinatura habilitada para logon único do Tableau Online</span><span class="sxs-lookup"><span data-stu-id="2f5fd-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f5fd-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f5fd-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2f5fd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f5fd-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f5fd-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f5fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f5fd-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2f5fd-118">Scenario description</span></span>
<span data-ttu-id="2f5fd-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f5fd-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="2f5fd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f5fd-121">Adicionando Tableau Online da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2f5fd-121">Adding Tableau Online from hello gallery</span></span>
2. <span data-ttu-id="2f5fd-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f5fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-hello-gallery"></a><span data-ttu-id="2f5fd-123">Adicionando Tableau Online da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2f5fd-123">Adding Tableau Online from hello gallery</span></span>
<span data-ttu-id="2f5fd-124">integração de saudação tooconfigure do Tableau Online no AD do Azure, você precisa tooadd Tableau Online na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-124">tooconfigure hello integration of Tableau Online into Azure AD, you need tooadd Tableau Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2f5fd-125">**tooadd Tableau on-line da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f5fd-125">**tooadd Tableau Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f5fd-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f5fd-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2f5fd-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="2f5fd-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="2f5fd-133">Na caixa de pesquisa hello, digite **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-133">In hello search box, type **Tableau Online**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="2f5fd-135">No painel de resultados de saudação, selecione **Tableau Online**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-135">In hello results panel, select **Tableau Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f5fd-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f5fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f5fd-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Tableau Online, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2f5fd-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Tableau Online é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Online is tooa user in Azure AD.</span></span> <span data-ttu-id="2f5fd-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Tableau Online precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Online needs toobe established.</span></span>

<span data-ttu-id="2f5fd-141">Tableau Online, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-141">In Tableau Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2f5fd-142">tooconfigure e teste de logon único do AD do Azure com Tableau Online, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f5fd-142">tooconfigure and test Azure AD single sign-on with Tableau Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2f5fd-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2f5fd-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f5fd-145">**[Criar um usuário de teste Online Tableau](#creating-a-tableau-online-test-user)**  -toohave um equivalente do Britta Simon em Tableau Online que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - toohave a counterpart of Britta Simon in Tableau Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f5fd-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f5fd-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f5fd-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f5fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f5fd-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="2f5fd-150">**tooconfigure AD do Azure-logon único com Tableau Online, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f5fd-150">**tooconfigure Azure AD single sign-on with Tableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f5fd-151">Em Olá portal do Azure, Olá **Tableau Online** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-151">In hello Azure portal, on hello **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2f5fd-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="2f5fd-155">Em Olá **URLs e domínio Online Tableau** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f5fd-155">On hello **Tableau Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="2f5fd-157">a.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-157">a.</span></span> <span data-ttu-id="2f5fd-158">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="2f5fd-158">In hello **Sign-on URL** textbox, type hello URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="2f5fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-159">b.</span></span> <span data-ttu-id="2f5fd-160">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="2f5fd-160">In hello **Identifier** textbox, type hello URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="2f5fd-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="2f5fd-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2f5fd-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2f5fd-165">Em uma janela de navegador diferente, logon tooyour aplicativo Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-165">In a different browser window, sign-on tooyour Tableau Online application.</span></span> <span data-ttu-id="2f5fd-166">Vá muito**configurações** e **autenticação**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-166">Go too**Settings** and then **Authentication**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="2f5fd-168">tooenable SAML, em **tipos de autenticação** seção.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-168">tooenable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="2f5fd-169">Verificar Olá **logon único com SAML** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-169">Check hello **Single sign-on with SAML** checkbox.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="2f5fd-171">Role para baixo até a seção **Import metadata file into Tableau Online** .</span><span class="sxs-lookup"><span data-stu-id="2f5fd-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="2f5fd-172">Clique em Procurar e importe o arquivo de metadados de saudação que baixou do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-172">Click Browse and import hello metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="2f5fd-173">Em seguida, clique em **Apply**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-173">Then, click **Apply**.</span></span>
   
   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="2f5fd-175">Em Olá **corresponder asserções** seção, insira o nome asserção provedor de identidade de saudação correspondente para **endereço de email**, **nome**, e **sobrenome** .</span><span class="sxs-lookup"><span data-stu-id="2f5fd-175">In hello **Match assertions** section, insert hello corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="2f5fd-176">tooget essas informações do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="2f5fd-176">tooget this information from Azure AD:</span></span> 
  
    <span data-ttu-id="2f5fd-177">a.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-177">a.</span></span> <span data-ttu-id="2f5fd-178">No hello portal do Azure, vá Olá **Tableau Online** página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-178">In hello Azure portal, go on hello **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="2f5fd-179">b.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-179">b.</span></span> <span data-ttu-id="2f5fd-180">Na seção de atributos de saudação, selecione Olá **"Exibir e editar todos os outros atributos de usuário"** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-180">In hello attributes section, Select hello **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="2f5fd-182">c.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-182">c.</span></span> <span data-ttu-id="2f5fd-183">Copie o valor do namespace Olá para esses atributos: givenname, email e sobrenome usando Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2f5fd-183">Copy hello namespace value for these attributes: givenname, email and surname by using hello following steps:</span></span>

   ![Logon Único do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="2f5fd-185">d.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-185">d.</span></span> <span data-ttu-id="2f5fd-186">Clique no valor **user.givenname**</span><span class="sxs-lookup"><span data-stu-id="2f5fd-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="2f5fd-187">e.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-187">e.</span></span> <span data-ttu-id="2f5fd-188">Copie o valor de saudação da saudação **namespace** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-188">Copy hello value from hello **namespace** textbox.</span></span>

   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="2f5fd-190">f.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-190">f.</span></span> <span data-ttu-id="2f5fd-191">valores de namesapce toocopy Olá para email hello e sobrenome siga Olá etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-191">toocopy hello namesapce values for hello email and surname follow hello preceding steps.</span></span>

    <span data-ttu-id="2f5fd-192">g.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-192">g.</span></span> <span data-ttu-id="2f5fd-193">Alternar aplicativo Online Tableau toohello, então, configurar Olá **atributos Online Tableau** seção da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="2f5fd-193">Switch toohello Tableau Online application, then set hello **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="2f5fd-194">Email: **mail** ou **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="2f5fd-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="2f5fd-195">Nome: **givenname**</span><span class="sxs-lookup"><span data-stu-id="2f5fd-195">First name: **givenname**</span></span>
     * <span data-ttu-id="2f5fd-196">Sobrenome: **surname**</span><span class="sxs-lookup"><span data-stu-id="2f5fd-196">Last name: **surname**</span></span>
   
   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="2f5fd-198">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="2f5fd-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2f5fd-199">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2f5fd-200">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f5fd-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f5fd-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f5fd-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f5fd-202">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="2f5fd-204">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f5fd-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f5fd-205">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f5fd-207">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f5fd-209">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f5fd-211">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f5fd-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f5fd-213">a.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-213">a.</span></span> <span data-ttu-id="2f5fd-214">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f5fd-215">b.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-215">b.</span></span> <span data-ttu-id="2f5fd-216">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f5fd-217">c.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-217">c.</span></span> <span data-ttu-id="2f5fd-218">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2f5fd-219">d.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-219">d.</span></span> <span data-ttu-id="2f5fd-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="2f5fd-221">Criação de um usuário de teste do Tableau Online</span><span class="sxs-lookup"><span data-stu-id="2f5fd-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="2f5fd-222">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="2f5fd-223">No **Tableau Online**, clique em **Configurações** e na seção **Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="2f5fd-224">Role para baixo demais**selecionar usuários** seção.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-224">Scroll down too**Select Users** section.</span></span> <span data-ttu-id="2f5fd-225">Clique em **Adicionar Usuários** e em **Inserir Endereços de Email**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="2f5fd-227">Selecione **Adicionar usuários para autenticação de logon único (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="2f5fd-228">Em Olá **insira endereços de Email** Adicionar caixa de textobritta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="2f5fd-228">In hello **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="2f5fd-230">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-230">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2f5fd-231">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f5fd-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2f5fd-232">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTableau on-line.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Online.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="2f5fd-234">**tooassign Britta Simon tooTableau Online, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f5fd-234">**tooassign Britta Simon tooTableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f5fd-235">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2f5fd-237">Na lista de aplicativos hello, selecione **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-237">In hello applications list, select **Tableau Online**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="2f5fd-239">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="2f5fd-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-241">Click **Add** button.</span></span> <span data-ttu-id="2f5fd-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="2f5fd-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2f5fd-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f5fd-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f5fd-247">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="2f5fd-247">Testing single sign-on</span></span>

<span data-ttu-id="2f5fd-248">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="2f5fd-249">Quando você clica em bloco Tableau Online Olá Olá painel de acesso, você deve obter aplicativo Tableau Online automaticamente assinado em tooyour.</span><span class="sxs-lookup"><span data-stu-id="2f5fd-249">When you click hello Tableau Online tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f5fd-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2f5fd-250">Additional resources</span></span>

* [<span data-ttu-id="2f5fd-251">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2f5fd-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f5fd-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f5fd-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

