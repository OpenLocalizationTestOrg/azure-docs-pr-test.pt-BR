---
title: "Tutorial: integração do Azure Active Directory com o Ceridian Dayforce HCM | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Ceridian Dayforce HCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="27e07-103">Tutorial: integração do Azure Active Directory ao Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="27e07-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="27e07-104">Neste tutorial, você aprenderá como toointegrate Ceridian Dayforce HCM com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="27e07-104">In this tutorial, you learn how toointegrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27e07-105">Integrando Ceridian Dayforce HCM AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="27e07-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="27e07-106">Você pode controlar no AD do Azure que tenha acesso tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="27e07-106">You can control in Azure AD who has access tooCeridian Dayforce HCM.</span></span>
- <span data-ttu-id="27e07-107">Você pode habilitar seu usuários tooautomatically get conectado tooCeridian Dayforce HCM (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="27e07-107">You can enable your users tooautomatically get signed-on tooCeridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="27e07-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="27e07-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="27e07-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="27e07-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27e07-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="27e07-110">Prerequisites</span></span>

<span data-ttu-id="27e07-111">tooconfigure integração do AD do Azure com Ceridian Dayforce HCM, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="27e07-111">tooconfigure Azure AD integration with Ceridian Dayforce HCM, you need hello following items:</span></span>

- <span data-ttu-id="27e07-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27e07-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27e07-113">Uma assinatura Ceridian Dayforce HCM com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="27e07-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27e07-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="27e07-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27e07-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="27e07-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27e07-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="27e07-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27e07-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27e07-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27e07-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="27e07-118">Scenario description</span></span>
<span data-ttu-id="27e07-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="27e07-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27e07-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="27e07-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27e07-121">Adicionando Ceridian Dayforce HCM da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="27e07-121">Adding Ceridian Dayforce HCM from hello gallery</span></span>
2. <span data-ttu-id="27e07-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27e07-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a><span data-ttu-id="27e07-123">Adicionando Ceridian Dayforce HCM da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="27e07-123">Adding Ceridian Dayforce HCM from hello gallery</span></span>
<span data-ttu-id="27e07-124">integração de saudação tooconfigure de Ceridian Dayforce HCM no AD do Azure, você precisa tooadd Ceridian Dayforce HCM da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="27e07-124">tooconfigure hello integration of Ceridian Dayforce HCM into Azure AD, you need tooadd Ceridian Dayforce HCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27e07-125">**tooadd Ceridian Dayforce HCM da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27e07-125">**tooadd Ceridian Dayforce HCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27e07-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="27e07-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="27e07-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="27e07-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="27e07-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="27e07-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="27e07-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27e07-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="27e07-133">Na caixa de pesquisa hello, digite **Ceridian Dayforce HCM**, selecione **Ceridian Dayforce HCM** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="27e07-133">In hello search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Ceridian Dayforce HCM na lista de resultados de saudação](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="27e07-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="27e07-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="27e07-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Ceridian Dayforce HCM com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="27e07-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27e07-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Ceridian Dayforce HCM é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="27e07-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ceridian Dayforce HCM is tooa user in Azure AD.</span></span> <span data-ttu-id="27e07-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Ceridian Dayforce HCM precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="27e07-138">In other words, a link relationship between an Azure AD user and hello related user in Ceridian Dayforce HCM needs toobe established.</span></span>

<span data-ttu-id="27e07-139">Ceridian Dayforce HCM, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="27e07-139">In Ceridian Dayforce HCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="27e07-140">tooconfigure e teste de logon único do AD do Azure com Ceridian Dayforce HCM, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="27e07-140">tooconfigure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27e07-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="27e07-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27e07-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27e07-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27e07-143">**[Criar um usuário de teste Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave um equivalente do Britta Simon em Ceridian Dayforce HCM que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="27e07-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - toohave a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="27e07-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="27e07-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27e07-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="27e07-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="27e07-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="27e07-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="27e07-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="27e07-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="27e07-148">**tooconfigure logon único do AD do Azure com Ceridian Dayforce HCM, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27e07-148">**tooconfigure Azure AD single sign-on with Ceridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="27e07-149">Em Olá portal do Azure, Olá **Ceridian Dayforce HCM** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="27e07-149">In hello Azure portal, on hello **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="27e07-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="27e07-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="27e07-153">Em Olá **Ceridian Dayforce HCM domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27e07-153">On hello **Ceridian Dayforce HCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="27e07-155">a.</span><span class="sxs-lookup"><span data-stu-id="27e07-155">a.</span></span> <span data-ttu-id="27e07-156">Em Olá **URL de logon** caixa de texto, digite a URL Olá usada por seu usuários em toosign tooyour aplicativo Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="27e07-156">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="27e07-157">Ambiente</span><span class="sxs-lookup"><span data-stu-id="27e07-157">Environment</span></span> | <span data-ttu-id="27e07-158">URL</span><span class="sxs-lookup"><span data-stu-id="27e07-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="27e07-159">Para produção</span><span class="sxs-lookup"><span data-stu-id="27e07-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="27e07-160">Para teste</span><span class="sxs-lookup"><span data-stu-id="27e07-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="27e07-161">b.</span><span class="sxs-lookup"><span data-stu-id="27e07-161">b.</span></span> <span data-ttu-id="27e07-162">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="27e07-162">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    
    | <span data-ttu-id="27e07-163">Ambiente</span><span class="sxs-lookup"><span data-stu-id="27e07-163">Environment</span></span> | <span data-ttu-id="27e07-164">URL</span><span class="sxs-lookup"><span data-stu-id="27e07-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="27e07-165">Para produção</span><span class="sxs-lookup"><span data-stu-id="27e07-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="27e07-166">Para teste</span><span class="sxs-lookup"><span data-stu-id="27e07-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="27e07-167">c.</span><span class="sxs-lookup"><span data-stu-id="27e07-167">c.</span></span> <span data-ttu-id="27e07-168">Em Olá **URL de resposta** caixa de texto, digite a URL do hello usada pela resposta de saudação do AD do Azure toopost.</span><span class="sxs-lookup"><span data-stu-id="27e07-168">In hello **Reply URL** textbox, type hello URL used by Azure AD toopost hello response.</span></span>
    
    | <span data-ttu-id="27e07-169">Ambiente</span><span class="sxs-lookup"><span data-stu-id="27e07-169">Environment</span></span> | <span data-ttu-id="27e07-170">URL</span><span class="sxs-lookup"><span data-stu-id="27e07-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="27e07-171">Para produção</span><span class="sxs-lookup"><span data-stu-id="27e07-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="27e07-172">Para teste</span><span class="sxs-lookup"><span data-stu-id="27e07-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="27e07-173">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="27e07-173">These values are not real.</span></span> <span data-ttu-id="27e07-174">Atualizar esses valores com hello real identificador, a URL de resposta e a URL de logon.</span><span class="sxs-lookup"><span data-stu-id="27e07-174">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="27e07-175">Entre em contato com [equipe de suporte do cliente de HCM Dayforce Ceridian](https://www.ceridian.com/contact-us/index.html) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="27e07-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) tooget these values.</span></span>

4. <span data-ttu-id="27e07-176">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="27e07-176">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="27e07-178">Seu aplicativo de Ceridian Dayforce HCM espera as asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="27e07-178">Your Ceridian Dayforce HCM application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="27e07-179">Trabalhar com [a equipe de suporte Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) primeiro identificador de usuário correto Olá tooidentify.</span><span class="sxs-lookup"><span data-stu-id="27e07-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first tooidentify hello correct user identifier.</span></span> <span data-ttu-id="27e07-180">A Microsoft recomenda usar Olá **"name"** atributo como identificador de usuário.</span><span class="sxs-lookup"><span data-stu-id="27e07-180">Microsoft recommends using hello **"name"** attribute as user identifier.</span></span> <span data-ttu-id="27e07-181">Você pode gerenciar os valores hello desses atributos de saudação **atributos de usuário** seção na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="27e07-181">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="27e07-182">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="27e07-182">hello following screenshot shows an example for this.</span></span>  

    ![Configurar Logon Único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="27e07-184">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27e07-184">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="27e07-185">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="27e07-185">Attribute Name</span></span>  | <span data-ttu-id="27e07-186">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="27e07-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="27e07-187">name</span><span class="sxs-lookup"><span data-stu-id="27e07-187">name</span></span>  | <span data-ttu-id="27e07-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="27e07-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="27e07-189">a.</span><span class="sxs-lookup"><span data-stu-id="27e07-189">a.</span></span> <span data-ttu-id="27e07-190">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27e07-190">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="27e07-193">b.</span><span class="sxs-lookup"><span data-stu-id="27e07-193">b.</span></span> <span data-ttu-id="27e07-194">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="27e07-194">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="27e07-195">c.</span><span class="sxs-lookup"><span data-stu-id="27e07-195">c.</span></span> <span data-ttu-id="27e07-196">Em Olá **valor** lista, selecione Olá usuário atributo que toouse para sua implementação.</span><span class="sxs-lookup"><span data-stu-id="27e07-196">In hello **Value** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="27e07-197">Por exemplo, se você quiser toouse Olá EmployeeID como identificador exclusivo do usuário e você armazenou o valor de atributo Olá Olá ExtensionAttribute2, selecione **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="27e07-197">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="27e07-198">d.</span><span class="sxs-lookup"><span data-stu-id="27e07-198">d.</span></span> <span data-ttu-id="27e07-199">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27e07-199">Click **Ok**.</span></span>

7. <span data-ttu-id="27e07-200">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="27e07-200">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="27e07-202">Em Olá **Ceridian Dayforce HCM configuração** seção, clique em **configurar HCM de Dayforce Ceridian** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="27e07-202">On hello **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="27e07-203">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="27e07-203">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="27e07-205">tooconfigure logon único no **Ceridian Dayforce HCM** lado, você precisa toosend Olá baixado **Metadata XML** e **URL de logout, ID de entidade de SAML e SAML Single Sign-On URL do serviço** muito[a equipe de suporte Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="27e07-205">tooconfigure single sign-on on **Ceridian Dayforce HCM** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="27e07-206">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="27e07-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="27e07-207">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="27e07-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="27e07-208">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27e07-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="27e07-209">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="27e07-209">Create an Azure AD test user</span></span>

<span data-ttu-id="27e07-210">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="27e07-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="27e07-212">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27e07-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27e07-213">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="27e07-213">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="27e07-215">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="27e07-215">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="27e07-217">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27e07-217">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="27e07-219">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27e07-219">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="27e07-221">a.</span><span class="sxs-lookup"><span data-stu-id="27e07-221">a.</span></span> <span data-ttu-id="27e07-222">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27e07-222">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27e07-223">b.</span><span class="sxs-lookup"><span data-stu-id="27e07-223">b.</span></span> <span data-ttu-id="27e07-224">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27e07-224">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="27e07-225">c.</span><span class="sxs-lookup"><span data-stu-id="27e07-225">c.</span></span> <span data-ttu-id="27e07-226">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="27e07-226">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="27e07-227">d.</span><span class="sxs-lookup"><span data-stu-id="27e07-227">d.</span></span> <span data-ttu-id="27e07-228">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="27e07-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="27e07-229">Criar um usuário de teste do Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="27e07-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="27e07-230">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="27e07-230">hello objective of this section is toocreate a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="27e07-231">Trabalhar com hello [a equipe de suporte Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) tooget usuários adicionados no hello aplicativo Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="27e07-231">Work with hello [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) tooget users added in hello Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="27e07-232">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27e07-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="27e07-233">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="27e07-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="27e07-235">**tooassign Britta Simon tooCeridian Dayforce HCM, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27e07-235">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="27e07-236">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="27e07-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="27e07-238">Na lista de aplicativos hello, selecione **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="27e07-238">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="27e07-240">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="27e07-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="27e07-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="27e07-242">Click **Add** button.</span></span> <span data-ttu-id="27e07-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27e07-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="27e07-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="27e07-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27e07-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27e07-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27e07-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27e07-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="27e07-248">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27e07-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="27e07-249">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="27e07-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="27e07-251">**tooassign Britta Simon tooCeridian Dayforce HCM, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27e07-251">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="27e07-252">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="27e07-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="27e07-254">Na lista de aplicativos hello, selecione **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="27e07-254">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![link de Ceridian Dayforce HCM Olá na lista de aplicativos Olá](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="27e07-256">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="27e07-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="27e07-258">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="27e07-258">Click **Add** button.</span></span> <span data-ttu-id="27e07-259">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27e07-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="27e07-261">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="27e07-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27e07-262">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27e07-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27e07-263">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27e07-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="27e07-264">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="27e07-264">Test single sign-on</span></span>

<span data-ttu-id="27e07-265">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="27e07-265">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="27e07-266">Quando você clica em bloco Ceridian Dayforce HCM Olá Olá painel de acesso, você deve obter o aplicativo de Ceridian Dayforce HCM tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="27e07-266">When you click hello Ceridian Dayforce HCM tile in hello Access Panel, you should get automatically signed-on tooyour Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="27e07-267">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="27e07-267">Additional resources</span></span>

* [<span data-ttu-id="27e07-268">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="27e07-268">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27e07-269">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="27e07-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

