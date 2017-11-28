---
title: "Tutorial: Integração do Azure Active Directory ao 10,000ft Plans | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e 10.000 pés planos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 9aa6fd079da4f931d4dd7277407a07e56091d7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="e239b-103">Tutorial: Integração do Azure Active Directory ao 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="e239b-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="e239b-104">Neste tutorial, você aprenderá como toointegrate 10.000 pés planos com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="e239b-104">In this tutorial, you learn how toointegrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e239b-105">Integrando a 10.000 pés planos AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="e239b-105">Integrating 10,000ft Plans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e239b-106">Você pode controlar no AD do Azure que tenha acesso too10, planos de ft 000</span><span class="sxs-lookup"><span data-stu-id="e239b-106">You can control in Azure AD who has access too10,000ft Plans</span></span>
- <span data-ttu-id="e239b-107">Você pode habilitar seus usuários tooautomatically get conectado too10, planos de ft 000 (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e239b-107">You can enable your users tooautomatically get signed-on too10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e239b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e239b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e239b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e239b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e239b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e239b-110">Prerequisites</span></span>

<span data-ttu-id="e239b-111">tooconfigure integração do AD do Azure com planos de 10.000 pés, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="e239b-111">tooconfigure Azure AD integration with 10,000ft Plans, you need hello following items:</span></span>

- <span data-ttu-id="e239b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e239b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e239b-113">Uma assinatura do 10,000ft Plans habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="e239b-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e239b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e239b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e239b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e239b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e239b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e239b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e239b-117">Caso não tenha um ambiente de avaliação do Azure AD, obtenha uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e239b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e239b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e239b-118">Scenario description</span></span>
<span data-ttu-id="e239b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e239b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e239b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="e239b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e239b-121">Adicionando a 10.000 pés planos da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e239b-121">Adding 10,000ft Plans from hello gallery</span></span>
2. <span data-ttu-id="e239b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e239b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-hello-gallery"></a><span data-ttu-id="e239b-123">Adicionando a 10.000 pés planos da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e239b-123">Adding 10,000ft Plans from hello gallery</span></span>
<span data-ttu-id="e239b-124">integração de saudação tooconfigure dos planos de 10.000 pés no AD do Azure, você precisa tooadd 10.000 pés planos de lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e239b-124">tooconfigure hello integration of 10,000ft Plans into Azure AD, you need tooadd 10,000ft Plans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e239b-125">**tooadd 10.000 pés planos da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e239b-125">**tooadd 10,000ft Plans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e239b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e239b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e239b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e239b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e239b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e239b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e239b-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e239b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e239b-133">Na caixa de pesquisa hello, digite **planos de 10.000 pés**.</span><span class="sxs-lookup"><span data-stu-id="e239b-133">In hello search box, type **10,000ft Plans**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="e239b-135">No painel de resultados de saudação, selecione **planos de 10.000 pés**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e239b-135">In hello results panel, select **10,000ft Plans**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e239b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e239b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e239b-138">Nesta seção, você configurará e testará o logon único do Azure AD com o 10,000ft Plans com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e239b-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e239b-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em planos de 10.000 pés é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e239b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 10,000ft Plans is tooa user in Azure AD.</span></span> <span data-ttu-id="e239b-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em 10.000 pés planos precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e239b-140">In other words, a link relationship between an Azure AD user and hello related user in 10,000ft Plans needs toobe established.</span></span>

<span data-ttu-id="e239b-141">Planos de 10.000 pés, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="e239b-141">In 10,000ft Plans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e239b-142">tooconfigure e teste de logon único do AD do Azure com planos de 10.000 pés, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="e239b-142">tooconfigure and test Azure AD single sign-on with 10,000ft Plans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e239b-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e239b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e239b-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e239b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e239b-145">**[Criando um 10.000 pés planos de usuário de teste](#creating-a-10000ft-plans-test-user)**  -toohave uma duplicata de Britta Simon em 10.000 pés planos que é vinculado a representação toohello AD do Azure do usuário.</span><span class="sxs-lookup"><span data-stu-id="e239b-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - toohave a counterpart of Britta Simon in 10,000ft Plans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e239b-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="e239b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e239b-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="e239b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e239b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e239b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e239b-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de planos de 10.000 pés.</span><span class="sxs-lookup"><span data-stu-id="e239b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="e239b-150">**tooconfigure AD do Azure-logon único com planos de 10.000 pés, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e239b-150">**tooconfigure Azure AD single sign-on with 10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="e239b-151">Em Olá portal do Azure, Olá **planos de 10.000 pés** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="e239b-151">In hello Azure portal, on hello **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e239b-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="e239b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="e239b-155">Em Olá **10.000 pés planos de domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e239b-155">On hello **10,000ft Plans Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="e239b-157">a.</span><span class="sxs-lookup"><span data-stu-id="e239b-157">a.</span></span> <span data-ttu-id="e239b-158">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="e239b-158">In hello **Sign-on URL** textbox, type hello URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="e239b-159">b.</span><span class="sxs-lookup"><span data-stu-id="e239b-159">b.</span></span> <span data-ttu-id="e239b-160">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="e239b-160">In hello **Identifier** textbox, type hello URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e239b-161">Olá valor **identificador** é diferente se você tiver um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="e239b-161">hello value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="e239b-162">Entre em contato com [equipe de suporte de planos de 10.000 pés](https://www.10000ft.com/plans/support) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="e239b-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="e239b-163">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e239b-163">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="e239b-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e239b-165">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e239b-167">Em Olá **10.000 pés planos configuração** seção, clique em **configurar planos de 10.000 pés** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="e239b-167">On hello **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e239b-168">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="e239b-168">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="e239b-170">tooconfigure logon único no **planos de 10.000 pés** lado, você precisa toosend Olá baixado **Certificate(Raw), URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** muito[ a equipe de suporte de planos de 10.000 pés](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="e239b-170">tooconfigure single sign-on on **10,000ft Plans** side, you need toosend hello downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="e239b-171">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="e239b-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e239b-172">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="e239b-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e239b-173">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e239b-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e239b-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e239b-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="e239b-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e239b-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e239b-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e239b-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e239b-178">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e239b-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e239b-180">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="e239b-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e239b-182">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e239b-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e239b-184">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e239b-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e239b-186">a.</span><span class="sxs-lookup"><span data-stu-id="e239b-186">a.</span></span> <span data-ttu-id="e239b-187">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e239b-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e239b-188">b.</span><span class="sxs-lookup"><span data-stu-id="e239b-188">b.</span></span> <span data-ttu-id="e239b-189">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e239b-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e239b-190">c.</span><span class="sxs-lookup"><span data-stu-id="e239b-190">c.</span></span> <span data-ttu-id="e239b-191">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="e239b-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e239b-192">d.</span><span class="sxs-lookup"><span data-stu-id="e239b-192">d.</span></span> <span data-ttu-id="e239b-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e239b-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="e239b-194">Criando um usuário de teste do 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="e239b-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="e239b-195">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon em planos de 10.000 pés.</span><span class="sxs-lookup"><span data-stu-id="e239b-195">hello objective of this section is toocreate a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="e239b-196">O 10,000ft Plans dá suporte ao provisionamento Just-In-Time, que é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="e239b-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="e239b-197">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="e239b-197">There is no action item for you in this section.</span></span> <span data-ttu-id="e239b-198">Um novo usuário é criado durante uma tentativa tooaccess 10.000 pés planos se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="e239b-198">A new user is created during an attempt tooaccess 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="e239b-199">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [equipe de suporte de planos de 10.000 pés](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="e239b-199">If you need toocreate a user manually, you need toocontact hello [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e239b-200">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e239b-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e239b-201">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso too10, 000ft planos.</span><span class="sxs-lookup"><span data-stu-id="e239b-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too10,000ft Plans.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e239b-203">**tooassign Britta Simon too10, planos de 000ft, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e239b-203">**tooassign Britta Simon too10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="e239b-204">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e239b-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e239b-206">Na lista de aplicativos hello, selecione **planos de 10.000 pés**.</span><span class="sxs-lookup"><span data-stu-id="e239b-206">In hello applications list, select **10,000ft Plans**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="e239b-208">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e239b-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e239b-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e239b-210">Click **Add** button.</span></span> <span data-ttu-id="e239b-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e239b-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e239b-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="e239b-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e239b-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e239b-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e239b-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e239b-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e239b-216">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e239b-216">Testing single sign-on</span></span>

<span data-ttu-id="e239b-217">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e239b-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="e239b-218">Quando você clica em Olá 10.000 pés planos de bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de planos de 10.000 pés.</span><span class="sxs-lookup"><span data-stu-id="e239b-218">When you click hello 10,000ft Plans tile in hello Access Panel, you should get automatically signed-on tooyour 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="e239b-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e239b-219">Additional resources</span></span>

* [<span data-ttu-id="e239b-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e239b-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e239b-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e239b-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

