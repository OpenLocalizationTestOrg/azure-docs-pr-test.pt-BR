---
title: "Tutorial: Integração do Azure Active Directory ao Tangoe Command Premium Mobile| Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Tangoe comando Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="5ee7b-103">Tutorial: Integração do Azure Active Directory ao Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="5ee7b-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="5ee7b-104">Neste tutorial, você aprenderá como toointegrate Tangoe comando Premium móvel com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5ee7b-104">In this tutorial, you learn how toointegrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ee7b-105">Integrando Tangoe comando Premium móvel com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee7b-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5ee7b-106">Você pode controlar no AD do Azure que tenha acesso tooTangoe comando Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="5ee7b-106">You can control in Azure AD who has access tooTangoe Command Premium Mobile</span></span>
- <span data-ttu-id="5ee7b-107">Você pode habilitar seu usuários tooautomatically get conectado tooTangoe comando Premium Mobile (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee7b-107">You can enable your users tooautomatically get signed-on tooTangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ee7b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee7b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5ee7b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ee7b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ee7b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5ee7b-110">Prerequisites</span></span>

<span data-ttu-id="5ee7b-111">tooconfigure integração do AD do Azure com Tangoe comando Premium móvel, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee7b-111">tooconfigure Azure AD integration with Tangoe Command Premium Mobile, you need hello following items:</span></span>

- <span data-ttu-id="5ee7b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee7b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ee7b-113">Uma assinatura do Tangoe Command Premium Mobile habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="5ee7b-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ee7b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ee7b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5ee7b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ee7b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ee7b-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ee7b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ee7b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5ee7b-118">Scenario description</span></span>
<span data-ttu-id="5ee7b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ee7b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="5ee7b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ee7b-121">Adicionar Tangoe comando Premium móvel da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5ee7b-121">Add Tangoe Command Premium Mobile from hello gallery</span></span>
2. <span data-ttu-id="5ee7b-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee7b-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a><span data-ttu-id="5ee7b-123">Adicionar Tangoe comando Premium móvel da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5ee7b-123">Add Tangoe Command Premium Mobile from hello gallery</span></span>
<span data-ttu-id="5ee7b-124">integração de Olá tooconfigure do Tangoe comando Premium Mobile no AD do Azure, você precisa tooadd Tangoe comando Premium móvel da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-124">tooconfigure hello integration of Tangoe Command Premium Mobile into Azure AD, you need tooadd Tangoe Command Premium Mobile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5ee7b-125">**tooadd Tangoe comando Premium móvel da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5ee7b-125">**tooadd Tangoe Command Premium Mobile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ee7b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ee7b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5ee7b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5ee7b-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5ee7b-133">Na caixa de pesquisa hello, digite **Tangoe comando Premium Mobile**, selecione **Tangoe comando Premium Mobile** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-133">In hello search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![<span data-ttu-id="5ee7b-134">Adicionar o Tangoe Command Premium Mobile da galeria</span><span class="sxs-lookup"><span data-stu-id="5ee7b-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5ee7b-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee7b-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5ee7b-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Tangoe Command Premium Mobile, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="5ee7b-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ee7b-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Tangoe comando Premium Mobile é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tangoe Command Premium Mobile is tooa user in Azure AD.</span></span> <span data-ttu-id="5ee7b-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Tangoe comando Premium Mobile precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-138">In other words, a link relationship between an Azure AD user and hello related user in Tangoe Command Premium Mobile needs toobe established.</span></span>

<span data-ttu-id="5ee7b-139">Tangoe comando Premium Mobile, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-139">In Tangoe Command Premium Mobile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5ee7b-140">tooconfigure e teste de logon único do AD do Azure com Tangoe comando Premium Mobile, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee7b-140">tooconfigure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5ee7b-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5ee7b-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ee7b-143">**[Criar um usuário de teste Tangoe comando Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave um equivalente do Britta Simon no Tangoe comando Premium Mobile que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - toohave a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ee7b-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ee7b-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5ee7b-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee7b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5ee7b-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo móvel do Tangoe comando Premium.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="5ee7b-148">**tooconfigure logon único do AD do Azure com Tangoe comando Premium Mobile, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5ee7b-148">**tooconfigure Azure AD single sign-on with Tangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ee7b-149">Em Olá portal do Azure, Olá **Tangoe comando Premium Mobile** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-149">In hello Azure portal, on hello **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5ee7b-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Logon único baseado em SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="5ee7b-153">Em Olá **Tangoe comando Premium Mobile domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee7b-153">On hello **Tangoe Command Premium Mobile Domain and URLs** section, perform hello following steps:</span></span>

    ![Domínio e URLs do Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="5ee7b-155">a.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-155">a.</span></span> <span data-ttu-id="5ee7b-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="5ee7b-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="5ee7b-157">b.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-157">b.</span></span> <span data-ttu-id="5ee7b-158">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="5ee7b-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5ee7b-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-159">These values are not real.</span></span> <span data-ttu-id="5ee7b-160">Atualize esses valores com URL de resposta real hello e a URL de logon.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-160">Update these values with hello actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="5ee7b-161">Entre em contato com [a equipe de suporte Tangoe comando Premium móveis cliente](https://www.tangoe.com/contact-2/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooget these values.</span></span> 

4. <span data-ttu-id="5ee7b-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="5ee7b-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5ee7b-164">Click **Save** button.</span></span>

    ![Botão Salvar](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="5ee7b-166">Em Olá **Tangoe comando Premium Mobile configuração** seção, clique em **configurar o Tangoe comando Premium Mobile** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-166">On hello **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5ee7b-167">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="5ee7b-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Seção Configuração do Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="5ee7b-169">tooget SSO configurado para o seu aplicativo, entre em contato com seu [a equipe de suporte Tangoe comando Premium móveis cliente](https://www.tangoe.com/contact-2/) e fornecer Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="5ee7b-169">tooget SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide hello following:</span></span>

   - <span data-ttu-id="5ee7b-170">arquivo de metadados baixado Olá</span><span class="sxs-lookup"><span data-stu-id="5ee7b-170">hello downloaded metadata file</span></span>
   - <span data-ttu-id="5ee7b-171">Olá **ID de entidade de SAML**</span><span class="sxs-lookup"><span data-stu-id="5ee7b-171">hello **SAML Entity ID**</span></span>
   - <span data-ttu-id="5ee7b-172">Olá **Single Sign-On URL do serviço SAML**</span><span class="sxs-lookup"><span data-stu-id="5ee7b-172">hello **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="5ee7b-173">Olá **URL de logout**</span><span class="sxs-lookup"><span data-stu-id="5ee7b-173">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="5ee7b-174">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="5ee7b-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5ee7b-175">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5ee7b-176">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5ee7b-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5ee7b-177">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee7b-177">Create an Azure AD test user</span></span>
<span data-ttu-id="5ee7b-178">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5ee7b-180">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5ee7b-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ee7b-181">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ee7b-183">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Usuários e grupos -> Todos os usuários](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ee7b-185">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Adicionar usuário](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ee7b-187">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee7b-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Página da caixa de diálogo do usuário](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ee7b-189">a.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-189">a.</span></span> <span data-ttu-id="5ee7b-190">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ee7b-191">b.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-191">b.</span></span> <span data-ttu-id="5ee7b-192">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ee7b-193">c.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-193">c.</span></span> <span data-ttu-id="5ee7b-194">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5ee7b-195">d.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-195">d.</span></span> <span data-ttu-id="5ee7b-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="5ee7b-197">Criar um usuário de teste do Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="5ee7b-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="5ee7b-198">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="5ee7b-199">Aplicativo Tangoe comando Premium Mobile precisa de todas as toobe de usuários Olá provisionado no aplicativo hello antes de fazer logon único.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-199">Tangoe Command Premium Mobile application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="5ee7b-200">Portanto, o trabalho com hello [a equipe de suporte Tangoe comando Premium móveis cliente](https://www.tangoe.com/contact-2/) tooprovision todos esses usuários para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-200">So please work with hello [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooprovision all these users into hello application.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5ee7b-201">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee7b-201">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5ee7b-202">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTangoe comando Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTangoe Command Premium Mobile.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5ee7b-204">**tooassign Britta Simon tooTangoe comando Premium móveis, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5ee7b-204">**tooassign Britta Simon tooTangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ee7b-205">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5ee7b-207">Na lista de aplicativos hello, selecione **Tangoe comando Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-207">In hello applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe Command Premium Mobile na lista de aplicativos](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="5ee7b-209">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5ee7b-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-211">Click **Add** button.</span></span> <span data-ttu-id="5ee7b-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5ee7b-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5ee7b-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ee7b-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5ee7b-217">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="5ee7b-217">Test single sign-on</span></span>

<span data-ttu-id="5ee7b-218">Nesta seção, você deve testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-218">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5ee7b-219">Quando você clica em bloco Tangoe comando Premium Mobile Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo móvel do Tangoe comando Premium.</span><span class="sxs-lookup"><span data-stu-id="5ee7b-219">When you click hello Tangoe Command Premium Mobile tile in hello Access Panel, you should get automatically signed-on tooyour Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="5ee7b-220">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5ee7b-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5ee7b-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5ee7b-221">Additional resources</span></span>

* [<span data-ttu-id="5ee7b-222">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee7b-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ee7b-223">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5ee7b-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

