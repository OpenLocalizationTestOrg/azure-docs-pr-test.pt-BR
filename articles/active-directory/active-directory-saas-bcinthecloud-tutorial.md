---
title: "Tutorial: Integração do Active Directory do Azure com continuidade de negócios na nuvem de saudação | Microsoft Docs"
description: "Saiba como tooconfigure logon único entre o Active Directory do Azure e continuidade de negócios em Olá nuvem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: e81ffb522b2c96c7e9b2919abd8d3b199c295eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-hello-cloud"></a><span data-ttu-id="c5975-103">Tutorial: Integração do Active Directory do Azure com continuidade de negócios na nuvem de saudação</span><span class="sxs-lookup"><span data-stu-id="c5975-103">Tutorial: Azure Active Directory integration with BC in hello Cloud</span></span>

<span data-ttu-id="c5975-104">Neste tutorial, você aprenderá como toointegrate BC em Olá nuvem com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c5975-104">In this tutorial, you learn how toointegrate BC in hello Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5975-105">Integração de continuidade de negócios em Olá nuvem com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5975-105">Integrating BC in hello Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5975-106">Você pode controlar no AD do Azure que tenha acesso tooBC em Olá nuvem</span><span class="sxs-lookup"><span data-stu-id="c5975-106">You can control in Azure AD who has access tooBC in hello Cloud</span></span>
- <span data-ttu-id="c5975-107">Você pode habilitar seu usuários tooautomatically get conectado tooBC em Olá nuvem (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5975-107">You can enable your users tooautomatically get signed-on tooBC in hello Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5975-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c5975-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c5975-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5975-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5975-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c5975-110">Prerequisites</span></span>

<span data-ttu-id="c5975-111">tooconfigure integração do AD do Azure com continuidade de negócios na nuvem do hello, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5975-111">tooconfigure Azure AD integration with BC in hello Cloud, you need hello following items:</span></span>

- <span data-ttu-id="c5975-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5975-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5975-113">Continuidade de negócios em Olá logon único de nuvem na assinatura habilitada</span><span class="sxs-lookup"><span data-stu-id="c5975-113">A BC in hello Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5975-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c5975-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5975-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c5975-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5975-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c5975-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5975-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5975-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5975-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c5975-118">Scenario description</span></span>
<span data-ttu-id="c5975-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c5975-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5975-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c5975-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5975-121">Adicionando a continuidade de negócios em Olá nuvem da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c5975-121">Adding BC in hello Cloud from hello gallery</span></span>
2. <span data-ttu-id="c5975-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5975-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-hello-cloud-from-hello-gallery"></a><span data-ttu-id="c5975-123">Adicionando a continuidade de negócios em Olá nuvem da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c5975-123">Adding BC in hello Cloud from hello gallery</span></span>
<span data-ttu-id="c5975-124">integração de saudação tooconfigure de continuidade de negócios em Olá nuvem no Azure AD, é necessário tooadd BC em Olá nuvem na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c5975-124">tooconfigure hello integration of BC in hello Cloud into Azure AD, you need tooadd BC in hello Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5975-125">**tooadd BC em Olá nuvem da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c5975-125">**tooadd BC in hello Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5975-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c5975-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5975-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c5975-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5975-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c5975-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c5975-131">tooadd novo aplicativo, clique em **adicionar** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5975-131">tooadd new application, click **Add** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c5975-133">Na caixa de pesquisa hello, digite **continuidade de negócios na nuvem de saudação**.</span><span class="sxs-lookup"><span data-stu-id="c5975-133">In hello search box, type **BC in hello Cloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="c5975-135">No painel de resultados de saudação, selecione **continuidade de negócios na nuvem de saudação**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c5975-135">In hello results panel, select **BC in hello Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5975-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5975-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5975-138">Nesta seção, configurar e testar o AD do Azure-logon único com BC em Olá baseada em nuvem em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c5975-138">In this section, you configure and test Azure AD single sign-on with BC in hello Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c5975-139">Para toowork de logon único, AD do Azure precisa tooknow quais Olá usuário correspondente na continuidade de negócios na nuvem de saudação é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5975-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BC in hello Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="c5975-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na continuidade de negócios na nuvem de saudação precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c5975-140">In other words, a link relationship between an Azure AD user and hello related user in BC in hello Cloud needs toobe established.</span></span>

<span data-ttu-id="c5975-141">Na continuidade de negócios na nuvem do hello, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5975-141">In BC in hello Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c5975-142">tooconfigure e teste de logon único do AD do Azure com continuidade de negócios na nuvem de Olá, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5975-142">tooconfigure and test Azure AD single sign-on with BC in hello Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5975-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c5975-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5975-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5975-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5975-145">**[Criando uma continuidade de negócios no usuário de teste de nuvem Olá](#creating-a-bc-in-the-cloud-test-user)**  -toohave um equivalente do Britta Simon na continuidade de negócios em Olá nuvem que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c5975-145">**[Creating a BC in hello Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - toohave a counterpart of Britta Simon in BC in hello Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5975-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c5975-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5975-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c5975-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5975-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5975-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5975-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único na continuidade de negócios no aplicativo de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="c5975-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BC in hello Cloud application.</span></span>

<span data-ttu-id="c5975-150">**tooconfigure AD do Azure-logon único com continuidade de negócios na nuvem, de saudação execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c5975-150">**tooconfigure Azure AD single sign-on with BC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5975-151">Em Olá portal do Azure, Olá **continuidade de negócios na nuvem de saudação** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c5975-151">In hello Azure portal, on hello **BC in hello Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c5975-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c5975-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="c5975-155">Em Olá **BC em hello domínio de nuvem e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5975-155">On hello **BC in hello Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="c5975-157">a.</span><span class="sxs-lookup"><span data-stu-id="c5975-157">a.</span></span> <span data-ttu-id="c5975-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="c5975-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="c5975-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5975-159">b.</span></span> <span data-ttu-id="c5975-160">Em Olá **identificador** caixa de texto, digite um URL como:`https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="c5975-160">In hello **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5975-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="c5975-161">This value is not real.</span></span> <span data-ttu-id="c5975-162">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="c5975-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c5975-163">Entre em contato com [BC na equipe de suporte de cliente de nuvem Olá](https://www.bcinthecloud.com/supportcenter/) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="c5975-163">Contact [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) tooget this value.</span></span> 
 
4. <span data-ttu-id="c5975-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c5975-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="c5975-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c5975-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5975-168">tooconfigure logon único no **continuidade de negócios na nuvem de saudação** lado, você precisa toosend Olá baixado **Metadata XML** muito[BC na equipe de suporte de nuvem Olá](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="c5975-168">tooconfigure single sign-on on **BC in hello Cloud** side, you need toosend hello downloaded **Metadata XML** too[BC in hello Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="c5975-169">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c5975-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5975-170">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c5975-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5975-171">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5975-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5975-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5975-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5975-173">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5975-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c5975-175">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c5975-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5975-176">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c5975-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5975-178">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c5975-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5975-180">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5975-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5975-182">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5975-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5975-184">a.</span><span class="sxs-lookup"><span data-stu-id="c5975-184">a.</span></span> <span data-ttu-id="c5975-185">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5975-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5975-186">b.</span><span class="sxs-lookup"><span data-stu-id="c5975-186">b.</span></span> <span data-ttu-id="c5975-187">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c5975-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5975-188">c.</span><span class="sxs-lookup"><span data-stu-id="c5975-188">c.</span></span> <span data-ttu-id="c5975-189">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c5975-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5975-190">d.</span><span class="sxs-lookup"><span data-stu-id="c5975-190">d.</span></span> <span data-ttu-id="c5975-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c5975-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-hello-cloud-test-user"></a><span data-ttu-id="c5975-192">Criando uma continuidade de negócios no usuário de teste de nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="c5975-192">Creating a BC in hello Cloud test user</span></span>

<span data-ttu-id="c5975-193">Nesta seção, você deve criar um usuário chamado Britta Simon na continuidade de negócios na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5975-193">In this section, you create a user called Britta Simon in BC in hello Cloud.</span></span> <span data-ttu-id="c5975-194">Trabalhar com [BC na equipe de suporte de cliente de nuvem Olá](https://www.bcinthecloud.com/supportcenter/) para adicionar usuários Olá Olá BC em Olá aplicativo em nuvem.</span><span class="sxs-lookup"><span data-stu-id="c5975-194">Work with [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add hello users in hello BC in hello Cloud application.</span></span> <span data-ttu-id="c5975-195">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c5975-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5975-196">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5975-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5975-197">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBC em Olá nuvem.</span><span class="sxs-lookup"><span data-stu-id="c5975-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBC in hello Cloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c5975-199">**tooassign Britta Simon tooBC em Olá nuvem, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c5975-199">**tooassign Britta Simon tooBC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5975-200">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c5975-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c5975-202">Na lista de aplicativos hello, selecione **continuidade de negócios na nuvem de saudação**.</span><span class="sxs-lookup"><span data-stu-id="c5975-202">In hello applications list, select **BC in hello Cloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="c5975-204">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c5975-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c5975-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c5975-206">Click **Add** button.</span></span> <span data-ttu-id="c5975-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5975-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c5975-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5975-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5975-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5975-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5975-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5975-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5975-212">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c5975-212">Testing single sign-on</span></span>

<span data-ttu-id="c5975-213">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5975-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

 <span data-ttu-id="c5975-214">Quando você clica em Olá BC no bloco de nuvem Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour BC em Olá aplicativo em nuvem.</span><span class="sxs-lookup"><span data-stu-id="c5975-214">When you click hello BC in hello Cloud tile in hello Access Panel, you should get automatically signed-on tooyour BC in hello Cloud application.</span></span> <span data-ttu-id="c5975-215">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5975-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5975-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c5975-216">Additional resources</span></span>

* [<span data-ttu-id="c5975-217">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c5975-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5975-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5975-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

