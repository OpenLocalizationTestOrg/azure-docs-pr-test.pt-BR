---
title: "Tutorial: Integração do Azure Active Directory com o HappyFox | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e HappyFox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 1190652d7d1144c7eddea339cb3f9175912407fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="c4f01-103">Tutorial: Integração do Azure Active Directory com o HappyFox</span><span class="sxs-lookup"><span data-stu-id="c4f01-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="c4f01-104">Neste tutorial, você aprenderá como toointegrate HappyFox com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c4f01-104">In this tutorial, you learn how toointegrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4f01-105">Integrando HappyFox com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4f01-105">Integrating HappyFox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c4f01-106">Você pode controlar no AD do Azure que tenha acesso tooHappyFox</span><span class="sxs-lookup"><span data-stu-id="c4f01-106">You can control in Azure AD who has access tooHappyFox</span></span>
- <span data-ttu-id="c4f01-107">Você pode habilitar seu usuários tooautomatically get conectado tooHappyFox (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4f01-107">You can enable your users tooautomatically get signed-on tooHappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4f01-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c4f01-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c4f01-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4f01-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4f01-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c4f01-110">Prerequisites</span></span>

<span data-ttu-id="c4f01-111">tooconfigure integração do AD do Azure com HappyFox, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4f01-111">tooconfigure Azure AD integration with HappyFox, you need hello following items:</span></span>

- <span data-ttu-id="c4f01-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4f01-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4f01-113">Uma assinatura do HappyFox com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="c4f01-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4f01-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c4f01-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4f01-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c4f01-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4f01-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c4f01-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4f01-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4f01-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4f01-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c4f01-118">Scenario description</span></span>
<span data-ttu-id="c4f01-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c4f01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4f01-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c4f01-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4f01-121">Adicionando HappyFox da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c4f01-121">Adding HappyFox from hello gallery</span></span>
2. <span data-ttu-id="c4f01-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4f01-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-hello-gallery"></a><span data-ttu-id="c4f01-123">Adicionando HappyFox da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c4f01-123">Adding HappyFox from hello gallery</span></span>
<span data-ttu-id="c4f01-124">integração de saudação tooconfigure de HappyFox no AD do Azure, você precisa tooadd HappyFox da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c4f01-124">tooconfigure hello integration of HappyFox into Azure AD, you need tooadd HappyFox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c4f01-125">**tooadd HappyFox da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4f01-125">**tooadd HappyFox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4f01-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c4f01-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4f01-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c4f01-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c4f01-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4f01-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c4f01-133">Na caixa de pesquisa hello, digite **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-133">In hello search box, type **HappyFox**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="c4f01-135">No painel de resultados de saudação, selecione **HappyFox**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c4f01-135">In hello results panel, select **HappyFox**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4f01-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4f01-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4f01-138">Nesta seção, você configurará e testará o logon único do Azure AD com o HappyFox, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="c4f01-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c4f01-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em HappyFox é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4f01-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HappyFox is tooa user in Azure AD.</span></span> <span data-ttu-id="c4f01-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em HappyFox precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c4f01-140">In other words, a link relationship between an Azure AD user and hello related user in HappyFox needs toobe established.</span></span>

<span data-ttu-id="c4f01-141">HappyFox, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4f01-141">In HappyFox, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c4f01-142">tooconfigure e teste de logon único do AD do Azure com HappyFox, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4f01-142">tooconfigure and test Azure AD single sign-on with HappyFox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c4f01-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c4f01-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c4f01-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4f01-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4f01-145">**[Criar um usuário de teste HappyFox](#creating-a-happyfox-test-user)**  -toohave um equivalente do Britta Simon em HappyFox é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c4f01-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - toohave a counterpart of Britta Simon in HappyFox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4f01-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c4f01-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4f01-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c4f01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4f01-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4f01-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4f01-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo HappyFox.</span><span class="sxs-lookup"><span data-stu-id="c4f01-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="c4f01-150">**tooconfigure AD do Azure-logon único com HappyFox, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4f01-150">**tooconfigure Azure AD single sign-on with HappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4f01-151">Em Olá portal do Azure, Olá **HappyFox** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-151">In hello Azure portal, on hello **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c4f01-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c4f01-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="c4f01-155">Em Olá **HappyFox domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4f01-155">On hello **HappyFox Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="c4f01-157">a.</span><span class="sxs-lookup"><span data-stu-id="c4f01-157">a.</span></span> <span data-ttu-id="c4f01-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="c4f01-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="c4f01-159">b.</span><span class="sxs-lookup"><span data-stu-id="c4f01-159">b.</span></span> <span data-ttu-id="c4f01-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="c4f01-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4f01-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c4f01-161">These values are not real.</span></span> <span data-ttu-id="c4f01-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="c4f01-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c4f01-163">Entre em contato com [equipe de suporte do cliente HappyFox](https://support.happyfox.com/home) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="c4f01-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) tooget these values.</span></span> 
 
4. <span data-ttu-id="c4f01-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c4f01-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="c4f01-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c4f01-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4f01-168">Em Olá **HappyFox configuração** seção, clique em **configurar HappyFox** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="c4f01-168">On hello **HappyFox Configuration** section, click **Configure HappyFox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c4f01-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="c4f01-171">Entre no portal de equipe HappyFox tooyour e navegue muito**gerenciar**, clique em **integrações** guia.</span><span class="sxs-lookup"><span data-stu-id="c4f01-171">Sign on tooyour HappyFox staff portal and navigate too**Manage**, Click on **Integrations** tab.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="c4f01-173">Na guia de integração de saudação, clique em **configurar** em **SAML integração** tooopen Olá logon único.</span><span class="sxs-lookup"><span data-stu-id="c4f01-173">In hello Integrations tab, Click **Configure** under **SAML Integration** tooopen hello Single Sign On Settings.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="c4f01-175">Dentro da seção de configuração do SAML, cole Olá **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure em **URL de destino SSO** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="c4f01-175">Inside SAML configuration section, paste hello **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="c4f01-177">Abra Olá certificado baixado do portal do Azure no bloco de notas e cole o conteúdo em **assinatura IdP** seção.</span><span class="sxs-lookup"><span data-stu-id="c4f01-177">Open hello certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="c4f01-179">Clique no botão **Salvar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-179">Click **Save Settings** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="c4f01-181">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c4f01-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c4f01-182">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c4f01-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c4f01-183">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4f01-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4f01-184">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4f01-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4f01-185">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4f01-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c4f01-187">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4f01-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4f01-188">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c4f01-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4f01-190">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4f01-192">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4f01-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4f01-194">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4f01-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4f01-196">a.</span><span class="sxs-lookup"><span data-stu-id="c4f01-196">a.</span></span> <span data-ttu-id="c4f01-197">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4f01-198">b.</span><span class="sxs-lookup"><span data-stu-id="c4f01-198">b.</span></span> <span data-ttu-id="c4f01-199">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c4f01-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4f01-200">c.</span><span class="sxs-lookup"><span data-stu-id="c4f01-200">c.</span></span> <span data-ttu-id="c4f01-201">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c4f01-202">d.</span><span class="sxs-lookup"><span data-stu-id="c4f01-202">d.</span></span> <span data-ttu-id="c4f01-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="c4f01-204">Criar um usuário de teste do HappyFox</span><span class="sxs-lookup"><span data-stu-id="c4f01-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="c4f01-205">Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação são criados automaticamente no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c4f01-205">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c4f01-206">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4f01-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c4f01-207">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHappyFox.</span><span class="sxs-lookup"><span data-stu-id="c4f01-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHappyFox.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c4f01-209">**tooassign Britta Simon tooHappyFox, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4f01-209">**tooassign Britta Simon tooHappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4f01-210">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c4f01-212">Na lista de aplicativos hello, selecione **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-212">In hello applications list, select **HappyFox**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="c4f01-214">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c4f01-216">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c4f01-216">Click **Add** button.</span></span> <span data-ttu-id="c4f01-217">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4f01-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c4f01-219">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4f01-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c4f01-220">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4f01-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4f01-221">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4f01-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4f01-222">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c4f01-222">Testing single sign-on</span></span>

<span data-ttu-id="c4f01-223">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4f01-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="c4f01-224">Quando você clica em bloco HappyFox Olá Olá painel de acesso, você deve obter a página de logon do aplicativo HappyFox.</span><span class="sxs-lookup"><span data-stu-id="c4f01-224">When you click hello HappyFox tile in hello Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="c4f01-225">Você deve ver Olá **'SAML'** botão na página de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="c4f01-225">You should see hello **‘SAML’** button on hello sign-in page.</span></span>

    ![Plug-in](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="c4f01-227">Clique em Olá **'SAML'** botão toolog em tooHappyFox usando sua conta do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4f01-227">Click hello **‘SAML’** button toolog in tooHappyFox using your Azure AD account.</span></span>

<span data-ttu-id="c4f01-228">Para obter mais informações sobre Olá painel de acesso, consulte [Introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4f01-228">For more information about hello Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c4f01-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c4f01-229">Additional resources</span></span>

* [<span data-ttu-id="c4f01-230">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c4f01-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4f01-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c4f01-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

