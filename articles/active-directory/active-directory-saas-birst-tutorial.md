---
title: "Tutorial: Integração do Azure Active Directory ao Birst Agile Business Analytics | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e análise de negócios Birst Agile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: f007edcec0fb8ece215ab69f7ec7ca59ca34bddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="568d4-103">Tutorial: Integração do Active Directory do Azure ao Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="568d4-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="568d4-104">Neste tutorial, você aprenderá como toointegrate Birst Agile análise de negócios com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="568d4-104">In this tutorial, you learn how toointegrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="568d4-105">Análise de negócios Agile Birst integrando o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="568d4-105">Integrating Birst Agile Business Analytics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="568d4-106">Você pode controlar no AD do Azure que tenha acesso tooBirst Agile análise de negócios</span><span class="sxs-lookup"><span data-stu-id="568d4-106">You can control in Azure AD who has access tooBirst Agile Business Analytics</span></span>
- <span data-ttu-id="568d4-107">Você pode habilitar seu usuários tooautomatically get conectado tooBirst Agile análise de negócios (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="568d4-107">You can enable your users tooautomatically get signed-on tooBirst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="568d4-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="568d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="568d4-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="568d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="568d4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="568d4-110">Prerequisites</span></span>

<span data-ttu-id="568d4-111">tooconfigure integração do AD do Azure com Birst Agile análise de negócios, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="568d4-111">tooconfigure Azure AD integration with Birst Agile Business Analytics, you need hello following items:</span></span>

- <span data-ttu-id="568d4-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="568d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="568d4-113">Uma assinatura do Birst Agile Business Analytics com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="568d4-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="568d4-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="568d4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="568d4-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="568d4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="568d4-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="568d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="568d4-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="568d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="568d4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="568d4-118">Scenario description</span></span>
<span data-ttu-id="568d4-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="568d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="568d4-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="568d4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="568d4-121">Adição de análise de negócios Agile Birst da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="568d4-121">Adding Birst Agile Business Analytics from hello gallery</span></span>
2. <span data-ttu-id="568d4-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="568d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-hello-gallery"></a><span data-ttu-id="568d4-123">Adição de análise de negócios Agile Birst da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="568d4-123">Adding Birst Agile Business Analytics from hello gallery</span></span>
<span data-ttu-id="568d4-124">integração de saudação tooconfigure de análise de negócios Agile Birst no AD do Azure, você precisa tooadd Birst Agile análise de negócios da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="568d4-124">tooconfigure hello integration of Birst Agile Business Analytics into Azure AD, you need tooadd Birst Agile Business Analytics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="568d4-125">**tooadd Birst Agile análise de negócios da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="568d4-125">**tooadd Birst Agile Business Analytics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="568d4-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="568d4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="568d4-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="568d4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="568d4-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="568d4-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="568d4-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="568d4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="568d4-133">Na caixa de pesquisa hello, digite **Birst Agile análise de negócios**.</span><span class="sxs-lookup"><span data-stu-id="568d4-133">In hello search box, type **Birst Agile Business Analytics**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="568d4-135">No painel de resultados de saudação, selecione **Birst Agile análise de negócios**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="568d4-135">In hello results panel, select **Birst Agile Business Analytics**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="568d4-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="568d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="568d4-138">Nesta seção, você configura e testa o logon único do Azure AD com o Birst Agile Business Analytics, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="568d4-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="568d4-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na análise de negócios Agile Birst é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="568d4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Birst Agile Business Analytics is tooa user in Azure AD.</span></span> <span data-ttu-id="568d4-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na análise de negócios Agile Birst precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="568d4-140">In other words, a link relationship between an Azure AD user and hello related user in Birst Agile Business Analytics needs toobe established.</span></span>

<span data-ttu-id="568d4-141">Birst Agile análise de negócios, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="568d4-141">In Birst Agile Business Analytics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="568d4-142">tooconfigure e teste de logon único do AD do Azure com Birst Agile análise de negócios, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="568d4-142">tooconfigure and test Azure AD single sign-on with Birst Agile Business Analytics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="568d4-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="568d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="568d4-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="568d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="568d4-145">**[Criar um usuário de teste de análise de negócios Agile Birst](#creating-a-birst-agile-business-analytics-test-user)**  -toohave um equivalente do Britta Simon em Birst Agile análise de negócios que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="568d4-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - toohave a counterpart of Britta Simon in Birst Agile Business Analytics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="568d4-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="568d4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="568d4-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="568d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="568d4-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="568d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="568d4-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de análise de negócios Birst Agile.</span><span class="sxs-lookup"><span data-stu-id="568d4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="568d4-150">**tooconfigure logon único do AD do Azure com análise de negócios Agile Birst, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="568d4-150">**tooconfigure Azure AD single sign-on with Birst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="568d4-151">Em Olá portal do Azure, Olá **Birst Agile análise de negócios** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="568d4-151">In hello Azure portal, on hello **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="568d4-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="568d4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="568d4-155">Em Olá **Birst Agile domínio de análise de negócios e as URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="568d4-155">On hello **Birst Agile Business Analytics Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="568d4-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="568d4-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="568d4-158">URL de saudação depende Olá datacenter que sua conta Birst está localizada:</span><span class="sxs-lookup"><span data-stu-id="568d4-158">hello URL depends on hello datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="568d4-159">Para o uso de datacenter US padrão Olá a seguir:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="568d4-159">For US datacenter use following hello pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="568d4-160">Para a Europa datacenter usar saudação padrão a seguir:`https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="568d4-160">For Europe datacenter use hello following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="568d4-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="568d4-161">This value is not real.</span></span> <span data-ttu-id="568d4-162">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="568d4-162">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="568d4-163">Entre em contato com [equipe de suporte do cliente de análise de negócios Agile Birst](mailto:info@birst.com) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="568d4-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="568d4-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="568d4-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="568d4-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="568d4-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="568d4-168">Em Olá **configuração da análise de negócios Agile Birst** seção, clique em **configurar Birst Agile análise de negócios** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="568d4-168">On hello **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="568d4-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="568d4-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="568d4-171">tooconfigure logon único no **Birst Agile análise de negócios** lado, você precisa toosend Olá baixado **certificado (Base64)**, **URL de logout, ID de entidade de SAML e logon único SAML URL do serviço** muito[equipe de suporte de análise de negócios Agile Birst](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="568d4-171">tooconfigure single sign-on on **Birst Agile Business Analytics** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="568d4-172">Mencione team tooBirst essa integração precisa algoritmo SHA256 (SHA1 não terão suporte) para que eles podem definir Olá SSO no servidor apropriado hello como **app2101** etc.</span><span class="sxs-lookup"><span data-stu-id="568d4-172">Mention tooBirst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set hello SSO on hello appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="568d4-173">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="568d4-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="568d4-174">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="568d4-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="568d4-175">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="568d4-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="568d4-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="568d4-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="568d4-177">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="568d4-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="568d4-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="568d4-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="568d4-180">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="568d4-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="568d4-182">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="568d4-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="568d4-184">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="568d4-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="568d4-186">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="568d4-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="568d4-188">a.</span><span class="sxs-lookup"><span data-stu-id="568d4-188">a.</span></span> <span data-ttu-id="568d4-189">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="568d4-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="568d4-190">b.</span><span class="sxs-lookup"><span data-stu-id="568d4-190">b.</span></span> <span data-ttu-id="568d4-191">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="568d4-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="568d4-192">c.</span><span class="sxs-lookup"><span data-stu-id="568d4-192">c.</span></span> <span data-ttu-id="568d4-193">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="568d4-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="568d4-194">d.</span><span class="sxs-lookup"><span data-stu-id="568d4-194">d.</span></span> <span data-ttu-id="568d4-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="568d4-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="568d4-196">Criando um usuário de teste do Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="568d4-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="568d4-197">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon na análise de negócios Birst Agile.</span><span class="sxs-lookup"><span data-stu-id="568d4-197">hello objective of this section is toocreate a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="568d4-198">Trabalhar com [equipe de suporte de análise de negócios Agile Birst](mailto:info@birst.com) tooadd usuários Olá Olá Birst conta.</span><span class="sxs-lookup"><span data-stu-id="568d4-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) tooadd hello users in hello Birst account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="568d4-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="568d4-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="568d4-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBirst Agile análise de negócios.</span><span class="sxs-lookup"><span data-stu-id="568d4-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBirst Agile Business Analytics.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="568d4-202">**tooassign Britta Simon tooBirst Agile análise de negócios, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="568d4-202">**tooassign Britta Simon tooBirst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="568d4-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="568d4-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="568d4-205">Na lista de aplicativos hello, selecione **Birst Agile análise de negócios**.</span><span class="sxs-lookup"><span data-stu-id="568d4-205">In hello applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="568d4-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="568d4-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="568d4-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="568d4-209">Click **Add** button.</span></span> <span data-ttu-id="568d4-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="568d4-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="568d4-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="568d4-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="568d4-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="568d4-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="568d4-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="568d4-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="568d4-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="568d4-215">Testing single sign-on</span></span>

<span data-ttu-id="568d4-216">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="568d4-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="568d4-217">Quando você clica em Olá análise de negócios Agile Birst lado a lado no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de análise de negócios Birst Agile.</span><span class="sxs-lookup"><span data-stu-id="568d4-217">When you click hello Birst Agile Business Analytics tile in hello Access Panel, you should get automatically signed-on tooyour Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="568d4-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="568d4-218">Additional resources</span></span>

* [<span data-ttu-id="568d4-219">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="568d4-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="568d4-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="568d4-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png

