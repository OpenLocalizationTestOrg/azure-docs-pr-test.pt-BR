---
title: "Tutorial: Integração do Azure Active Directory com o Asset Bank | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e banco de ativo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3006ad6e-8831-41cd-94aa-7e7ae770ce7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 32cb355fbe16557eca69dbad1d3e6fbe19b53517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asset-bank"></a><span data-ttu-id="b9ffe-103">Tutorial: Integração do Azure Active Directory ao Asset Bank</span><span class="sxs-lookup"><span data-stu-id="b9ffe-103">Tutorial: Azure Active Directory integration with Asset Bank</span></span>

<span data-ttu-id="b9ffe-104">Neste tutorial, você aprenderá como toointegrate ativo banco com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="b9ffe-104">In this tutorial, you learn how toointegrate Asset Bank with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9ffe-105">Integração do banco de ativos com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-105">Integrating Asset Bank with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9ffe-106">Você pode controlar no AD do Azure que tenha acesso tooAsset Bank</span><span class="sxs-lookup"><span data-stu-id="b9ffe-106">You can control in Azure AD who has access tooAsset Bank</span></span>
- <span data-ttu-id="b9ffe-107">Você pode habilitar seu usuários tooautomatically get conectado tooAsset Bank (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9ffe-107">You can enable your users tooautomatically get signed-on tooAsset Bank (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9ffe-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b9ffe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b9ffe-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9ffe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9ffe-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b9ffe-110">Prerequisites</span></span>

<span data-ttu-id="b9ffe-111">tooconfigure integração do Azure AD com o banco de ativo, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-111">tooconfigure Azure AD integration with Asset Bank, you need hello following items:</span></span>

- <span data-ttu-id="b9ffe-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9ffe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9ffe-113">Uma assinatura habilitada para logon único do Asset Bank</span><span class="sxs-lookup"><span data-stu-id="b9ffe-113">An Asset Bank single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9ffe-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9ffe-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9ffe-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9ffe-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9ffe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9ffe-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b9ffe-118">Scenario description</span></span>
<span data-ttu-id="b9ffe-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9ffe-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9ffe-121">Adicionando ativo banco da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b9ffe-121">Adding Asset Bank from hello gallery</span></span>
2. <span data-ttu-id="b9ffe-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9ffe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asset-bank-from-hello-gallery"></a><span data-ttu-id="b9ffe-123">Adicionando ativo banco da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b9ffe-123">Adding Asset Bank from hello gallery</span></span>
<span data-ttu-id="b9ffe-124">integração de saudação tooconfigure banco ativo no AD do Azure, você precisa tooadd Bank ativos na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-124">tooconfigure hello integration of Asset Bank into Azure AD, you need tooadd Asset Bank from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9ffe-125">**tooadd banco ativo da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b9ffe-125">**tooadd Asset Bank from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ffe-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9ffe-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9ffe-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="b9ffe-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="b9ffe-133">Na caixa de pesquisa hello, digite **Bank ativo**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-133">In hello search box, type **Asset Bank**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_search.png)

5. <span data-ttu-id="b9ffe-135">No painel de resultados de saudação, selecione **Bank ativo**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-135">In hello results panel, select **Asset Bank**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9ffe-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9ffe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9ffe-138">Nesta seção, você configura e testa o logon único do Azure AD com o Asset Bank, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-138">In this section, you configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b9ffe-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no banco de ativos é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asset Bank is tooa user in Azure AD.</span></span> <span data-ttu-id="b9ffe-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação ativo banco precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-140">In other words, a link relationship between an Azure AD user and hello related user in Asset Bank needs toobe established.</span></span>

<span data-ttu-id="b9ffe-141">No banco de ativo, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-141">In Asset Bank, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b9ffe-142">tooconfigure e teste logon único do AD do Azure com o banco de ativo, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-142">tooconfigure and test Azure AD single sign-on with Asset Bank, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9ffe-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9ffe-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9ffe-145">**[Criar um usuário de teste ativo banco](#creating-an-asset-bank-test-user)**  -toohave um equivalente do Britta Simon no banco de ativo que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-145">**[Creating an Asset Bank test user](#creating-an-asset-bank-test-user)** - toohave a counterpart of Britta Simon in Asset Bank that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9ffe-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9ffe-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9ffe-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ffe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9ffe-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de banco de ativo.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asset Bank application.</span></span>

<span data-ttu-id="b9ffe-150">**tooconfigure AD do Azure-logon único com banco de ativo, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b9ffe-150">**tooconfigure Azure AD single sign-on with Asset Bank, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ffe-151">Em Olá portal do Azure, Olá **Bank ativo** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-151">In hello Azure portal, on hello **Asset Bank** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="b9ffe-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_samlbase.png)

3. <span data-ttu-id="b9ffe-155">Em Olá **ativo banco domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-155">On hello **Asset Bank Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_url.png)

    <span data-ttu-id="b9ffe-157">a.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-157">a.</span></span> <span data-ttu-id="b9ffe-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.assetbank-server.com`</span><span class="sxs-lookup"><span data-stu-id="b9ffe-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.assetbank-server.com`</span></span>

    <span data-ttu-id="b9ffe-159">b.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-159">b.</span></span> <span data-ttu-id="b9ffe-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.assetbank-server.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="b9ffe-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.assetbank-server.com/shibboleth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9ffe-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-161">These values are not real.</span></span> <span data-ttu-id="b9ffe-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b9ffe-163">Entre em contato com [equipe de suporte do cliente do banco de ativo](mailto:support@assetbank.co.uk) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-163">Contact [Asset Bank Client support team](mailto:support@assetbank.co.uk) tooget these values.</span></span> 
 
4. <span data-ttu-id="b9ffe-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_certificate.png) 

5. <span data-ttu-id="b9ffe-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b9ffe-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-assetbank-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9ffe-168">tooconfigure logon único no **Bank ativo** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte ativo banco](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="b9ffe-168">tooconfigure single sign-on on **Asset Bank** side, you need toosend hello downloaded **Metadata XML** too[Asset Bank support team](mailto:support@assetbank.co.uk).</span></span> 


> [!TIP]
> <span data-ttu-id="b9ffe-169">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="b9ffe-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b9ffe-170">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b9ffe-171">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9ffe-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9ffe-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9ffe-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9ffe-173">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="b9ffe-175">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b9ffe-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ffe-176">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9ffe-178">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9ffe-180">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9ffe-182">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9ffe-184">a.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-184">a.</span></span> <span data-ttu-id="b9ffe-185">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9ffe-186">b.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-186">b.</span></span> <span data-ttu-id="b9ffe-187">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9ffe-188">c.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-188">c.</span></span> <span data-ttu-id="b9ffe-189">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b9ffe-190">d.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-190">d.</span></span> <span data-ttu-id="b9ffe-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-191">Click **Create**.</span></span>
 
### <a name="creating-an-asset-bank-test-user"></a><span data-ttu-id="b9ffe-192">Criando um usuário de teste do Asset Bank</span><span class="sxs-lookup"><span data-stu-id="b9ffe-192">Creating an Asset Bank test user</span></span>

<span data-ttu-id="b9ffe-193">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no banco de ativo.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-193">hello objective of this section is toocreate a user called Britta Simon in Asset Bank.</span></span> <span data-ttu-id="b9ffe-194">O Asset Bank dá suporte ao provisionamento just-in-time, que é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-194">Asset Bank supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="b9ffe-195">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-195">There is no action item for you in this section.</span></span> <span data-ttu-id="b9ffe-196">Um novo usuário é criado durante tooaccess uma tentativa de banco de ativo se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-196">A new user is created during an attempt tooaccess Asset Bank if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="b9ffe-197">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [a equipe de suporte ativo banco](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="b9ffe-197">If you need toocreate a user manually, you need toocontact hello [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b9ffe-198">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9ffe-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b9ffe-199">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAsset Bank.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsset Bank.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="b9ffe-201">**tooassign Britta Simon tooAsset Bank, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b9ffe-201">**tooassign Britta Simon tooAsset Bank, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ffe-202">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b9ffe-204">Na lista de aplicativos hello, selecione **Bank ativo**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-204">In hello applications list, select **Asset Bank**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_app.png) 

3. <span data-ttu-id="b9ffe-206">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="b9ffe-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-208">Click **Add** button.</span></span> <span data-ttu-id="b9ffe-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="b9ffe-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b9ffe-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9ffe-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9ffe-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="b9ffe-214">Testing single sign-on</span></span>

<span data-ttu-id="b9ffe-215">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b9ffe-216">Quando você clica em bloco ativo banco Olá Olá painel de acesso, você deve obter o aplicativo de banco de ativos de automaticamente assinado em tooyour.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-216">When you click hello Asset Bank tile in hello Access Panel, you should get automatically signed-on tooyour Asset Bank application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b9ffe-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b9ffe-217">Additional resources</span></span>

* [<span data-ttu-id="b9ffe-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b9ffe-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9ffe-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9ffe-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_203.png

