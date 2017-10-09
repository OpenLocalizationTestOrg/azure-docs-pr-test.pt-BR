---
title: "Tutorial: integração do Azure Active Directory com o TOPdesk - Público | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e TOPdesk - público."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="ffb11-103">Tutorial: integração do Azure Active Directory com o TOPdesk – Public</span><span class="sxs-lookup"><span data-stu-id="ffb11-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="ffb11-104">Neste tutorial, você aprenderá como toointegrate TOPdesk - público com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="ffb11-104">In this tutorial, you learn how toointegrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ffb11-105">Integração do TOPdesk - público com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb11-105">Integrating TOPdesk - Public with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ffb11-106">Você pode controlar no AD do Azure que tenha acesso tooTOPdesk - público.</span><span class="sxs-lookup"><span data-stu-id="ffb11-106">You can control in Azure AD who has access tooTOPdesk - Public.</span></span>
- <span data-ttu-id="ffb11-107">Você pode habilitar seu usuários tooautomatically get conectado tooTOPdesk - público (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb11-107">You can enable your users tooautomatically get signed-on tooTOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ffb11-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb11-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="ffb11-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ffb11-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffb11-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ffb11-110">Prerequisites</span></span>

<span data-ttu-id="ffb11-111">tooconfigure integração do AD do Azure com TOPdesk - público, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb11-111">tooconfigure Azure AD integration with TOPdesk - Public, you need hello following items:</span></span>

- <span data-ttu-id="ffb11-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffb11-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ffb11-113">Uma assinatura do TOPdesk – Public habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="ffb11-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ffb11-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ffb11-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ffb11-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ffb11-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ffb11-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ffb11-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ffb11-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ffb11-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ffb11-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ffb11-118">Scenario description</span></span>
<span data-ttu-id="ffb11-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ffb11-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ffb11-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="ffb11-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ffb11-121">Adicionando TOPdesk - público da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ffb11-121">Adding TOPdesk - Public from hello gallery</span></span>
2. <span data-ttu-id="ffb11-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffb11-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-hello-gallery"></a><span data-ttu-id="ffb11-123">Adicionando TOPdesk - público da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ffb11-123">Adding TOPdesk - Public from hello gallery</span></span>
<span data-ttu-id="ffb11-124">integração de saudação do tooconfigure do TOPdesk - público no Azure AD, é necessário tooadd TOPdesk - público na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ffb11-124">tooconfigure hello integration of TOPdesk - Public into Azure AD, you need tooadd TOPdesk - Public from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ffb11-125">**tooadd TOPdesk - público da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ffb11-125">**tooadd TOPdesk - Public from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffb11-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ffb11-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="ffb11-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ffb11-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="ffb11-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ffb11-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="ffb11-133">Na caixa de pesquisa hello, digite **TOPdesk - público**, selecione **TOPdesk - público** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ffb11-133">In hello search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TOPdesk - público na lista de resultados de saudação](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ffb11-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffb11-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ffb11-136">Nesta seção, você configurará e testará o logon único do Azure AD com o TOPdesk – Public, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ffb11-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ffb11-137">Para toowork de logon único, AD do Azure precisa tooknow que usuário de contraparte Olá no TOPdesk - público é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb11-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TOPdesk - Public is tooa user in Azure AD.</span></span> <span data-ttu-id="ffb11-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no TOPdesk - público precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ffb11-138">In other words, a link relationship between an Azure AD user and hello related user in TOPdesk - Public needs toobe established.</span></span>

<span data-ttu-id="ffb11-139">No TOPdesk - público, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffb11-139">In TOPdesk - Public, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ffb11-140">tooconfigure e testar o AD do Azure-logon único com TOPdesk - público, será necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb11-140">tooconfigure and test Azure AD single sign-on with TOPdesk - Public, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ffb11-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ffb11-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ffb11-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffb11-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ffb11-143">**[Criar um TOPdesk - público testar usuário](#create-a-topdesk---public-test-user)**  - toohave um equivalente do Britta Simon no TOPdesk - público que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="ffb11-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - toohave a counterpart of Britta Simon in TOPdesk - Public that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ffb11-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ffb11-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ffb11-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ffb11-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ffb11-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffb11-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ffb11-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no TOPdesk - público aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ffb11-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="ffb11-148">**tooconfigure logon único do AD do Azure com TOPdesk - público, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ffb11-148">**tooconfigure Azure AD single sign-on with TOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffb11-149">Em Olá portal do Azure, Olá **TOPdesk - público** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-149">In hello Azure portal, on hello **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="ffb11-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="ffb11-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="ffb11-153">Em Olá **TOPdesk - domínio público e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb11-153">On hello **TOPdesk - Public Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do TOPdesk – Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="ffb11-155">a.</span><span class="sxs-lookup"><span data-stu-id="ffb11-155">a.</span></span> <span data-ttu-id="ffb11-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="ffb11-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="ffb11-157">b.</span><span class="sxs-lookup"><span data-stu-id="ffb11-157">b.</span></span> <span data-ttu-id="ffb11-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="ffb11-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="ffb11-159">c.</span><span class="sxs-lookup"><span data-stu-id="ffb11-159">c.</span></span> <span data-ttu-id="ffb11-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="ffb11-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="ffb11-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="ffb11-161">These values are not real.</span></span> <span data-ttu-id="ffb11-162">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="ffb11-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ffb11-163">A URL de resposta é explicada posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="ffb11-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="ffb11-164">Entre em contato com [TOPdesk - a equipe de suporte de cliente público](https://help.topdesk.com/saas/enterprise/user/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="ffb11-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) tooget these values.</span></span>  

4. <span data-ttu-id="ffb11-165">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ffb11-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="ffb11-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ffb11-167">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ffb11-169">Em Olá **TOPdesk - público configuração** seção, clique em **configurar TOPdesk - público** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="ffb11-169">On hello **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ffb11-170">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ffb11-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do TOPdesk – Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="ffb11-172">Logon tooyour **TOPdesk - público** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="ffb11-172">Sign on tooyour **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="ffb11-173">Em Olá **TOPdesk** menu, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-173">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="ffb11-174">![Configurações](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="ffb11-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="ffb11-175">Clique em **Configurações de Logon**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="ffb11-176">![Configurações de logon](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Configurações de logon")</span><span class="sxs-lookup"><span data-stu-id="ffb11-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="ffb11-177">Expanda Olá **configurações de logon** menu e clique **geral**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-177">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="ffb11-178">![Geral](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "Geral")</span><span class="sxs-lookup"><span data-stu-id="ffb11-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="ffb11-179">Em Olá **pública** seção Olá **logon SAML** configuração, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb11-179">In hello **Public** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ffb11-180">![Configurações técnicas](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Configurações técnicas")</span><span class="sxs-lookup"><span data-stu-id="ffb11-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="ffb11-181">a.</span><span class="sxs-lookup"><span data-stu-id="ffb11-181">a.</span></span> <span data-ttu-id="ffb11-182">Clique em **baixar** toodownload Olá arquivo de metadados público e, em seguida, salve-o localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="ffb11-182">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="ffb11-183">b.</span><span class="sxs-lookup"><span data-stu-id="ffb11-183">b.</span></span> <span data-ttu-id="ffb11-184">Abra o arquivo de metadados Olá baixado e localize Olá **AssertionConsumerService** nó.</span><span class="sxs-lookup"><span data-stu-id="ffb11-184">Open hello downloaded metadata file, and then locate hello **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="ffb11-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="ffb11-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="ffb11-186">c.</span><span class="sxs-lookup"><span data-stu-id="ffb11-186">c.</span></span> <span data-ttu-id="ffb11-187">Saudação de cópia **AssertionConsumerService** valor, cole esse valor Olá **URL de resposta** textbox em **TOPdesk - domínio público e URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="ffb11-187">Copy hello **AssertionConsumerService** value, paste this value in hello **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="ffb11-188">toocreate um arquivo de certificado, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb11-188">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="ffb11-189">![Certificado](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificado")</span><span class="sxs-lookup"><span data-stu-id="ffb11-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="ffb11-190">a.</span><span class="sxs-lookup"><span data-stu-id="ffb11-190">a.</span></span> <span data-ttu-id="ffb11-191">Abra Olá baixou o arquivo de metadados do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb11-191">Open hello downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="ffb11-192">b.</span><span class="sxs-lookup"><span data-stu-id="ffb11-192">b.</span></span> <span data-ttu-id="ffb11-193">Expanda Olá **RoleDescriptor** nó que possui um **xsi: Type** de **fed: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-193">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="ffb11-194">c.</span><span class="sxs-lookup"><span data-stu-id="ffb11-194">c.</span></span> <span data-ttu-id="ffb11-195">Copie o valor Olá Olá **X509Certificate** nó.</span><span class="sxs-lookup"><span data-stu-id="ffb11-195">Copy hello value of hello **X509Certificate** node.</span></span>
    
    <span data-ttu-id="ffb11-196">d.</span><span class="sxs-lookup"><span data-stu-id="ffb11-196">d.</span></span> <span data-ttu-id="ffb11-197">Salvar Olá copiado **X509Certificate** valor localmente no seu computador em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="ffb11-197">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="ffb11-198">Em Olá **pública** seção, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-198">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="ffb11-199">![Logon SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "logon SAML")</span><span class="sxs-lookup"><span data-stu-id="ffb11-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="ffb11-200">Em Olá **Assistente de configuração SAML** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb11-200">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="ffb11-201">![Assistente de configuração SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Assistente de configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="ffb11-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="ffb11-202">a.</span><span class="sxs-lookup"><span data-stu-id="ffb11-202">a.</span></span> <span data-ttu-id="ffb11-203">tooupload seus metadados de download de arquivo do portal do Azure, em **metadados de Federação**, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-203">tooupload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="ffb11-204">b.</span><span class="sxs-lookup"><span data-stu-id="ffb11-204">b.</span></span> <span data-ttu-id="ffb11-205">tooupload arquivo seu certificado, em **certificado (RSA)**, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-205">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="ffb11-206">c.</span><span class="sxs-lookup"><span data-stu-id="ffb11-206">c.</span></span> <span data-ttu-id="ffb11-207">arquivo de logotipo Olá tooupload você obteve da equipe de suporte do TOPdesk hello, em **ícone do logotipo**, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-207">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="ffb11-208">d.</span><span class="sxs-lookup"><span data-stu-id="ffb11-208">d.</span></span> <span data-ttu-id="ffb11-209">Em Olá **atributo de nome de usuário** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="ffb11-209">In hello **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="ffb11-210">e.</span><span class="sxs-lookup"><span data-stu-id="ffb11-210">e.</span></span> <span data-ttu-id="ffb11-211">Em Olá **nome de exibição** caixa de texto, digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="ffb11-211">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="ffb11-212">f.</span><span class="sxs-lookup"><span data-stu-id="ffb11-212">f.</span></span> <span data-ttu-id="ffb11-213">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ffb11-214">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="ffb11-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ffb11-215">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ffb11-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ffb11-216">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ffb11-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ffb11-217">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffb11-217">Create an Azure AD test user</span></span>

<span data-ttu-id="ffb11-218">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb11-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="ffb11-220">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ffb11-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffb11-221">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="ffb11-221">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ffb11-223">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-223">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ffb11-225">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ffb11-225">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ffb11-227">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb11-227">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ffb11-229">a.</span><span class="sxs-lookup"><span data-stu-id="ffb11-229">a.</span></span> <span data-ttu-id="ffb11-230">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-230">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ffb11-231">b.</span><span class="sxs-lookup"><span data-stu-id="ffb11-231">b.</span></span> <span data-ttu-id="ffb11-232">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffb11-232">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ffb11-233">c.</span><span class="sxs-lookup"><span data-stu-id="ffb11-233">c.</span></span> <span data-ttu-id="ffb11-234">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="ffb11-234">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ffb11-235">d.</span><span class="sxs-lookup"><span data-stu-id="ffb11-235">d.</span></span> <span data-ttu-id="ffb11-236">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="ffb11-237">Criar um usuário de teste do TOPdesk – Public</span><span class="sxs-lookup"><span data-stu-id="ffb11-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="ffb11-238">Em ordem toolog de usuários tooenable AD do Azure no TOPdesk - público, eles devem ser provisionados no TOPdesk - público.</span><span class="sxs-lookup"><span data-stu-id="ffb11-238">In order tooenable Azure AD users toolog into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="ffb11-239">No caso de saudação do TOPdesk - público, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="ffb11-239">In hello case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="ffb11-240">tooconfigure provisionamento de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb11-240">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="ffb11-241">Logon tooyour **TOPdesk - público** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="ffb11-241">Sign on tooyour **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="ffb11-242">No menu de saudação na parte superior de saudação, clique em **TOPdesk \> novo \> arquivos de suporte \> pessoa**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-242">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="ffb11-243">![Pessoa](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Pessoa")</span><span class="sxs-lookup"><span data-stu-id="ffb11-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="ffb11-244">Na caixa de diálogo de nova pessoa hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb11-244">On hello New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="ffb11-245">![Nova pessoa](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Nova pessoa")</span><span class="sxs-lookup"><span data-stu-id="ffb11-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="ffb11-246">a.</span><span class="sxs-lookup"><span data-stu-id="ffb11-246">a.</span></span> <span data-ttu-id="ffb11-247">Clique em guia Geral hello.</span><span class="sxs-lookup"><span data-stu-id="ffb11-247">Click hello General tab.</span></span>

    <span data-ttu-id="ffb11-248">b.</span><span class="sxs-lookup"><span data-stu-id="ffb11-248">b.</span></span> <span data-ttu-id="ffb11-249">Em Olá **Sobrenome** caixa de texto, digite o sobrenome do usuário, Olá como Simon</span><span class="sxs-lookup"><span data-stu-id="ffb11-249">In hello **Surname** textbox, type Surname of hello user like Simon</span></span>
 
    <span data-ttu-id="ffb11-250">c.</span><span class="sxs-lookup"><span data-stu-id="ffb11-250">c.</span></span> <span data-ttu-id="ffb11-251">Selecione um **Site** conta hello.</span><span class="sxs-lookup"><span data-stu-id="ffb11-251">Select a **Site** for hello account.</span></span>
 
    <span data-ttu-id="ffb11-252">d.</span><span class="sxs-lookup"><span data-stu-id="ffb11-252">d.</span></span> <span data-ttu-id="ffb11-253">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="ffb11-254">Você pode usar qualquer outra TOPdesk - ferramenta de criação de conta de usuário público ou APIs fornecidos pelo TOPdesk - público tooprovision AD do Azure contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="ffb11-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ffb11-255">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffb11-255">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ffb11-256">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTOPdesk - público.</span><span class="sxs-lookup"><span data-stu-id="ffb11-256">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTOPdesk - Public.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="ffb11-258">**tooassign Britta Simon tooTOPdesk - público, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ffb11-258">**tooassign Britta Simon tooTOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffb11-259">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-259">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ffb11-261">Na lista de aplicativos hello, selecione **TOPdesk - público**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-261">In hello applications list, select **TOPdesk - Public**.</span></span>

    ![Olá TOPdesk - público link na lista de aplicativos Olá](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="ffb11-263">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-263">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="ffb11-265">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ffb11-265">Click **Add** button.</span></span> <span data-ttu-id="ffb11-266">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ffb11-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="ffb11-268">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffb11-268">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ffb11-269">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ffb11-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ffb11-270">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ffb11-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ffb11-271">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="ffb11-271">Test single sign-on</span></span>

<span data-ttu-id="ffb11-272">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffb11-272">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ffb11-273">Quando você clica em Olá TOPdesk - público lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour TOPdesk - público aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ffb11-273">When you click hello TOPdesk - Public tile in hello Access Panel, you should get automatically signed-on tooyour TOPdesk - Public application.</span></span>
<span data-ttu-id="ffb11-274">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ffb11-274">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ffb11-275">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ffb11-275">Additional resources</span></span>

* [<span data-ttu-id="ffb11-276">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ffb11-276">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ffb11-277">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ffb11-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

