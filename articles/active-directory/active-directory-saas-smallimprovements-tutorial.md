---
title: "Tutorial: Integração do Azure Active Directory com o Small Improvements | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e pequenas melhorias."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33213fe4b61f5005cf78bee2c05b2b1e5e71ae8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="3c70d-103">Tutorial: Integração do Active Directory do Azure com o Small Improvements</span><span class="sxs-lookup"><span data-stu-id="3c70d-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="3c70d-104">Neste tutorial, você aprenderá como toointegrate pequenas melhorias com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="3c70d-104">In this tutorial, you learn how toointegrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3c70d-105">Integrando pequenas melhorias do AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c70d-105">Integrating Small Improvements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3c70d-106">Você pode controlar no AD do Azure que tenha acesso tooSmall melhorias</span><span class="sxs-lookup"><span data-stu-id="3c70d-106">You can control in Azure AD who has access tooSmall Improvements</span></span>
- <span data-ttu-id="3c70d-107">Você pode habilitar seu usuários tooautomatically get conectado tooSmall melhorias (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c70d-107">You can enable your users tooautomatically get signed-on tooSmall Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3c70d-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3c70d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3c70d-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3c70d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c70d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3c70d-110">Prerequisites</span></span>

<span data-ttu-id="3c70d-111">tooconfigure integração do AD do Azure com pequenas melhorias, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c70d-111">tooconfigure Azure AD integration with Small Improvements, you need hello following items:</span></span>

- <span data-ttu-id="3c70d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c70d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3c70d-113">Uma assinatura habilitada para logon único do Small Improvements</span><span class="sxs-lookup"><span data-stu-id="3c70d-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3c70d-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3c70d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3c70d-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3c70d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3c70d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3c70d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3c70d-117">Caso não tenha um ambiente de avaliação do Azure AD, obtenha uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c70d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3c70d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3c70d-118">Scenario description</span></span>
<span data-ttu-id="3c70d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3c70d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3c70d-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="3c70d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3c70d-121">Adicionando pequenas melhorias na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3c70d-121">Adding Small Improvements from hello gallery</span></span>
2. <span data-ttu-id="3c70d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c70d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-hello-gallery"></a><span data-ttu-id="3c70d-123">Adicionando pequenas melhorias na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3c70d-123">Adding Small Improvements from hello gallery</span></span>
<span data-ttu-id="3c70d-124">integração de saudação tooconfigure pequenas melhorias no AD do Azure, você precisa tooadd pequenas melhorias na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3c70d-124">tooconfigure hello integration of Small Improvements into Azure AD, you need tooadd Small Improvements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3c70d-125">**tooadd pequenas melhorias na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3c70d-125">**tooadd Small Improvements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c70d-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3c70d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3c70d-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3c70d-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3c70d-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c70d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3c70d-133">Na caixa de pesquisa hello, digite **pequenas melhorias**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-133">In hello search box, type **Small Improvements**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="3c70d-135">No painel de resultados de saudação, selecione **pequenas melhorias**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3c70d-135">In hello results panel, select **Small Improvements**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3c70d-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c70d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3c70d-138">Nesta seção, você configura e testa o logon único do Azure AD com o Small Improvements, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3c70d-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3c70d-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em pequenas melhorias é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c70d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Small Improvements is tooa user in Azure AD.</span></span> <span data-ttu-id="3c70d-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em pequenas melhorias precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3c70d-140">In other words, a link relationship between an Azure AD user and hello related user in Small Improvements needs toobe established.</span></span>

<span data-ttu-id="3c70d-141">Pequenas melhorias, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c70d-141">In Small Improvements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3c70d-142">tooconfigure e teste de logon único do AD do Azure com pequenas melhorias, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c70d-142">tooconfigure and test Azure AD single sign-on with Small Improvements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3c70d-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3c70d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3c70d-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3c70d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3c70d-145">**[Criar um usuário de teste pequenas melhorias](#creating-a-small-improvements-test-user)**  -toohave um equivalente do Britta Simon em pequenas melhorias que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3c70d-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - toohave a counterpart of Britta Simon in Small Improvements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3c70d-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="3c70d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3c70d-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="3c70d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3c70d-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c70d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3c70d-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo pequenas melhorias.</span><span class="sxs-lookup"><span data-stu-id="3c70d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="3c70d-150">**tooconfigure AD do Azure-logon único com pequenas melhorias, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3c70d-150">**tooconfigure Azure AD single sign-on with Small Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c70d-151">Em Olá portal do Azure, Olá **pequenas melhorias** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-151">In hello Azure portal, on hello **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3c70d-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="3c70d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="3c70d-155">Em Olá **pequeno domínio aprimoramentos e as URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c70d-155">On hello **Small Improvements Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="3c70d-157">a.</span><span class="sxs-lookup"><span data-stu-id="3c70d-157">a.</span></span> <span data-ttu-id="3c70d-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="3c70d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="3c70d-159">b.</span><span class="sxs-lookup"><span data-stu-id="3c70d-159">b.</span></span> <span data-ttu-id="3c70d-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="3c70d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3c70d-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="3c70d-161">These values are not real.</span></span> <span data-ttu-id="3c70d-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="3c70d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3c70d-163">Entre em contato com [equipe de suporte do cliente de pequenas melhorias](mailto:support@small-improvements.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="3c70d-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="3c70d-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3c70d-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="3c70d-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3c70d-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3c70d-168">Em Olá **configuração melhorias pequena** seção, clique em **configurar pequenas melhorias** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="3c70d-168">On hello **Small Improvements Configuration** section, click **Configure Small Improvements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3c70d-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="3c70d-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="3c70d-171">Em outra janela do navegador, entre no site da empresa tooyour pequenas melhorias como um administrador.</span><span class="sxs-lookup"><span data-stu-id="3c70d-171">In another browser window, sign on tooyour Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="3c70d-172">Na página de painel principal hello, clique **administração** botão Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="3c70d-172">From hello main dashboard page, click **Administration** button on hello left.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="3c70d-174">Clique em Olá **SSO do SAML** botão de **integrações** seção.</span><span class="sxs-lookup"><span data-stu-id="3c70d-174">Click hello **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="3c70d-176">Na página de configuração de SSO de hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c70d-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="3c70d-178">a.</span><span class="sxs-lookup"><span data-stu-id="3c70d-178">a.</span></span> <span data-ttu-id="3c70d-179">Em Olá **ponto de extremidade HTTP** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c70d-179">In hello **HTTP Endpoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3c70d-180">b.</span><span class="sxs-lookup"><span data-stu-id="3c70d-180">b.</span></span> <span data-ttu-id="3c70d-181">Abra seu certificado baixado no bloco de notas, Olá de cópia de conteúdo e, em seguida, cole-o em Olá **x509 certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3c70d-181">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="3c70d-182">c.</span><span class="sxs-lookup"><span data-stu-id="3c70d-182">c.</span></span> <span data-ttu-id="3c70d-183">Se você quiser toohave SSO e logon formulário opção de autenticação disponível para usuários, marque Olá **habilitar o acesso por meio de logon e senha muito** opção.</span><span class="sxs-lookup"><span data-stu-id="3c70d-183">If you wish toohave SSO and Login form authentication option available for users, then check hello **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="3c70d-184">d.</span><span class="sxs-lookup"><span data-stu-id="3c70d-184">d.</span></span> <span data-ttu-id="3c70d-185">Insira o botão de logon de SSO de saudação do hello valor apropriado tooName em Olá **SAML Prompt** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3c70d-185">Enter hello appropriate value tooName hello SSO Login button in hello **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="3c70d-186">e.</span><span class="sxs-lookup"><span data-stu-id="3c70d-186">e.</span></span> <span data-ttu-id="3c70d-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3c70d-188">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="3c70d-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3c70d-189">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="3c70d-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3c70d-190">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3c70d-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3c70d-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c70d-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="3c70d-192">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c70d-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3c70d-194">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3c70d-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c70d-195">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3c70d-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3c70d-197">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3c70d-199">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c70d-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3c70d-201">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c70d-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3c70d-203">a.</span><span class="sxs-lookup"><span data-stu-id="3c70d-203">a.</span></span> <span data-ttu-id="3c70d-204">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3c70d-205">b.</span><span class="sxs-lookup"><span data-stu-id="3c70d-205">b.</span></span> <span data-ttu-id="3c70d-206">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3c70d-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3c70d-207">c.</span><span class="sxs-lookup"><span data-stu-id="3c70d-207">c.</span></span> <span data-ttu-id="3c70d-208">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3c70d-209">d.</span><span class="sxs-lookup"><span data-stu-id="3c70d-209">d.</span></span> <span data-ttu-id="3c70d-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="3c70d-211">Criar um usuário de teste para Small Improvements</span><span class="sxs-lookup"><span data-stu-id="3c70d-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="3c70d-212">tooenable AD do Azure usuários toolog em tooSmall melhorias, eles devem ser provisionados no pequenas melhorias.</span><span class="sxs-lookup"><span data-stu-id="3c70d-212">tooenable Azure AD users toolog in tooSmall Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="3c70d-213">No caso de saudação de pequenas melhorias, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="3c70d-213">In hello case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="3c70d-214">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3c70d-214">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c70d-215">Site de empresa de pequenas melhorias tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="3c70d-215">Sign-on tooyour Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="3c70d-216">Na página de início hello, vá toohello menu saudação à esquerda, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-216">From hello Home page, go toohello menu on hello left, click **Administration**.</span></span>

3. <span data-ttu-id="3c70d-217">Clique em Olá **diretório de usuário** botão da seção de gerenciamento de usuário.</span><span class="sxs-lookup"><span data-stu-id="3c70d-217">Click hello **User Directory** button from User Management section.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="3c70d-219">Clique em **Adicionar usuários**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-219">Click **Add users**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="3c70d-221">Em Olá **adicionar usuários** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c70d-221">On hello **Add Users** dialog, perform hello following steps:</span></span> 

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="3c70d-223">a.</span><span class="sxs-lookup"><span data-stu-id="3c70d-223">a.</span></span> <span data-ttu-id="3c70d-224">Digite hello **nome** do usuário como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-224">Enter hello **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="3c70d-225">b.</span><span class="sxs-lookup"><span data-stu-id="3c70d-225">b.</span></span> <span data-ttu-id="3c70d-226">Digite hello **Sobrenome** do usuário como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-226">Enter hello **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="3c70d-227">c.</span><span class="sxs-lookup"><span data-stu-id="3c70d-227">c.</span></span> <span data-ttu-id="3c70d-228">Digite hello **Email** do usuário como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="3c70d-228">Enter hello **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="3c70d-229">d.</span><span class="sxs-lookup"><span data-stu-id="3c70d-229">d.</span></span> <span data-ttu-id="3c70d-230">Você pode escolher também mensagem pessoal do tooenter Olá Olá **enviar email de notificação** caixa.</span><span class="sxs-lookup"><span data-stu-id="3c70d-230">You can also choose tooenter hello personal message in hello **Send notification email** box.</span></span> <span data-ttu-id="3c70d-231">Se não desejar notificação de saudação toosend, em seguida, desmarque essa caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="3c70d-231">If you do not wish toosend hello notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="3c70d-232">e.</span><span class="sxs-lookup"><span data-stu-id="3c70d-232">e.</span></span> <span data-ttu-id="3c70d-233">Clique em **Criar Usuários**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-233">Click **Create Users**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3c70d-234">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c70d-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3c70d-235">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSmall melhorias.</span><span class="sxs-lookup"><span data-stu-id="3c70d-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmall Improvements.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3c70d-237">**tooassign Britta Simon tooSmall melhorias, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3c70d-237">**tooassign Britta Simon tooSmall Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c70d-238">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3c70d-240">Na lista de aplicativos hello, selecione **pequenas melhorias**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-240">In hello applications list, select **Small Improvements**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="3c70d-242">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3c70d-244">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3c70d-244">Click **Add** button.</span></span> <span data-ttu-id="3c70d-245">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c70d-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3c70d-247">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c70d-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3c70d-248">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c70d-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3c70d-249">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c70d-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3c70d-250">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3c70d-250">Testing single sign-on</span></span>

<span data-ttu-id="3c70d-251">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="3c70d-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="3c70d-252">Quando você clica em Olá pequenas melhorias bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado em aplicativos pequenos aperfeiçoamentos.</span><span class="sxs-lookup"><span data-stu-id="3c70d-252">When you click hello Small Improvements tile in hello Access Panel, you should get automatically signed-on tooyour Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3c70d-253">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3c70d-253">Additional resources</span></span>

* [<span data-ttu-id="3c70d-254">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3c70d-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3c70d-255">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3c70d-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

