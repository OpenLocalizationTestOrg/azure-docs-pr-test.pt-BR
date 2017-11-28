---
title: "Tutorial: integração do Azure Active Directory com o LearnUpon | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="d5900-103">Tutorial: Integração do Active Directory do Azure com o LearnUpon</span><span class="sxs-lookup"><span data-stu-id="d5900-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="d5900-104">Neste tutorial, você aprenderá como toointegrate LearnUpon com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d5900-104">In this tutorial, you learn how toointegrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d5900-105">Integrando LearnUpon com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5900-105">Integrating LearnUpon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d5900-106">Você pode controlar no AD do Azure que tenha acesso tooLearnUpon</span><span class="sxs-lookup"><span data-stu-id="d5900-106">You can control in Azure AD who has access tooLearnUpon</span></span>
- <span data-ttu-id="d5900-107">Você pode habilitar seu usuários tooautomatically get conectado tooLearnUpon (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5900-107">You can enable your users tooautomatically get signed-on tooLearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d5900-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d5900-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d5900-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d5900-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5900-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d5900-110">Prerequisites</span></span>

<span data-ttu-id="d5900-111">tooconfigure integração do AD do Azure com LearnUpon, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5900-111">tooconfigure Azure AD integration with LearnUpon, you need hello following items:</span></span>

- <span data-ttu-id="d5900-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5900-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d5900-113">Uma assinatura do LearnUpon habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="d5900-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d5900-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d5900-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d5900-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d5900-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d5900-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d5900-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d5900-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5900-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d5900-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d5900-118">Scenario description</span></span>
<span data-ttu-id="d5900-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d5900-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d5900-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="d5900-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d5900-121">Adicionando LearnUpon da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d5900-121">Adding LearnUpon from hello gallery</span></span>
2. <span data-ttu-id="d5900-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5900-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-hello-gallery"></a><span data-ttu-id="d5900-123">Adicionando LearnUpon da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d5900-123">Adding LearnUpon from hello gallery</span></span>
<span data-ttu-id="d5900-124">integração de saudação tooconfigure de LearnUpon no AD do Azure, você precisa tooadd LearnUpon da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d5900-124">tooconfigure hello integration of LearnUpon into Azure AD, you need tooadd LearnUpon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d5900-125">**tooadd LearnUpon da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d5900-125">**tooadd LearnUpon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5900-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d5900-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d5900-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d5900-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d5900-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d5900-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d5900-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5900-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d5900-133">Na caixa de pesquisa hello, digite **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="d5900-133">In hello search box, type **LearnUpon**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="d5900-135">No painel de resultados de saudação, selecione **LearnUpon**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d5900-135">In hello results panel, select **LearnUpon**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d5900-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5900-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d5900-138">Nesta seção, você configurará e testará o logon único do Azure AD com o LearnUpon, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d5900-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d5900-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em LearnUpon é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5900-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LearnUpon is tooa user in Azure AD.</span></span> <span data-ttu-id="d5900-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em LearnUpon precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d5900-140">In other words, a link relationship between an Azure AD user and hello related user in LearnUpon needs toobe established.</span></span>

<span data-ttu-id="d5900-141">LearnUpon, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5900-141">In LearnUpon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d5900-142">tooconfigure e teste de logon único do AD do Azure com LearnUpon, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5900-142">tooconfigure and test Azure AD single sign-on with LearnUpon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d5900-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d5900-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d5900-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d5900-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d5900-145">**[Criar um usuário de teste LearnUpon](#creating-a-learnupon-test-user)**  -toohave um equivalente do Britta Simon em LearnUpon é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="d5900-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - toohave a counterpart of Britta Simon in LearnUpon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d5900-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="d5900-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d5900-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="d5900-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d5900-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5900-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d5900-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="d5900-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="d5900-150">**tooconfigure AD do Azure-logon único com LearnUpon, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d5900-150">**tooconfigure Azure AD single sign-on with LearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5900-151">Em Olá portal do Azure, Olá **LearnUpon** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="d5900-151">In hello Azure portal, on hello **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d5900-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="d5900-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="d5900-155">Em Olá **LearnUpon domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5900-155">On hello **LearnUpon Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="d5900-157">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="d5900-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d5900-158">Observe que isso não é um valor real hello.</span><span class="sxs-lookup"><span data-stu-id="d5900-158">Please note that this is not hello real value.</span></span> <span data-ttu-id="d5900-159">Você tem tooupdate esse valor com a URL de resposta real hello.</span><span class="sxs-lookup"><span data-stu-id="d5900-159">you have tooupdate this value with hello actual Reply URL.</span></span> <span data-ttu-id="d5900-160">entre em contato com tooget esse valor [a equipe de suporte LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="d5900-160">tooget this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="d5900-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d5900-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="d5900-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d5900-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d5900-165">Em Olá **LearnUpon configuração** seção, clique em **configurar LearnUpon** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="d5900-165">On hello **LearnUpon Configuration** section, click **Configure LearnUpon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d5900-166">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="d5900-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="d5900-168">Abra outra instância do navegador e faça logon no LearnUpon com uma conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="d5900-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="d5900-169">Clique em Olá **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="d5900-169">Click hello **settings** tab.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="d5900-171">Clique em **logon único - SAML**e, em seguida, clique em **configurações gerais** tooconfigure configurações do SAML.</span><span class="sxs-lookup"><span data-stu-id="d5900-171">Click **Single Sign On - SAML**, and then click **General Settings** tooconfigure SAML settings.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="d5900-173">Em Olá **configurações gerais** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5900-173">In hello **General Settings** section, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="d5900-175">a.</span><span class="sxs-lookup"><span data-stu-id="d5900-175">a.</span></span> <span data-ttu-id="d5900-176">Selecione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="d5900-176">Select **Enabled**.</span></span>

    <span data-ttu-id="d5900-177">b.</span><span class="sxs-lookup"><span data-stu-id="d5900-177">b.</span></span> <span data-ttu-id="d5900-178">Selecione **versão** como **2.0**.</span><span class="sxs-lookup"><span data-stu-id="d5900-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="d5900-179">c.</span><span class="sxs-lookup"><span data-stu-id="d5900-179">c.</span></span> <span data-ttu-id="d5900-180">Selecione **Ignorar condições** como **Não**.</span><span class="sxs-lookup"><span data-stu-id="d5900-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="d5900-181">d.</span><span class="sxs-lookup"><span data-stu-id="d5900-181">d.</span></span> <span data-ttu-id="d5900-182">Em Olá **nome do parâmetro de postagem de Token SAML** caixa de texto, nome de saudação do tipo de solicitação post parâmetro toohello SAML consumidor URL indicado acima que contém a saudação de asserção SAML toobe verificado e é autenticado - por exemplo  **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="d5900-182">In hello **SAML Token Post param name** textbox, type hello name of request post parameter toohello SAML consumer URL indicated above that contains hello SAML Assertion toobe verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="d5900-183">e.</span><span class="sxs-lookup"><span data-stu-id="d5900-183">e.</span></span> <span data-ttu-id="d5900-184">Em Olá **formato de nome de identificador** texto, o valor do tipo hello indica onde em seus usuários de saudação de asserção SAML identificador (endereço de Email) reside - por exemplo **urn: oasis: nomes: tc: SAML: 1.1 nameid-format: endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="d5900-184">In hello **Name Identifier Format** textbox, type hello value that indicates where in your SAML Assertion hello users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="d5900-185">f.</span><span class="sxs-lookup"><span data-stu-id="d5900-185">f.</span></span> <span data-ttu-id="d5900-186">Em Olá **identificar o local do provedor** caixa de texto, o valor do tipo hello indica onde hello, os usuários são enviados tooif clicarem em seu ícone carregado na sua tela de logon do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5900-186">In hello **Identify Provider Location** textbox, type hello value that indicates where hello users are sent tooif they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="d5900-187">g.</span><span class="sxs-lookup"><span data-stu-id="d5900-187">g.</span></span> <span data-ttu-id="d5900-188">Em Olá **sair URL** caixa de texto, colar Olá **URL de logout** que você copiou de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5900-188">In hello **Sign out URL** textbox, paste hello **Sign-Out URL** which you have copied from hello Azure portal.</span></span>
    
    <span data-ttu-id="d5900-189">h.</span><span class="sxs-lookup"><span data-stu-id="d5900-189">h.</span></span> <span data-ttu-id="d5900-190">Clique em **gerenciar imprime dedo**e, em seguida, carregar a impressão digital de saudação do seu certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="d5900-190">Click **Manage finger prints**, and then upload hello finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="d5900-191">Clique em **as configurações do usuário**e, em seguida, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5900-191">Click **User Settings**, and then perform hello following steps:</span></span>
   
     ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="d5900-193">a.</span><span class="sxs-lookup"><span data-stu-id="d5900-193">a.</span></span> <span data-ttu-id="d5900-194">Em Olá **formato do identificador de nome** caixa de texto valor do tipo hello informa qual em seu nome de usuários de asserção SAML Olá reside - por exemplo: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="d5900-194">In hello **First Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="d5900-195">b.</span><span class="sxs-lookup"><span data-stu-id="d5900-195">b.</span></span> <span data-ttu-id="d5900-196">Em Olá **último nome de identificador de formato** caixa de texto valor do tipo hello informa qual em seu sobrenome de usuários de asserção SAML Olá reside - por exemplo: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="d5900-196">In hello **Last Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="d5900-197">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="d5900-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d5900-198">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="d5900-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d5900-199">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d5900-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d5900-200">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5900-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="d5900-201">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5900-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d5900-203">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d5900-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5900-204">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d5900-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d5900-206">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="d5900-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d5900-208">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5900-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d5900-210">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5900-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d5900-212">a.</span><span class="sxs-lookup"><span data-stu-id="d5900-212">a.</span></span> <span data-ttu-id="d5900-213">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d5900-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d5900-214">b.</span><span class="sxs-lookup"><span data-stu-id="d5900-214">b.</span></span> <span data-ttu-id="d5900-215">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d5900-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d5900-216">c.</span><span class="sxs-lookup"><span data-stu-id="d5900-216">c.</span></span> <span data-ttu-id="d5900-217">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="d5900-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d5900-218">d.</span><span class="sxs-lookup"><span data-stu-id="d5900-218">d.</span></span> <span data-ttu-id="d5900-219">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d5900-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="d5900-220">Criar um usuário de teste do LearnUpon</span><span class="sxs-lookup"><span data-stu-id="d5900-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="d5900-221">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="d5900-221">hello objective of this section is toocreate a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="d5900-222">O LearnUpon dá suporte ao provisionamento just-in-time, que é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="d5900-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d5900-223">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="d5900-223">There is no action item for you in this section.</span></span> <span data-ttu-id="d5900-224">Será criado um novo usuário durante uma tentativa tooaccess LearnUpon se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="d5900-224">A new user will be created during an attempt tooaccess LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="d5900-225">[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d5900-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="d5900-226">Se você precisar toocreate um usuário manualmente, será necessário toocontact [a equipe de suporte LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="d5900-226">If you need toocreate an user manually, you need toocontact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d5900-227">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5900-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d5900-228">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLearnUpon.</span><span class="sxs-lookup"><span data-stu-id="d5900-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearnUpon.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d5900-230">**tooassign Britta Simon tooLearnUpon, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d5900-230">**tooassign Britta Simon tooLearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5900-231">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d5900-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d5900-233">Na lista de aplicativos hello, selecione **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="d5900-233">In hello applications list, select **LearnUpon**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="d5900-235">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d5900-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d5900-237">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d5900-237">Click **Add** button.</span></span> <span data-ttu-id="d5900-238">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5900-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d5900-240">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5900-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d5900-241">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5900-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d5900-242">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5900-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d5900-243">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d5900-243">Testing single sign-on</span></span>

<span data-ttu-id="d5900-244">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5900-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d5900-245">Quando você clica em bloco LearnUpon Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour LearnUpon aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5900-245">When you click hello LearnUpon tile in hello Access Panel, you should get automatically signed-on tooyour LearnUpon application.</span></span>
<span data-ttu-id="d5900-246">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d5900-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d5900-247">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d5900-247">Additional resources</span></span>

* [<span data-ttu-id="d5900-248">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d5900-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d5900-249">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d5900-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

