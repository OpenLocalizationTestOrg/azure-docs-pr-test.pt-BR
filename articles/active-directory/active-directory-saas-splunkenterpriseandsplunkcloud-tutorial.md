---
title: "Tutorial: Integração do Azure Active Directory com o Splunk Enterprise e o Splunk Cloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Splunk Enterprise e Splunk nuvem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 848e0485131321479f2375501b330c798627e7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="d35e8-103">Tutorial: Integração do Azure Active Directory com o Splunk Enterprise e o Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="d35e8-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="d35e8-104">Neste tutorial, você aprenderá como toointegrate Splunk Enterprise e Splunk nuvem com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d35e8-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d35e8-105">Integração Splunk Enterprise e Splunk nuvem com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="d35e8-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d35e8-106">Você pode controlar no AD do Azure que tenha acesso tooSplunk Enterprise e nuvem Splunk</span><span class="sxs-lookup"><span data-stu-id="d35e8-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="d35e8-107">Você pode habilitar seus usuários tooautomatically get conectado tooSplunk Enterprise e a nuvem Splunk (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d35e8-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d35e8-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d35e8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d35e8-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d35e8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d35e8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d35e8-110">Prerequisites</span></span>

<span data-ttu-id="d35e8-111">tooconfigure integração do AD do Azure com Splunk Enterprise e Splunk nuvem, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d35e8-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="d35e8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d35e8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d35e8-113">Uma assinatura do Splunk Enterprise e do Splunk Cloud habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="d35e8-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d35e8-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d35e8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d35e8-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d35e8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d35e8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d35e8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d35e8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d35e8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d35e8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d35e8-118">Scenario description</span></span>
<span data-ttu-id="d35e8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d35e8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d35e8-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="d35e8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d35e8-121">Adicionando Splunk Enterprise e nuvem Splunk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d35e8-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="d35e8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d35e8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="d35e8-123">Adicionando Splunk Enterprise e nuvem Splunk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d35e8-123">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="d35e8-124">integração de saudação tooconfigure do Splunk Enterprise e Splunk nuvem no Azure AD, você precisa tooadd Splunk Enterprise e gerenciado de nuvem Splunk de lista de tooyour Olá Galeria de aplicativos SaaS.</span><span class="sxs-lookup"><span data-stu-id="d35e8-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d35e8-125">**tooadd Splunk Enterprise e nuvem Splunk da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d35e8-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d35e8-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d35e8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d35e8-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d35e8-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d35e8-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d35e8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d35e8-133">Na caixa de pesquisa hello, digite **Splunk Enterprise e nuvem Splunk**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-133">In hello search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

5. <span data-ttu-id="d35e8-135">No painel de resultados de saudação, selecione **Splunk Enterprise e nuvem Splunk**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d35e8-135">In hello results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d35e8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d35e8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d35e8-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Splunk Enterprise e o Splunk Cloud, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="d35e8-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d35e8-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá Splunk Enterprise e nuvem Splunk é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d35e8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="d35e8-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Splunk Enterprise e nuvem Splunk precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d35e8-140">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="d35e8-141">Splunk Enterprise e nuvem Splunk, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="d35e8-141">In Splunk Enterprise and Splunk Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d35e8-142">tooconfigure e teste de logon único do AD do Azure com Splunk Enterprise e Splunk nuvem, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d35e8-142">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d35e8-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d35e8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d35e8-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d35e8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d35e8-145">**[Criar um usuário de teste Splunk Enterprise e nuvem Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave um equivalente de Britta Simon Splunk empresa e Splunk em nuvem que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="d35e8-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d35e8-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="d35e8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d35e8-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="d35e8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d35e8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d35e8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d35e8-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Splunk Enterprise e Splunk nuvem.</span><span class="sxs-lookup"><span data-stu-id="d35e8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="d35e8-150">**tooconfigure logon único do AD do Azure com Splunk Enterprise e nuvem Splunk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d35e8-150">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="d35e8-151">Em Olá portal do Azure, Olá **Splunk Enterprise e nuvem Splunk** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-151">In hello Azure portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d35e8-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="d35e8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

3. <span data-ttu-id="d35e8-155">Em Olá **Splunk Enterprise e o domínio de nuvem Splunk e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="d35e8-155">On hello **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="d35e8-157">a.</span><span class="sxs-lookup"><span data-stu-id="d35e8-157">a.</span></span> <span data-ttu-id="d35e8-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="d35e8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="d35e8-159">b.</span><span class="sxs-lookup"><span data-stu-id="d35e8-159">b.</span></span> <span data-ttu-id="d35e8-160">Em Olá **identificador** caixa de texto, digite a URL de saudação do servidor Splunk.</span><span class="sxs-lookup"><span data-stu-id="d35e8-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>

    <span data-ttu-id="d35e8-161">c.</span><span class="sxs-lookup"><span data-stu-id="d35e8-161">c.</span></span> <span data-ttu-id="d35e8-162">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="d35e8-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d35e8-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="d35e8-163">These values are not real.</span></span> <span data-ttu-id="d35e8-164">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="d35e8-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d35e8-165">Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação.</span><span class="sxs-lookup"><span data-stu-id="d35e8-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="d35e8-166">Entre em contato com [Splunk Enterprise e o cliente de nuvem Splunk equipe de suporte](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="d35e8-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget these values.</span></span> 

4. <span data-ttu-id="d35e8-167">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d35e8-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

5. <span data-ttu-id="d35e8-169">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d35e8-169">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d35e8-171">tooconfigure logon único no **Splunk Enterprise e nuvem Splunk** lado, você precisa toosend Olá baixado **Metadata XML** muito[daequipedesuportedoSplunkEnterpriseenuvemSplunk](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="d35e8-171">tooconfigure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need toosend hello downloaded **Metadata XML** too[Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="d35e8-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="d35e8-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d35e8-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="d35e8-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d35e8-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d35e8-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d35e8-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d35e8-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="d35e8-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d35e8-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d35e8-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d35e8-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d35e8-179">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d35e8-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d35e8-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d35e8-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d35e8-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d35e8-185">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d35e8-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d35e8-187">a.</span><span class="sxs-lookup"><span data-stu-id="d35e8-187">a.</span></span> <span data-ttu-id="d35e8-188">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d35e8-189">b.</span><span class="sxs-lookup"><span data-stu-id="d35e8-189">b.</span></span> <span data-ttu-id="d35e8-190">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d35e8-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d35e8-191">c.</span><span class="sxs-lookup"><span data-stu-id="d35e8-191">c.</span></span> <span data-ttu-id="d35e8-192">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d35e8-193">d.</span><span class="sxs-lookup"><span data-stu-id="d35e8-193">d.</span></span> <span data-ttu-id="d35e8-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="d35e8-195">Criação de um usuário de teste do Splunk Enterprise e do Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="d35e8-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="d35e8-196">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Splunk Enterprise e no Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="d35e8-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="d35e8-197">Trabalhar com [Splunk Enterprise e nuvem Splunk equipe de suporte](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) usuários Olá tooadd Olá Splunk Enterprise e plataforma de nuvem Splunk.</span><span class="sxs-lookup"><span data-stu-id="d35e8-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d35e8-198">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d35e8-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d35e8-199">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSplunk Enterprise e Splunk nuvem.</span><span class="sxs-lookup"><span data-stu-id="d35e8-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d35e8-201">**tooassign Britta Simon tooSplunk Enterprise e nuvem Splunk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d35e8-201">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="d35e8-202">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d35e8-204">Na lista de aplicativos hello, selecione **Splunk Enterprise e nuvem Splunk**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-204">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

3. <span data-ttu-id="d35e8-206">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d35e8-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d35e8-208">Click **Add** button.</span></span> <span data-ttu-id="d35e8-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d35e8-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d35e8-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="d35e8-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d35e8-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d35e8-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d35e8-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d35e8-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d35e8-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d35e8-214">Testing single sign-on</span></span>

<span data-ttu-id="d35e8-215">Nesta seção, você deve testar seu SSOonfiguration do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d35e8-215">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="d35e8-216">Quando você clica em hello Splunk Enterprise e o bloco de nuvem Splunk no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Splunk Enterprise e nuvem Splunk o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d35e8-216">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d35e8-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d35e8-217">Additional resources</span></span>

* [<span data-ttu-id="d35e8-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d35e8-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d35e8-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d35e8-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png

