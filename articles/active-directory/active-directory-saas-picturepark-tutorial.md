---
title: "Tutorial: Integração do Azure Active Directory ao Picturepark | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="eeee8-103">Tutorial: Integração do Azure Active Directory ao Picturepark</span><span class="sxs-lookup"><span data-stu-id="eeee8-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="eeee8-104">Neste tutorial, você aprenderá como toointegrate Picturepark com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="eeee8-104">In this tutorial, you learn how toointegrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eeee8-105">Integrando o Picturepark com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeee8-105">Integrating Picturepark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eeee8-106">Você pode controlar no AD do Azure que tenha acesso tooPicturepark</span><span class="sxs-lookup"><span data-stu-id="eeee8-106">You can control in Azure AD who has access tooPicturepark</span></span>
- <span data-ttu-id="eeee8-107">Você pode habilitar seu usuários tooautomatically get conectado tooPicturepark (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eeee8-107">You can enable your users tooautomatically get signed-on tooPicturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eeee8-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="eeee8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eeee8-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eeee8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eeee8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eeee8-110">Prerequisites</span></span>

<span data-ttu-id="eeee8-111">tooconfigure integração do AD do Azure com o Picturepark, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeee8-111">tooconfigure Azure AD integration with Picturepark, you need hello following items:</span></span>

- <span data-ttu-id="eeee8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eeee8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eeee8-113">Uma assinatura habilitada para logon único do Picturepark</span><span class="sxs-lookup"><span data-stu-id="eeee8-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eeee8-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="eeee8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eeee8-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="eeee8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eeee8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="eeee8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eeee8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eeee8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eeee8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="eeee8-118">Scenario description</span></span>
<span data-ttu-id="eeee8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="eeee8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eeee8-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="eeee8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eeee8-121">Adicionando Picturepark da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="eeee8-121">Adding Picturepark from hello gallery</span></span>
2. <span data-ttu-id="eeee8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eeee8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-hello-gallery"></a><span data-ttu-id="eeee8-123">Adicionando Picturepark da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="eeee8-123">Adding Picturepark from hello gallery</span></span>
<span data-ttu-id="eeee8-124">integração de saudação tooconfigure do Picturepark no AD do Azure, você precisa tooadd Picturepark da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="eeee8-124">tooconfigure hello integration of Picturepark into Azure AD, you need tooadd Picturepark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eeee8-125">**tooadd Picturepark da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eeee8-125">**tooadd Picturepark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eeee8-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="eeee8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eeee8-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eeee8-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="eeee8-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eeee8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="eeee8-133">Na caixa de pesquisa hello, digite **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-133">In hello search box, type **Picturepark**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="eeee8-135">No painel de resultados de saudação, selecione **Picturepark**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="eeee8-135">In hello results panel, select **Picturepark**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eeee8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eeee8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eeee8-138">Nesta seção, você configura e testa o logon único do Azure AD com o Picturepark, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="eeee8-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eeee8-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Picturepark é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="eeee8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Picturepark is tooa user in Azure AD.</span></span> <span data-ttu-id="eeee8-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Picturepark precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="eeee8-140">In other words, a link relationship between an Azure AD user and hello related user in Picturepark needs toobe established.</span></span>

<span data-ttu-id="eeee8-141">No Picturepark, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="eeee8-141">In Picturepark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eeee8-142">tooconfigure e teste de logon único do AD do Azure com o Picturepark, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeee8-142">tooconfigure and test Azure AD single sign-on with Picturepark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eeee8-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="eeee8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eeee8-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eeee8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eeee8-145">**[Criar um usuário de teste do Picturepark](#creating-a-picturepark-test-user)**  -toohave um equivalente do Britta Simon no Picturepark é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="eeee8-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - toohave a counterpart of Britta Simon in Picturepark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eeee8-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="eeee8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eeee8-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="eeee8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eeee8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeee8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eeee8-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Picturepark.</span><span class="sxs-lookup"><span data-stu-id="eeee8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="eeee8-150">**tooconfigure AD do Azure-logon único com o Picturepark, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eeee8-150">**tooconfigure Azure AD single sign-on with Picturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="eeee8-151">Em Olá portal do Azure, Olá **Picturepark** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-151">In hello Azure portal, on hello **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="eeee8-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="eeee8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="eeee8-155">Em Olá **Picturepark domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeee8-155">On hello **Picturepark Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="eeee8-157">a.</span><span class="sxs-lookup"><span data-stu-id="eeee8-157">a.</span></span> <span data-ttu-id="eeee8-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="eeee8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="eeee8-159">b.</span><span class="sxs-lookup"><span data-stu-id="eeee8-159">b.</span></span> <span data-ttu-id="eeee8-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeee8-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="eeee8-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="eeee8-161">These values are not real.</span></span> <span data-ttu-id="eeee8-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="eeee8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eeee8-163">Entre em contato com [equipe de suporte do cliente do Picturepark](https://picturepark.com/about/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="eeee8-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="eeee8-164">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="eeee8-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="eeee8-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="eeee8-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eeee8-168">Em Olá **Picturepark configuração** seção, clique em **configurar Picturepark** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="eeee8-168">On hello **Picturepark Configuration** section, click **Configure Picturepark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eeee8-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="eeee8-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="eeee8-171">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do Picturepark como administrador.</span><span class="sxs-lookup"><span data-stu-id="eeee8-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="eeee8-172">Na barra de ferramentas de saudação na parte superior do hello, clique em **ferramentas administrativas**e, em seguida, clique em **Console de gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-172">In hello toolbar on hello top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="eeee8-173">![Console de Gerenciamento](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Console de Gerenciamento")</span><span class="sxs-lookup"><span data-stu-id="eeee8-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="eeee8-174">Clique em **Autenticação** e em **Provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="eeee8-175">![Autenticação](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Autenticação")</span><span class="sxs-lookup"><span data-stu-id="eeee8-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="eeee8-176">Em Olá **configuração do provedor de identidade** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeee8-176">In hello **Identity provider configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="eeee8-177">![Configuração do Provedor de Identidade](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configuração do Provedor de Identidade")</span><span class="sxs-lookup"><span data-stu-id="eeee8-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="eeee8-178">a.</span><span class="sxs-lookup"><span data-stu-id="eeee8-178">a.</span></span> <span data-ttu-id="eeee8-179">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-179">Click **Add**.</span></span>
  
    <span data-ttu-id="eeee8-180">b.</span><span class="sxs-lookup"><span data-stu-id="eeee8-180">b.</span></span> <span data-ttu-id="eeee8-181">Digite um nome para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="eeee8-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="eeee8-182">c.</span><span class="sxs-lookup"><span data-stu-id="eeee8-182">c.</span></span> <span data-ttu-id="eeee8-183">Selecione **Definir como padrão**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="eeee8-184">d.</span><span class="sxs-lookup"><span data-stu-id="eeee8-184">d.</span></span> <span data-ttu-id="eeee8-185">Em **URI do emissor** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eeee8-185">In **Issuer URI** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="eeee8-186">e.</span><span class="sxs-lookup"><span data-stu-id="eeee8-186">e.</span></span> <span data-ttu-id="eeee8-187">Em **impressão digital do emissor confiável** caixa de texto valor Olá colar **impressão digital** que você copiou de **o certificado de autenticação SAML** seção.</span><span class="sxs-lookup"><span data-stu-id="eeee8-187">In **Trusted Issuer Thumb Print** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="eeee8-188">Clique em **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="eeee8-189">Olá tooset **Emailaddress** atributo Olá **declaração** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-189">tooset hello **Emailaddress** attribute in hello **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="eeee8-190">![Configuração](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="eeee8-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="eeee8-191">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="eeee8-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eeee8-192">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="eeee8-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eeee8-193">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eeee8-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eeee8-194">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eeee8-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="eeee8-195">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eeee8-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="eeee8-197">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eeee8-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eeee8-198">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="eeee8-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eeee8-200">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eeee8-202">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="eeee8-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eeee8-204">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeee8-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eeee8-206">a.</span><span class="sxs-lookup"><span data-stu-id="eeee8-206">a.</span></span> <span data-ttu-id="eeee8-207">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eeee8-208">b.</span><span class="sxs-lookup"><span data-stu-id="eeee8-208">b.</span></span> <span data-ttu-id="eeee8-209">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eeee8-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eeee8-210">c.</span><span class="sxs-lookup"><span data-stu-id="eeee8-210">c.</span></span> <span data-ttu-id="eeee8-211">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eeee8-212">d.</span><span class="sxs-lookup"><span data-stu-id="eeee8-212">d.</span></span> <span data-ttu-id="eeee8-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="eeee8-214">Criando um usuário de teste do Picturepark</span><span class="sxs-lookup"><span data-stu-id="eeee8-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="eeee8-215">Ordem tooenable AD do Azure usuários toolog no Picturepark, eles devem ser provisionados no Picturepark.</span><span class="sxs-lookup"><span data-stu-id="eeee8-215">In order tooenable Azure AD users toolog into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="eeee8-216">No caso de saudação do Picturepark, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="eeee8-216">In hello case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="eeee8-217">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eeee8-217">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="eeee8-218">Faça logon no tooyour **Picturepark** locatário.</span><span class="sxs-lookup"><span data-stu-id="eeee8-218">Log in tooyour **Picturepark** tenant.</span></span>

2. <span data-ttu-id="eeee8-219">Na barra de ferramentas de saudação na parte superior do hello, clique em **ferramentas administrativas**e, em seguida, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-219">In hello toolbar on hello top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="eeee8-220">![Usuários](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="eeee8-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="eeee8-221">Em Olá **visão geral sobre usuários** , clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-221">In hello **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="eeee8-222">![Gerenciamento de usuário](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Gerenciamento de usuário")</span><span class="sxs-lookup"><span data-stu-id="eeee8-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="eeee8-223">Em Olá **Create User** caixa de diálogo, executar Olá seguindo as etapas de um válida do Azure Active Directory usuário você deseja tooprovision:</span><span class="sxs-lookup"><span data-stu-id="eeee8-223">On hello **Create User** dialog, perform hello following steps of a valid Azure Active Directory User you want tooprovision:</span></span>
   
    <span data-ttu-id="eeee8-224">![Criar usuário](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="eeee8-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="eeee8-225">a.</span><span class="sxs-lookup"><span data-stu-id="eeee8-225">a.</span></span> <span data-ttu-id="eeee8-226">Em Olá **endereço de Email** caixa de texto, Olá tipo **endereço de email** do usuário Olá  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="eeee8-226">In hello **Email Address** textbox, type hello **email address** of hello user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="eeee8-227">b.</span><span class="sxs-lookup"><span data-stu-id="eeee8-227">b.</span></span> <span data-ttu-id="eeee8-228">Em Olá **senha** e **Confirmar senha** caixas de texto, Olá tipo **senha** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eeee8-228">In hello **Password** and **Confirm Password** textboxes, type hello **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="eeee8-229">c.</span><span class="sxs-lookup"><span data-stu-id="eeee8-229">c.</span></span> <span data-ttu-id="eeee8-230">Em Olá **nome** caixa de texto, Olá tipo **nome** do usuário Olá **Britta**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-230">In hello **First Name** textbox, type hello **First Name** of hello user **Britta**.</span></span> 
   
    <span data-ttu-id="eeee8-231">d.</span><span class="sxs-lookup"><span data-stu-id="eeee8-231">d.</span></span> <span data-ttu-id="eeee8-232">Em Olá **Sobrenome** caixa de texto, Olá tipo **Sobrenome** do usuário Olá **Simon**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-232">In hello **Last Name** textbox, type hello **Last Name** of hello user **Simon**.</span></span>
   
    <span data-ttu-id="eeee8-233">e.</span><span class="sxs-lookup"><span data-stu-id="eeee8-233">e.</span></span> <span data-ttu-id="eeee8-234">Em Olá **empresa** caixa de texto, Olá tipo **nome da empresa** do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="eeee8-234">In hello **Company** textbox, type hello **Company name** of hello user.</span></span> 
   
    <span data-ttu-id="eeee8-235">f.</span><span class="sxs-lookup"><span data-stu-id="eeee8-235">f.</span></span> <span data-ttu-id="eeee8-236">Em Olá **país** caixa de texto, selecione Olá **país** do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="eeee8-236">In hello **Country** textbox, select hello **Country** of hello user.</span></span>
  
    <span data-ttu-id="eeee8-237">g.</span><span class="sxs-lookup"><span data-stu-id="eeee8-237">g.</span></span> <span data-ttu-id="eeee8-238">Em Olá **ZIP** caixa de texto, Olá tipo **CEP** de cidade hello.</span><span class="sxs-lookup"><span data-stu-id="eeee8-238">In hello **ZIP** textbox, type hello **ZIP code** of hello city.</span></span>
   
    <span data-ttu-id="eeee8-239">h.</span><span class="sxs-lookup"><span data-stu-id="eeee8-239">h.</span></span> <span data-ttu-id="eeee8-240">Em Olá **Cidade** caixa de texto, Olá tipo **nome da cidade** do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="eeee8-240">In hello **City** textbox, type hello **City name** of hello user.</span></span>

    <span data-ttu-id="eeee8-241">i.</span><span class="sxs-lookup"><span data-stu-id="eeee8-241">i.</span></span> <span data-ttu-id="eeee8-242">Selecione um **Idioma**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="eeee8-243">j.</span><span class="sxs-lookup"><span data-stu-id="eeee8-243">j.</span></span> <span data-ttu-id="eeee8-244">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="eeee8-245">Você pode usar qualquer ferramenta de criação outros Picturepark usuário conta ou APIs fornecidas pelo Picturepark tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="eeee8-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eeee8-246">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eeee8-246">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eeee8-247">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPicturepark.</span><span class="sxs-lookup"><span data-stu-id="eeee8-247">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPicturepark.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="eeee8-249">**tooassign Britta Simon tooPicturepark, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eeee8-249">**tooassign Britta Simon tooPicturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="eeee8-250">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-250">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="eeee8-252">Na lista de aplicativos hello, selecione **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-252">In hello applications list, select **Picturepark**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="eeee8-254">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-254">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="eeee8-256">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="eeee8-256">Click **Add** button.</span></span> <span data-ttu-id="eeee8-257">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eeee8-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="eeee8-259">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="eeee8-259">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eeee8-260">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eeee8-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eeee8-261">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eeee8-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eeee8-262">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="eeee8-262">Testing single sign-on</span></span>

<span data-ttu-id="eeee8-263">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="eeee8-263">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eeee8-264">Quando você clica em bloco Picturepark Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Picturepark aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eeee8-264">When you click hello Picturepark tile in hello Access Panel, you should get automatically signed-on tooyour Picturepark application.</span></span> <span data-ttu-id="eeee8-265">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eeee8-265">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eeee8-266">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="eeee8-266">Additional resources</span></span>

* [<span data-ttu-id="eeee8-267">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="eeee8-267">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eeee8-268">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eeee8-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

