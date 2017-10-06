---
title: "Tutorial: Integração do Azure Active Directory ao AppDynamics | Microsoft Azure"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e AppDynamics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9b63afec73d7442e6ac1ce34b511beea6f43ffe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="95a88-103">Tutorial: Integração do Active Directory do Azure ao AppDynamics</span><span class="sxs-lookup"><span data-stu-id="95a88-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="95a88-104">Neste tutorial, você aprenderá como toointegrate AppDynamics com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="95a88-104">In this tutorial, you learn how toointegrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95a88-105">Integrando o AppDynamics com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a88-105">Integrating AppDynamics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="95a88-106">Você pode controlar no AD do Azure que tenha acesso tooAppDynamics</span><span class="sxs-lookup"><span data-stu-id="95a88-106">You can control in Azure AD who has access tooAppDynamics</span></span>
- <span data-ttu-id="95a88-107">Você pode habilitar seus usuários tooautomatically get conectado tooAppDynamics (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a88-107">You can enable your users tooautomatically get signed-on tooAppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="95a88-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="95a88-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="95a88-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="95a88-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95a88-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="95a88-110">Prerequisites</span></span>

<span data-ttu-id="95a88-111">tooconfigure integração do AD do Azure com AppDynamics, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a88-111">tooconfigure Azure AD integration with AppDynamics, you need hello following items:</span></span>

- <span data-ttu-id="95a88-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a88-112">An Azure AD subscription</span></span>
- <span data-ttu-id="95a88-113">Uma assinatura habilitada para logon único do AppDynamics</span><span class="sxs-lookup"><span data-stu-id="95a88-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="95a88-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="95a88-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="95a88-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="95a88-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="95a88-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="95a88-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="95a88-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95a88-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95a88-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="95a88-118">Scenario description</span></span>
<span data-ttu-id="95a88-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="95a88-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95a88-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="95a88-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95a88-121">Adicionando AppDynamics da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="95a88-121">Adding AppDynamics from hello gallery</span></span>
2. <span data-ttu-id="95a88-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a88-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-hello-gallery"></a><span data-ttu-id="95a88-123">Adicionando AppDynamics da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="95a88-123">Adding AppDynamics from hello gallery</span></span>
<span data-ttu-id="95a88-124">integração de saudação tooconfigure do AppDynamics no AD do Azure, você precisa tooadd AppDynamics da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="95a88-124">tooconfigure hello integration of AppDynamics into Azure AD, you need tooadd AppDynamics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="95a88-125">**tooadd AppDynamics da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95a88-125">**tooadd AppDynamics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a88-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="95a88-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="95a88-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="95a88-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="95a88-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="95a88-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="95a88-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95a88-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="95a88-133">Na caixa de pesquisa hello, digite **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="95a88-133">In hello search box, type **AppDynamics**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="95a88-135">No painel de resultados de saudação, selecione **AppDynamics**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="95a88-135">In hello results panel, select **AppDynamics**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="95a88-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a88-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="95a88-138">Nesta seção, você configura e testa o logon único do Azure AD com o AppDynamics, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="95a88-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="95a88-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no AppDynamics é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="95a88-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppDynamics is tooa user in Azure AD.</span></span> <span data-ttu-id="95a88-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no AppDynamics precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="95a88-140">In other words, a link relationship between an Azure AD user and hello related user in AppDynamics needs toobe established.</span></span>

<span data-ttu-id="95a88-141">No AppDynamics, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="95a88-141">In AppDynamics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="95a88-142">tooconfigure e teste de logon único do AD do Azure com AppDynamics, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a88-142">tooconfigure and test Azure AD single sign-on with AppDynamics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="95a88-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="95a88-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="95a88-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95a88-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="95a88-145">**[Criar um usuário de teste do AppDynamics](#creating-an-appdynamics-test-user)**  -toohave um equivalente do Britta Simon no AppDynamics é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="95a88-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - toohave a counterpart of Britta Simon in AppDynamics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="95a88-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="95a88-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="95a88-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="95a88-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="95a88-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="95a88-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="95a88-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="95a88-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="95a88-150">**tooconfigure AD do Azure-logon único com AppDynamics, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95a88-150">**tooconfigure Azure AD single sign-on with AppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a88-151">Em Olá portal do Azure, Olá **AppDynamics** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="95a88-151">In hello Azure portal, on hello **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="95a88-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="95a88-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="95a88-155">Em Olá **AppDynamics domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a88-155">On hello **AppDynamics Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="95a88-157">a.</span><span class="sxs-lookup"><span data-stu-id="95a88-157">a.</span></span> <span data-ttu-id="95a88-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="95a88-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="95a88-159">b.</span><span class="sxs-lookup"><span data-stu-id="95a88-159">b.</span></span> <span data-ttu-id="95a88-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="95a88-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="95a88-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="95a88-161">These values are not real.</span></span> <span data-ttu-id="95a88-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="95a88-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="95a88-163">Entre em contato com [equipe de suporte do cliente AppDynamics](https://www.appdynamics.com/support/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="95a88-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="95a88-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="95a88-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="95a88-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="95a88-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="95a88-168">Em Olá **AppDynamics configuração** seção, clique em **configurar AppDynamics** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="95a88-168">On hello **AppDynamics Configuration** section, click **Configure AppDynamics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="95a88-169">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="95a88-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="95a88-171">Em uma janela de navegador web diferente, faça logon no site da empresa AppDynamics tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="95a88-171">In a different web browser window, log in tooyour AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="95a88-172">Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações**e, em seguida, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="95a88-172">In hello toolbar on hello top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="95a88-173">![Administração](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="95a88-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="95a88-174">Clique em Olá **provedor de autenticação** guia.</span><span class="sxs-lookup"><span data-stu-id="95a88-174">Click hello **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="95a88-175">![Provedor de Autenticação](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Provedor de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="95a88-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="95a88-176">Em Olá **provedor de autenticação** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a88-176">In hello **Authentication Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="95a88-177">![Configuração SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="95a88-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="95a88-178">a.</span><span class="sxs-lookup"><span data-stu-id="95a88-178">a.</span></span> <span data-ttu-id="95a88-179">Como **Provedor de Autenticação**, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="95a88-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="95a88-180">b.</span><span class="sxs-lookup"><span data-stu-id="95a88-180">b.</span></span> <span data-ttu-id="95a88-181">Em Olá **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="95a88-181">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="95a88-182">c.</span><span class="sxs-lookup"><span data-stu-id="95a88-182">c.</span></span> <span data-ttu-id="95a88-183">Em Olá **URL de Logout** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="95a88-183">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="95a88-184">d.</span><span class="sxs-lookup"><span data-stu-id="95a88-184">d.</span></span> <span data-ttu-id="95a88-185">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado** caixa de texto</span><span class="sxs-lookup"><span data-stu-id="95a88-185">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox</span></span>

    <span data-ttu-id="95a88-186">e.</span><span class="sxs-lookup"><span data-stu-id="95a88-186">e.</span></span> <span data-ttu-id="95a88-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="95a88-187">Click **Save**.</span></span>

     <span data-ttu-id="95a88-188">![Salvar](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Salvar")</span><span class="sxs-lookup"><span data-stu-id="95a88-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="95a88-189">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="95a88-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="95a88-190">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="95a88-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="95a88-191">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="95a88-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="95a88-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a88-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="95a88-193">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="95a88-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="95a88-195">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95a88-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a88-196">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="95a88-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="95a88-198">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="95a88-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="95a88-200">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="95a88-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="95a88-202">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a88-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="95a88-204">a.</span><span class="sxs-lookup"><span data-stu-id="95a88-204">a.</span></span> <span data-ttu-id="95a88-205">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="95a88-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="95a88-206">b.</span><span class="sxs-lookup"><span data-stu-id="95a88-206">b.</span></span> <span data-ttu-id="95a88-207">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="95a88-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="95a88-208">c.</span><span class="sxs-lookup"><span data-stu-id="95a88-208">c.</span></span> <span data-ttu-id="95a88-209">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="95a88-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="95a88-210">d.</span><span class="sxs-lookup"><span data-stu-id="95a88-210">d.</span></span> <span data-ttu-id="95a88-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="95a88-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="95a88-212">Criando um usuário de teste do AppDynamics</span><span class="sxs-lookup"><span data-stu-id="95a88-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="95a88-213">tooenable AD do Azure usuários toolog em tooAppDynamics, eles devem ser provisionados no AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="95a88-213">tooenable Azure AD users toolog in tooAppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="95a88-214">No caso de saudação do AppDynamics, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="95a88-214">In hello case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="95a88-215">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95a88-215">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a88-216">Faça logon no tooyour site da empresa AppDynamics como um administrador.</span><span class="sxs-lookup"><span data-stu-id="95a88-216">Log in tooyour AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="95a88-217">Vá muito**usuários**e, em seguida, clique em  **+**  tooopen Olá **Create User** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95a88-217">Go too**Users**, and then click **+** tooopen hello **Create User** dialog.</span></span>
   
    <span data-ttu-id="95a88-218">![Usuários](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="95a88-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="95a88-219">Em Olá **Create User** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a88-219">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="95a88-220">![Criar usuário](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="95a88-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="95a88-221">a.</span><span class="sxs-lookup"><span data-stu-id="95a88-221">a.</span></span> <span data-ttu-id="95a88-222">Saudação de tipo **Username**, **nome**, **Email**, **nova senha**, **repetir nova senha** de um AAD válido conta você deseja tooprovision em Olá relacionadas a caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="95a88-222">Type hello **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="95a88-223">b.</span><span class="sxs-lookup"><span data-stu-id="95a88-223">b.</span></span> <span data-ttu-id="95a88-224">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="95a88-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="95a88-225">Você pode usar qualquer ferramenta de criação outros AppDynamics usuário conta ou APIs fornecidas pelo AppDynamics tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="95a88-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="95a88-226">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a88-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="95a88-227">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAppDynamics.</span><span class="sxs-lookup"><span data-stu-id="95a88-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppDynamics.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="95a88-229">**tooassign Britta Simon tooAppDynamics, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95a88-229">**tooassign Britta Simon tooAppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a88-230">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="95a88-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="95a88-232">Na lista de aplicativos hello, selecione **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="95a88-232">In hello applications list, select **AppDynamics**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="95a88-234">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="95a88-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="95a88-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="95a88-236">Click **Add** button.</span></span> <span data-ttu-id="95a88-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95a88-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="95a88-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="95a88-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="95a88-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95a88-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="95a88-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95a88-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="95a88-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="95a88-242">Testing single sign-on</span></span>

<span data-ttu-id="95a88-243">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="95a88-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="95a88-244">Quando você clica em Olá AppDynamics bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="95a88-244">When you click hello AppDynamics tile in hello Access Panel, you should get automatically signed-on tooyour AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="95a88-245">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="95a88-245">Additional resources</span></span>

* [<span data-ttu-id="95a88-246">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="95a88-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95a88-247">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="95a88-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

