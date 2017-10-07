---
title: "Tutorial: Integração do Azure Active Directory com o Jitbit Helpdesk | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Jitbit Helpdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="cfbdd-103">Tutorial: Integração do Active Directory do Azure com o Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="cfbdd-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="cfbdd-104">Neste tutorial, você aprenderá como toointegrate Jitbit Helpdesk com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="cfbdd-104">In this tutorial, you learn how toointegrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cfbdd-105">Integrando Jitbit Helpdesk com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="cfbdd-105">Integrating Jitbit Helpdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cfbdd-106">Você pode controlar no AD do Azure que tenha acesso tooJitbit suporte técnico</span><span class="sxs-lookup"><span data-stu-id="cfbdd-106">You can control in Azure AD who has access tooJitbit Helpdesk</span></span>
- <span data-ttu-id="cfbdd-107">Você pode habilitar seu usuários tooautomatically get conectado tooJitbit suporte técnico (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cfbdd-107">You can enable your users tooautomatically get signed-on tooJitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cfbdd-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cfbdd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cfbdd-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cfbdd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfbdd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cfbdd-110">Prerequisites</span></span>

<span data-ttu-id="cfbdd-111">tooconfigure integração do AD do Azure com o Jitbit Helpdesk, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="cfbdd-111">tooconfigure Azure AD integration with Jitbit Helpdesk, you need hello following items:</span></span>

- <span data-ttu-id="cfbdd-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cfbdd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cfbdd-113">Uma assinatura habilitada para logon único do Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="cfbdd-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cfbdd-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cfbdd-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cfbdd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cfbdd-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cfbdd-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cfbdd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cfbdd-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cfbdd-118">Scenario description</span></span>
<span data-ttu-id="cfbdd-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cfbdd-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="cfbdd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cfbdd-121">Adicionando Jitbit Helpdesk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cfbdd-121">Adding Jitbit Helpdesk from hello gallery</span></span>
2. <span data-ttu-id="cfbdd-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cfbdd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a><span data-ttu-id="cfbdd-123">Adicionando Jitbit Helpdesk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cfbdd-123">Adding Jitbit Helpdesk from hello gallery</span></span>
<span data-ttu-id="cfbdd-124">integração de saudação tooconfigure do Jitbit Helpdesk no AD do Azure, você precisa tooadd Jitbit Helpdesk da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-124">tooconfigure hello integration of Jitbit Helpdesk into Azure AD, you need tooadd Jitbit Helpdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cfbdd-125">**tooadd Jitbit Helpdesk da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cfbdd-125">**tooadd Jitbit Helpdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfbdd-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cfbdd-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cfbdd-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cfbdd-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cfbdd-133">Na caixa de pesquisa hello, digite **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-133">In hello search box, type **Jitbit Helpdesk**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="cfbdd-135">No painel de resultados de saudação, selecione **Jitbit Helpdesk**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-135">In hello results panel, select **Jitbit Helpdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cfbdd-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cfbdd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cfbdd-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o Jitbit Helpdesk, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="cfbdd-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cfbdd-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Jitbit Helpdesk é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jitbit Helpdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="cfbdd-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Jitbit Helpdesk precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-140">In other words, a link relationship between an Azure AD user and hello related user in Jitbit Helpdesk needs toobe established.</span></span>

<span data-ttu-id="cfbdd-141">No Jitbit Helpdesk, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-141">In Jitbit Helpdesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cfbdd-142">tooconfigure e teste de logon único do AD do Azure com o Jitbit Helpdesk, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="cfbdd-142">tooconfigure and test Azure AD single sign-on with Jitbit Helpdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cfbdd-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cfbdd-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cfbdd-145">**[Criar um usuário de teste do Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**  -toohave um equivalente do Britta Simon no Jitbit Helpdesk é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - toohave a counterpart of Britta Simon in Jitbit Helpdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cfbdd-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cfbdd-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cfbdd-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfbdd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cfbdd-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="cfbdd-150">**tooconfigure AD do Azure-logon único com o Jitbit Helpdesk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cfbdd-150">**tooconfigure Azure AD single sign-on with Jitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfbdd-151">Em Olá portal do Azure, Olá **Jitbit Helpdesk** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-151">In hello Azure portal, on hello **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cfbdd-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="cfbdd-155">Em Olá **Jitbit Helpdesk domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cfbdd-155">On hello **Jitbit Helpdesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="cfbdd-157">a.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-157">a.</span></span> <span data-ttu-id="cfbdd-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="cfbdd-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="cfbdd-159">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-159">This value is not real.</span></span> <span data-ttu-id="cfbdd-160">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="cfbdd-161">Entre em contato com [equipe de suporte do Jitbit Helpdesk cliente](https://www.jitbit.com/support/) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) tooget this value.</span></span> 
    
    <span data-ttu-id="cfbdd-162">b.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-162">b.</span></span>  <span data-ttu-id="cfbdd-163">Em Olá **identificador** caixa de texto, digite um URL como a seguir:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="cfbdd-163">In hello **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="cfbdd-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="cfbdd-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="cfbdd-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cfbdd-168">Em Olá **Jitbit Helpdesk configuração** seção, clique em **configurar Jitbit Helpdesk** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-168">On hello **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cfbdd-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="cfbdd-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="cfbdd-171">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Jitbit Helpdesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="cfbdd-172">Na barra de ferramentas de saudação na parte superior do hello, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-172">In hello toolbar on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="cfbdd-173">![Administração](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="cfbdd-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="cfbdd-174">Clique em **Configurações gerais**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="cfbdd-175">![Usuários, empresas e permissões](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Usuários, empresas e permissões")</span><span class="sxs-lookup"><span data-stu-id="cfbdd-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="cfbdd-176">Em Olá **configurações de autenticação** configuração, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cfbdd-176">In hello **Authentication settings** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cfbdd-177">![Configurações de autenticação](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Configurações de autenticação")</span><span class="sxs-lookup"><span data-stu-id="cfbdd-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="cfbdd-178">a.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-178">a.</span></span> <span data-ttu-id="cfbdd-179">Selecione **habilitar SAML 2.0 único logon**, toosign usando Single Sign-On (SSO), com **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-179">Select **Enable SAML 2.0 single sign on**, toosign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="cfbdd-180">b.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-180">b.</span></span> <span data-ttu-id="cfbdd-181">Em Olá **URL de ponto de extremidade** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-181">In hello **EndPoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cfbdd-182">c.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-182">c.</span></span> <span data-ttu-id="cfbdd-183">Abra seu **base 64** codificado certificado no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto</span><span class="sxs-lookup"><span data-stu-id="cfbdd-183">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="cfbdd-184">d.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-184">d.</span></span> <span data-ttu-id="cfbdd-185">Clique em **Salvar alterações**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="cfbdd-186">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="cfbdd-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cfbdd-187">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cfbdd-188">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cfbdd-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cfbdd-189">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cfbdd-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="cfbdd-190">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cfbdd-192">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cfbdd-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfbdd-193">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cfbdd-195">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cfbdd-197">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cfbdd-199">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cfbdd-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cfbdd-201">a.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-201">a.</span></span> <span data-ttu-id="cfbdd-202">Em Olá **nome** caixa de texto Nome do tipo como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-202">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="cfbdd-203">b.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-203">b.</span></span> <span data-ttu-id="cfbdd-204">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cfbdd-205">c.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-205">c.</span></span> <span data-ttu-id="cfbdd-206">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cfbdd-207">d.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-207">d.</span></span> <span data-ttu-id="cfbdd-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="cfbdd-209">Criação de um usuário de teste do Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="cfbdd-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="cfbdd-210">Em ordem tooenable AD do Azure usuários toolog no Jitbit Helpdesk, eles devem ser provisionados no Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-210">In order tooenable Azure AD users toolog into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="cfbdd-211">No caso de saudação do Jitbit Helpdesk, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-211">In hello case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="cfbdd-212">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cfbdd-212">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfbdd-213">Faça logon no tooyour **Jitbit Helpdesk** locatário.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-213">Log in tooyour **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="cfbdd-214">No menu de saudação na parte superior de saudação, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-214">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="cfbdd-215">![Administração](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="cfbdd-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="cfbdd-216">Clique em **Usuários, empresas e permissões**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="cfbdd-217">![Usuários, empresas e permissões](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Usuários, empresas e permissões")</span><span class="sxs-lookup"><span data-stu-id="cfbdd-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="cfbdd-218">Clique em **Adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="cfbdd-219">![Adicionar Usuário](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="cfbdd-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="cfbdd-220">Na Olá seção "criar", digite dados saudação da conta do AD do Azure Olá que tooprovision desejado da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cfbdd-220">In hello Create section, type hello data of hello Azure AD account you want tooprovision as follows:</span></span>

    <span data-ttu-id="cfbdd-221">![Criar](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Criar")</span><span class="sxs-lookup"><span data-stu-id="cfbdd-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="cfbdd-222">a.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-222">a.</span></span> <span data-ttu-id="cfbdd-223">Em Olá **Username** caixa de texto, tipo **BrittaSimon**, nome de usuário hello como Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-223">In hello **Username** textbox, type **BrittaSimon**, hello user name as in hello Azure portal.</span></span>

   <span data-ttu-id="cfbdd-224">b.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-224">b.</span></span> <span data-ttu-id="cfbdd-225">Em Olá **Email** caixa de texto, como o tipo de email do usuário Olá  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="cfbdd-225">In hello **Email** textbox, type email of hello user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="cfbdd-226">c.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-226">c.</span></span> <span data-ttu-id="cfbdd-227">Em Olá **nome** caixa de texto, nome do primeiro tipo de usuário hello como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-227">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>

   <span data-ttu-id="cfbdd-228">d.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-228">d.</span></span> <span data-ttu-id="cfbdd-229">Em Olá **Sobrenome** caixa de texto, digite sobrenome do usuário hello como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-229">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span>
   
   <span data-ttu-id="cfbdd-230">e.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-230">e.</span></span> <span data-ttu-id="cfbdd-231">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="cfbdd-232">Você pode usar qualquer ferramenta de criação outros Jitbit Helpdesk usuário conta ou APIs fornecidas pelo Jitbit Helpdesk tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk tooprovision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cfbdd-233">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cfbdd-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cfbdd-234">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooJitbit suporte técnico.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJitbit Helpdesk.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cfbdd-236">**tooassign Britta Simon tooJitbit Helpdesk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cfbdd-236">**tooassign Britta Simon tooJitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfbdd-237">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cfbdd-239">Na lista de aplicativos hello, selecione **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-239">In hello applications list, select **Jitbit Helpdesk**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="cfbdd-241">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cfbdd-243">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-243">Click **Add** button.</span></span> <span data-ttu-id="cfbdd-244">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cfbdd-246">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cfbdd-247">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cfbdd-248">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cfbdd-249">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cfbdd-249">Testing single sign-on</span></span>

<span data-ttu-id="cfbdd-250">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cfbdd-251">Quando você clica em Olá Jitbit Helpdesk bloco no painel de acesso de saudação, você deve obter a página de logon do aplicativo do Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="cfbdd-251">When you click hello Jitbit Helpdesk tile in hello Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="cfbdd-252">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cfbdd-252">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cfbdd-253">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cfbdd-253">Additional resources</span></span>

* [<span data-ttu-id="cfbdd-254">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cfbdd-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cfbdd-255">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cfbdd-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

