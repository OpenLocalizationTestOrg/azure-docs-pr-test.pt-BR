---
title: "Tutorial: Integração do Azure Active Directory com o Pantheon | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Pantheon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c3e54aef1f64dbab77d40a8c098172d609bfec8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="5b7dc-103">Tutorial: Integração do Azure Active Directory com o Pantheon</span><span class="sxs-lookup"><span data-stu-id="5b7dc-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="5b7dc-104">Neste tutorial, você aprenderá como toointegrate Pantheon com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5b7dc-104">In this tutorial, you learn how toointegrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b7dc-105">Integrando Pantheon com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b7dc-105">Integrating Pantheon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b7dc-106">Você pode controlar no AD do Azure que tenha acesso tooPantheon</span><span class="sxs-lookup"><span data-stu-id="5b7dc-106">You can control in Azure AD who has access tooPantheon</span></span>
- <span data-ttu-id="5b7dc-107">Você pode habilitar seu usuários tooautomatically get conectado tooPantheon (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5b7dc-107">You can enable your users tooautomatically get signed-on tooPantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b7dc-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5b7dc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b7dc-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b7dc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b7dc-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5b7dc-110">Prerequisites</span></span>

<span data-ttu-id="5b7dc-111">tooconfigure integração do AD do Azure com Pantheon, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b7dc-111">tooconfigure Azure AD integration with Pantheon, you need hello following items:</span></span>

- <span data-ttu-id="5b7dc-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5b7dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b7dc-113">Uma assinatura do Pantheon habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="5b7dc-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b7dc-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b7dc-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5b7dc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b7dc-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b7dc-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b7dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b7dc-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5b7dc-118">Scenario description</span></span>
<span data-ttu-id="5b7dc-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b7dc-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="5b7dc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b7dc-121">Adicionando Pantheon da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5b7dc-121">Adding Pantheon from hello gallery</span></span>
2. <span data-ttu-id="5b7dc-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5b7dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-hello-gallery"></a><span data-ttu-id="5b7dc-123">Adicionando Pantheon da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5b7dc-123">Adding Pantheon from hello gallery</span></span>
<span data-ttu-id="5b7dc-124">integração de saudação tooconfigure de Pantheon no AD do Azure, você precisa tooadd Pantheon da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-124">tooconfigure hello integration of Pantheon into Azure AD, you need tooadd Pantheon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b7dc-125">**tooadd Pantheon da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5b7dc-125">**tooadd Pantheon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b7dc-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b7dc-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b7dc-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5b7dc-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5b7dc-133">Na caixa de pesquisa hello, digite **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-133">In hello search box, type **Pantheon**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="5b7dc-135">No painel de resultados de saudação, selecione **Pantheon**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-135">In hello results panel, select **Pantheon**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b7dc-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5b7dc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b7dc-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Pantheon, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b7dc-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Pantheon é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pantheon is tooa user in Azure AD.</span></span> <span data-ttu-id="5b7dc-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Pantheon precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-140">In other words, a link relationship between an Azure AD user and hello related user in Pantheon needs toobe established.</span></span>

<span data-ttu-id="5b7dc-141">Pantheon, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-141">In Pantheon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5b7dc-142">tooconfigure e teste de logon único do AD do Azure com Pantheon, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b7dc-142">tooconfigure and test Azure AD single sign-on with Pantheon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b7dc-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b7dc-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b7dc-145">**[Criar um usuário de teste Pantheon](#creating-a-pantheon-test-user)**  -toohave um equivalente do Britta Simon em Pantheon é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - toohave a counterpart of Britta Simon in Pantheon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b7dc-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b7dc-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b7dc-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b7dc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b7dc-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Pantheon.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="5b7dc-150">**tooconfigure AD do Azure-logon único com Pantheon, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5b7dc-150">**tooconfigure Azure AD single sign-on with Pantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b7dc-151">Em Olá portal do Azure, Olá **Pantheon** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-151">In hello Azure portal, on hello **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5b7dc-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="5b7dc-155">Em Olá **Pantheon domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b7dc-155">On hello **Pantheon Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="5b7dc-157">a.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-157">a.</span></span> <span data-ttu-id="5b7dc-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="5b7dc-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="5b7dc-159">b.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-159">b.</span></span> <span data-ttu-id="5b7dc-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="5b7dc-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b7dc-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-161">These values are not real.</span></span> <span data-ttu-id="5b7dc-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="5b7dc-163">Entre em contato com [a equipe de suporte Pantheon](https://pantheon.io/docs/getting-support/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) tooget these values.</span></span>

4. <span data-ttu-id="5b7dc-164">Aplicativo de pantheon espera de asserção SAML Olá em formato específico, o que exige que você tooset Olá UserIdentifier o valor do atributo com o endereço de email do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-164">Pantheon application expects hello SAML assertion in specific format, which requires you tooset hello UserIdentifier attribute value with hello user’s email address.</span></span> <span data-ttu-id="5b7dc-165">Por padrão o AD do Azure usa Olá UserPrincipalName UserIdentifier atributo.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-165">By default Azure AD uses hello UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="5b7dc-166">Mas, para integração bem-sucedida, é necessário tooadjust toomatch esse valor com o endereço de email do usuário.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-166">But for successful integration you need tooadjust this value toomatch with user’s email address.</span></span> <span data-ttu-id="5b7dc-167">integração de saudação só funcionará depois de fazer o mapeamento correto do hello.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-167">hello integration will only work after doing hello correct mapping.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="5b7dc-169">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="5b7dc-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5b7dc-171">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5b7dc-173">Em Olá **Pantheon configuração** seção, clique em **configurar Pantheon** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-173">On hello **Pantheon Configuration** section, click **Configure Pantheon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5b7dc-174">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="5b7dc-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="5b7dc-176">tooconfigure logon único no **Pantheon** lado, você precisa toosend Olá baixado **certificado** e **Single Sign-On URL do serviço SAML** muito[Pantheon equipe de suporte](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="5b7dc-176">tooconfigure single sign-on on **Pantheon** side, you need toosend hello downloaded **Certificate** and **SAML Single Sign-On Service URL** too[Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="5b7dc-177">Você também precisa tooprovide informações de domínio de Email de saudação e a hora de data quando desejar tooenable essa conexão.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-177">You also need tooprovide hello Email Domain(s) information and Date Time when you want tooenable this connection.</span></span> <span data-ttu-id="5b7dc-178">Você pode encontrar mais detalhes sobre isso [aqui](https://pantheon.io/docs/sso-organizations/)</span><span class="sxs-lookup"><span data-stu-id="5b7dc-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="5b7dc-179">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="5b7dc-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b7dc-180">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b7dc-181">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b7dc-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b7dc-182">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5b7dc-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b7dc-183">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5b7dc-185">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5b7dc-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b7dc-186">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b7dc-188">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b7dc-190">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b7dc-192">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b7dc-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b7dc-194">a.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-194">a.</span></span> <span data-ttu-id="5b7dc-195">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b7dc-196">b.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-196">b.</span></span> <span data-ttu-id="5b7dc-197">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b7dc-198">c.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-198">c.</span></span> <span data-ttu-id="5b7dc-199">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b7dc-200">d.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-200">d.</span></span> <span data-ttu-id="5b7dc-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="5b7dc-202">Criação de um usuário de teste do Pantheon</span><span class="sxs-lookup"><span data-stu-id="5b7dc-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="5b7dc-203">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Pantheon.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="5b7dc-204">Siga Olá abaixo de usuário de saudação etapas tooadd em Pantheon.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-204">Please follow hello below steps tooadd hello user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="5b7dc-205">Para SSO toowork usuário precisa toobe criado primeiro em Pantheon.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-205">For SSO toowork user needs toobe created first in Pantheon.</span></span>

1. <span data-ttu-id="5b7dc-206">TooPantheon de logon com credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-206">Login tooPantheon with admin credentials.</span></span>

2. <span data-ttu-id="5b7dc-207">Navegue muito**organização** página do painel.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-207">Navigate too**Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="5b7dc-208">Clique em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-208">Click **People**.</span></span>

4. <span data-ttu-id="5b7dc-209">Clique em **Adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-209">Click **Add user**.</span></span>

5. <span data-ttu-id="5b7dc-210">Insira o endereço de email do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-210">Enter hello user's email address.</span></span>

6. <span data-ttu-id="5b7dc-211">Escolha a função de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-211">Choose hello user's role.</span></span>

7. <span data-ttu-id="5b7dc-212">Clique em **Adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-212">Click **Add user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b7dc-213">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5b7dc-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b7dc-214">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPantheon.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPantheon.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5b7dc-216">**tooassign Britta Simon tooPantheon, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5b7dc-216">**tooassign Britta Simon tooPantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b7dc-217">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5b7dc-219">Na lista de aplicativos hello, selecione **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-219">In hello applications list, select **Pantheon**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="5b7dc-221">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5b7dc-223">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-223">Click **Add** button.</span></span> <span data-ttu-id="5b7dc-224">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5b7dc-226">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b7dc-227">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b7dc-228">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b7dc-229">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5b7dc-229">Testing single sign-on</span></span>

<span data-ttu-id="5b7dc-230">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5b7dc-231">Quando você clica em bloco Pantheon Olá Olá painel de acesso, você deve obter o aplicativo de Pantheon tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="5b7dc-231">When you click hello Pantheon tile in hello Access Panel, you should get automatically signed-on tooyour Pantheon application.</span></span>
<span data-ttu-id="5b7dc-232">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5b7dc-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5b7dc-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5b7dc-233">Additional resources</span></span>

* [<span data-ttu-id="5b7dc-234">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5b7dc-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b7dc-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b7dc-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

