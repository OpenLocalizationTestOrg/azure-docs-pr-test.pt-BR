---
title: "Tutorial: integração do Azure Active Directory ao Blackboard Learn - Shibboleth | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e aprenda-quadro-negro - o Shibboleth."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 40aa3ec5f42b93157af3c56daaadfa66203b21d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="cac5f-103">Tutorial: integração do Azure Active Directory ao Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="cac5f-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="cac5f-104">Neste tutorial, você aprenderá como toointegrate-quadro-negro Saiba - Shibboleth com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="cac5f-104">In this tutorial, you learn how toointegrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cac5f-105">Integrar-quadro-negro Saiba - Shibboleth com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="cac5f-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cac5f-106">Você pode controlar no AD do Azure que tenha acesso tooBlackboard Saiba - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="cac5f-106">You can control in Azure AD who has access tooBlackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="cac5f-107">Você pode habilitar seu usuários tooautomatically get conectado tooBlackboard Saiba - Shibboleth (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cac5f-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cac5f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cac5f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cac5f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cac5f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cac5f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cac5f-110">Prerequisites</span></span>

<span data-ttu-id="cac5f-111">tooconfigure integração do AD do Azure com-quadro-negro Saiba - Shibboleth, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="cac5f-111">tooconfigure Azure AD integration with Blackboard Learn - Shibboleth, you need hello following items:</span></span>

- <span data-ttu-id="cac5f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cac5f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cac5f-113">Uma assinatura com logon único habilitado do Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="cac5f-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cac5f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cac5f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cac5f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cac5f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cac5f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cac5f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cac5f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cac5f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cac5f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cac5f-118">Scenario description</span></span>
<span data-ttu-id="cac5f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cac5f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cac5f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="cac5f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cac5f-121">Adicionando-quadro-negro Saiba - Shibboleth da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cac5f-121">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
2. <span data-ttu-id="cac5f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cac5f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-hello-gallery"></a><span data-ttu-id="cac5f-123">Adicionando-quadro-negro Saiba - Shibboleth da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cac5f-123">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
<span data-ttu-id="cac5f-124">integração de saudação tooconfigure de-quadro-negro Saiba - Shibboleth no AD do Azure, você precisa tooadd-quadro-negro Saiba - Shibboleth na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cac5f-124">tooconfigure hello integration of Blackboard Learn - Shibboleth into Azure AD, you need tooadd Blackboard Learn - Shibboleth from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cac5f-125">**tooadd-quadro-negro Saiba - Shibboleth da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cac5f-125">**tooadd Blackboard Learn - Shibboleth from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cac5f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cac5f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cac5f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cac5f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cac5f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cac5f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cac5f-133">Na caixa de pesquisa hello, digite **-quadro-negro Saiba - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-133">In hello search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="cac5f-135">No painel de resultados de saudação, selecione **-quadro-negro Saiba - Shibboleth**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cac5f-135">In hello results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cac5f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cac5f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cac5f-138">Nesta seção, você configura e testa o logon único do Azure AD com o Blackboard Learn – Shibboleth, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cac5f-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cac5f-139">Para toowork de logon único, AD do Azure precisa tooknow que usuário de contraparte Olá em aprender-quadro-negro - Shibboleth tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cac5f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn - Shibboleth is tooa user in Azure AD.</span></span> <span data-ttu-id="cac5f-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em aprender-quadro-negro - Shibboleth deve toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="cac5f-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn - Shibboleth needs toobe established.</span></span>

<span data-ttu-id="cac5f-141">Saiba-quadro-negro - Shibboleth, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="cac5f-141">In Blackboard Learn - Shibboleth, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cac5f-142">tooconfigure e teste de logon único do AD do Azure com-quadro-negro Saiba - Shibboleth, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="cac5f-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cac5f-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cac5f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cac5f-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cac5f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cac5f-145">**[Criando um saber de-quadro-negro - usuário de teste de Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)**  - toohave um equivalente do Britta Simon em aprender-quadro-negro - Shibboleth é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="cac5f-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cac5f-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="cac5f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cac5f-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="cac5f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cac5f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cac5f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cac5f-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu saber de-quadro-negro - aplicativo de Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="cac5f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="cac5f-150">**tooconfigure AD do Azure-logon único com-quadro-negro Saiba - Shibboleth, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cac5f-150">**tooconfigure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="cac5f-151">Em Olá portal do Azure, Olá **-quadro-negro Saiba - Shibboleth** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-151">In hello Azure portal, on hello **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cac5f-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="cac5f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="cac5f-155">Em Olá **-quadro-negro Saiba - domínio Shibboleth e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cac5f-155">On hello **Blackboard Learn - Shibboleth Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="cac5f-157">a.</span><span class="sxs-lookup"><span data-stu-id="cac5f-157">a.</span></span> <span data-ttu-id="cac5f-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="cac5f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="cac5f-159">b.</span><span class="sxs-lookup"><span data-stu-id="cac5f-159">b.</span></span> <span data-ttu-id="cac5f-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="cac5f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="cac5f-161">c.</span><span class="sxs-lookup"><span data-stu-id="cac5f-161">c.</span></span> <span data-ttu-id="cac5f-162">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="cac5f-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="cac5f-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="cac5f-163">These values are not real.</span></span> <span data-ttu-id="cac5f-164">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="cac5f-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="cac5f-165">Entre em contato com [-quadro-negro Saiba - equipe de suporte do cliente de Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="cac5f-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="cac5f-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cac5f-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="cac5f-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="cac5f-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="cac5f-170">Em Olá **-quadro-negro Saiba - configuração de Shibboleth** seção, clique em **configurar-quadro-negro Saiba - Shibboleth** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="cac5f-170">On hello **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cac5f-171">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="cac5f-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="cac5f-173">tooconfigure logon único no **-quadro-negro Saiba - Shibboleth** lado, você precisa toosend Olá baixado **Metadata XML** e **URL de logout, ID de entidade de SAML e serviço de logon único SAML URL** muito[-quadro-negro saiba - a equipe de suporte Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="cac5f-173">tooconfigure single sign-on on **Blackboard Learn - Shibboleth** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="cac5f-174">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="cac5f-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cac5f-175">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="cac5f-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cac5f-176">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cac5f-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cac5f-177">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cac5f-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="cac5f-178">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cac5f-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cac5f-180">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cac5f-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cac5f-181">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cac5f-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cac5f-183">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cac5f-185">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cac5f-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cac5f-187">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cac5f-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cac5f-189">a.</span><span class="sxs-lookup"><span data-stu-id="cac5f-189">a.</span></span> <span data-ttu-id="cac5f-190">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cac5f-191">b.</span><span class="sxs-lookup"><span data-stu-id="cac5f-191">b.</span></span> <span data-ttu-id="cac5f-192">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cac5f-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cac5f-193">c.</span><span class="sxs-lookup"><span data-stu-id="cac5f-193">c.</span></span> <span data-ttu-id="cac5f-194">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cac5f-195">d.</span><span class="sxs-lookup"><span data-stu-id="cac5f-195">d.</span></span> <span data-ttu-id="cac5f-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="cac5f-197">Criando um usuário de teste do Blackboard Learn – Shibboleth</span><span class="sxs-lookup"><span data-stu-id="cac5f-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="cac5f-198">Nesta seção, você deve criar um usuário chamado Brenda Fernandes no Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="cac5f-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="cac5f-199">Trabalhar com seu [-quadro-negro Saiba - equipe de suporte do Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd usuários Olá Olá-quadro-negro Saiba - plataforma Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="cac5f-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd hello users in hello Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cac5f-200">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cac5f-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cac5f-201">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBlackboard Saiba - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="cac5f-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn - Shibboleth.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cac5f-203">**tooassign Britta Simon tooBlackboard Saiba - Shibboleth, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cac5f-203">**tooassign Britta Simon tooBlackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="cac5f-204">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cac5f-206">Na lista de aplicativos hello, selecione **-quadro-negro Saiba - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-206">In hello applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="cac5f-208">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cac5f-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cac5f-210">Click **Add** button.</span></span> <span data-ttu-id="cac5f-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cac5f-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cac5f-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="cac5f-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cac5f-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cac5f-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cac5f-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cac5f-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cac5f-216">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cac5f-216">Testing single sign-on</span></span>

<span data-ttu-id="cac5f-217">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="cac5f-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cac5f-218">Quando você clica em hello-quadro-negro Saiba - bloco do Shibboleth no hello painel de acesso, você deve obter automaticamente assinado em tooyour-quadro-negro Saiba - aplicativo de Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="cac5f-218">When you click hello Blackboard Learn - Shibboleth tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cac5f-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cac5f-219">Additional resources</span></span>

* [<span data-ttu-id="cac5f-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cac5f-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cac5f-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cac5f-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

