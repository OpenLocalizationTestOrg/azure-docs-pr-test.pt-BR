---
title: "Tutorial: Integração do Azure Active Directory ao SkyDesk Email | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o SkyDesk Email."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="23a8b-103">Tutorial: integração do Azure Active Directory ao SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="23a8b-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="23a8b-104">Neste tutorial, você aprenderá como toointegrate SkyDesk de Email com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="23a8b-104">In this tutorial, you learn how toointegrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23a8b-105">Integração de SkyDesk Email com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="23a8b-105">Integrating SkyDesk Email with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="23a8b-106">Você pode controlar no AD do Azure que tenha acesso tooSkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="23a8b-106">You can control in Azure AD who has access tooSkyDesk Email</span></span>
- <span data-ttu-id="23a8b-107">Você pode habilitar seu usuários tooautomatically get conectado tooSkyDesk Email (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23a8b-107">You can enable your users tooautomatically get signed-on tooSkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="23a8b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="23a8b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="23a8b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="23a8b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23a8b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="23a8b-110">Prerequisites</span></span>

<span data-ttu-id="23a8b-111">tooconfigure integração do AD do Azure com SkyDesk Email, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="23a8b-111">tooconfigure Azure AD integration with SkyDesk Email, you need hello following items:</span></span>

- <span data-ttu-id="23a8b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23a8b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23a8b-113">Uma assinatura habilitada para logon único do SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="23a8b-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23a8b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="23a8b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23a8b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="23a8b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23a8b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="23a8b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="23a8b-117">Caso não tenha um ambiente de avaliação do Azure AD, obtenha uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="23a8b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23a8b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="23a8b-118">Scenario description</span></span>
<span data-ttu-id="23a8b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="23a8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23a8b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="23a8b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23a8b-121">Adicionando SkyDesk Email da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="23a8b-121">Adding SkyDesk Email from hello gallery</span></span>
2. <span data-ttu-id="23a8b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23a8b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-hello-gallery"></a><span data-ttu-id="23a8b-123">Adicionando SkyDesk Email da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="23a8b-123">Adding SkyDesk Email from hello gallery</span></span>
<span data-ttu-id="23a8b-124">integração de Olá tooconfigure de SkyDesk Email no AD do Azure, você precisa tooadd SkyDesk Email da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="23a8b-124">tooconfigure hello integration of SkyDesk Email into Azure AD, you need tooadd SkyDesk Email from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="23a8b-125">**tooadd SkyDesk Email da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="23a8b-125">**tooadd SkyDesk Email from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="23a8b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="23a8b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="23a8b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="23a8b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="23a8b-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23a8b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="23a8b-133">Na caixa de pesquisa hello, digite **SkyDesk Email**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-133">In hello search box, type **SkyDesk Email**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="23a8b-135">No painel de resultados de saudação, selecione **SkyDesk Email**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="23a8b-135">In hello results panel, select **SkyDesk Email**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="23a8b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23a8b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="23a8b-138">Nesta seção, você configura e testa o logon único do Azure AD com o SkyDesk Email, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="23a8b-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="23a8b-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Email de SkyDesk é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="23a8b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SkyDesk Email is tooa user in Azure AD.</span></span> <span data-ttu-id="23a8b-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no SkyDesk Email precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="23a8b-140">In other words, a link relationship between an Azure AD user and hello related user in SkyDesk Email needs toobe established.</span></span>

<span data-ttu-id="23a8b-141">No Email de SkyDesk atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="23a8b-141">In SkyDesk Email, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="23a8b-142">tooconfigure e teste de logon único do AD do Azure com SkyDesk Email, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="23a8b-142">tooconfigure and test Azure AD single sign-on with SkyDesk Email, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="23a8b-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="23a8b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="23a8b-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23a8b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="23a8b-145">**[Criar um usuário de teste de SkyDesk Email](#creating-a-skydesk-email-test-user)**  -toohave um equivalente do Britta Simon no SkyDesk Email toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="23a8b-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - toohave a counterpart of Britta Simon in SkyDesk Email that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="23a8b-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="23a8b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="23a8b-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="23a8b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="23a8b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="23a8b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="23a8b-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="23a8b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="23a8b-150">**tooconfigure AD do Azure-logon único com SkyDesk Email, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="23a8b-150">**tooconfigure Azure AD single sign-on with SkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="23a8b-151">Em Olá portal do Azure, Olá **SkyDesk Email** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-151">In hello Azure portal, on hello **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="23a8b-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="23a8b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="23a8b-155">Em Olá **SkyDesk domínio de Email e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="23a8b-155">On hello **SkyDesk Email Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="23a8b-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="23a8b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="23a8b-158">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="23a8b-158">hello value is not real.</span></span> <span data-ttu-id="23a8b-159">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="23a8b-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="23a8b-160">Entre em contato com [equipe de suporte do cliente de Email SkyDesk](https://www.skydesk.sg/support/) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="23a8b-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="23a8b-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="23a8b-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="23a8b-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="23a8b-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="23a8b-165">Em Olá **SkyDesk Email configuração** seção, clique em **Configurar Email de SkyDesk** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="23a8b-165">On hello **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="23a8b-166">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="23a8b-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="23a8b-168">tooenable SSO em **SkyDesk Email**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="23a8b-168">tooenable SSO in **SkyDesk Email**, perform hello following steps:</span></span>

    <span data-ttu-id="23a8b-169">a.</span><span class="sxs-lookup"><span data-stu-id="23a8b-169">a.</span></span> <span data-ttu-id="23a8b-170">Logon tooyour conta de SkyDesk Email como administrador.</span><span class="sxs-lookup"><span data-stu-id="23a8b-170">Sign-on tooyour SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="23a8b-171">b.</span><span class="sxs-lookup"><span data-stu-id="23a8b-171">b.</span></span> <span data-ttu-id="23a8b-172">No menu de saudação na parte superior de saudação, clique em **instalação**e selecione **Org**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-172">In hello menu on hello top, click **Setup**, and select **Org**.</span></span> 
    
      ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="23a8b-174">c.</span><span class="sxs-lookup"><span data-stu-id="23a8b-174">c.</span></span> <span data-ttu-id="23a8b-175">Clique em **domínios** do painel esquerdo do hello.</span><span class="sxs-lookup"><span data-stu-id="23a8b-175">Click on **Domains** from hello left panel.</span></span>
    
      ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="23a8b-177">d.</span><span class="sxs-lookup"><span data-stu-id="23a8b-177">d.</span></span> <span data-ttu-id="23a8b-178">Clique em **Adicionar Domínio**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-178">Click on **Add Domain**.</span></span>
    
      ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="23a8b-180">e.</span><span class="sxs-lookup"><span data-stu-id="23a8b-180">e.</span></span> <span data-ttu-id="23a8b-181">Insira seu nome de domínio e, em seguida, verifique se Olá domínio.</span><span class="sxs-lookup"><span data-stu-id="23a8b-181">Enter your Domain name, and then verify hello Domain.</span></span>
    
      ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="23a8b-183">f.</span><span class="sxs-lookup"><span data-stu-id="23a8b-183">f.</span></span> <span data-ttu-id="23a8b-184">Clique em **autenticação SAML** do painel esquerdo do hello.</span><span class="sxs-lookup"><span data-stu-id="23a8b-184">Click on **SAML Authentication** from hello left panel.</span></span>
    
      ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="23a8b-186">Em Olá **autenticação SAML** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="23a8b-186">On hello **SAML Authentication** dialog page, perform hello following steps:</span></span>
   
      ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="23a8b-188">autenticação baseada em toouse SAML, você deve ter **verificar domínio** ou **portal URL** instalação.</span><span class="sxs-lookup"><span data-stu-id="23a8b-188">toouse SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="23a8b-189">Você pode definir o portal de saudação URL com nome exclusivo da saudação.</span><span class="sxs-lookup"><span data-stu-id="23a8b-189">You can set hello portal URL with hello unique name.</span></span>
    > 
    > 
   
    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="23a8b-191">a.</span><span class="sxs-lookup"><span data-stu-id="23a8b-191">a.</span></span> <span data-ttu-id="23a8b-192">Em Olá **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="23a8b-192">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="23a8b-193">b.</span><span class="sxs-lookup"><span data-stu-id="23a8b-193">b.</span></span> <span data-ttu-id="23a8b-194">Em Olá **Logout** caixa de texto da URL, valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="23a8b-194">In hello **Logout** URL textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="23a8b-195">c.</span><span class="sxs-lookup"><span data-stu-id="23a8b-195">c.</span></span> <span data-ttu-id="23a8b-196">A **URL de Alteração de Senha** é opcional, portanto, deixe-a em branco.</span><span class="sxs-lookup"><span data-stu-id="23a8b-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="23a8b-197">d.</span><span class="sxs-lookup"><span data-stu-id="23a8b-197">d.</span></span> <span data-ttu-id="23a8b-198">Clique em **obter chave de arquivo** tooselect seu certificado baixado do portal do Azure e clique **abrir** certificado de saudação tooupload.</span><span class="sxs-lookup"><span data-stu-id="23a8b-198">Click on **Get Key From File** tooselect your downloaded certificate from Azure portal, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="23a8b-199">e.</span><span class="sxs-lookup"><span data-stu-id="23a8b-199">e.</span></span> <span data-ttu-id="23a8b-200">Para **Algoritmo**, selecione **RSA**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="23a8b-201">f.</span><span class="sxs-lookup"><span data-stu-id="23a8b-201">f.</span></span> <span data-ttu-id="23a8b-202">Clique em **Okey** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="23a8b-202">Click **Ok** toosave hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="23a8b-203">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="23a8b-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="23a8b-204">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="23a8b-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="23a8b-205">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="23a8b-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="23a8b-206">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23a8b-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="23a8b-207">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="23a8b-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="23a8b-209">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="23a8b-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="23a8b-210">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="23a8b-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="23a8b-212">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="23a8b-214">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="23a8b-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="23a8b-216">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="23a8b-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="23a8b-218">a.</span><span class="sxs-lookup"><span data-stu-id="23a8b-218">a.</span></span> <span data-ttu-id="23a8b-219">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23a8b-220">b.</span><span class="sxs-lookup"><span data-stu-id="23a8b-220">b.</span></span> <span data-ttu-id="23a8b-221">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="23a8b-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="23a8b-222">c.</span><span class="sxs-lookup"><span data-stu-id="23a8b-222">c.</span></span> <span data-ttu-id="23a8b-223">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="23a8b-224">d.</span><span class="sxs-lookup"><span data-stu-id="23a8b-224">d.</span></span> <span data-ttu-id="23a8b-225">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="23a8b-226">Criar um usuário de teste do SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="23a8b-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="23a8b-227">Nesta seção, você criará uma usuária chamada Brenda Fernandes no SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="23a8b-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="23a8b-228">Clique em **acesso de usuário** de saudação à esquerda do painel no SkyDesk Email e, em seguida, insira seu nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="23a8b-228">Click on **User Access** from hello left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="23a8b-230">Se você precisar que os usuários em massa de toocreate, você precisa Olá toocontact [equipe de suporte do cliente de Email SkyDesk](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="23a8b-230">If you need toocreate bulk users, you need toocontact hello [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="23a8b-231">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23a8b-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="23a8b-232">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="23a8b-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkyDesk Email.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="23a8b-234">**tooassign Britta Simon tooSkyDesk Email, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="23a8b-234">**tooassign Britta Simon tooSkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="23a8b-235">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="23a8b-237">Na lista de aplicativos hello, selecione **SkyDesk Email**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-237">In hello applications list, select **SkyDesk Email**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="23a8b-239">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="23a8b-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="23a8b-241">Click **Add** button.</span></span> <span data-ttu-id="23a8b-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23a8b-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="23a8b-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="23a8b-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="23a8b-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23a8b-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="23a8b-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23a8b-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="23a8b-247">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="23a8b-247">Testing single sign-on</span></span>

<span data-ttu-id="23a8b-248">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="23a8b-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="23a8b-249">Quando você clica em Olá SkyDesk Email bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="23a8b-249">When you click hello SkyDesk Email tile in hello Access Panel, you should get automatically signed-on tooyour SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="23a8b-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="23a8b-250">Additional resources</span></span>

* [<span data-ttu-id="23a8b-251">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="23a8b-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="23a8b-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="23a8b-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

