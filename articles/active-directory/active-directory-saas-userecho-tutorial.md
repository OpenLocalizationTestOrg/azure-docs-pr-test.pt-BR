---
title: "Tutorial: integração do Azure Active Directory ao UserEcho | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e UserEcho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="e8368-103">Tutorial: Integração do Active Directory do Azure com o UserEcho</span><span class="sxs-lookup"><span data-stu-id="e8368-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="e8368-104">Neste tutorial, você aprenderá como toointegrate UserEcho com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="e8368-104">In this tutorial, you learn how toointegrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8368-105">Integrando UserEcho com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8368-105">Integrating UserEcho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e8368-106">Você pode controlar no AD do Azure que tenha acesso tooUserEcho</span><span class="sxs-lookup"><span data-stu-id="e8368-106">You can control in Azure AD who has access tooUserEcho</span></span>
- <span data-ttu-id="e8368-107">Você pode habilitar seu usuários tooautomatically get conectado tooUserEcho (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e8368-107">You can enable your users tooautomatically get signed-on tooUserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e8368-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e8368-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e8368-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e8368-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8368-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e8368-110">Prerequisites</span></span>

<span data-ttu-id="e8368-111">tooconfigure integração do AD do Azure com UserEcho, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8368-111">tooconfigure Azure AD integration with UserEcho, you need hello following items:</span></span>

- <span data-ttu-id="e8368-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e8368-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8368-113">Uma assinatura do UserEcho habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="e8368-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8368-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e8368-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8368-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e8368-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8368-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e8368-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e8368-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8368-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8368-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e8368-118">Scenario description</span></span>
<span data-ttu-id="e8368-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e8368-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8368-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="e8368-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8368-121">Adicionando UserEcho da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e8368-121">Adding UserEcho from hello gallery</span></span>
2. <span data-ttu-id="e8368-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e8368-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-hello-gallery"></a><span data-ttu-id="e8368-123">Adicionando UserEcho da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e8368-123">Adding UserEcho from hello gallery</span></span>
<span data-ttu-id="e8368-124">integração de saudação tooconfigure de UserEcho no AD do Azure, você precisa tooadd UserEcho da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e8368-124">tooconfigure hello integration of UserEcho into Azure AD, you need tooadd UserEcho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e8368-125">**tooadd UserEcho da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e8368-125">**tooadd UserEcho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8368-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e8368-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e8368-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e8368-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e8368-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e8368-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e8368-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e8368-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e8368-133">Na caixa de pesquisa hello, digite **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="e8368-133">In hello search box, type **UserEcho**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="e8368-135">No painel de resultados de saudação, selecione **UserEcho**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e8368-135">In hello results panel, select **UserEcho**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e8368-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e8368-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e8368-138">Nesta seção, você configurará e testará o logon único do Azure AD com o UserEcho com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e8368-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e8368-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em UserEcho é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8368-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserEcho is tooa user in Azure AD.</span></span> <span data-ttu-id="e8368-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em UserEcho precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e8368-140">In other words, a link relationship between an Azure AD user and hello related user in UserEcho needs toobe established.</span></span>

<span data-ttu-id="e8368-141">UserEcho, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8368-141">In UserEcho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e8368-142">tooconfigure e teste de logon único do AD do Azure com UserEcho, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8368-142">tooconfigure and test Azure AD single sign-on with UserEcho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e8368-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e8368-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e8368-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8368-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8368-145">**[Criar um usuário de teste UserEcho](#creating-a-userecho-test-user)**  -toohave um equivalente do Britta Simon em UserEcho é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="e8368-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - toohave a counterpart of Britta Simon in UserEcho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e8368-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="e8368-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8368-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="e8368-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e8368-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8368-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e8368-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo UserEcho.</span><span class="sxs-lookup"><span data-stu-id="e8368-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="e8368-150">**tooconfigure AD do Azure-logon único com UserEcho, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e8368-150">**tooconfigure Azure AD single sign-on with UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8368-151">Em Olá portal do Azure, Olá **UserEcho** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="e8368-151">In hello Azure portal, on hello **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e8368-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="e8368-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="e8368-155">Em Olá **UserEcho domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8368-155">On hello **UserEcho Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="e8368-157">a.</span><span class="sxs-lookup"><span data-stu-id="e8368-157">a.</span></span> <span data-ttu-id="e8368-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="e8368-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="e8368-159">b.</span><span class="sxs-lookup"><span data-stu-id="e8368-159">b.</span></span> <span data-ttu-id="e8368-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="e8368-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e8368-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e8368-161">These values are not real.</span></span> <span data-ttu-id="e8368-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="e8368-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e8368-163">Entre em contato com [equipe de suporte do cliente UserEcho](https://feedback.userecho.com/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="e8368-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) tooget these values.</span></span> 

4. <span data-ttu-id="e8368-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e8368-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="e8368-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e8368-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e8368-168">Em Olá **UserEcho configuração** seção, clique em **configurar UserEcho** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="e8368-168">On hello **UserEcho Configuration** section, click **Configure UserEcho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e8368-169">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="e8368-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="e8368-171">Em outra janela do navegador, entre no site da empresa UserEcho tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="e8368-171">In another browser window, sign on tooyour UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="e8368-172">Na barra de ferramentas de saudação na parte superior do hello, clique em seu menu de saudação de tooexpand de nome de usuário e, em seguida, clique em **instalação**.</span><span class="sxs-lookup"><span data-stu-id="e8368-172">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="e8368-174">Clique em **Integrações**.</span><span class="sxs-lookup"><span data-stu-id="e8368-174">Click **Integrations**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="e8368-176">Clique em **site** e em **Logon único (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="e8368-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="e8368-178">Em Olá **(SAML) de logon único** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8368-178">On hello **Single sign-on (SAML)** page, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="e8368-180">a.</span><span class="sxs-lookup"><span data-stu-id="e8368-180">a.</span></span> <span data-ttu-id="e8368-181">Para **Habilitado para SAML**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="e8368-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="e8368-182">b.</span><span class="sxs-lookup"><span data-stu-id="e8368-182">b.</span></span> <span data-ttu-id="e8368-183">Colar **Single Sign-On URL do serviço SAML**, que você copiou de saudação portal do Azure em hello **URL SSO SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e8368-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="e8368-184">c.</span><span class="sxs-lookup"><span data-stu-id="e8368-184">c.</span></span> <span data-ttu-id="e8368-185">Colar **URL de logout**, que você copiou de saudação portal do Azure em hello **logoout remoto URL** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e8368-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="e8368-186">d.</span><span class="sxs-lookup"><span data-stu-id="e8368-186">d.</span></span> <span data-ttu-id="e8368-187">Abra seu certificado baixado no bloco de notas, Olá de cópia de conteúdo e, em seguida, cole-o em Olá **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e8368-187">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="e8368-188">e.</span><span class="sxs-lookup"><span data-stu-id="e8368-188">e.</span></span> <span data-ttu-id="e8368-189">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e8368-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e8368-190">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="e8368-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e8368-191">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="e8368-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e8368-192">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e8368-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e8368-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e8368-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="e8368-194">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8368-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e8368-196">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e8368-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8368-197">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e8368-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e8368-199">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="e8368-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e8368-201">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8368-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e8368-203">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8368-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e8368-205">a.</span><span class="sxs-lookup"><span data-stu-id="e8368-205">a.</span></span> <span data-ttu-id="e8368-206">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8368-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8368-207">b.</span><span class="sxs-lookup"><span data-stu-id="e8368-207">b.</span></span> <span data-ttu-id="e8368-208">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e8368-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e8368-209">c.</span><span class="sxs-lookup"><span data-stu-id="e8368-209">c.</span></span> <span data-ttu-id="e8368-210">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="e8368-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e8368-211">d.</span><span class="sxs-lookup"><span data-stu-id="e8368-211">d.</span></span> <span data-ttu-id="e8368-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e8368-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="e8368-213">Criando um usuário de teste do UserEcho</span><span class="sxs-lookup"><span data-stu-id="e8368-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="e8368-214">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no UserEcho.</span><span class="sxs-lookup"><span data-stu-id="e8368-214">hello objective of this section is toocreate a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="e8368-215">**toocreate um usuário chamado Britta Simon no UserEcho, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e8368-215">**toocreate a user called Britta Simon in UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8368-216">Site de empresa de UserEcho tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="e8368-216">Sign-on tooyour UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="e8368-217">Na barra de ferramentas de saudação na parte superior do hello, clique em seu menu de saudação de tooexpand de nome de usuário e, em seguida, clique em **instalação**.</span><span class="sxs-lookup"><span data-stu-id="e8368-217">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="e8368-219">Clique em **usuários**, Olá tooexpand **usuários** seção.</span><span class="sxs-lookup"><span data-stu-id="e8368-219">Click **Users**, tooexpand hello **Users** section.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="e8368-221">Clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="e8368-221">Click **Users**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="e8368-223">Clique em **Convidar um novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="e8368-223">Click **Invite a new user**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="e8368-225">Em Olá **convidar um novo usuário** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8368-225">On hello **Invite a new user** dialog, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="e8368-227">a.</span><span class="sxs-lookup"><span data-stu-id="e8368-227">a.</span></span> <span data-ttu-id="e8368-228">Em Olá **nome** caixa de texto, nome de usuário, Olá como Britta Simon tipo.</span><span class="sxs-lookup"><span data-stu-id="e8368-228">In hello **Name** textbox, type name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="e8368-229">b.</span><span class="sxs-lookup"><span data-stu-id="e8368-229">b.</span></span>  <span data-ttu-id="e8368-230">Em Olá **Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e8368-230">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="e8368-231">c.</span><span class="sxs-lookup"><span data-stu-id="e8368-231">c.</span></span> <span data-ttu-id="e8368-232">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="e8368-232">Click **Invite**.</span></span>

<span data-ttu-id="e8368-233">Um convite é enviado tooBritta, que permite que seu toostart usando UserEcho.</span><span class="sxs-lookup"><span data-stu-id="e8368-233">An invitation is sent tooBritta, which enables her toostart using UserEcho.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e8368-234">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e8368-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e8368-235">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooUserEcho.</span><span class="sxs-lookup"><span data-stu-id="e8368-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserEcho.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e8368-237">**tooassign Britta Simon tooUserEcho, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e8368-237">**tooassign Britta Simon tooUserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8368-238">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e8368-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e8368-240">Na lista de aplicativos hello, selecione **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="e8368-240">In hello applications list, select **UserEcho**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="e8368-242">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e8368-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e8368-244">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e8368-244">Click **Add** button.</span></span> <span data-ttu-id="e8368-245">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e8368-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e8368-247">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8368-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e8368-248">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e8368-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8368-249">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e8368-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e8368-250">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e8368-250">Testing single sign-on</span></span>

<span data-ttu-id="e8368-251">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e8368-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="e8368-252">Quando você clica em bloco UserEcho Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour UserEcho aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8368-252">When you click hello UserEcho tile in hello Access Panel, you should get automatically signed-on tooyour UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e8368-253">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e8368-253">Additional resources</span></span>

* [<span data-ttu-id="e8368-254">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e8368-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8368-255">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e8368-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

