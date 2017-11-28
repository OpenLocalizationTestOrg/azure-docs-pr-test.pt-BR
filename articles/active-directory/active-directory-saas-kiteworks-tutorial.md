---
title: "Tutorial: integração do Azure Active Directory ao Kiteworks | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Kiteworks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 406417dd7f58cc3f1fa0d9e86b5cad0c1d7be750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="64be9-103">Tutorial: Integração do Active Directory do Azure com o Kiteworks</span><span class="sxs-lookup"><span data-stu-id="64be9-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="64be9-104">Neste tutorial, você aprenderá como toointegrate Kiteworks com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="64be9-104">In this tutorial, you learn how toointegrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64be9-105">Integrando Kiteworks com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="64be9-105">Integrating Kiteworks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="64be9-106">Você pode controlar no AD do Azure que tenha acesso tooKiteworks</span><span class="sxs-lookup"><span data-stu-id="64be9-106">You can control in Azure AD who has access tooKiteworks</span></span>
- <span data-ttu-id="64be9-107">Você pode habilitar seus usuários tooautomatically get conectado tooKiteworks (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64be9-107">You can enable your users tooautomatically get signed-on tooKiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="64be9-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="64be9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="64be9-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64be9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64be9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="64be9-110">Prerequisites</span></span>

<span data-ttu-id="64be9-111">tooconfigure integração do AD do Azure com Kiteworks, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="64be9-111">tooconfigure Azure AD integration with Kiteworks, you need hello following items:</span></span>

- <span data-ttu-id="64be9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64be9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64be9-113">Uma assinatura habilitada para logon único do Kiteworks</span><span class="sxs-lookup"><span data-stu-id="64be9-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64be9-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="64be9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64be9-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="64be9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64be9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="64be9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64be9-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64be9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64be9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="64be9-118">Scenario description</span></span>
<span data-ttu-id="64be9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="64be9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64be9-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="64be9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64be9-121">Adicionando Kiteworks da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="64be9-121">Adding Kiteworks from hello gallery</span></span>
2. <span data-ttu-id="64be9-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64be9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-hello-gallery"></a><span data-ttu-id="64be9-123">Adicionando Kiteworks da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="64be9-123">Adding Kiteworks from hello gallery</span></span>
<span data-ttu-id="64be9-124">integração de saudação tooconfigure de Kiteworks no AD do Azure, você precisa tooadd Kiteworks da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="64be9-124">tooconfigure hello integration of Kiteworks into Azure AD, you need tooadd Kiteworks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="64be9-125">**tooadd Kiteworks da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64be9-125">**tooadd Kiteworks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="64be9-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="64be9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="64be9-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="64be9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="64be9-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="64be9-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="64be9-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64be9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="64be9-133">Na caixa de pesquisa hello, digite **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="64be9-133">In hello search box, type **Kiteworks**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="64be9-135">No painel de resultados de saudação, selecione **Kiteworks**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="64be9-135">In hello results panel, select **Kiteworks**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="64be9-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64be9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="64be9-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Kiteworks, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="64be9-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="64be9-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Kiteworks é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="64be9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kiteworks is tooa user in Azure AD.</span></span> <span data-ttu-id="64be9-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Kiteworks precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="64be9-140">In other words, a link relationship between an Azure AD user and hello related user in Kiteworks needs toobe established.</span></span>

<span data-ttu-id="64be9-141">Kiteworks, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="64be9-141">In Kiteworks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="64be9-142">tooconfigure e teste de logon único do AD do Azure com Kiteworks, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="64be9-142">tooconfigure and test Azure AD single sign-on with Kiteworks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="64be9-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="64be9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="64be9-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64be9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64be9-145">**[Criar um usuário de teste Kiteworks](#creating-a-kiteworks-test-user)**  -toohave um equivalente do Britta Simon em Kiteworks é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="64be9-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - toohave a counterpart of Britta Simon in Kiteworks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="64be9-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="64be9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64be9-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="64be9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="64be9-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="64be9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="64be9-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="64be9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="64be9-150">**tooconfigure AD do Azure-logon único com Kiteworks, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64be9-150">**tooconfigure Azure AD single sign-on with Kiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="64be9-151">Em Olá portal do Azure, Olá **Kiteworks** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="64be9-151">In hello Azure portal, on hello **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="64be9-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="64be9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="64be9-155">Em Olá **Kiteworks domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="64be9-155">On hello **Kiteworks Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="64be9-157">a.</span><span class="sxs-lookup"><span data-stu-id="64be9-157">a.</span></span> <span data-ttu-id="64be9-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="64be9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="64be9-159">b.</span><span class="sxs-lookup"><span data-stu-id="64be9-159">b.</span></span> <span data-ttu-id="64be9-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="64be9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="64be9-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="64be9-161">These values are not real.</span></span> <span data-ttu-id="64be9-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="64be9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="64be9-163">Entre em contato com [equipe de suporte do cliente Kiteworks](http://accellion.com/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="64be9-163">Contact [Kiteworks Client support team](http://accellion.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="64be9-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="64be9-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="64be9-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="64be9-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="64be9-168">Em Olá **Kiteworks configuração** seção, clique em **configurar Kiteworks** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="64be9-168">On hello **Kiteworks Configuration** section, click **Configure Kiteworks** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="64be9-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="64be9-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="64be9-171">Site da empresa tooyour Kiteworks com logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="64be9-171">Sign on tooyour Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="64be9-172">Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="64be9-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="64be9-174">Em Olá **autenticação e autorização** seção, clique em **SSO instalação**.</span><span class="sxs-lookup"><span data-stu-id="64be9-174">In hello **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="64be9-176">Na página de configuração de SSO de hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="64be9-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="64be9-178">a.</span><span class="sxs-lookup"><span data-stu-id="64be9-178">a.</span></span> <span data-ttu-id="64be9-179">Selecione **Autenticar via SSO**.</span><span class="sxs-lookup"><span data-stu-id="64be9-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="64be9-180">b.</span><span class="sxs-lookup"><span data-stu-id="64be9-180">b.</span></span> <span data-ttu-id="64be9-181">Selecione **Iniciar AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="64be9-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="64be9-182">c.</span><span class="sxs-lookup"><span data-stu-id="64be9-182">c.</span></span> <span data-ttu-id="64be9-183">Em hello **ID da entidade IDP** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64be9-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="64be9-184">d.</span><span class="sxs-lookup"><span data-stu-id="64be9-184">d.</span></span> <span data-ttu-id="64be9-185">Em Olá **o URL de serviço de logon único** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64be9-185">In hello **Single Sign-On Service URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="64be9-186">e.</span><span class="sxs-lookup"><span data-stu-id="64be9-186">e.</span></span> <span data-ttu-id="64be9-187">Em Olá **URL do serviço de Logout único** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64be9-187">In hello **Single Logout Service URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="64be9-188">f.</span><span class="sxs-lookup"><span data-stu-id="64be9-188">f.</span></span> <span data-ttu-id="64be9-189">Abra seu certificado baixado no bloco de notas, Olá de cópia de conteúdo e, em seguida, cole-o em Olá **o certificado de chave pública RSA** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="64be9-189">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="64be9-190">g.</span><span class="sxs-lookup"><span data-stu-id="64be9-190">g.</span></span> <span data-ttu-id="64be9-191">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="64be9-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="64be9-192">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="64be9-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="64be9-193">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="64be9-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="64be9-194">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="64be9-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="64be9-195">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64be9-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="64be9-196">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64be9-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="64be9-198">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64be9-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="64be9-199">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="64be9-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="64be9-201">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="64be9-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="64be9-203">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="64be9-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64be9-205">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="64be9-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="64be9-207">a.</span><span class="sxs-lookup"><span data-stu-id="64be9-207">a.</span></span> <span data-ttu-id="64be9-208">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64be9-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64be9-209">b.</span><span class="sxs-lookup"><span data-stu-id="64be9-209">b.</span></span> <span data-ttu-id="64be9-210">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="64be9-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="64be9-211">c.</span><span class="sxs-lookup"><span data-stu-id="64be9-211">c.</span></span> <span data-ttu-id="64be9-212">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="64be9-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="64be9-213">d.</span><span class="sxs-lookup"><span data-stu-id="64be9-213">d.</span></span> <span data-ttu-id="64be9-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="64be9-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="64be9-215">Criar um usuário de teste do Kiteworks</span><span class="sxs-lookup"><span data-stu-id="64be9-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="64be9-216">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="64be9-216">hello objective of this section is toocreate a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="64be9-217">O Kiteworks oferece suporte ao provisionamento Just-In-Time, que é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="64be9-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="64be9-218">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="64be9-218">There is no action item for you in this section.</span></span> <span data-ttu-id="64be9-219">Um novo usuário é criado durante uma tentativa tooaccess Kitewors se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="64be9-219">A new user is created during an attempt tooaccess Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="64be9-220">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [equipe de suporte do Kiteworks](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="64be9-220">If you need toocreate a user manually, you need toocontact hello [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="64be9-221">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64be9-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="64be9-222">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooKiteworks.</span><span class="sxs-lookup"><span data-stu-id="64be9-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKiteworks.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="64be9-224">**tooassign Britta Simon tooKiteworks, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64be9-224">**tooassign Britta Simon tooKiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="64be9-225">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="64be9-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="64be9-227">Na lista de aplicativos hello, selecione **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="64be9-227">In hello applications list, select **Kiteworks**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="64be9-229">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="64be9-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="64be9-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="64be9-231">Click **Add** button.</span></span> <span data-ttu-id="64be9-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64be9-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="64be9-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="64be9-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="64be9-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64be9-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64be9-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64be9-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="64be9-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="64be9-237">Testing single sign-on</span></span>

<span data-ttu-id="64be9-238">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="64be9-238">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="64be9-239">Quando você clica em Olá Kiteworks bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Kiteworks aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64be9-239">When you click hello Kiteworks tile in hello Access Panel, you should get automatically signed-on tooyour Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64be9-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="64be9-240">Additional resources</span></span>

* [<span data-ttu-id="64be9-241">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="64be9-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64be9-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="64be9-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

