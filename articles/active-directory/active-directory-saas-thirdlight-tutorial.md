---
title: "Tutorial: integração do Azure Active Directory com o ThirdLight | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ThirdLight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a510e514f6a8c4e89220b9a6f6db29668b451b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="13ac7-103">Tutorial: integração do Azure Active Directory com o ThirdLight</span><span class="sxs-lookup"><span data-stu-id="13ac7-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="13ac7-104">Neste tutorial, você aprenderá como toointegrate ThirdLight com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="13ac7-104">In this tutorial, you learn how toointegrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="13ac7-105">Integrando ThirdLight com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="13ac7-105">Integrating ThirdLight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="13ac7-106">Você pode controlar no AD do Azure que tenha acesso tooThirdLight</span><span class="sxs-lookup"><span data-stu-id="13ac7-106">You can control in Azure AD who has access tooThirdLight</span></span>
- <span data-ttu-id="13ac7-107">Você pode habilitar seu usuários tooautomatically get conectado tooThirdLight (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="13ac7-107">You can enable your users tooautomatically get signed-on tooThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="13ac7-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="13ac7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="13ac7-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="13ac7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13ac7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="13ac7-110">Prerequisites</span></span>

<span data-ttu-id="13ac7-111">tooconfigure integração do AD do Azure com ThirdLight, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="13ac7-111">tooconfigure Azure AD integration with ThirdLight, you need hello following items:</span></span>

- <span data-ttu-id="13ac7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="13ac7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="13ac7-113">Uma assinatura habilitada para logon único do ThirdLight</span><span class="sxs-lookup"><span data-stu-id="13ac7-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="13ac7-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="13ac7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="13ac7-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="13ac7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="13ac7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="13ac7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="13ac7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13ac7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="13ac7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="13ac7-118">Scenario description</span></span>
<span data-ttu-id="13ac7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="13ac7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="13ac7-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="13ac7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="13ac7-121">Adicionando ThirdLight da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="13ac7-121">Adding ThirdLight from hello gallery</span></span>
2. <span data-ttu-id="13ac7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="13ac7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-hello-gallery"></a><span data-ttu-id="13ac7-123">Adicionando ThirdLight da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="13ac7-123">Adding ThirdLight from hello gallery</span></span>
<span data-ttu-id="13ac7-124">integração de saudação tooconfigure de ThirdLight no AD do Azure, você precisa tooadd ThirdLight da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="13ac7-124">tooconfigure hello integration of ThirdLight into Azure AD, you need tooadd ThirdLight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="13ac7-125">**tooadd ThirdLight da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="13ac7-125">**tooadd ThirdLight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="13ac7-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="13ac7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="13ac7-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="13ac7-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="13ac7-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="13ac7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="13ac7-133">Na caixa de pesquisa hello, digite **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-133">In hello search box, type **ThirdLight**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="13ac7-135">No painel de resultados de saudação, selecione **ThirdLight**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="13ac7-135">In hello results panel, select **ThirdLight**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="13ac7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="13ac7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="13ac7-138">Nesta seção, você configurará e testará o logon único do Azure AD com o ThirdLight, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="13ac7-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="13ac7-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em ThirdLight é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="13ac7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThirdLight is tooa user in Azure AD.</span></span> <span data-ttu-id="13ac7-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em ThirdLight precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="13ac7-140">In other words, a link relationship between an Azure AD user and hello related user in ThirdLight needs toobe established.</span></span>

<span data-ttu-id="13ac7-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="13ac7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ThirdLight.</span></span>

<span data-ttu-id="13ac7-142">tooconfigure e teste de logon único do AD do Azure com ThirdLight, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="13ac7-142">tooconfigure and test Azure AD single sign-on with ThirdLight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="13ac7-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="13ac7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="13ac7-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13ac7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="13ac7-145">**[Criar um usuário de teste ThirdLight](#creating-a-thirdlight-test-user)**  -toohave um equivalente do Britta Simon em ThirdLight é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="13ac7-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - toohave a counterpart of Britta Simon in ThirdLight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="13ac7-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="13ac7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="13ac7-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="13ac7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="13ac7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="13ac7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="13ac7-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="13ac7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="13ac7-150">**tooconfigure AD do Azure-logon único com ThirdLight, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="13ac7-150">**tooconfigure Azure AD single sign-on with ThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="13ac7-151">Em Olá portal do Azure, Olá **ThirdLight** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-151">In hello Azure portal, on hello **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="13ac7-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="13ac7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="13ac7-155">Em Olá **ThirdLight domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="13ac7-155">On hello **ThirdLight Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="13ac7-157">a.</span><span class="sxs-lookup"><span data-stu-id="13ac7-157">a.</span></span> <span data-ttu-id="13ac7-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="13ac7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="13ac7-159">b.</span><span class="sxs-lookup"><span data-stu-id="13ac7-159">b.</span></span> <span data-ttu-id="13ac7-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="13ac7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="13ac7-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="13ac7-161">These values are not real.</span></span> <span data-ttu-id="13ac7-162">Atualizar esses valores com hello real URL de logon e Identiifer.</span><span class="sxs-lookup"><span data-stu-id="13ac7-162">Update these values with hello actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="13ac7-163">Entre em contato com [equipe de suporte do cliente ThirdLight](https://www.thirdlight.com/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="13ac7-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="13ac7-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="13ac7-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="13ac7-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="13ac7-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="13ac7-168">Em uma janela de navegador web diferente, faça logon no site da empresa ThirdLight tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="13ac7-168">In a different web browser window, log in tooyour ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="13ac7-169">Vá muito**configuração \> administração do sistema**e, em seguida, clique em **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-169">Go too**Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="13ac7-170">![Administração do Sistema](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Administração do Sistema")</span><span class="sxs-lookup"><span data-stu-id="13ac7-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="13ac7-171">Na seção de configuração Olá SAML2, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="13ac7-171">In hello SAML2 configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="13ac7-172">![Logon Único do SAML](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="13ac7-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="13ac7-173">a.</span><span class="sxs-lookup"><span data-stu-id="13ac7-173">a.</span></span> <span data-ttu-id="13ac7-174">Selecione **Habilitar Logon Único do SAML2**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="13ac7-175">b.</span><span class="sxs-lookup"><span data-stu-id="13ac7-175">b.</span></span> <span data-ttu-id="13ac7-176">Como **Fonte de metadados do IdP**, selecione **Carregar Metadados do IdP do XML**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="13ac7-177">c.</span><span class="sxs-lookup"><span data-stu-id="13ac7-177">c.</span></span> <span data-ttu-id="13ac7-178">Abrir o arquivo de metadados de saudação baixado, copie o conteúdo de hello e, em seguida, cole-o em Olá **XML de metadados IdP** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="13ac7-178">Open hello downloaded metadata file, copy hello content, and then paste it into hello **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="13ac7-179">d.</span><span class="sxs-lookup"><span data-stu-id="13ac7-179">d.</span></span> <span data-ttu-id="13ac7-180">Clique em **Salvar configurações do SAML2**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="13ac7-181">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="13ac7-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="13ac7-182">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="13ac7-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="13ac7-183">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="13ac7-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="13ac7-184">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="13ac7-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="13ac7-185">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="13ac7-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="13ac7-187">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="13ac7-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="13ac7-188">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="13ac7-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="13ac7-190">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="13ac7-192">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="13ac7-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="13ac7-194">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="13ac7-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="13ac7-196">a.</span><span class="sxs-lookup"><span data-stu-id="13ac7-196">a.</span></span> <span data-ttu-id="13ac7-197">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="13ac7-198">b.</span><span class="sxs-lookup"><span data-stu-id="13ac7-198">b.</span></span> <span data-ttu-id="13ac7-199">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13ac7-199">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="13ac7-200">c.</span><span class="sxs-lookup"><span data-stu-id="13ac7-200">c.</span></span> <span data-ttu-id="13ac7-201">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="13ac7-202">d.</span><span class="sxs-lookup"><span data-stu-id="13ac7-202">d.</span></span> <span data-ttu-id="13ac7-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="13ac7-204">Criação de um usuário de teste do ThirdLight</span><span class="sxs-lookup"><span data-stu-id="13ac7-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="13ac7-205">tooenable AD do Azure usuários toolog em tooThirdLight, eles devem ser provisionados no ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="13ac7-205">tooenable Azure AD users toolog in tooThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="13ac7-206">No caso de saudação de ThirdLight, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="13ac7-206">In hello case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="13ac7-207">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="13ac7-207">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="13ac7-208">Faça logon no tooyour **ThirdLight** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="13ac7-208">Log in tooyour **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="13ac7-209">Vá muito**usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="13ac7-209">Go too**Users** tab.</span></span>

3. <span data-ttu-id="13ac7-210">Selecione **Usuários e Grupos**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="13ac7-211">Clique no botão **Adicionar novo Usuário** .</span><span class="sxs-lookup"><span data-stu-id="13ac7-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="13ac7-212">Digite **hello nome de usuário, nome ou descrição, Email, escolha uma predefinição ou grupo dos novos membros** de uma conta válida do AAD você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="13ac7-212">Enter **hello Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want tooprovision.</span></span>

6. <span data-ttu-id="13ac7-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="13ac7-214">Você pode usar qualquer ferramenta de criação outros Thirdlight usuário conta ou APIs fornecidas pelo Thirdlight tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="13ac7-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="13ac7-215">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="13ac7-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="13ac7-216">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooThirdLight.</span><span class="sxs-lookup"><span data-stu-id="13ac7-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThirdLight.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="13ac7-218">**tooassign Britta Simon tooThirdLight, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="13ac7-218">**tooassign Britta Simon tooThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="13ac7-219">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="13ac7-221">Na lista de aplicativos hello, selecione **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-221">In hello applications list, select **ThirdLight**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="13ac7-223">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="13ac7-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="13ac7-225">Click **Add** button.</span></span> <span data-ttu-id="13ac7-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="13ac7-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="13ac7-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="13ac7-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="13ac7-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="13ac7-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="13ac7-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="13ac7-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="13ac7-231">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="13ac7-231">Testing single sign-on</span></span>

<span data-ttu-id="13ac7-232">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="13ac7-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="13ac7-233">Quando você clica em bloco ThirdLight Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour ThirdLight aplicativo.</span><span class="sxs-lookup"><span data-stu-id="13ac7-233">When you click hello ThirdLight tile in hello Access Panel, you should get automatically signed-on tooyour ThirdLight application.</span></span>
<span data-ttu-id="13ac7-234">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="13ac7-234">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="13ac7-235">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="13ac7-235">Additional resources</span></span>

* [<span data-ttu-id="13ac7-236">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="13ac7-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13ac7-237">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="13ac7-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

