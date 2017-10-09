---
title: "Tutorial: integração do Azure Active Directory com o Learningpool Act | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o ato de Learningpool."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: f343623f08bb60e143aaff07d93e4ef773232e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="4a2e3-103">Tutorial: integração do Azure Active Directory com o Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="4a2e3-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="4a2e3-104">Neste tutorial, você aprenderá como toointegrate Learningpool agir com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-104">In this tutorial, you learn how toointegrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a2e3-105">Integrar o ato de Learningpool com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-105">Integrating Learningpool Act with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4a2e3-106">Você pode controlar no AD do Azure que tenha acesso tooLearningpool Act</span><span class="sxs-lookup"><span data-stu-id="4a2e3-106">You can control in Azure AD who has access tooLearningpool Act</span></span>
- <span data-ttu-id="4a2e3-107">Você pode habilitar seu usuários tooautomatically get conectado tooLearningpool Act (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4a2e3-107">You can enable your users tooautomatically get signed-on tooLearningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a2e3-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4a2e3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4a2e3-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a2e3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4a2e3-110">Prerequisites</span></span>

<span data-ttu-id="4a2e3-111">tooconfigure integração do AD do Azure com o Learningpool Act, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-111">tooconfigure Azure AD integration with Learningpool Act, you need hello following items:</span></span>

- <span data-ttu-id="4a2e3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4a2e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a2e3-113">Uma assinatura com logon único habilitado do Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="4a2e3-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a2e3-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4a2e3-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a2e3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a2e3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a2e3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4a2e3-118">Scenario description</span></span>
<span data-ttu-id="4a2e3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a2e3-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a2e3-121">Adicionando Learningpool ato da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4a2e3-121">Adding Learningpool Act from hello gallery</span></span>
2. <span data-ttu-id="4a2e3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4a2e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-hello-gallery"></a><span data-ttu-id="4a2e3-123">Adicionando Learningpool ato da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4a2e3-123">Adding Learningpool Act from hello gallery</span></span>
<span data-ttu-id="4a2e3-124">integração de saudação tooconfigure do Learningpool Act no AD do Azure, você precisa tooadd Learningpool ato da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-124">tooconfigure hello integration of Learningpool Act into Azure AD, you need tooadd Learningpool Act from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4a2e3-125">**tooadd Learningpool ato da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4a2e3-125">**tooadd Learningpool Act from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a2e3-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4a2e3-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4a2e3-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4a2e3-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4a2e3-133">Na caixa de pesquisa hello, digite **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-133">In hello search box, type **Learningpool Act**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="4a2e3-135">No painel de resultados de saudação, selecione **Learningpool Act**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-135">In hello results panel, select **Learningpool Act**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a2e3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4a2e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a2e3-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Learningpool Act, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="4a2e3-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4a2e3-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Learningpool Act é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learningpool Act is tooa user in Azure AD.</span></span> <span data-ttu-id="4a2e3-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação do Learningpool Act precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-140">In other words, a link relationship between an Azure AD user and hello related user in Learningpool Act needs toobe established.</span></span>

<span data-ttu-id="4a2e3-141">No Learningpool Act, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-141">In Learningpool Act, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4a2e3-142">tooconfigure e teste de logon único do AD do Azure com o Learningpool Act, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-142">tooconfigure and test Azure AD single sign-on with Learningpool Act, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4a2e3-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4a2e3-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4a2e3-145">**[Criar um usuário de teste do Learningpool Act](#creating-a-learningpool-act-test-user)**  -toohave um equivalente do Britta Simon do Learningpool Act que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - toohave a counterpart of Britta Simon in Learningpool Act that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4a2e3-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4a2e3-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4a2e3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a2e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4a2e3-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="4a2e3-150">**tooconfigure AD do Azure-logon único com o Learningpool Act, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4a2e3-150">**tooconfigure Azure AD single sign-on with Learningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a2e3-151">Em Olá portal do Azure, Olá **Learningpool Act** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-151">In hello Azure portal, on hello **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4a2e3-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="4a2e3-155">Em Olá **Learningpool Act domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-155">On hello **Learningpool Act Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="4a2e3-157">a.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-157">a.</span></span> <span data-ttu-id="4a2e3-158">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="4a2e3-158">In hello **Sign-on URL** textbox, type hello URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="4a2e3-159">b.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-159">b.</span></span> <span data-ttu-id="4a2e3-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="4a2e3-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-161">These values are not real.</span></span> <span data-ttu-id="4a2e3-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4a2e3-163">Entre em contato com [equipe de suporte do Learningpool Act cliente](https://www.Learningpool.com/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="4a2e3-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="4a2e3-166">Aplicativo Learningpool Act espera as asserções de SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-166">Learningpool Act application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="4a2e3-167">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="4a2e3-168">Você pode gerenciar os valores hello desses atributos de saudação **"Atributo"** guia do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-168">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="4a2e3-169">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-169">hello following screenshot shows an example for this.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="4a2e3-171">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="4a2e3-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="4a2e3-172">Attribute Name</span></span> | <span data-ttu-id="4a2e3-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="4a2e3-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="4a2e3-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="4a2e3-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="4a2e3-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="4a2e3-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="4a2e3-176">urn: oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="4a2e3-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="4a2e3-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4a2e3-177">user.givenname</span></span> |
    | <span data-ttu-id="4a2e3-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="4a2e3-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="4a2e3-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="4a2e3-179">user.mail</span></span> |    
    | <span data-ttu-id="4a2e3-180">urn: oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="4a2e3-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="4a2e3-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="4a2e3-181">user.surname</span></span> |
    
    <span data-ttu-id="4a2e3-182">a.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-182">a.</span></span> <span data-ttu-id="4a2e3-183">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4a2e3-186">b.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-186">b.</span></span> <span data-ttu-id="4a2e3-187">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="4a2e3-188">c.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-188">c.</span></span> <span data-ttu-id="4a2e3-189">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="4a2e3-190">d.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-190">d.</span></span> <span data-ttu-id="4a2e3-191">Deixe Olá **Namespace** em branco.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-191">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="4a2e3-192">e.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-192">e.</span></span> <span data-ttu-id="4a2e3-193">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-193">Click **Ok**.</span></span>

7. <span data-ttu-id="4a2e3-194">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4a2e3-194">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4a2e3-196">tooconfigure logon único no **Learningpool Act** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-196">tooconfigure single sign-on on **Learningpool Act** side, you need toosend hello downloaded **Metadata XML** too[Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="4a2e3-197">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4a2e3-198">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="4a2e3-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4a2e3-199">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4a2e3-200">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4a2e3-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a2e3-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4a2e3-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a2e3-202">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4a2e3-204">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4a2e3-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a2e3-205">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4a2e3-207">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a2e3-209">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a2e3-211">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a2e3-213">a.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-213">a.</span></span> <span data-ttu-id="4a2e3-214">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a2e3-215">b.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-215">b.</span></span> <span data-ttu-id="4a2e3-216">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a2e3-217">c.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-217">c.</span></span> <span data-ttu-id="4a2e3-218">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4a2e3-219">d.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-219">d.</span></span> <span data-ttu-id="4a2e3-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="4a2e3-221">Criação de um usuário de teste do Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="4a2e3-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="4a2e3-222">tooenable AD do Azure usuários toolog em tooLearningpool Act, eles devem ser provisionados no Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-222">tooenable Azure AD users toolog in tooLearningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="4a2e3-223">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-223">There is no action item for you tooconfigure user provisioning tooLearningpool Act.</span></span>  
<span data-ttu-id="4a2e3-224">Os usuários precisam toobe criado por seu [equipe de suporte do Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-224">Users need toobe created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="4a2e3-225">Você pode usar qualquer ferramenta de criação outros Learningpool Act usuário conta ou APIs fornecidas pelo Learningpool Act tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4a2e3-226">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4a2e3-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4a2e3-227">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearningpool Act.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4a2e3-229">**tooassign Britta Simon tooLearningpool Act, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4a2e3-229">**tooassign Britta Simon tooLearningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a2e3-230">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4a2e3-232">Na lista de aplicativos hello, selecione **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-232">In hello applications list, select **Learningpool Act**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="4a2e3-234">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4a2e3-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-236">Click **Add** button.</span></span> <span data-ttu-id="4a2e3-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4a2e3-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4a2e3-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4a2e3-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4a2e3-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4a2e3-242">Testing single sign-on</span></span>

<span data-ttu-id="4a2e3-243">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4a2e3-244">Quando você clica em Olá Learningpool Act bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-244">When you click hello Learningpool Act tile in hello Access Panel, you should get automatically signed-on tooyour Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a2e3-245">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4a2e3-245">Additional resources</span></span>

* [<span data-ttu-id="4a2e3-246">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4a2e3-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a2e3-247">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4a2e3-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

