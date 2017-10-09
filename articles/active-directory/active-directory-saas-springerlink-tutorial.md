---
title: "Tutorial: Integração do Azure Active Directory ao Springer Link | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Springer Link."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: dabd2f72b3a195fc359826a4863a197e5019f5c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="2dd8b-103">Tutorial: Integração do Azure Active Directory ao Springer Link</span><span class="sxs-lookup"><span data-stu-id="2dd8b-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="2dd8b-104">Neste tutorial, você aprenderá como toointegrate Springer vincular com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="2dd8b-104">In this tutorial, you learn how toointegrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2dd8b-105">Integrando Springer Link com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dd8b-105">Integrating Springer Link with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2dd8b-106">Você pode controlar no AD do Azure que tenha acesso tooSpringer Link.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-106">You can control in Azure AD who has access tooSpringer Link.</span></span>
- <span data-ttu-id="2dd8b-107">Você pode habilitar seu usuários tooautomatically get conectado tooSpringer Link (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-107">You can enable your users tooautomatically get signed-on tooSpringer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2dd8b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="2dd8b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2dd8b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2dd8b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2dd8b-110">Prerequisites</span></span>

<span data-ttu-id="2dd8b-111">tooconfigure integração do AD do Azure com Springer Link, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dd8b-111">tooconfigure Azure AD integration with Springer Link, you need hello following items:</span></span>

- <span data-ttu-id="2dd8b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2dd8b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2dd8b-113">Uma assinatura do Springer Link habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="2dd8b-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2dd8b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2dd8b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2dd8b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2dd8b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2dd8b-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2dd8b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2dd8b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2dd8b-118">Scenario description</span></span>
<span data-ttu-id="2dd8b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2dd8b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="2dd8b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2dd8b-121">Adicionar Link Springer da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2dd8b-121">Adding Springer Link from hello gallery</span></span>
2. <span data-ttu-id="2dd8b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2dd8b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-hello-gallery"></a><span data-ttu-id="2dd8b-123">Adicionar Link Springer da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2dd8b-123">Adding Springer Link from hello gallery</span></span>
<span data-ttu-id="2dd8b-124">integração de Olá tooconfigure de Link Springer no AD do Azure, você precisa tooadd Springer Link na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-124">tooconfigure hello integration of Springer Link into Azure AD, you need tooadd Springer Link from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2dd8b-125">**tooadd Springer Link da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2dd8b-125">**tooadd Springer Link from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2dd8b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="2dd8b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2dd8b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="2dd8b-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="2dd8b-133">Na caixa de pesquisa hello, digite **Springer Link**, selecione **Springer Link** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-133">In hello search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Link Springer na lista de resultados de saudação](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2dd8b-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dd8b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2dd8b-136">Nesta seção, você configura e testa o logon único do Azure AD com o Springer Link, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2dd8b-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá Springer link é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Springer Link is tooa user in Azure AD.</span></span> <span data-ttu-id="2dd8b-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Link Springer precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-138">In other words, a link relationship between an Azure AD user and hello related user in Springer Link needs toobe established.</span></span>

<span data-ttu-id="2dd8b-139">No Link Springer, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-139">In Springer Link, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2dd8b-140">tooconfigure e teste de logon único do AD do Azure com Springer Link, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dd8b-140">tooconfigure and test Azure AD single sign-on with Springer Link, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2dd8b-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2dd8b-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2dd8b-143">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="2dd8b-144">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-144">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2dd8b-145">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dd8b-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2dd8b-146">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Springer Link.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-146">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="2dd8b-147">**tooconfigure AD do Azure-logon único com Link Springer, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2dd8b-147">**tooconfigure Azure AD single sign-on with Springer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="2dd8b-148">Em Olá portal do Azure, Olá **Springer Link** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-148">In hello Azure portal, on hello **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="2dd8b-150">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-150">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="2dd8b-152">Em Olá **Springer Link domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="2dd8b-152">On hello **Springer Link Domain and URLs** section,  If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Informações de logon único em Domínio e URLs do Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="2dd8b-154">a.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-154">a.</span></span> <span data-ttu-id="2dd8b-155">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="2dd8b-155">In hello **Identifier** textbox, type hello URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="2dd8b-156">b.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-156">b.</span></span> <span data-ttu-id="2dd8b-157">Em Olá **URL de resposta** caixa de texto, digite a URL de saudação:`https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="2dd8b-157">In hello **Reply URL** textbox, type hello URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="2dd8b-158">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2dd8b-159">Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="2dd8b-159">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informações de logon único em Domínio e URLs do Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="2dd8b-161">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="2dd8b-161">In hello **Sign-on URL** textbox, type hello URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="2dd8b-162">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2dd8b-162">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2dd8b-164">Olá toogenerate **metadados** url, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dd8b-164">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="2dd8b-165">a.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-165">a.</span></span> <span data-ttu-id="2dd8b-166">Clique em **Registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-166">Click **App registrations**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="2dd8b-168">b.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-168">b.</span></span> <span data-ttu-id="2dd8b-169">Clique em **pontos de extremidade** tooopen **pontos de extremidade** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-169">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar Logon Único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="2dd8b-171">c.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-171">c.</span></span> <span data-ttu-id="2dd8b-172">Clique em Olá cópia botão toocopy **documento de METADADOS de Federação** url e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-172">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="2dd8b-174">d.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-174">d.</span></span> <span data-ttu-id="2dd8b-175">Agora vá toohello a página de propriedades de **Springer Link** e cópia hello **Id do aplicativo** usando **cópia** botão e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-175">Now go toohello property page of **Springer Link** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="2dd8b-177">e.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-177">e.</span></span> <span data-ttu-id="2dd8b-178">Gerar Olá **URL de metadados** usando saudação padrão a seguir:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="2dd8b-178">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="2dd8b-179">tooconfigure logon único no **Springer Link** lado, você precisa toosend Olá gerado **URL de metadados** muito[equipe de suporte de Link Springer](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="2dd8b-179">tooconfigure single sign-on on **Springer Link** side, you need toosend hello generated **Metadata URL** too[Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="2dd8b-180">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="2dd8b-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2dd8b-181">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2dd8b-182">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2dd8b-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2dd8b-183">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dd8b-183">Create an Azure AD test user</span></span>

<span data-ttu-id="2dd8b-184">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="2dd8b-186">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2dd8b-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2dd8b-187">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2dd8b-189">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2dd8b-191">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2dd8b-193">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dd8b-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2dd8b-195">a.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-195">a.</span></span> <span data-ttu-id="2dd8b-196">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2dd8b-197">b.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-197">b.</span></span> <span data-ttu-id="2dd8b-198">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="2dd8b-199">c.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-199">c.</span></span> <span data-ttu-id="2dd8b-200">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="2dd8b-201">d.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-201">d.</span></span> <span data-ttu-id="2dd8b-202">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-202">Click **Create**.</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2dd8b-203">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2dd8b-203">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2dd8b-204">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSpringer Link.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringer Link.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="2dd8b-206">**tooassign Britta Simon tooSpringer Link, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2dd8b-206">**tooassign Britta Simon tooSpringer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="2dd8b-207">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2dd8b-209">Na lista de aplicativos hello, selecione **Springer Link**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-209">In hello applications list, select **Springer Link**.</span></span>

    ![vínculo Springer Olá na lista de aplicativos Olá](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="2dd8b-211">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="2dd8b-213">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-213">Click **Add** button.</span></span> <span data-ttu-id="2dd8b-214">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="2dd8b-216">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2dd8b-217">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2dd8b-218">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2dd8b-219">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="2dd8b-219">Test single sign-on</span></span>

<span data-ttu-id="2dd8b-220">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2dd8b-221">Quando você clica em um bloco de Link Springer Olá Olá painel de acesso, você deve obter aplicativos de Link Springer automaticamente assinado em tooyour.</span><span class="sxs-lookup"><span data-stu-id="2dd8b-221">When you click hello Springer Link tile in hello Access Panel, you should get automatically signed-on tooyour Springer Link application.</span></span>
<span data-ttu-id="2dd8b-222">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2dd8b-222">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2dd8b-223">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2dd8b-223">Additional resources</span></span>

* [<span data-ttu-id="2dd8b-224">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2dd8b-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2dd8b-225">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2dd8b-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

