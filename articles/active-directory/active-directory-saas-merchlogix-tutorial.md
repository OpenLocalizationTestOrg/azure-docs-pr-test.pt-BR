---
title: "Tutorial: Integração do Azure Active Directory com o Merchlogix | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Merchlogix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a1f49bb8-6b17-433d-8f25-9d26fb390e77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: jeedes
ms.openlocfilehash: bf8d244d9705c06651a65777d6f085b790a5207d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-merchlogix"></a><span data-ttu-id="c5bb3-103">Tutorial: Integração do Azure Active Directory com o Merchlogix</span><span class="sxs-lookup"><span data-stu-id="c5bb3-103">Tutorial: Azure Active Directory integration with Merchlogix</span></span>

<span data-ttu-id="c5bb3-104">Neste tutorial, você aprenderá como toointegrate Merchlogix com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c5bb3-104">In this tutorial, you learn how toointegrate Merchlogix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5bb3-105">Integrando Merchlogix com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5bb3-105">Integrating Merchlogix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5bb3-106">Você pode controlar no AD do Azure que tenha acesso tooMerchlogix.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-106">You can control in Azure AD who has access tooMerchlogix.</span></span>
- <span data-ttu-id="c5bb3-107">Você pode habilitar seu usuários tooautomatically get conectado tooMerchlogix (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-107">You can enable your users tooautomatically get signed-on tooMerchlogix (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c5bb3-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c5bb3-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5bb3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5bb3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c5bb3-110">Prerequisites</span></span>

<span data-ttu-id="c5bb3-111">tooconfigure integração do AD do Azure com Merchlogix, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5bb3-111">tooconfigure Azure AD integration with Merchlogix, you need hello following items:</span></span>

- <span data-ttu-id="c5bb3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5bb3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5bb3-113">Assinatura habilitada para logon único do Merchlogix</span><span class="sxs-lookup"><span data-stu-id="c5bb3-113">A Merchlogix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5bb3-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5bb3-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c5bb3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5bb3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5bb3-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5bb3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5bb3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c5bb3-118">Scenario description</span></span>
<span data-ttu-id="c5bb3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5bb3-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c5bb3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5bb3-121">Adicionando Merchlogix da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c5bb3-121">Adding Merchlogix from hello gallery</span></span>
2. <span data-ttu-id="c5bb3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5bb3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-merchlogix-from-hello-gallery"></a><span data-ttu-id="c5bb3-123">Adicionando Merchlogix da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c5bb3-123">Adding Merchlogix from hello gallery</span></span>
<span data-ttu-id="c5bb3-124">integração de saudação tooconfigure de Merchlogix no AD do Azure, você precisa tooadd Merchlogix da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-124">tooconfigure hello integration of Merchlogix into Azure AD, you need tooadd Merchlogix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5bb3-125">**tooadd Merchlogix da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c5bb3-125">**tooadd Merchlogix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5bb3-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="c5bb3-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5bb3-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="c5bb3-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="c5bb3-133">Na caixa de pesquisa hello, digite **Merchlogix**, selecione **Merchlogix** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-133">In hello search box, type **Merchlogix**, select **Merchlogix** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merchlogix na lista de resultados de saudação](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c5bb3-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5bb3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c5bb3-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Merchlogix, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-136">In this section, you configure and test Azure AD single sign-on with Merchlogix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5bb3-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Merchlogix é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Merchlogix is tooa user in Azure AD.</span></span> <span data-ttu-id="c5bb3-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Merchlogix precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-138">In other words, a link relationship between an Azure AD user and hello related user in Merchlogix needs toobe established.</span></span>

<span data-ttu-id="c5bb3-139">Merchlogix, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-139">In Merchlogix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c5bb3-140">tooconfigure e teste de logon único do AD do Azure com Merchlogix, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5bb3-140">tooconfigure and test Azure AD single sign-on with Merchlogix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5bb3-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5bb3-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5bb3-143">**[Criar um usuário de teste Merchlogix](#create-a-merchlogix-test-user)**  -toohave um equivalente do Britta Simon em Merchlogix é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-143">**[Create a Merchlogix test user](#create-a-merchlogix-test-user)** - toohave a counterpart of Britta Simon in Merchlogix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5bb3-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5bb3-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c5bb3-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5bb3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c5bb3-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Merchlogix application.</span></span>

<span data-ttu-id="c5bb3-148">**tooconfigure AD do Azure-logon único com Merchlogix, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c5bb3-148">**tooconfigure Azure AD single sign-on with Merchlogix, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5bb3-149">Em Olá portal do Azure, Olá **Merchlogix** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-149">In hello Azure portal, on hello **Merchlogix** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="c5bb3-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_samlbase.png)

3. <span data-ttu-id="c5bb3-153">Em Olá **Merchlogix domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5bb3-153">On hello **Merchlogix Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Merchlogix](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_url.png)

    <span data-ttu-id="c5bb3-155">a.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-155">a.</span></span> <span data-ttu-id="c5bb3-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<DOMAIN>/login.php?saml=true`</span><span class="sxs-lookup"><span data-stu-id="c5bb3-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<DOMAIN>/login.php?saml=true`</span></span>

    <span data-ttu-id="c5bb3-157">b.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-157">b.</span></span> <span data-ttu-id="c5bb3-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<DOMAIN>/simplesaml/module.php/saml/sp/metadata.php/<SAML_NAME>`</span><span class="sxs-lookup"><span data-stu-id="c5bb3-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<DOMAIN>/simplesaml/module.php/saml/sp/metadata.php/<SAML_NAME>`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c5bb3-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-159">These values are not real.</span></span> <span data-ttu-id="c5bb3-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c5bb3-161">Entre em contato com [Merchlogix a equipe de suporte](http://www.merchlogix.com/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-161">Contact [Merchlogix support team](http://www.merchlogix.com/contact/) tooget these values.</span></span>

4. <span data-ttu-id="c5bb3-162">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_certificate.png) 

5. <span data-ttu-id="c5bb3-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c5bb3-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-merchlogix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5bb3-166">Em Olá **Merchlogix configuração** seção, clique em **configurar Merchlogix** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-166">On hello **Merchlogix Configuration** section, click **Configure Merchlogix** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c5bb3-167">Saudação de cópia **URL de logout, ID de entidade de SAML,** e **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c5bb3-167">Copy hello **Sign-Out URL, SAML Entity ID,** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Merchlogix](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_configure.png) 

7. <span data-ttu-id="c5bb3-169">tooconfigure logon único no **Merchlogix** lado, você precisa toosend Olá baixado **certificado (Base64)**, **URL de logout, ID de entidade de SAML e SAML Single Sign-On URL do serviço** muito[a equipe de suporte Merchlogix](http://www.merchlogix.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="c5bb3-169">tooconfigure single sign-on on **Merchlogix** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Merchlogix support team](http://www.merchlogix.com/contact/).</span></span> <span data-ttu-id="c5bb3-170">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c5bb3-171">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c5bb3-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5bb3-172">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5bb3-173">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5bb3-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c5bb3-174">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5bb3-174">Create an Azure AD test user</span></span>

<span data-ttu-id="c5bb3-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="c5bb3-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c5bb3-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5bb3-178">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c5bb3-180">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c5bb3-182">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c5bb3-184">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5bb3-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c5bb3-186">a.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-186">a.</span></span> <span data-ttu-id="c5bb3-187">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5bb3-188">b.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-188">b.</span></span> <span data-ttu-id="c5bb3-189">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c5bb3-190">c.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-190">c.</span></span> <span data-ttu-id="c5bb3-191">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c5bb3-192">d.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-192">d.</span></span> <span data-ttu-id="c5bb3-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-193">Click **Create**.</span></span>
 
### <a name="create-a-merchlogix-test-user"></a><span data-ttu-id="c5bb3-194">Criar um usuário de teste do Merchlogix</span><span class="sxs-lookup"><span data-stu-id="c5bb3-194">Create a Merchlogix test user</span></span>

<span data-ttu-id="c5bb3-195">Nesta seção, você criará um usuário chamado Brenda Fernandes no Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-195">In this section, you create a user called Britta Simon in Merchlogix.</span></span> <span data-ttu-id="c5bb3-196">Trabalhar com [Merchlogix a equipe de suporte](http://www.merchlogix.com/contact/) tooadd usuários de saudação na plataforma de Merchlogix hello.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-196">Work with [Merchlogix support team](http://www.merchlogix.com/contact/) tooadd hello users in hello Merchlogix platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c5bb3-197">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5bb3-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c5bb3-198">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMerchlogix.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMerchlogix.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="c5bb3-200">**tooassign Britta Simon tooMerchlogix, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c5bb3-200">**tooassign Britta Simon tooMerchlogix, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5bb3-201">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c5bb3-203">Na lista de aplicativos hello, selecione **Merchlogix**.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-203">In hello applications list, select **Merchlogix**.</span></span>

    ![link de Merchlogix Olá na lista de aplicativos Olá](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_app.png)  

3. <span data-ttu-id="c5bb3-205">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="c5bb3-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-207">Click **Add** button.</span></span> <span data-ttu-id="c5bb3-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="c5bb3-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5bb3-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5bb3-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c5bb3-213">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="c5bb3-213">Test single sign-on</span></span>

<span data-ttu-id="c5bb3-214">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5bb3-215">Quando você clica em bloco Merchlogix Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Merchlogix aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c5bb3-215">When you click hello Merchlogix tile in hello Access Panel, you should get automatically signed-on tooyour Merchlogix application.</span></span>
<span data-ttu-id="c5bb3-216">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5bb3-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c5bb3-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c5bb3-217">Additional resources</span></span>

* [<span data-ttu-id="c5bb3-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c5bb3-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5bb3-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5bb3-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_203.png

