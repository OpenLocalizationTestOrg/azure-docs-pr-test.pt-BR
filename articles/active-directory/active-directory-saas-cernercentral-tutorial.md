---
title: "Tutorial: integração do Azure Active Directory ao Cerner Central | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Cerner Central."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="81505-103">Tutorial: integração do Azure Active Directory ao Cerner Central</span><span class="sxs-lookup"><span data-stu-id="81505-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="81505-104">Neste tutorial, você aprenderá como toointegrate Cerner Central com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="81505-104">In this tutorial, you learn how toointegrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81505-105">Integrando Cerner Central com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="81505-105">Integrating Cerner Central with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="81505-106">Você pode controlar no AD do Azure que tenha acesso tooCerner Central</span><span class="sxs-lookup"><span data-stu-id="81505-106">You can control in Azure AD who has access tooCerner Central</span></span>
- <span data-ttu-id="81505-107">Você pode habilitar seu usuários tooautomatically get conectado tooCerner Central (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="81505-107">You can enable your users tooautomatically get signed-on tooCerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81505-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="81505-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="81505-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81505-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81505-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="81505-110">Prerequisites</span></span>

<span data-ttu-id="81505-111">tooconfigure integração do AD do Azure com Cerner Central, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="81505-111">tooconfigure Azure AD integration with Cerner Central, you need hello following items:</span></span>

- <span data-ttu-id="81505-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="81505-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81505-113">Uma Conta Sistema aprovada do Cerner Central</span><span class="sxs-lookup"><span data-stu-id="81505-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="81505-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="81505-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81505-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="81505-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81505-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="81505-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81505-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81505-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81505-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="81505-118">Scenario description</span></span>
<span data-ttu-id="81505-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="81505-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81505-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="81505-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81505-121">Adicionando Cerner Central da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="81505-121">Adding Cerner Central from hello gallery</span></span>
2. <span data-ttu-id="81505-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="81505-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-hello-gallery"></a><span data-ttu-id="81505-123">Adicionando Cerner Central da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="81505-123">Adding Cerner Central from hello gallery</span></span>
<span data-ttu-id="81505-124">integração de Olá tooconfigure do Cerner Central no AD do Azure, você precisa tooadd Cerner Central na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="81505-124">tooconfigure hello integration of Cerner Central into Azure AD, you need tooadd Cerner Central from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="81505-125">**tooadd Cerner Central da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="81505-125">**tooadd Cerner Central from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="81505-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="81505-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81505-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="81505-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="81505-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="81505-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="81505-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="81505-131">tooadd new application, click **New application** button on top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="81505-133">Na caixa de pesquisa hello, digite **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="81505-133">In hello search box, type **Cerner Central**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="81505-135">No painel de resultados de saudação, selecione **Cerner Central**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="81505-135">In hello results panel, select **Cerner Central**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81505-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="81505-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81505-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Cerner Central, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="81505-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="81505-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Centro de Cerner é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="81505-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cerner Central is tooa user in Azure AD.</span></span> <span data-ttu-id="81505-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Centro de Cerner precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="81505-140">In other words, a link relationship between an Azure AD user and hello related user in Cerner Central needs toobe established.</span></span>

<span data-ttu-id="81505-141">tooconfigure e teste de logon único do AD do Azure com Cerner Central, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="81505-141">tooconfigure and test Azure AD single sign-on with Cerner Central, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="81505-142">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="81505-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="81505-143">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81505-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81505-144">**[Criar um usuário de teste Cerner Central](#creating-a-cerner-central-test-user)**  -toohave um equivalente do Britta Simon no centro Cerner que é vinculado toohello AD do Azure representação do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="81505-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - toohave a counterpart of Britta Simon in Cerner Central that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="81505-145">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="81505-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81505-146">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="81505-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81505-147">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="81505-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81505-148">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="81505-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="81505-149">**tooconfigure AD do Azure-logon único com Cerner Central, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="81505-149">**tooconfigure Azure AD single sign-on with Cerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="81505-150">Em Olá portal do Azure, Olá **Cerner Central** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="81505-150">In hello Azure portal, on hello **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="81505-152">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="81505-152">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="81505-154">Em Olá **domínio Central Cerner e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="81505-154">On hello **Cerner Central Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="81505-156">a.</span><span class="sxs-lookup"><span data-stu-id="81505-156">a.</span></span> <span data-ttu-id="81505-157">Em Olá **identificador** texto, o valor do tipo hello usando Olá padrões a seguir:</span><span class="sxs-lookup"><span data-stu-id="81505-157">In hello **Identifier** textbox, type hello value using hello following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="81505-158">b.</span><span class="sxs-lookup"><span data-stu-id="81505-158">b.</span></span> <span data-ttu-id="81505-159">Em Olá **URL de resposta** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="81505-159">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="81505-160">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="81505-160">These values are not hello real.</span></span> <span data-ttu-id="81505-161">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="81505-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="81505-162">Entre em contato com [equipe de suporte do Centro de Cerner](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="81505-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget these values.</span></span>
 
4. <span data-ttu-id="81505-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="81505-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="81505-165">Olá toogenerate **metadados** url, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="81505-165">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="81505-166">a.</span><span class="sxs-lookup"><span data-stu-id="81505-166">a.</span></span> <span data-ttu-id="81505-167">Clique em **Registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="81505-167">Click **App registrations**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="81505-169">b.</span><span class="sxs-lookup"><span data-stu-id="81505-169">b.</span></span> <span data-ttu-id="81505-170">Clique em **pontos de extremidade** tooopen **pontos de extremidade** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81505-170">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="81505-172">c.</span><span class="sxs-lookup"><span data-stu-id="81505-172">c.</span></span> <span data-ttu-id="81505-173">Clique em Olá cópia botão toocopy **documento de METADADOS de Federação** url e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="81505-173">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="81505-175">d.</span><span class="sxs-lookup"><span data-stu-id="81505-175">d.</span></span> <span data-ttu-id="81505-176">Agora vá toohello a página de propriedades de **Cerner Central** e cópia hello **Id do aplicativo** usando **cópia** botão e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="81505-176">Now go toohello property page of **Cerner Central** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="81505-178">e.</span><span class="sxs-lookup"><span data-stu-id="81505-178">e.</span></span> <span data-ttu-id="81505-179">Gerar Olá **URL de metadados** usando saudação padrão a seguir:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="81505-179">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="81505-180">tooconfigure logon único no **Cerner Central** lado, você precisa Olá toosend **URL de metadados** muito[suporte Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="81505-180">tooconfigure single sign-on on **Cerner Central** side, you need toosend hello **Metadata URL** too[Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="81505-181">Eles configurar Olá SSO lado toocomplete saudação à integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="81505-181">They configure hello SSO on application side toocomplete hello integration.</span></span>

> [!TIP]
> <span data-ttu-id="81505-182">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="81505-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="81505-183">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="81505-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="81505-184">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81505-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81505-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="81505-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="81505-186">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="81505-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span> 

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="81505-188">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="81505-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="81505-189">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="81505-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81505-191">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="81505-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81505-193">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="81505-193">tooopen hello **User** dialog, click **Add**.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81505-195">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="81505-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81505-197">a.</span><span class="sxs-lookup"><span data-stu-id="81505-197">a.</span></span> <span data-ttu-id="81505-198">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81505-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81505-199">b.</span><span class="sxs-lookup"><span data-stu-id="81505-199">b.</span></span> <span data-ttu-id="81505-200">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81505-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="81505-201">c.</span><span class="sxs-lookup"><span data-stu-id="81505-201">c.</span></span> <span data-ttu-id="81505-202">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="81505-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="81505-203">d.</span><span class="sxs-lookup"><span data-stu-id="81505-203">d.</span></span> <span data-ttu-id="81505-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="81505-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="81505-205">Criar um usuário de teste do Cerner Central</span><span class="sxs-lookup"><span data-stu-id="81505-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="81505-206">O aplicativo **Cerner Central** permite a autenticação por meio de qualquer provedor de identidade federada.</span><span class="sxs-lookup"><span data-stu-id="81505-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="81505-207">Se um usuário é capaz de toolog na home page do aplicativo toohello, eles são agrupados e não precisam de nenhum provisionamento manual.</span><span class="sxs-lookup"><span data-stu-id="81505-207">If a user is able toolog in toohello application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="81505-208">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="81505-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="81505-209">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCerner Central.</span><span class="sxs-lookup"><span data-stu-id="81505-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCerner Central.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="81505-211">**tooassign Britta Simon tooCerner Central, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="81505-211">**tooassign Britta Simon tooCerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="81505-212">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="81505-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="81505-214">Na lista de aplicativos hello, selecione **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="81505-214">In hello applications list, select **Cerner Central**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="81505-216">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="81505-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="81505-218">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="81505-218">Click **Add** button.</span></span> <span data-ttu-id="81505-219">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81505-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="81505-221">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="81505-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="81505-222">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81505-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81505-223">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81505-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81505-224">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="81505-224">Testing single sign-on</span></span>

<span data-ttu-id="81505-225">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="81505-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="81505-226">Quando você clica em Olá Cerner Central bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="81505-226">When you click hello Cerner Central tile in hello Access Panel, you should get automatically signed-on tooyour Cerner Central application.</span></span> <span data-ttu-id="81505-227">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="81505-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81505-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="81505-228">Additional resources</span></span>

* [<span data-ttu-id="81505-229">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="81505-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81505-230">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81505-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

