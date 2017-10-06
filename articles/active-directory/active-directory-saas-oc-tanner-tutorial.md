---
title: "Tutorial: Integração do Azure Active Directory ao O.C. Tanner - AppreciateHub | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e O.C. Tanner - AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="3ba50-105">Tutorial: Integração do Azure Active Directory ao O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="3ba50-106">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="3ba50-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="3ba50-107">Neste tutorial, você aprenderá como toointegrate O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-107">In this tutorial, you learn how toointegrate O.C.</span></span> <span data-ttu-id="3ba50-108">Tanner - AppreciateHub ao Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="3ba50-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ba50-109">Integração do O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-109">Integrating O.C.</span></span> <span data-ttu-id="3ba50-110">Lemos - AppreciateHub com o Azure AD fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ba50-110">Tanner - AppreciateHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3ba50-111">Você pode controlar no AD do Azure que tenha acesso tooO.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-111">You can control in Azure AD who has access tooO.C.</span></span> <span data-ttu-id="3ba50-112">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="3ba50-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="3ba50-113">Você pode habilitar seus usuários tooautomatically get conectado tooO.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-113">You can enable your users tooautomatically get signed-on tooO.C.</span></span> <span data-ttu-id="3ba50-114">Tanner - AppreciateHub (Logon Único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ba50-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ba50-115">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3ba50-115">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3ba50-116">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ba50-116">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ba50-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3ba50-117">Prerequisites</span></span>

<span data-ttu-id="3ba50-118">tooconfigure integração do AD do Azure com O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-118">tooconfigure Azure AD integration with O.C.</span></span> <span data-ttu-id="3ba50-119">Lemos - AppreciateHub, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ba50-119">Tanner - AppreciateHub, you need hello following items:</span></span>

- <span data-ttu-id="3ba50-120">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ba50-120">An Azure AD subscription</span></span>
- <span data-ttu-id="3ba50-121">Um</span><span class="sxs-lookup"><span data-stu-id="3ba50-121">A O.C.</span></span> <span data-ttu-id="3ba50-122">Assinatura habilitada para logon único do Tanner – AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="3ba50-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ba50-123">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3ba50-123">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ba50-124">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3ba50-124">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ba50-125">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3ba50-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ba50-126">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ba50-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ba50-127">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3ba50-127">Scenario description</span></span>
<span data-ttu-id="3ba50-128">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3ba50-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ba50-129">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="3ba50-129">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ba50-130">Adicionar o O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-130">Adding O.C.</span></span> <span data-ttu-id="3ba50-131">Lemos - AppreciateHub da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3ba50-131">Tanner - AppreciateHub from hello gallery</span></span>
2. <span data-ttu-id="3ba50-132">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ba50-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a><span data-ttu-id="3ba50-133">Adicionar o O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-133">Adding O.C.</span></span> <span data-ttu-id="3ba50-134">Lemos - AppreciateHub da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3ba50-134">Tanner - AppreciateHub from hello gallery</span></span>
<span data-ttu-id="3ba50-135">integração de saudação do tooconfigure do O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-135">tooconfigure hello integration of O.C.</span></span> <span data-ttu-id="3ba50-136">Lemos - AppreciateHub no AD do Azure, você precisa tooadd O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-136">Tanner - AppreciateHub into Azure AD, you need tooadd O.C.</span></span> <span data-ttu-id="3ba50-137">Lemos - AppreciateHub na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3ba50-137">Tanner - AppreciateHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3ba50-138">**tooadd O.C. Lemos - AppreciateHub da Galeria hello, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3ba50-138">**tooadd O.C. Tanner - AppreciateHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ba50-139">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3ba50-139">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ba50-141">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-141">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3ba50-142">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-142">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3ba50-144">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ba50-144">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3ba50-146">Na caixa de pesquisa hello, digite **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-146">In hello search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="3ba50-148">No painel de resultados de saudação, selecione **O.C. Lemos - AppreciateHub**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3ba50-148">In hello results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ba50-150">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ba50-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ba50-151">Nesta seção, configura e testa o logon único do Azure AD com o O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="3ba50-152">Tanner - AppreciateHub com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="3ba50-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3ba50-153">Para toowork de logon único, AD do Azure precisa tooknow que usuário de contraparte Olá em O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-153">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in O.C.</span></span> <span data-ttu-id="3ba50-154">Lemos - AppreciateHub é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba50-154">Tanner - AppreciateHub is tooa user in Azure AD.</span></span> <span data-ttu-id="3ba50-155">Em outras palavras, uma relação entre um usuário do AD do Azure e o usuário relacionado de saudação em O.C. de link</span><span class="sxs-lookup"><span data-stu-id="3ba50-155">In other words, a link relationship between an Azure AD user and hello related user in O.C.</span></span> <span data-ttu-id="3ba50-156">Lemos - AppreciateHub precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3ba50-156">Tanner - AppreciateHub needs toobe established.</span></span>

