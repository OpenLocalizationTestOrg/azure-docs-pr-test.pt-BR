---
title: "Tutorial: Integração do Azure Active Directory com o Kudos | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Kudos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: c1b481463574461f9948db2b83843fefa5d74e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="78bb5-103">Tutorial: Integração do Active Directory do Azure com o Kudos</span><span class="sxs-lookup"><span data-stu-id="78bb5-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="78bb5-104">Neste tutorial, você aprenderá como toointegrate muito bem com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="78bb5-104">In this tutorial, you learn how toointegrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78bb5-105">Integrando o Kudos com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="78bb5-105">Integrating Kudos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="78bb5-106">Você pode controlar no AD do Azure que tenha acesso tooKudos</span><span class="sxs-lookup"><span data-stu-id="78bb5-106">You can control in Azure AD who has access tooKudos</span></span>
- <span data-ttu-id="78bb5-107">Você pode habilitar seus usuários tooautomatically get conectado tooKudos (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="78bb5-107">You can enable your users tooautomatically get signed-on tooKudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78bb5-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="78bb5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="78bb5-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="78bb5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78bb5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="78bb5-110">Prerequisites</span></span>

<span data-ttu-id="78bb5-111">tooconfigure integração do AD do Azure com o Kudos, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="78bb5-111">tooconfigure Azure AD integration with Kudos, you need hello following items:</span></span>

- <span data-ttu-id="78bb5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="78bb5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78bb5-113">Uma assinatura habilitada para logon único do Kudos</span><span class="sxs-lookup"><span data-stu-id="78bb5-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78bb5-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="78bb5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78bb5-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="78bb5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78bb5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="78bb5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78bb5-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78bb5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78bb5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="78bb5-118">Scenario description</span></span>
<span data-ttu-id="78bb5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="78bb5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78bb5-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="78bb5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78bb5-121">Adicionando Kudos da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="78bb5-121">Adding Kudos from hello gallery</span></span>
2. <span data-ttu-id="78bb5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="78bb5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-hello-gallery"></a><span data-ttu-id="78bb5-123">Adicionando Kudos da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="78bb5-123">Adding Kudos from hello gallery</span></span>
<span data-ttu-id="78bb5-124">integração de saudação tooconfigure do Kudos no AD do Azure, você precisa tooadd Kudos da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="78bb5-124">tooconfigure hello integration of Kudos into Azure AD, you need tooadd Kudos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="78bb5-125">**tooadd Kudos da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="78bb5-125">**tooadd Kudos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="78bb5-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="78bb5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="78bb5-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="78bb5-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="78bb5-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="78bb5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="78bb5-133">Na caixa de pesquisa hello, digite **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-133">In hello search box, type **Kudos**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="78bb5-135">No painel de resultados de saudação, selecione **Kudos**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="78bb5-135">In hello results panel, select **Kudos**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78bb5-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="78bb5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78bb5-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Kudos, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="78bb5-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="78bb5-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Kudos é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="78bb5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kudos is tooa user in Azure AD.</span></span> <span data-ttu-id="78bb5-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Kudos precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="78bb5-140">In other words, a link relationship between an Azure AD user and hello related user in Kudos needs toobe established.</span></span>

<span data-ttu-id="78bb5-141">No Kudos, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="78bb5-141">In Kudos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="78bb5-142">tooconfigure e teste de logon único do AD do Azure com o Kudos, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="78bb5-142">tooconfigure and test Azure AD single sign-on with Kudos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="78bb5-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="78bb5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="78bb5-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78bb5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78bb5-145">**[Criar um usuário de teste do Kudos](#creating-a-kudos-test-user)**  -toohave um equivalente do Britta Simon no Kudos é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="78bb5-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - toohave a counterpart of Britta Simon in Kudos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="78bb5-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="78bb5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78bb5-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="78bb5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78bb5-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="78bb5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78bb5-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Kudos.</span><span class="sxs-lookup"><span data-stu-id="78bb5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="78bb5-150">**tooconfigure AD do Azure-logon único com o Kudos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="78bb5-150">**tooconfigure Azure AD single sign-on with Kudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="78bb5-151">Em Olá portal do Azure, Olá **Kudos** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-151">In hello Azure portal, on hello **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="78bb5-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="78bb5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="78bb5-155">Em Olá **Kudos domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="78bb5-155">On hello **Kudos Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="78bb5-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="78bb5-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="78bb5-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="78bb5-158">This value is not real.</span></span> <span data-ttu-id="78bb5-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="78bb5-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="78bb5-160">Entre em contato com [equipe de suporte do cliente do Kudos](http://success.kudosnow.com/home) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="78bb5-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) tooget this value.</span></span> 
 
4. <span data-ttu-id="78bb5-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="78bb5-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="78bb5-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="78bb5-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78bb5-165">Em Olá **Kudos configuração** seção, clique em **configurar Kudos** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="78bb5-165">On hello **Kudos Configuration** section, click **Configure Kudos** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="78bb5-166">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="78bb5-166">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="78bb5-168">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Kudos como administrador.</span><span class="sxs-lookup"><span data-stu-id="78bb5-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="78bb5-169">No menu de saudação na parte superior de saudação, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-169">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="78bb5-170">![Configurações](./media/active-directory-saas-kudos-tutorial/ic787806.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="78bb5-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="78bb5-171">Clique em **Integrações \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="78bb5-172">Em Olá **SSO** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="78bb5-172">In hello **SSO** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="78bb5-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="78bb5-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="78bb5-174">a.</span><span class="sxs-lookup"><span data-stu-id="78bb5-174">a.</span></span> <span data-ttu-id="78bb5-175">Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="78bb5-175">In **Sign on URL** textbox, paste hello value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="78bb5-176">b.</span><span class="sxs-lookup"><span data-stu-id="78bb5-176">b.</span></span> <span data-ttu-id="78bb5-177">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto</span><span class="sxs-lookup"><span data-stu-id="78bb5-177">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="78bb5-178">c.</span><span class="sxs-lookup"><span data-stu-id="78bb5-178">c.</span></span> <span data-ttu-id="78bb5-179">Em **Logout tooURL**, cole o valor de saudação do **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="78bb5-179">In **Logout tooURL**, paste hello value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="78bb5-180">d.</span><span class="sxs-lookup"><span data-stu-id="78bb5-180">d.</span></span> <span data-ttu-id="78bb5-181">Em Olá **sua URL do Kudos** caixa de texto, digite o nome da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="78bb5-181">In hello **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="78bb5-182">e.</span><span class="sxs-lookup"><span data-stu-id="78bb5-182">e.</span></span> <span data-ttu-id="78bb5-183">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="78bb5-184">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="78bb5-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="78bb5-185">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="78bb5-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="78bb5-186">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78bb5-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78bb5-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="78bb5-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="78bb5-188">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="78bb5-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="78bb5-190">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="78bb5-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="78bb5-191">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="78bb5-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78bb5-193">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78bb5-195">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="78bb5-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78bb5-197">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="78bb5-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78bb5-199">a.</span><span class="sxs-lookup"><span data-stu-id="78bb5-199">a.</span></span> <span data-ttu-id="78bb5-200">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78bb5-201">b.</span><span class="sxs-lookup"><span data-stu-id="78bb5-201">b.</span></span> <span data-ttu-id="78bb5-202">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="78bb5-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78bb5-203">c.</span><span class="sxs-lookup"><span data-stu-id="78bb5-203">c.</span></span> <span data-ttu-id="78bb5-204">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="78bb5-205">d.</span><span class="sxs-lookup"><span data-stu-id="78bb5-205">d.</span></span> <span data-ttu-id="78bb5-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="78bb5-207">Criar um usuário de teste do Kudos</span><span class="sxs-lookup"><span data-stu-id="78bb5-207">Creating a Kudos test user</span></span>

<span data-ttu-id="78bb5-208">Em ordem tooenable AD do Azure usuários toolog no Kudos, eles devem ser provisionados no Kudos.</span><span class="sxs-lookup"><span data-stu-id="78bb5-208">In order tooenable Azure AD users toolog into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="78bb5-209">No caso de saudação do Kudos, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="78bb5-209">In hello case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="78bb5-210">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="78bb5-210">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="78bb5-211">Faça logon no tooyour **Kudos** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="78bb5-211">Log in tooyour **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="78bb5-212">No menu de saudação na parte superior de saudação, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-212">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="78bb5-213">![Configurações](./media/active-directory-saas-kudos-tutorial/ic787806.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="78bb5-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="78bb5-214">Clique em **Usuário Administrador**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="78bb5-215">Clique em Olá **usuários** guia e, em seguida, clique em **adicionar um usuário**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-215">Click hello **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="78bb5-216">![Usuário Administrador](./media/active-directory-saas-kudos-tutorial/ic787809.png "Usuário Administrador")</span><span class="sxs-lookup"><span data-stu-id="78bb5-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="78bb5-217">Em Olá **adicionar um usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="78bb5-217">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="78bb5-218">![Adicionar um Usuário](./media/active-directory-saas-kudos-tutorial/ic787810.png "Adicionar um Usuário")</span><span class="sxs-lookup"><span data-stu-id="78bb5-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="78bb5-219">a.</span><span class="sxs-lookup"><span data-stu-id="78bb5-219">a.</span></span> <span data-ttu-id="78bb5-220">Saudação de tipo **nome**, **Sobrenome**, **Email** e outros detalhes de uma conta válida do Active Directory do Azure você deseja tooprovision em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="78bb5-220">Type hello **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="78bb5-221">b.</span><span class="sxs-lookup"><span data-stu-id="78bb5-221">b.</span></span> <span data-ttu-id="78bb5-222">Clique em **Criar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="78bb5-223">Você pode usar qualquer ferramenta de criação outros Kudos usuário conta ou APIs fornecidas pelo Kudos tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="78bb5-223">You can use any other Kudos user account creation tools or APIs provided by Kudos tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="78bb5-224">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="78bb5-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="78bb5-225">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooKudos.</span><span class="sxs-lookup"><span data-stu-id="78bb5-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKudos.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="78bb5-227">**tooassign Britta Simon tooKudos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="78bb5-227">**tooassign Britta Simon tooKudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="78bb5-228">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="78bb5-230">Na lista de aplicativos hello, selecione **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-230">In hello applications list, select **Kudos**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="78bb5-232">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="78bb5-234">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="78bb5-234">Click **Add** button.</span></span> <span data-ttu-id="78bb5-235">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="78bb5-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="78bb5-237">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="78bb5-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="78bb5-238">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="78bb5-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78bb5-239">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="78bb5-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78bb5-240">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="78bb5-240">Testing single sign-on</span></span>

<span data-ttu-id="78bb5-241">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="78bb5-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="78bb5-242">Quando você clica em bloco Kudos Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Kudos.</span><span class="sxs-lookup"><span data-stu-id="78bb5-242">When you click hello Kudos tile in hello Access Panel, you should get automatically signed-on tooyour Kudos application.</span></span> <span data-ttu-id="78bb5-243">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="78bb5-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78bb5-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="78bb5-244">Additional resources</span></span>

* [<span data-ttu-id="78bb5-245">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="78bb5-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78bb5-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78bb5-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

