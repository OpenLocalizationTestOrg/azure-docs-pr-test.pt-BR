---
title: "Tutorial: integração do Azure Active Directory do ao Dropbox for Business | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="5682a-103">Tutorial: integração do Active Directory do Azure ao Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="5682a-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="5682a-104">Neste tutorial, você aprenderá como toointegrate Dropbox para empresas com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5682a-104">In this tutorial, you learn how toointegrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5682a-105">Integrando o Dropbox for Business com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="5682a-105">Integrating Dropbox for Business with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5682a-106">Você pode controlar no AD do Azure que tenha acesso tooDropbox para empresas</span><span class="sxs-lookup"><span data-stu-id="5682a-106">You can control in Azure AD who has access tooDropbox for Business</span></span>
- <span data-ttu-id="5682a-107">Você pode habilitar seu usuários tooautomatically get conectado tooDropbox para negócios (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5682a-107">You can enable your users tooautomatically get signed-on tooDropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5682a-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5682a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5682a-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5682a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5682a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5682a-110">Prerequisites</span></span>

<span data-ttu-id="5682a-111">tooconfigure integração do Azure AD com Dropbox for Business, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="5682a-111">tooconfigure Azure AD integration with Dropbox for Business, you need hello following items:</span></span>

- <span data-ttu-id="5682a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5682a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5682a-113">Uma assinatura habilitada para logon único do Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="5682a-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5682a-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5682a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5682a-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5682a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5682a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5682a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5682a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5682a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5682a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5682a-118">Scenario description</span></span>
<span data-ttu-id="5682a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5682a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5682a-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="5682a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5682a-121">Adicionando Dropbox for Business da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5682a-121">Adding Dropbox for Business from hello gallery</span></span>
2. <span data-ttu-id="5682a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5682a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-hello-gallery"></a><span data-ttu-id="5682a-123">Adicionando Dropbox for Business da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5682a-123">Adding Dropbox for Business from hello gallery</span></span>
<span data-ttu-id="5682a-124">integração de saudação do tooconfigure do Dropbox for Business no AD do Azure, você precisa tooadd Dropbox para empresas da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5682a-124">tooconfigure hello integration of Dropbox for Business into Azure AD, you need tooadd Dropbox for Business from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5682a-125">**tooadd Dropbox for Business da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5682a-125">**tooadd Dropbox for Business from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5682a-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5682a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5682a-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5682a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5682a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5682a-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5682a-131">Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5682a-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5682a-133">Na caixa de pesquisa hello, digite **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="5682a-133">In hello search box, type **Dropbox for Business**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="5682a-135">No painel de resultados de saudação, selecione **Dropbox for Business**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5682a-135">In hello results panel, select **Dropbox for Business**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5682a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5682a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5682a-138">Nesta seção, você configura e testa o logon único do Azure AD com o Dropbox for Business, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5682a-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5682a-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Dropbox for Business é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5682a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dropbox for Business is tooa user in Azure AD.</span></span> <span data-ttu-id="5682a-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Dropbox for Business precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5682a-140">In other words, a link relationship between an Azure AD user and hello related user in Dropbox for Business needs toobe established.</span></span>

<span data-ttu-id="5682a-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="5682a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="5682a-142">tooconfigure e teste de logon único do Azure AD com Dropbox para empresas, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="5682a-142">tooconfigure and test Azure AD single sign-on with Dropbox for Business, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5682a-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5682a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5682a-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5682a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5682a-145">**[Criar uma pasta de transferência para o usuário de teste de negócios](#creating-a-dropbox-for-business-test-user)**  -toohave um equivalente do Britta Simon no Dropbox para empresas que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5682a-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - toohave a counterpart of Britta Simon in Dropbox for Business that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5682a-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="5682a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5682a-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="5682a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5682a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5682a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5682a-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu Dropbox para o aplicativo de negócios.</span><span class="sxs-lookup"><span data-stu-id="5682a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="5682a-150">**tooconfigure AD do Azure-logon único com Dropbox for Business, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5682a-150">**tooconfigure Azure AD single sign-on with Dropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="5682a-151">Em Olá portal do Azure, Olá **Dropbox for Business** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="5682a-151">In hello Azure portal, on hello **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5682a-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="5682a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="5682a-155">Em Olá **Dropbox para o domínio de negócios e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5682a-155">On hello **Dropbox for Business Domain and URLs** section, perform hello following steps:</span></span>

    <span data-ttu-id="5682a-156">a.</span><span class="sxs-lookup"><span data-stu-id="5682a-156">a.</span></span> <span data-ttu-id="5682a-157">Faça logon no tooyour Dropbox para o locatário de negócios.</span><span class="sxs-lookup"><span data-stu-id="5682a-157">Sign on tooyour Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="5682a-158">![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="5682a-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="5682a-159">b.</span><span class="sxs-lookup"><span data-stu-id="5682a-159">b.</span></span> <span data-ttu-id="5682a-160">No painel de navegação Olá no lado esquerdo do hello, clique em **Console de administração**.</span><span class="sxs-lookup"><span data-stu-id="5682a-160">In hello navigation pane on hello left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="5682a-161">![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="5682a-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="5682a-162">c.</span><span class="sxs-lookup"><span data-stu-id="5682a-162">c.</span></span> <span data-ttu-id="5682a-163">Em Olá **Console de administração**, clique em **autenticação** no painel de navegação esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="5682a-163">On hello **Admin Console**, click **Authentication** in hello left navigation pane.</span></span> 
   
    <span data-ttu-id="5682a-164">![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="5682a-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="5682a-165">d.</span><span class="sxs-lookup"><span data-stu-id="5682a-165">d.</span></span> <span data-ttu-id="5682a-166">Em Olá **o logon único** seção, selecione **habilitar logon único**e, em seguida, clique em **mais** tooexpand nesta seção.</span><span class="sxs-lookup"><span data-stu-id="5682a-166">In hello **Single sign-on** section, select **Enable single sign-on**, and then click **More** tooexpand this section.</span></span>  
   
    <span data-ttu-id="5682a-167">![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="5682a-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="5682a-168">e.</span><span class="sxs-lookup"><span data-stu-id="5682a-168">e.</span></span> <span data-ttu-id="5682a-169">Copiar URL da saudação Avançar muito**os usuários podem entrar digitando seu endereço de email ou podem ir diretamente para**.</span><span class="sxs-lookup"><span data-stu-id="5682a-169">Copy hello URL next too**Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Configurar o logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="5682a-171">f.</span><span class="sxs-lookup"><span data-stu-id="5682a-171">f.</span></span> <span data-ttu-id="5682a-172">Em Olá portal do Azure, na Olá **URL de logon** caixa de texto, colar Olá URL.</span><span class="sxs-lookup"><span data-stu-id="5682a-172">On hello Azure portal, in hello **Sign-on URL** textbox, paste hello URL.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="5682a-174">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="5682a-174">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5682a-175">Esse valor não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="5682a-175">This value is not real value.</span></span> <span data-ttu-id="5682a-176">Atualize o valor de saudação com hello real URL de logon você obter de sua seção de logon único.</span><span class="sxs-lookup"><span data-stu-id="5682a-176">Update hello value with hello actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="5682a-177">Entre em contato com [Dropbox para a equipe de suporte do cliente de negócios](https://www.dropbox.com/business/contact) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="5682a-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="5682a-178">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5682a-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="5682a-180">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5682a-180">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5682a-182">Em Olá **Dropbox for Business configuração** seção, clique em **configurar Dropbox for Business** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="5682a-182">On hello **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5682a-183">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="5682a-183">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="5682a-185">tooconfigure logon único no **Dropbox for Business** lado, vá em seu locatário Dropbox for Business, em Olá **o logon único** seção Olá **autenticação** página, Execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5682a-185">tooconfigure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in hello **Single sign-on** section of hello **Authentication** page, perform hello following steps:</span></span> 
   
    <span data-ttu-id="5682a-186">![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="5682a-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="5682a-187">a.</span><span class="sxs-lookup"><span data-stu-id="5682a-187">a.</span></span> <span data-ttu-id="5682a-188">Clique em **Obrigatório**.</span><span class="sxs-lookup"><span data-stu-id="5682a-188">Click **Required**.</span></span>
   
    <span data-ttu-id="5682a-189">b.</span><span class="sxs-lookup"><span data-stu-id="5682a-189">b.</span></span> <span data-ttu-id="5682a-190">Em Olá portal do Azure, Olá **configurar o logon** janela, Olá cópia **Single Sign-On URL do serviço SAML** valor e, em seguida, cole-o em Olá **URL de entrada** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="5682a-190">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="5682a-191">c.</span><span class="sxs-lookup"><span data-stu-id="5682a-191">c.</span></span> <span data-ttu-id="5682a-192">Clique em **escolher certificado**e, em seguida, procure tooyour **arquivo de certificado codificado em Base64**.</span><span class="sxs-lookup"><span data-stu-id="5682a-192">Click **Choose certificate**, and then browse tooyour **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="5682a-193">d.</span><span class="sxs-lookup"><span data-stu-id="5682a-193">d.</span></span> <span data-ttu-id="5682a-194">Clique em **salvar alterações** toocomplete configuração de saudação em seu locatário DropBox for Business.</span><span class="sxs-lookup"><span data-stu-id="5682a-194">Click **Save changes** toocomplete hello configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="5682a-195">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="5682a-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5682a-196">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5682a-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5682a-197">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5682a-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5682a-198">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5682a-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="5682a-199">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5682a-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5682a-201">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5682a-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5682a-202">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5682a-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="5682a-204">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="5682a-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5682a-206">Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5682a-206">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5682a-208">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5682a-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5682a-210">a.</span><span class="sxs-lookup"><span data-stu-id="5682a-210">a.</span></span> <span data-ttu-id="5682a-211">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5682a-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5682a-212">b.</span><span class="sxs-lookup"><span data-stu-id="5682a-212">b.</span></span> <span data-ttu-id="5682a-213">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5682a-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5682a-214">c.</span><span class="sxs-lookup"><span data-stu-id="5682a-214">c.</span></span> <span data-ttu-id="5682a-215">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="5682a-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5682a-216">d.</span><span class="sxs-lookup"><span data-stu-id="5682a-216">d.</span></span> <span data-ttu-id="5682a-217">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5682a-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="5682a-218">Criando um usuário de teste do Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="5682a-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="5682a-219">Nesta seção, um usuário chamado Brenda Fernandes é criado no Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="5682a-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="5682a-220">O Dropbox for Business dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="5682a-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="5682a-221">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="5682a-221">There is no action item for you in this section.</span></span> <span data-ttu-id="5682a-222">Se um usuário não existir no Dropbox for Business, um novo é criado quando você tenta tooaccess Dropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="5682a-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt tooaccess Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="5682a-223">Se você precisar toocreate um usuário manualmente, entre em contato com [Dropbox para a equipe de suporte do cliente de negócios](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="5682a-223">If you need toocreate a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5682a-224">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5682a-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5682a-225">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooDropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="5682a-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDropbox for Business.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5682a-227">**tooassign Britta Simon tooDropbox para empresas, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5682a-227">**tooassign Britta Simon tooDropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="5682a-228">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5682a-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5682a-230">Na lista de aplicativos hello, selecione **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="5682a-230">In hello applications list, select **Dropbox for Business**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="5682a-232">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5682a-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5682a-234">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5682a-234">Click **Add** button.</span></span> <span data-ttu-id="5682a-235">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5682a-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5682a-237">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="5682a-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5682a-238">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5682a-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5682a-239">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5682a-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5682a-240">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5682a-240">Testing single sign-on</span></span>

<span data-ttu-id="5682a-241">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5682a-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5682a-242">Quando você clica em hello Dropbox para o bloco de negócios no hello painel de acesso, você deve obter a página de logon do seu Dropbox para aplicativo de negócios.</span><span class="sxs-lookup"><span data-stu-id="5682a-242">When you click hello Dropbox for Business tile in hello Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5682a-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5682a-243">Additional resources</span></span>

* [<span data-ttu-id="5682a-244">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5682a-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5682a-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5682a-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="5682a-246">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="5682a-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