<span data-ttu-id="3ba50-157">No O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-157">In O.C.</span></span> <span data-ttu-id="3ba50-158">Lemos - AppreciateHub, atribuir Olá valor Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ba50-158">Tanner - AppreciateHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3ba50-159">tooconfigure e teste de logon único do AD do Azure com O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-159">tooconfigure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="3ba50-160">Lemos - AppreciateHub, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ba50-160">Tanner - AppreciateHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3ba50-161">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3ba50-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3ba50-162">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ba50-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ba50-163">**[Criar um usuário teste do O.C. Lemos - usuário de teste AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)**  -toohave um equivalente do Britta Simon em O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - toohave a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="3ba50-164">Lemos - AppreciateHub é vinculado toohello representação do AD do Azure do usuário.</span><span class="sxs-lookup"><span data-stu-id="3ba50-164">Tanner - AppreciateHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ba50-165">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="3ba50-165">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ba50-166">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="3ba50-166">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ba50-167">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ba50-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ba50-168">Nesta seção, você pode habilitar AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-168">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="3ba50-169">Aplicativo Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="3ba50-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="3ba50-170">**tooconfigure AD do Azure-logon único com O.C. Lemos - AppreciateHub, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3ba50-170">**tooconfigure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ba50-171">Em Olá portal do Azure, Olá **O.C. Tanner – AppreciateHub**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-171">In hello Azure portal, on hello **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3ba50-173">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="3ba50-173">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="3ba50-175">Em Olá **O.C. Lemos - domínio AppreciateHub e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ba50-175">On hello **O.C. Tanner - AppreciateHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="3ba50-177">a.</span><span class="sxs-lookup"><span data-stu-id="3ba50-177">a.</span></span> <span data-ttu-id="3ba50-178">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="3ba50-178">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3ba50-179">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="3ba50-179">This value is not real.</span></span> <span data-ttu-id="3ba50-180">Atualize esse valor com hello URL de resposta real.</span><span class="sxs-lookup"><span data-stu-id="3ba50-180">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="3ba50-181">Contate a [Equipe de suporte do O.C. Lemos - a equipe de suporte AppreciateHub](mailto:sso@octanner.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="3ba50-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) tooget this value.</span></span>

    <span data-ttu-id="3ba50-182">b.</span><span class="sxs-lookup"><span data-stu-id="3ba50-182">b.</span></span> <span data-ttu-id="3ba50-183">Arquivo de metadados de saudação aberta usando Olá link a seguir: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="3ba50-183">Open hello metadata file using hello following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="3ba50-184">c.</span><span class="sxs-lookup"><span data-stu-id="3ba50-184">c.</span></span> <span data-ttu-id="3ba50-185">Localizar Olá **md:AssertionConsumerService** nó.</span><span class="sxs-lookup"><span data-stu-id="3ba50-185">Locate hello **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="3ba50-186">d.</span><span class="sxs-lookup"><span data-stu-id="3ba50-186">d.</span></span> <span data-ttu-id="3ba50-187">Copie o valor Olá Olá **local** atributo.</span><span class="sxs-lookup"><span data-stu-id="3ba50-187">Copy hello value of hello **Location** attribute.</span></span> 
   
    ![Definir configurações de aplicativo][12]
   
    <span data-ttu-id="3ba50-189">e.</span><span class="sxs-lookup"><span data-stu-id="3ba50-189">e.</span></span> <span data-ttu-id="3ba50-190">Em Olá **URL de logon** caixa de texto valor Olá você obteve na etapa anterior Olá já.</span><span class="sxs-lookup"><span data-stu-id="3ba50-190">In hello **Sign On URL** textbox, past hello value you have obtained in hello previous step.</span></span>

4. <span data-ttu-id="3ba50-191">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3ba50-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="3ba50-193">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3ba50-193">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3ba50-195">tooconfigure logon único no **O.C. Lemos - AppreciateHub** lado, você precisa toosend Olá baixado **Metadata XML** muito[O.C. Tanner – AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="3ba50-195">tooconfigure single sign-on on **O.C. Tanner - AppreciateHub** side, you need toosend hello downloaded **Metadata XML** too[O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="3ba50-196">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="3ba50-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3ba50-197">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="3ba50-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3ba50-198">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3ba50-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ba50-199">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ba50-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ba50-200">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba50-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3ba50-202">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3ba50-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ba50-203">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3ba50-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ba50-205">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ba50-207">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ba50-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ba50-209">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ba50-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ba50-211">a.</span><span class="sxs-lookup"><span data-stu-id="3ba50-211">a.</span></span> <span data-ttu-id="3ba50-212">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ba50-213">b.</span><span class="sxs-lookup"><span data-stu-id="3ba50-213">b.</span></span> <span data-ttu-id="3ba50-214">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3ba50-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ba50-215">c.</span><span class="sxs-lookup"><span data-stu-id="3ba50-215">c.</span></span> <span data-ttu-id="3ba50-216">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3ba50-217">d.</span><span class="sxs-lookup"><span data-stu-id="3ba50-217">d.</span></span> <span data-ttu-id="3ba50-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="3ba50-219">Criar um usuário teste do O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-219">Creating a O.C.</span></span> <span data-ttu-id="3ba50-220">Usuário de teste do Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="3ba50-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="3ba50-221">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-221">hello objective of this section is toocreate a user called Britta Simon in O.C.</span></span> <span data-ttu-id="3ba50-222">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="3ba50-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="3ba50-223">**toocreate um usuário chamado Britta Simon em O.C. Lemos - AppreciateHub, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3ba50-223">**toocreate a user called Britta Simon in O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

<span data-ttu-id="3ba50-224">Peça à sua [equipe de suporte do O.C. Lemos - a equipe de suporte AppreciateHub](mailto:sso@octanner.com) toocreate um usuário que tem como saudação do atributo nameID mesmo valor como nome de usuário de saudação do Britta Simon no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba50-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) toocreate a user that has as nameID attribute hello same value as hello user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3ba50-225">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ba50-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3ba50-226">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooO.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooO.C.</span></span> <span data-ttu-id="3ba50-227">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="3ba50-227">Tanner - AppreciateHub.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3ba50-229">**tooassign Britta Simon tooO.C. Lemos - AppreciateHub, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3ba50-229">**tooassign Britta Simon tooO.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ba50-230">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3ba50-232">Na lista de aplicativos hello, selecione **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-232">In hello applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="3ba50-234">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3ba50-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3ba50-236">Click **Add** button.</span></span> <span data-ttu-id="3ba50-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ba50-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3ba50-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ba50-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3ba50-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ba50-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ba50-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ba50-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ba50-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3ba50-242">Testing single sign-on</span></span>

<span data-ttu-id="3ba50-243">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="3ba50-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="3ba50-244">Quando você clica em Olá O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-244">When you click hello O.C.</span></span> <span data-ttu-id="3ba50-245">Olá de Lemos - AppreciateHub bloco no painel de acesso, você deve obter automaticamente assinado em tooyour O.C.</span><span class="sxs-lookup"><span data-stu-id="3ba50-245">Tanner - AppreciateHub tile in hello Access Panel, you should get automatically signed-on tooyour O.C.</span></span> <span data-ttu-id="3ba50-246">Aplicativo Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="3ba50-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3ba50-247">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3ba50-247">Additional resources</span></span>

* [<span data-ttu-id="3ba50-248">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3ba50-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ba50-249">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3ba50-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

