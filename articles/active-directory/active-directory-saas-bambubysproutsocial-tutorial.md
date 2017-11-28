---
title: "Tutorial: Integração do Azure Active Directory ao Bambu by Sprout Social | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Bambu por Sprout sociais."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c9998772c032476f9a18054873022f55b4bb78be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="9f12e-103">Tutorial: Integração do Azure Active Directory com Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="9f12e-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="9f12e-104">Neste tutorial, você aprenderá como toointegrate Bambu por Sprout Social com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="9f12e-104">In this tutorial, you learn how toointegrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f12e-105">Integrando Bambu por Sprout sociais do AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f12e-105">Integrating Bambu by Sprout Social with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9f12e-106">Você pode controlar no AD do Azure que tenha acesso tooBambu por Sprout Social</span><span class="sxs-lookup"><span data-stu-id="9f12e-106">You can control in Azure AD who has access tooBambu by Sprout Social</span></span>
- <span data-ttu-id="9f12e-107">Você pode habilitar seu usuários tooautomatically get conectado tooBambu por Sprout Social (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f12e-107">You can enable your users tooautomatically get signed-on tooBambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f12e-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9f12e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9f12e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f12e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Bambu by Sprout Social, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="9f12e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9f12e-110">Prerequisites</span></span>

<span data-ttu-id="9f12e-111">tooconfigure integração do AD do Azure com Bambu por Sprout sociais, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f12e-111">tooconfigure Azure AD integration with Bambu by Sprout Social, you need hello following items:</span></span>

- <span data-ttu-id="9f12e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f12e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f12e-113">Uma assinatura habilitada de logon único do Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="9f12e-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f12e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9f12e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f12e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9f12e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f12e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9f12e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9f12e-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f12e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f12e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9f12e-118">Scenario description</span></span>
<span data-ttu-id="9f12e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9f12e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f12e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="9f12e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f12e-121">Adicionando Bambu por Sprout Social da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9f12e-121">Adding Bambu by Sprout Social from hello gallery</span></span>
2. <span data-ttu-id="9f12e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f12e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-hello-gallery"></a><span data-ttu-id="9f12e-123">Adicionando Bambu por Sprout Social da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9f12e-123">Adding Bambu by Sprout Social from hello gallery</span></span>
<span data-ttu-id="9f12e-124">integração de saudação tooconfigure de Bambu por Sprout Social no AD do Azure, você precisa tooadd Bambu por Sprout Social da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9f12e-124">tooconfigure hello integration of Bambu by Sprout Social into Azure AD, you need tooadd Bambu by Sprout Social from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f12e-125">**tooadd Bambu por Sprout Social da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f12e-125">**tooadd Bambu by Sprout Social from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f12e-126">Em Olá  **[Portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9f12e-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9f12e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9f12e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9f12e-131">Clique em **novo aplicativo** botão na parte superior de saudação do novo aplicativo do hello diálogo tooadd.</span><span class="sxs-lookup"><span data-stu-id="9f12e-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9f12e-133">Na caixa de pesquisa hello, digite **Bambu por Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-133">In hello search box, type **Bambu by Sprout Social**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="9f12e-135">No painel de resultados de saudação, selecione **Bambu por Sprout Social**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9f12e-135">In hello results panel, select **Bambu by Sprout Social**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f12e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f12e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f12e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Bambu by Sprout Social, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9f12e-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9f12e-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte de saudação em Bambu por Sprout Social é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f12e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bambu by Sprout Social is tooa user in Azure AD.</span></span> <span data-ttu-id="9f12e-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Bambu por Sprout Social precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9f12e-140">In other words, a link relationship between an Azure AD user and hello related user in Bambu by Sprout Social needs toobe established.</span></span>

<span data-ttu-id="9f12e-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Bambu por Sprout sociais.</span><span class="sxs-lookup"><span data-stu-id="9f12e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="9f12e-142">tooconfigure e teste de logon único do AD do Azure com Bambu por Sprout sociais, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f12e-142">tooconfigure and test Azure AD single sign-on with Bambu by Sprout Social, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f12e-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9f12e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f12e-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f12e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f12e-145">**[Criando um Bambu pelo usuário de teste Sprout Social](#creating-a-bambu-by-sprout-social-test-user)**  -toohave um equivalente do Britta Simon em Bambu por Sprout sociais que é a representação toohello vinculado do Azure AD de seus.</span><span class="sxs-lookup"><span data-stu-id="9f12e-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - toohave a counterpart of Britta Simon in Bambu by Sprout Social that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9f12e-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="9f12e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f12e-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="9f12e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f12e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f12e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f12e-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu Bambu pelo aplicativo Sprout sociais.</span><span class="sxs-lookup"><span data-stu-id="9f12e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="9f12e-150">**tooconfigure logon único do AD do Azure com Bambu por Sprout sociais, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f12e-150">**tooconfigure Azure AD single sign-on with Bambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f12e-151">Em Olá portal do Azure, Olá **Bambu por Sprout Social** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-151">In hello Azure portal, on hello **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9f12e-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="9f12e-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="9f12e-155">Em Olá **Bambu Sprout domínio sociais e URLs** seção, hello usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="9f12e-155">On hello **Bambu by Sprout Social Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="9f12e-157">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9f12e-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="9f12e-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9f12e-159">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="9f12e-161">Em Olá **Bambu pela configuração Social Sprout** seção, clique em **configurar Bambu por Sprout Social** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="9f12e-161">On hello **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9f12e-162">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="9f12e-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="9f12e-164">tooconfigure logon único no **Bambu por Sprout Social** lado, você precisa toosend Olá baixado **Metadata XML** e **Single Sign-On URL do serviço SAML** muito[Bambu pelo suporte Sprout Social](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="9f12e-164">tooconfigure single sign-on on **Bambu by Sprout Social** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="9f12e-165">Eles serão configurados isso no hello toohave de ordem conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="9f12e-165">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9f12e-166">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="9f12e-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9f12e-167">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar no hello **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="9f12e-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click on hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9f12e-168">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f12e-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

tooensure users can sign-in tooBambu by Sprout Social after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooBambu by Sprout Social in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f12e-169">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f12e-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f12e-170">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f12e-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9f12e-172">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f12e-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f12e-173">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9f12e-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f12e-175">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="9f12e-175">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f12e-177">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f12e-177">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f12e-179">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f12e-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f12e-181">a.</span><span class="sxs-lookup"><span data-stu-id="9f12e-181">a.</span></span> <span data-ttu-id="9f12e-182">Em Olá **nome** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-182">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="9f12e-183">b.</span><span class="sxs-lookup"><span data-stu-id="9f12e-183">b.</span></span> <span data-ttu-id="9f12e-184">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f12e-184">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="9f12e-185">c.</span><span class="sxs-lookup"><span data-stu-id="9f12e-185">c.</span></span> <span data-ttu-id="9f12e-186">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9f12e-187">d.</span><span class="sxs-lookup"><span data-stu-id="9f12e-187">d.</span></span> <span data-ttu-id="9f12e-188">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="9f12e-189">Criando um usuário de teste Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="9f12e-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="9f12e-190">Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação serão criados no aplicativo hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9f12e-190">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9f12e-191">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f12e-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9f12e-192">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooBambu seu acesso por Sprout sociais.</span><span class="sxs-lookup"><span data-stu-id="9f12e-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBambu by Sprout Social.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9f12e-194">**tooassign Britta Simon tooBambu por Sprout sociais, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f12e-194">**tooassign Britta Simon tooBambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f12e-195">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9f12e-197">Na lista de aplicativos hello, selecione **Bambu por Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-197">In hello applications list, select **Bambu by Sprout Social**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="9f12e-199">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9f12e-201">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-201">Click **Add** button.</span></span> <span data-ttu-id="9f12e-202">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f12e-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9f12e-204">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f12e-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9f12e-205">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f12e-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f12e-206">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f12e-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f12e-207">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9f12e-207">Testing single sign-on</span></span>

<span data-ttu-id="9f12e-208">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f12e-208">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9f12e-209">Quando você clica em Olá Bambu pelo bloco Sprout Social Olá painel de acesso, você deve obter automaticamente assinado em tooyour Bambu pelo aplicativo Sprout sociais.</span><span class="sxs-lookup"><span data-stu-id="9f12e-209">When you click hello Bambu by Sprout Social tile in hello Access Panel, you should get automatically signed-on tooyour Bambu by Sprout Social application.</span></span> <span data-ttu-id="9f12e-210">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9f12e-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9f12e-211">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9f12e-211">Additional resources</span></span>

* [<span data-ttu-id="9f12e-212">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9f12e-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f12e-213">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f12e-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

