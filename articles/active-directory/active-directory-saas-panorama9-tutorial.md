---
title: "Tutorial: Integração do Azure Active Directory com o Panorama9 | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="70e3a-103">Tutorial: Integração do Active Directory do Azure com o Panorama9</span><span class="sxs-lookup"><span data-stu-id="70e3a-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="70e3a-104">Neste tutorial, você aprenderá como toointegrate Panorama9 com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="70e3a-104">In this tutorial, you learn how toointegrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70e3a-105">Integração do Panorama9 com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="70e3a-105">Integrating Panorama9 with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70e3a-106">Você pode controlar no AD do Azure que tenha acesso tooPanorama9</span><span class="sxs-lookup"><span data-stu-id="70e3a-106">You can control in Azure AD who has access tooPanorama9</span></span>
- <span data-ttu-id="70e3a-107">Você pode habilitar seus usuários tooautomatically get conectado tooPanorama9 (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="70e3a-107">You can enable your users tooautomatically get signed-on tooPanorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70e3a-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="70e3a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="70e3a-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70e3a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70e3a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="70e3a-110">Prerequisites</span></span>

<span data-ttu-id="70e3a-111">tooconfigure integração do AD do Azure com Panorama9, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="70e3a-111">tooconfigure Azure AD integration with Panorama9, you need hello following items:</span></span>

- <span data-ttu-id="70e3a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="70e3a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70e3a-113">Uma assinatura habilitada para logon único do Panorama9</span><span class="sxs-lookup"><span data-stu-id="70e3a-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70e3a-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="70e3a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70e3a-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="70e3a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70e3a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="70e3a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70e3a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70e3a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70e3a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="70e3a-118">Scenario description</span></span>
<span data-ttu-id="70e3a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="70e3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70e3a-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="70e3a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70e3a-121">Adicionando Panorama9 da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="70e3a-121">Adding Panorama9 from hello gallery</span></span>
2. <span data-ttu-id="70e3a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="70e3a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-hello-gallery"></a><span data-ttu-id="70e3a-123">Adicionando Panorama9 da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="70e3a-123">Adding Panorama9 from hello gallery</span></span>
<span data-ttu-id="70e3a-124">integração de saudação tooconfigure do Panorama9 no AD do Azure, você precisa tooadd Panorama9 da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="70e3a-124">tooconfigure hello integration of Panorama9 into Azure AD, you need tooadd Panorama9 from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70e3a-125">**tooadd Panorama9 da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="70e3a-125">**tooadd Panorama9 from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e3a-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="70e3a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70e3a-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70e3a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="70e3a-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70e3a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="70e3a-133">Na caixa de pesquisa hello, digite **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-133">In hello search box, type **Panorama9**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="70e3a-135">No painel de resultados de saudação, selecione **Panorama9**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="70e3a-135">In hello results panel, select **Panorama9**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70e3a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="70e3a-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="70e3a-138">Nesta seção, você configura e testa o logon único do Azure AD com o Panorama9, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="70e3a-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="70e3a-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Panorama9 é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="70e3a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panorama9 is tooa user in Azure AD.</span></span> <span data-ttu-id="70e3a-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Panorama9 precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="70e3a-140">In other words, a link relationship between an Azure AD user and hello related user in Panorama9 needs toobe established.</span></span>

<span data-ttu-id="70e3a-141">No Panorama9, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="70e3a-141">In Panorama9, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="70e3a-142">tooconfigure e teste de logon único do AD do Azure com Panorama9, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="70e3a-142">tooconfigure and test Azure AD single sign-on with Panorama9, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70e3a-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="70e3a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70e3a-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70e3a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70e3a-145">**[Criar um usuário de teste do Panorama9](#creating-a-panorama9-test-user)**  -toohave um equivalente do Britta Simon no Panorama9 é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="70e3a-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - toohave a counterpart of Britta Simon in Panorama9 that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70e3a-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="70e3a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70e3a-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="70e3a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70e3a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="70e3a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70e3a-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Panorama9.</span><span class="sxs-lookup"><span data-stu-id="70e3a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="70e3a-150">**tooconfigure AD do Azure-logon único com Panorama9, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="70e3a-150">**tooconfigure Azure AD single sign-on with Panorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e3a-151">Em Olá portal do Azure, Olá **Panorama9** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-151">In hello Azure portal, on hello **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="70e3a-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="70e3a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="70e3a-155">Em Olá **Panorama9 domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="70e3a-155">On hello **Panorama9 Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="70e3a-157">a.</span><span class="sxs-lookup"><span data-stu-id="70e3a-157">a.</span></span> <span data-ttu-id="70e3a-158">Em Olá **URL de logon** caixa de texto, digite um URL como:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="70e3a-158">In hello **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="70e3a-159">b.</span><span class="sxs-lookup"><span data-stu-id="70e3a-159">b.</span></span> <span data-ttu-id="70e3a-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="70e3a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70e3a-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="70e3a-161">These values are not real.</span></span> <span data-ttu-id="70e3a-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="70e3a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="70e3a-163">Entre em contato com [equipe de suporte do cliente do Panorama9](https://support.panorama9.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="70e3a-163">Contact [Panorama9 Client support team](https://support.panorama9.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="70e3a-164">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="70e3a-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="70e3a-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="70e3a-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="70e3a-168">Em Olá **Panorama9 configuração** seção, clique em **configurar Panorama9** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="70e3a-168">On hello **Panorama9 Configuration** section, click **Configure Panorama9** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="70e3a-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="70e3a-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="70e3a-171">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do Panorama9 como administrador.</span><span class="sxs-lookup"><span data-stu-id="70e3a-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="70e3a-172">Na barra de ferramentas de saudação na parte superior do hello, clique em **gerenciar**e, em seguida, clique em **extensões**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-172">In hello toolbar on hello top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="70e3a-173">![Extensões](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensões")</span><span class="sxs-lookup"><span data-stu-id="70e3a-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="70e3a-174">Em Olá **extensões** caixa de diálogo, clique em **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-174">On hello **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="70e3a-175">![Logon Único](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="70e3a-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="70e3a-176">Em Olá **configurações** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="70e3a-176">In hello **Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="70e3a-177">![Configurações](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="70e3a-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="70e3a-178">a.</span><span class="sxs-lookup"><span data-stu-id="70e3a-178">a.</span></span> <span data-ttu-id="70e3a-179">Em **URL do provedor de identidade** caixa de texto valor Olá colar **o URL de serviço de logon único**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="70e3a-179">In **Identity provider URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="70e3a-180">b.</span><span class="sxs-lookup"><span data-stu-id="70e3a-180">b.</span></span> <span data-ttu-id="70e3a-181">Em **impressão digital do certificado** caixa de texto, colar Olá **impressão digital** valor de certificado, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="70e3a-181">In **Certificate fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="70e3a-182">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="70e3a-183">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="70e3a-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="70e3a-184">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="70e3a-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="70e3a-185">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70e3a-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70e3a-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="70e3a-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="70e3a-187">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="70e3a-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="70e3a-189">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="70e3a-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e3a-190">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="70e3a-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70e3a-192">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70e3a-194">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="70e3a-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70e3a-196">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="70e3a-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70e3a-198">a.</span><span class="sxs-lookup"><span data-stu-id="70e3a-198">a.</span></span> <span data-ttu-id="70e3a-199">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70e3a-200">b.</span><span class="sxs-lookup"><span data-stu-id="70e3a-200">b.</span></span> <span data-ttu-id="70e3a-201">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="70e3a-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70e3a-202">c.</span><span class="sxs-lookup"><span data-stu-id="70e3a-202">c.</span></span> <span data-ttu-id="70e3a-203">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="70e3a-204">d.</span><span class="sxs-lookup"><span data-stu-id="70e3a-204">d.</span></span> <span data-ttu-id="70e3a-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="70e3a-206">Criando um usuário de teste do Panorama9</span><span class="sxs-lookup"><span data-stu-id="70e3a-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="70e3a-207">Ordem tooenable AD do Azure usuários toolog no Panorama9, eles devem ser provisionados no Panorama9.</span><span class="sxs-lookup"><span data-stu-id="70e3a-207">In order tooenable Azure AD users toolog into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="70e3a-208">No caso de saudação do Panorama9, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="70e3a-208">In hello case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="70e3a-209">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="70e3a-209">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e3a-210">Faça logon no tooyour **Panorama9** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="70e3a-210">Log in tooyour **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="70e3a-211">No menu de saudação na parte superior de saudação, clique em **gerenciar**e, em seguida, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-211">In hello menu on hello top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="70e3a-212">![Usuários](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="70e3a-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="70e3a-213">Na seção usuários de Olá, clique em  **+**  tooadd novo usuário.</span><span class="sxs-lookup"><span data-stu-id="70e3a-213">In hello Users section, Click **+** tooadd new user.</span></span>

 <span data-ttu-id="70e3a-214">![Usuários](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="70e3a-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="70e3a-215">Vá toohello seção de dados de usuário, Olá tipo endereço de email de um usuário válido do Active Directory do Azure você deseja tooprovision em Olá **Email** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="70e3a-215">Go toohello User data section, type hello email address of a valid Azure Active Directory user you want tooprovision into hello **Email** textbox.</span></span>

5. <span data-ttu-id="70e3a-216">Vêm toohello seção usuários, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-216">Come toohello Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="70e3a-217">proprietário de conta do Active Directory do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="70e3a-217">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="70e3a-218">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="70e3a-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="70e3a-219">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPanorama9.</span><span class="sxs-lookup"><span data-stu-id="70e3a-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanorama9.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="70e3a-221">**tooassign Britta Simon tooPanorama9, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="70e3a-221">**tooassign Britta Simon tooPanorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e3a-222">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="70e3a-224">Na lista de aplicativos hello, selecione **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-224">In hello applications list, select **Panorama9**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="70e3a-226">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="70e3a-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-228">Click **Add** button.</span></span> <span data-ttu-id="70e3a-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70e3a-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="70e3a-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="70e3a-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70e3a-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70e3a-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70e3a-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70e3a-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70e3a-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="70e3a-234">Testing single sign-on</span></span>

<span data-ttu-id="70e3a-235">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="70e3a-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="70e3a-236">Quando você clica em bloco Olá Panorama9 Olá painel de acesso, você deve obter tooPanorama9 automaticamente conectado no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70e3a-236">When you click hello Panorama9 tile in hello Access Panel, you should get automatically signed-on tooPanorama9 application.</span></span>
<span data-ttu-id="70e3a-237">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="70e3a-237">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="70e3a-238">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="70e3a-238">Additional resources</span></span>

* [<span data-ttu-id="70e3a-239">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="70e3a-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70e3a-240">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="70e3a-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

