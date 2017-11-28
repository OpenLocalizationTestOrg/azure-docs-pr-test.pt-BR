---
title: "Tutorial: integração do Azure Active Directory ao FreshDesk | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="cdeb3-103">Tutorial: integração do Azure Active Directory ao FreshDesk</span><span class="sxs-lookup"><span data-stu-id="cdeb3-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="cdeb3-104">Neste tutorial, você aprenderá como toointegrate FreshDesk com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="cdeb3-104">In this tutorial, you learn how toointegrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cdeb3-105">Integrando o FreshDesk com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdeb3-105">Integrating FreshDesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cdeb3-106">Você pode controlar no AD do Azure que tenha acesso tooFreshDesk</span><span class="sxs-lookup"><span data-stu-id="cdeb3-106">You can control in Azure AD who has access tooFreshDesk</span></span>
- <span data-ttu-id="cdeb3-107">Você pode habilitar seu usuários tooautomatically get conectado tooFreshDesk (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cdeb3-107">You can enable your users tooautomatically get signed-on tooFreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cdeb3-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="cdeb3-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="cdeb3-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cdeb3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdeb3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cdeb3-110">Prerequisites</span></span>

<span data-ttu-id="cdeb3-111">tooconfigure integração do AD do Azure com o FreshDesk, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdeb3-111">tooconfigure Azure AD integration with FreshDesk, you need hello following items:</span></span>

- <span data-ttu-id="cdeb3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cdeb3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cdeb3-113">Uma assinatura do FreshDesk com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="cdeb3-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cdeb3-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cdeb3-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cdeb3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cdeb3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cdeb3-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cdeb3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cdeb3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cdeb3-118">Scenario description</span></span>
<span data-ttu-id="cdeb3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cdeb3-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="cdeb3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cdeb3-121">Adicionando FreshDesk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cdeb3-121">Adding FreshDesk from hello gallery</span></span>
2. <span data-ttu-id="cdeb3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cdeb3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-hello-gallery"></a><span data-ttu-id="cdeb3-123">Adicionando FreshDesk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cdeb3-123">Adding FreshDesk from hello gallery</span></span>
<span data-ttu-id="cdeb3-124">integração de saudação tooconfigure do FreshDesk no AD do Azure, você precisa tooadd FreshDesk da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-124">tooconfigure hello integration of FreshDesk into Azure AD, you need tooadd FreshDesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cdeb3-125">**tooadd FreshDesk da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cdeb3-125">**tooadd FreshDesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdeb3-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cdeb3-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cdeb3-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cdeb3-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cdeb3-133">Na caixa de pesquisa hello, digite **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-133">In hello search box, type **FreshDesk**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="cdeb3-135">No painel de resultados de saudação, selecione **FreshDesk**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-135">In hello results panel, select **FreshDesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cdeb3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cdeb3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cdeb3-138">Nesta seção, você configurará e testará o logon único do Azure AD com o FreshDesk, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cdeb3-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no FreshDesk é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshDesk is tooa user in Azure AD.</span></span> <span data-ttu-id="cdeb3-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no FreshDesk precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-140">In other words, a link relationship between an Azure AD user and hello related user in FreshDesk needs toobe established.</span></span>

<span data-ttu-id="cdeb3-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FreshDesk.</span></span>

<span data-ttu-id="cdeb3-142">tooconfigure e teste de logon único do AD do Azure com o FreshDesk, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdeb3-142">tooconfigure and test Azure AD single sign-on with FreshDesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cdeb3-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cdeb3-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cdeb3-145">**[Criar um usuário de teste do FreshDesk](#creating-a-freshdesk-test-user)**  -toohave um equivalente do Britta Simon no FreshDesk é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - toohave a counterpart of Britta Simon in FreshDesk that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="cdeb3-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cdeb3-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cdeb3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdeb3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cdeb3-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo do Freshservice.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="cdeb3-150">**tooconfigure AD do Azure-logon único com o FreshDesk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cdeb3-150">**tooconfigure Azure AD single sign-on with FreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdeb3-151">No portal de gerenciamento do Azure do hello, no hello **FreshDesk** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-151">In hello Azure Management portal, on hello **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cdeb3-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="cdeb3-155">Em Olá **FreshDesk domínio e URLs** seção, digite Olá **URL de logon** como: `https://<tenant-name>.freshdesk.com` ou qualquer outro valor Freshdesk sugeriu.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-155">On hello **FreshDesk Domain and URLs** section, please enter hello **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="cdeb3-157">Observe que esse não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-157">Please note that this is not the real value.</span></span> <span data-ttu-id="cdeb3-158">Você precisa atualizar o valor com a URL de Entrada real.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="cdeb3-159">Para obter esse valor, entre em contato com a [equipe de suporte do cliente FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg).</span><span class="sxs-lookup"><span data-stu-id="cdeb3-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="cdeb3-160">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado** e, em seguida, salve o certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-160">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="cdeb3-162">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="cdeb3-162">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cdeb3-164">Em Olá **FreshDesk configuração** seção, clique em **FreshDesk configurar** tooopen configurar o logon na janela.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-164">On hello **FreshDesk Configuration** section, click **Configure FreshDesk** tooopen Configure sign-on window.</span></span> <span data-ttu-id="cdeb3-165">Copiar hello SAML Single Sign-On URL do serviço e a URL de logout de saudação **referência rápida** seção.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-165">Copy hello SAML Single Sign-On Service URL and Sign-Out URL from hello **Quick Reference** section.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="cdeb3-167">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Freshdesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="cdeb3-168">No menu de saudação na parte superior de saudação, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-168">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="cdeb3-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="cdeb3-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="cdeb3-170">Em Olá **configurações gerais** , clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-170">In hello **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="cdeb3-171">![Segurança](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="cdeb3-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="cdeb3-172">Em Olá **segurança** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdeb3-172">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cdeb3-173">![Logon Único](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="cdeb3-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="cdeb3-174">a.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-174">a.</span></span> <span data-ttu-id="cdeb3-175">Para **SSO (Logon Único)**, selecione **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="cdeb3-176">b.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-176">b.</span></span> <span data-ttu-id="cdeb3-177">Selecione **SSO do SAML**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="cdeb3-178">c.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-178">c.</span></span> <span data-ttu-id="cdeb3-179">Saudação de tipo **Single Sign-On URL do serviço SAML** você copiou do portal do Azure para Olá **URL de logon** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-179">Type hello **SAML Single Sign-On Service URL** you copied from Azure portal into hello **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="cdeb3-180">d.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-180">d.</span></span> <span data-ttu-id="cdeb3-181">Saudação de tipo **URL de logout** você copiou do portal do Azure para Olá **URL de Logout** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-181">Type hello **Sign-Out URL**  you copied from Azure portal into hello **Logout URL** textbox.</span></span>

    <span data-ttu-id="cdeb3-182">e.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-182">e.</span></span> <span data-ttu-id="cdeb3-183">Saudação de cópia **impressão digital** valor de certificado Olá baixado do portal do Azure e cole-a saudação **impressão digital do certificado de segurança** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-183">Copy hello **Thumbprint** value from hello downloaded certificate from Azure portal and paste it into hello **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="cdeb3-184">Para obter mais detalhes, consulte [como tooretrieve o valor de impressão digital do certificado](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="cdeb3-184">For more details, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="cdeb3-185">f.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-185">f.</span></span> <span data-ttu-id="cdeb3-186">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cdeb3-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cdeb3-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="cdeb3-188">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cdeb3-190">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cdeb3-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdeb3-191">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cdeb3-193">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cdeb3-195">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cdeb3-197">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdeb3-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cdeb3-199">a.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-199">a.</span></span> <span data-ttu-id="cdeb3-200">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cdeb3-201">b.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-201">b.</span></span> <span data-ttu-id="cdeb3-202">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cdeb3-203">c.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-203">c.</span></span> <span data-ttu-id="cdeb3-204">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cdeb3-205">d.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-205">d.</span></span> <span data-ttu-id="cdeb3-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="cdeb3-207">Criar um usuário de teste FreshDesk</span><span class="sxs-lookup"><span data-stu-id="cdeb3-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="cdeb3-208">Ordem tooenable AD do Azure usuários toolog no FreshDesk, eles devem ser provisionados no FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-208">In order tooenable Azure AD users toolog into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="cdeb3-209">No caso de saudação do FreshDesk, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-209">In hello case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="cdeb3-210">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cdeb3-210">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdeb3-211">Faça logon no tooyour **Freshdesk** locatário.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-211">Log in tooyour **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="cdeb3-212">No menu de saudação na parte superior de saudação, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-212">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="cdeb3-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="cdeb3-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="cdeb3-214">Em Olá **configurações gerais** , clique em **agentes**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-214">In hello **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="cdeb3-215">![Agentes](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agentes")</span><span class="sxs-lookup"><span data-stu-id="cdeb3-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="cdeb3-216">Clique em **Novo Agente**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="cdeb3-217">![Novo Agente](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "Novo Agente")</span><span class="sxs-lookup"><span data-stu-id="cdeb3-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="cdeb3-218">Na caixa de diálogo de informações de agentes hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdeb3-218">On hello Agent Information dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="cdeb3-219">![Informações de Agente](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Informações de Agente")</span><span class="sxs-lookup"><span data-stu-id="cdeb3-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="cdeb3-220">a.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-220">a.</span></span> <span data-ttu-id="cdeb3-221">Em Olá **nome completo** caixa de texto, nome de saudação do tipo da conta de saudação do AD do Azure que você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-221">In hello **Full Name** textbox, type hello name of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="cdeb3-222">b.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-222">b.</span></span> <span data-ttu-id="cdeb3-223">Em Olá **Email** caixa de texto, Olá tipo AD do Azure endereço de email da conta de saudação do AD do Azure que você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-223">In hello **Email** textbox, type hello Azure AD email address of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="cdeb3-224">c.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-224">c.</span></span> <span data-ttu-id="cdeb3-225">Em Olá **título** caixa de texto, digite o título da saudação da conta de saudação do AD do Azure que você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-225">In hello **Title** textbox, type hello title of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="cdeb3-226">d.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-226">d.</span></span> <span data-ttu-id="cdeb3-227">Selecione **Função de agentes** e clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="cdeb3-228">e.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-228">e.</span></span> <span data-ttu-id="cdeb3-229">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="cdeb3-230">proprietário de conta do AD do Azure Olá receberá um email que inclui uma conta de saudação do link tooconfirm antes que ele seja ativado.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-230">hello Azure AD account holder will get an email that includes a link tooconfirm hello account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="cdeb3-231">Você pode usar qualquer ferramenta de criação outros Freshdesk usuário conta ou APIs fornecidas pelo Freshdesk tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk tooprovision AAD user accounts.</span></span> <span data-ttu-id="cdeb3-232">tooFreshDesk.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-232">tooFreshDesk.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cdeb3-233">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cdeb3-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cdeb3-234">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooBox seu acesso.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBox.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cdeb3-236">**tooassign Britta Simon tooFreshDesk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cdeb3-236">**tooassign Britta Simon tooFreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdeb3-237">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-237">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cdeb3-239">Na lista de aplicativos hello, selecione **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-239">In hello applications list, select **FreshDesk**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="cdeb3-241">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cdeb3-243">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-243">Click **Add** button.</span></span> <span data-ttu-id="cdeb3-244">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cdeb3-246">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cdeb3-247">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cdeb3-248">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cdeb3-249">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cdeb3-249">Testing single sign-on</span></span>

<span data-ttu-id="cdeb3-250">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cdeb3-251">Quando você clica em bloco FreshDesk Olá Olá painel de acesso, você deve obter logon página tooget conectado tooyour FreshDesk aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cdeb3-251">When you click hello FreshDesk tile in hello Access Panel, you should get login page tooget signed-on tooyour FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cdeb3-252">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cdeb3-252">Additional resources</span></span>

* [<span data-ttu-id="cdeb3-253">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cdeb3-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cdeb3-254">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cdeb3-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

