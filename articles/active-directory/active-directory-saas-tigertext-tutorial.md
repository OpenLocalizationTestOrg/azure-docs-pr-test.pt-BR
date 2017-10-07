---
title: "Tutorial: Integração do Azure Active Directory ao TigerText Secure Messenger | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e TigerText proteger Messenger."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: a3d7bb9598658c75c567c15751740d885fe4fc27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="66f9d-103">Tutorial: Integração do Azure Active Directory ao TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="66f9d-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="66f9d-104">Neste tutorial, você aprenderá como toointegrate TigerText seguro Messenger com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="66f9d-104">In this tutorial, you learn how toointegrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66f9d-105">Integrando TigerText proteger Messenger com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="66f9d-105">Integrating TigerText Secure Messenger with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="66f9d-106">Você pode controlar no AD do Azure que tenha acesso tooTigerText Messenger segura</span><span class="sxs-lookup"><span data-stu-id="66f9d-106">You can control in Azure AD who has access tooTigerText Secure Messenger</span></span>
- <span data-ttu-id="66f9d-107">Você pode habilitar seu usuários tooautomatically get conectado tooTigerText Messenger seguro (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66f9d-107">You can enable your users tooautomatically get signed-on tooTigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66f9d-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="66f9d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="66f9d-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66f9d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66f9d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="66f9d-110">Prerequisites</span></span>

<span data-ttu-id="66f9d-111">tooconfigure integração do AD do Azure com TigerText proteger Messenger, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="66f9d-111">tooconfigure Azure AD integration with TigerText Secure Messenger, you need hello following items:</span></span>

- <span data-ttu-id="66f9d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66f9d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66f9d-113">Uma assinatura do TigerText Secure Messenger habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="66f9d-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66f9d-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="66f9d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66f9d-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="66f9d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66f9d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="66f9d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66f9d-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66f9d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66f9d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="66f9d-118">Scenario description</span></span>
<span data-ttu-id="66f9d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="66f9d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66f9d-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="66f9d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66f9d-121">Adicionar TigerText proteger Messenger da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="66f9d-121">Add TigerText Secure Messenger from hello gallery</span></span>
2. <span data-ttu-id="66f9d-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="66f9d-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-hello-gallery"></a><span data-ttu-id="66f9d-123">Adicionar TigerText proteger Messenger da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="66f9d-123">Add TigerText Secure Messenger from hello gallery</span></span>
<span data-ttu-id="66f9d-124">integração de saudação tooconfigure do TigerText proteger Messenger no AD do Azure, você precisa tooadd TigerText proteger Messenger da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="66f9d-124">tooconfigure hello integration of TigerText Secure Messenger into Azure AD, you need tooadd TigerText Secure Messenger from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="66f9d-125">**tooadd TigerText proteger Messenger da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="66f9d-125">**tooadd TigerText Secure Messenger from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="66f9d-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="66f9d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66f9d-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="66f9d-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="66f9d-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66f9d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="66f9d-133">Na caixa de pesquisa hello, digite **TigerText proteger Messenger**, selecione **TigerText proteger Messenger** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="66f9d-133">In hello search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Adicionar da galeria](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="66f9d-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="66f9d-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="66f9d-136">Nesta seção, você vai configurar e testar o logon único do Azure AD com o TigerText Secure Messenger, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="66f9d-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="66f9d-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no TigerText proteger Messenger é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="66f9d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TigerText Secure Messenger is tooa user in Azure AD.</span></span> <span data-ttu-id="66f9d-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em TigerText proteger Messenger deve toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="66f9d-138">In other words, a link relationship between an Azure AD user and hello related user in TigerText Secure Messenger needs toobe established.</span></span>

<span data-ttu-id="66f9d-139">TigerText proteger Messenger, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="66f9d-139">In TigerText Secure Messenger, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="66f9d-140">tooconfigure e teste de logon único do AD do Azure com TigerText proteger Messenger, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="66f9d-140">tooconfigure and test Azure AD single sign-on with TigerText Secure Messenger, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="66f9d-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="66f9d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="66f9d-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66f9d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66f9d-143">**[Criar um usuário de teste TigerText proteger Messenger](#create-a-tigertext-secure-messenger-test-user)**  -toohave um equivalente do Britta Simon no Messenger TigerText segura que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="66f9d-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - toohave a counterpart of Britta Simon in TigerText Secure Messenger that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="66f9d-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="66f9d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66f9d-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="66f9d-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="66f9d-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="66f9d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="66f9d-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo TigerText proteger Messenger.</span><span class="sxs-lookup"><span data-stu-id="66f9d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="66f9d-148">**tooconfigure logon único do AD do Azure com TigerText proteger Messenger, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="66f9d-148">**tooconfigure Azure AD single sign-on with TigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="66f9d-149">Em Olá portal do Azure, Olá **TigerText proteger Messenger** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-149">In hello Azure portal, on hello **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="66f9d-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="66f9d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Logon único baseado em SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="66f9d-153">Em Olá **TigerText proteger Messenger domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="66f9d-153">On hello **TigerText Secure Messenger Domain and URLs** section, perform hello following steps:</span></span>

    ![Seção Domínio e URLs do TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="66f9d-155">a.</span><span class="sxs-lookup"><span data-stu-id="66f9d-155">a.</span></span> <span data-ttu-id="66f9d-156">Em Olá **URL de logon** caixa de texto, digite a URL como:`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="66f9d-156">In hello **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="66f9d-157">b.</span><span class="sxs-lookup"><span data-stu-id="66f9d-157">b.</span></span> <span data-ttu-id="66f9d-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="66f9d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="66f9d-159">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="66f9d-159">This value is not real.</span></span> <span data-ttu-id="66f9d-160">Atualize esse valor com hello identificador real.</span><span class="sxs-lookup"><span data-stu-id="66f9d-160">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="66f9d-161">Entre em contato com [equipe de suporte do cliente de mensagens segura TigerText](mailTo:prosupport@tigertext.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="66f9d-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="66f9d-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="66f9d-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="66f9d-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="66f9d-164">Click **Save** button.</span></span>

    ![Botão Salvar](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66f9d-166">tooget logon único configurado para o seu aplicativo, entre em contato com [a equipe de suporte TigerText proteger Messenger](mailTo:prosupport@tigertext.com) e fornecê-los Olá **metadados baixado**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-166">tooget single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them hello **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="66f9d-167">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="66f9d-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="66f9d-168">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="66f9d-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="66f9d-169">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66f9d-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="66f9d-170">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="66f9d-170">Create an Azure AD test user</span></span>
<span data-ttu-id="66f9d-171">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="66f9d-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="66f9d-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="66f9d-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="66f9d-174">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="66f9d-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66f9d-176">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Usuários e grupos->Todos os usuários](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66f9d-178">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="66f9d-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Botão Adicionar](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66f9d-180">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="66f9d-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Diálogo do usuário](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66f9d-182">a.</span><span class="sxs-lookup"><span data-stu-id="66f9d-182">a.</span></span> <span data-ttu-id="66f9d-183">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66f9d-184">b.</span><span class="sxs-lookup"><span data-stu-id="66f9d-184">b.</span></span> <span data-ttu-id="66f9d-185">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="66f9d-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66f9d-186">c.</span><span class="sxs-lookup"><span data-stu-id="66f9d-186">c.</span></span> <span data-ttu-id="66f9d-187">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="66f9d-188">d.</span><span class="sxs-lookup"><span data-stu-id="66f9d-188">d.</span></span> <span data-ttu-id="66f9d-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="66f9d-190">Criar um usuário de teste do TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="66f9d-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="66f9d-191">Nesta seção, você criará um usuário chamado Brenda Fernandes no TigerText.</span><span class="sxs-lookup"><span data-stu-id="66f9d-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="66f9d-192">Entre em contato muito[equipe de suporte do cliente de mensagens segura TigerText](mailTo:prosupport@tigertext.com) tooadd usuários de saudação na plataforma de TigerText hello.</span><span class="sxs-lookup"><span data-stu-id="66f9d-192">Please reach out too[TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooadd hello users in hello TigerText platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="66f9d-193">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66f9d-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="66f9d-194">Nesta seção, você deve habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTigerText Messenger seguro.</span><span class="sxs-lookup"><span data-stu-id="66f9d-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTigerText Secure Messenger.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="66f9d-196">**tooassign Britta Simon tooTigerText Messenger segura, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="66f9d-196">**tooassign Britta Simon tooTigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="66f9d-197">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="66f9d-199">Na lista de aplicativos hello, selecione **TigerText proteger Messenger**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-199">In hello applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger na lista de aplicativos](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="66f9d-201">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="66f9d-203">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="66f9d-203">Click **Add** button.</span></span> <span data-ttu-id="66f9d-204">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66f9d-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="66f9d-206">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="66f9d-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="66f9d-207">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66f9d-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66f9d-208">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66f9d-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="66f9d-209">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="66f9d-209">Test single sign-on</span></span>

<span data-ttu-id="66f9d-210">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="66f9d-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="66f9d-211">Quando você clica em bloco TigerText Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour TigerText aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66f9d-211">When you click hello TigerText tile in hello Access Panel, you should get automatically signed-on tooyour TigerText application.</span></span> <span data-ttu-id="66f9d-212">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="66f9d-212">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66f9d-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="66f9d-213">Additional resources</span></span>

* [<span data-ttu-id="66f9d-214">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="66f9d-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66f9d-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="66f9d-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

