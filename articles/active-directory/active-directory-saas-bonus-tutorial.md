---
title: "Tutorial: Integração do Azure Active Directory ao Bonusly | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="2ce61-103">Tutorial: integração do Azure Active Directory ao Bonusly</span><span class="sxs-lookup"><span data-stu-id="2ce61-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="2ce61-104">Neste tutorial, você aprenderá como toointegrate Bonusly com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="2ce61-104">In this tutorial, you learn how toointegrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ce61-105">Integrando Bonusly com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ce61-105">Integrating Bonusly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2ce61-106">Você pode controlar no AD do Azure que tenha acesso tooBonusly</span><span class="sxs-lookup"><span data-stu-id="2ce61-106">You can control in Azure AD who has access tooBonusly</span></span>
- <span data-ttu-id="2ce61-107">Você pode habilitar seu usuários tooautomatically get conectado tooBonusly (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2ce61-107">You can enable your users tooautomatically get signed-on tooBonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ce61-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2ce61-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2ce61-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ce61-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ce61-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2ce61-110">Prerequisites</span></span>

<span data-ttu-id="2ce61-111">tooconfigure integração do AD do Azure com Bonusly, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ce61-111">tooconfigure Azure AD integration with Bonusly, you need hello following items:</span></span>

- <span data-ttu-id="2ce61-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2ce61-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ce61-113">Uma assinatura do Bonusly habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="2ce61-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ce61-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2ce61-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ce61-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2ce61-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ce61-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2ce61-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ce61-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ce61-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ce61-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2ce61-118">Scenario description</span></span>
<span data-ttu-id="2ce61-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2ce61-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ce61-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="2ce61-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ce61-121">Adicionando Bonusly da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2ce61-121">Adding Bonusly from hello gallery</span></span>
2. <span data-ttu-id="2ce61-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2ce61-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-hello-gallery"></a><span data-ttu-id="2ce61-123">Adicionando Bonusly da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2ce61-123">Adding Bonusly from hello gallery</span></span>
<span data-ttu-id="2ce61-124">integração de saudação tooconfigure de Bonusly no AD do Azure, você precisa tooadd Bonusly da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2ce61-124">tooconfigure hello integration of Bonusly into Azure AD, you need tooadd Bonusly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2ce61-125">**tooadd Bonusly da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2ce61-125">**tooadd Bonusly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ce61-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="2ce61-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="2ce61-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2ce61-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="2ce61-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2ce61-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="2ce61-133">Na caixa de pesquisa hello, digite **Bonusly**, selecione **Bonusly** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2ce61-133">In hello search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Bonusly na lista de resultados de saudação](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2ce61-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ce61-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2ce61-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Bonusly, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="2ce61-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2ce61-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Bonusly é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ce61-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bonusly is tooa user in Azure AD.</span></span> <span data-ttu-id="2ce61-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Bonusly precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="2ce61-138">In other words, a link relationship between an Azure AD user and hello related user in Bonusly needs toobe established.</span></span>

<span data-ttu-id="2ce61-139">Bonusly, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ce61-139">In Bonusly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2ce61-140">tooconfigure e teste de logon único do AD do Azure com Bonusly, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ce61-140">tooconfigure and test Azure AD single sign-on with Bonusly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2ce61-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2ce61-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2ce61-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ce61-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ce61-143">**[Criar um usuário de teste Bonusly](#create-a-bonusly-test-user)**  -toohave um equivalente do Britta Simon em Bonusly é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="2ce61-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - toohave a counterpart of Britta Simon in Bonusly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ce61-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="2ce61-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ce61-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="2ce61-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2ce61-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ce61-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2ce61-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Bonusly.</span><span class="sxs-lookup"><span data-stu-id="2ce61-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="2ce61-148">**tooconfigure AD do Azure-logon único com Bonusly, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2ce61-148">**tooconfigure Azure AD single sign-on with Bonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ce61-149">Em Olá portal do Azure, Olá **Bonusly** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-149">In hello Azure portal, on hello **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2ce61-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="2ce61-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="2ce61-153">Em Olá **Bonusly de domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ce61-153">On hello **Bonusly Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="2ce61-155">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="2ce61-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2ce61-156">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="2ce61-156">hello value is not real.</span></span> <span data-ttu-id="2ce61-157">Valor de saudação de atualização com hello URL de resposta real.</span><span class="sxs-lookup"><span data-stu-id="2ce61-157">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="2ce61-158">Entre em contato com [a equipe de suporte Bonusly](https://Bonusly/contact) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ce61-158">Contact [Bonusly support team](https://Bonusly/contact) tooget hello value.</span></span>
 
4. <span data-ttu-id="2ce61-159">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** valor de certificado hello.</span><span class="sxs-lookup"><span data-stu-id="2ce61-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="2ce61-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2ce61-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2ce61-163">Em Olá **configuração Bonusly** seção, clique em **configurar Bonusly** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="2ce61-163">On hello **Bonusly Configuration** section, click **Configure Bonusly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2ce61-164">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="2ce61-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="2ce61-166">Em uma janela de navegador diferente, faça logon no tooyour **Bonusly** locatário.</span><span class="sxs-lookup"><span data-stu-id="2ce61-166">In a different browser window, log in tooyour **Bonusly** tenant.</span></span>

8. <span data-ttu-id="2ce61-167">Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações**e, em seguida, selecione **integrações e aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-167">In hello toolbar on hello top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="2ce61-168">![Seção Social Bonusly](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="2ce61-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="2ce61-169">Em **Logon Único**, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="2ce61-170">Em Olá **SAML** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ce61-170">On hello **SAML** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="2ce61-171">![Página de Diálogo Saml do Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="2ce61-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="2ce61-172">a.</span><span class="sxs-lookup"><span data-stu-id="2ce61-172">a.</span></span> <span data-ttu-id="2ce61-173">Em Olá **URL de destino IdP SSO** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ce61-173">In hello **IdP SSO target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="2ce61-174">b.</span><span class="sxs-lookup"><span data-stu-id="2ce61-174">b.</span></span> <span data-ttu-id="2ce61-175">Em hello **emissor IdP** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ce61-175">In hello **IdP Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="2ce61-176">c.</span><span class="sxs-lookup"><span data-stu-id="2ce61-176">c.</span></span> <span data-ttu-id="2ce61-177">Em Olá **URL de logon IdP** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ce61-177">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2ce61-178">d.</span><span class="sxs-lookup"><span data-stu-id="2ce61-178">d.</span></span> <span data-ttu-id="2ce61-179">Colar o **impressão digital** valor copiado do portal do Azure para Olá **impressão digital do certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2ce61-179">Paste the **Thumbprint** value copied from Azure portal into hello **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="2ce61-180">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2ce61-181">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="2ce61-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2ce61-182">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="2ce61-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2ce61-183">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ce61-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2ce61-184">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ce61-184">Create an Azure AD test user</span></span>
<span data-ttu-id="2ce61-185">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ce61-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="2ce61-187">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2ce61-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ce61-188">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="2ce61-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ce61-190">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ce61-192">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ce61-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ce61-194">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ce61-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ce61-196">a.</span><span class="sxs-lookup"><span data-stu-id="2ce61-196">a.</span></span> <span data-ttu-id="2ce61-197">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ce61-198">b.</span><span class="sxs-lookup"><span data-stu-id="2ce61-198">b.</span></span> <span data-ttu-id="2ce61-199">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2ce61-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ce61-200">c.</span><span class="sxs-lookup"><span data-stu-id="2ce61-200">c.</span></span> <span data-ttu-id="2ce61-201">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2ce61-202">d.</span><span class="sxs-lookup"><span data-stu-id="2ce61-202">d.</span></span> <span data-ttu-id="2ce61-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="2ce61-204">Criar um usuário de teste do Bonusly</span><span class="sxs-lookup"><span data-stu-id="2ce61-204">Create a Bonusly test user</span></span>

<span data-ttu-id="2ce61-205">Em ordem tooenable AD do Azure usuários toolog em tooBonusly, eles devem ser provisionados no Bonusly.</span><span class="sxs-lookup"><span data-stu-id="2ce61-205">In order tooenable Azure AD users toolog in tooBonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="2ce61-206">No caso de saudação de Bonusly, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="2ce61-206">In hello case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="2ce61-207">Você pode usar qualquer outra ferramenta de criação do usuário Bonusly conta ou APIs fornecidas pelo tooprovision Bonusly AAD contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="2ce61-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly tooprovision AAD user accounts.</span></span>
>  

<span data-ttu-id="2ce61-208">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2ce61-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ce61-209">Em uma janela de navegador da web, faça logon no locatário Bonusly tooyour.</span><span class="sxs-lookup"><span data-stu-id="2ce61-209">In a web browser window, log in tooyour Bonusly tenant.</span></span>

2. <span data-ttu-id="2ce61-210">Clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="2ce61-211">![Configurações](./media/active-directory-saas-bonus-tutorial/ic781041.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="2ce61-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="2ce61-212">Clique em Olá **usuários e bônus** guia.</span><span class="sxs-lookup"><span data-stu-id="2ce61-212">Click hello **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="2ce61-213">![Usuários e bônus](./media/active-directory-saas-bonus-tutorial/ic781042.png "Usuários e bônus")</span><span class="sxs-lookup"><span data-stu-id="2ce61-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="2ce61-214">Clique em **Gerenciar Usuários**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="2ce61-215">![Gerenciar Usuários](./media/active-directory-saas-bonus-tutorial/ic781043.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="2ce61-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="2ce61-216">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="2ce61-217">![Adicionar Usuário](./media/active-directory-saas-bonus-tutorial/ic781044.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="2ce61-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="2ce61-218">Em Olá **adicionar usuário** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ce61-218">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="2ce61-219">![Adicionar Usuário](./media/active-directory-saas-bonus-tutorial/ic781045.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="2ce61-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="2ce61-220">a.</span><span class="sxs-lookup"><span data-stu-id="2ce61-220">a.</span></span> <span data-ttu-id="2ce61-221">Em Olá **nome** caixa de texto, digite Olá primeiro nome do usuário, como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-221">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="2ce61-222">b.</span><span class="sxs-lookup"><span data-stu-id="2ce61-222">b.</span></span> <span data-ttu-id="2ce61-223">Em Olá **Sobrenome** caixa de texto, digite o sobrenome de saudação do usuário como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-223">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="2ce61-224">c.</span><span class="sxs-lookup"><span data-stu-id="2ce61-224">c.</span></span> <span data-ttu-id="2ce61-225">Em Olá **Email** caixa de texto, insira o email de saudação do usuário como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="2ce61-225">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="2ce61-226">d.</span><span class="sxs-lookup"><span data-stu-id="2ce61-226">d.</span></span> <span data-ttu-id="2ce61-227">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="2ce61-228">proprietário de conta do AD do Azure Olá recebe um email que inclui uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="2ce61-228">hello Azure AD account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span>
     >  

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2ce61-229">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2ce61-229">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2ce61-230">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBonusly.</span><span class="sxs-lookup"><span data-stu-id="2ce61-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBonusly.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="2ce61-232">**tooassign Britta Simon tooBonusly, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2ce61-232">**tooassign Britta Simon tooBonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ce61-233">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2ce61-235">Na lista de aplicativos hello, selecione **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-235">In hello applications list, select **Bonusly**.</span></span>

    ![Olá Bonusly link na lista de aplicativos Olá](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="2ce61-237">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202] 

4. <span data-ttu-id="2ce61-239">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2ce61-239">Click **Add** button.</span></span> <span data-ttu-id="2ce61-240">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2ce61-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="2ce61-242">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ce61-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2ce61-243">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2ce61-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ce61-244">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2ce61-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2ce61-245">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="2ce61-245">Test single sign-on</span></span>

<span data-ttu-id="2ce61-246">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="2ce61-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2ce61-247">Quando você clica em bloco Bonusly Olá em Olá painel de acesso, você deverá obter o aplicativo Bonusly tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="2ce61-247">When you click hello Bonusly tile in hello Access Panel, you should get automatically signed-on tooyour Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ce61-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2ce61-248">Additional resources</span></span>

* [<span data-ttu-id="2ce61-249">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2ce61-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ce61-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2ce61-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

