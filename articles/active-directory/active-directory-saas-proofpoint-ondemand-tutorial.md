---
title: "Tutorial: integração do Azure Active Directory com o Proofpoint on Demand | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Proofpoint sob demanda."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0f9472ddc01f2c18ffc9e8d2b59a17b3b595515e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="a2465-103">Tutorial: integração do Azure Active Directory ao Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="a2465-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="a2465-104">Neste tutorial, você aprenderá como toointegrate Proofpoint sob demanda com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="a2465-104">In this tutorial, you learn how toointegrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2465-105">Integrando Proofpoint sob demanda com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2465-105">Integrating Proofpoint on Demand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a2465-106">Você pode controlar no AD do Azure que tenha acesso tooProofpoint sob demanda</span><span class="sxs-lookup"><span data-stu-id="a2465-106">You can control in Azure AD who has access tooProofpoint on Demand</span></span>
- <span data-ttu-id="a2465-107">Você pode habilitar seu usuários tooautomatically get conectado tooProofpoint sob demanda (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a2465-107">You can enable your users tooautomatically get signed-on tooProofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2465-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a2465-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a2465-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2465-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2465-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a2465-110">Prerequisites</span></span>

<span data-ttu-id="a2465-111">integração do AD do Azure de tooconfigure com Proofpoint sob demanda, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2465-111">tooconfigure Azure AD integration with Proofpoint on Demand, you need hello following items:</span></span>

- <span data-ttu-id="a2465-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a2465-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2465-113">Uma assinatura de logon único do Proofpoint on Demand habilitada</span><span class="sxs-lookup"><span data-stu-id="a2465-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2465-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a2465-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2465-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a2465-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2465-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a2465-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2465-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2465-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2465-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a2465-118">Scenario description</span></span>
<span data-ttu-id="a2465-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a2465-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2465-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="a2465-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2465-121">Adicionando Proofpoint sob demanda da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a2465-121">Adding Proofpoint on Demand from hello gallery</span></span>
2. <span data-ttu-id="a2465-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a2465-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-hello-gallery"></a><span data-ttu-id="a2465-123">Adicionando Proofpoint sob demanda da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a2465-123">Adding Proofpoint on Demand from hello gallery</span></span>
<span data-ttu-id="a2465-124">integração de saudação tooconfigure do Proofpoint sob demanda no Azure AD, é necessário tooadd Proofpoint sob demanda na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a2465-124">tooconfigure hello integration of Proofpoint on Demand into Azure AD, you need tooadd Proofpoint on Demand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a2465-125">**tooadd Proofpoint sob demanda da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a2465-125">**tooadd Proofpoint on Demand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2465-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a2465-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2465-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a2465-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a2465-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a2465-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a2465-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a2465-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a2465-133">Na caixa de pesquisa hello, digite **Proofpoint sob demanda**.</span><span class="sxs-lookup"><span data-stu-id="a2465-133">In hello search box, type **Proofpoint on Demand**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="a2465-135">No painel de resultados de saudação, selecione **Proofpoint sob demanda**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a2465-135">In hello results panel, select **Proofpoint on Demand**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2465-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a2465-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2465-138">Nesta seção, você configura e testa o logon único do Azure AD com o Proofpoint on Demand com base em uma usuária de teste chamada “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a2465-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2465-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Proofpoint sob demanda é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2465-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Proofpoint on Demand is tooa user in Azure AD.</span></span> <span data-ttu-id="a2465-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Proofpoint sob demanda precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a2465-140">In other words, a link relationship between an Azure AD user and hello related user in Proofpoint on Demand needs toobe established.</span></span>

<span data-ttu-id="a2465-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Proofpoint sob demanda.</span><span class="sxs-lookup"><span data-stu-id="a2465-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="a2465-142">teste do AD do Azure e tooconfigure o logon único com Proofpoint sob demanda, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2465-142">tooconfigure and test Azure AD single sign-on with Proofpoint on Demand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a2465-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a2465-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a2465-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2465-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2465-145">**[Criando um Proofpoint no usuário de teste de demanda](#creating-a-proofpoint-on-demand-test-user)**  -toohave um equivalente do Britta Simon em Proofpoint sob demanda que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="a2465-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - toohave a counterpart of Britta Simon in Proofpoint on Demand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2465-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="a2465-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2465-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="a2465-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2465-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2465-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2465-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu Proofpoint no aplicativo de demanda.</span><span class="sxs-lookup"><span data-stu-id="a2465-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="a2465-150">**tooconfigure AD do Azure-logon único com Proofpoint sob demanda, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a2465-150">**tooconfigure Azure AD single sign-on with Proofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2465-151">Em Olá portal do Azure, Olá **Proofpoint sob demanda** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="a2465-151">In hello Azure portal, on hello **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a2465-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="a2465-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
  
    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="a2465-155">Em Olá **Proofpoint no domínio de demanda e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2465-155">On hello **Proofpoint on Demand Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="a2465-157">Olá a.In **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="a2465-157">a.In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="a2465-158">b.</span><span class="sxs-lookup"><span data-stu-id="a2465-158">b.</span></span> <span data-ttu-id="a2465-159">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="a2465-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="a2465-160">c.</span><span class="sxs-lookup"><span data-stu-id="a2465-160">c.</span></span>  <span data-ttu-id="a2465-161">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="a2465-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a2465-162">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="a2465-162">These values are not hello real.</span></span> <span data-ttu-id="a2465-163">Atualizar esses valores com hello real identificador, a URL de resposta e a URL de logon.</span><span class="sxs-lookup"><span data-stu-id="a2465-163">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="a2465-164">Entre em contato com [Proofpoint da equipe de suporte de cliente de demanda](https://www.proofpoint.com/us/support-services) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="a2465-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooget these values.</span></span> 

4. <span data-ttu-id="a2465-165">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a2465-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="a2465-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a2465-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="a2465-169">Em Olá **Proofpoint na configuração de demanda** seção, clique em **Proofpoint configurar sob demanda** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="a2465-169">On hello **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a2465-170">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="a2465-170">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="a2465-172">tooconfigure logon único no **Proofpoint sob demanda** lado, você precisa toosend Olá baixado **Certificate(Base64)**,**ID da entidade SAML**, e **SAML URL do serviço de logon em um único** muito[Proofpoint da equipe de suporte de cliente de demanda](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="a2465-172">tooconfigure single sign-on on **Proofpoint on Demand** side, you need toosend hello downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="a2465-173">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="a2465-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a2465-174">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="a2465-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a2465-175">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2465-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2465-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a2465-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2465-177">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2465-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a2465-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a2465-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2465-180">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a2465-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2465-182">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="a2465-182">These values are not hello real.</span></span> <span data-ttu-id="a2465-183">Atualizar esses valores com hello real</span><span class="sxs-lookup"><span data-stu-id="a2465-183">Update these values with hello actual</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2465-185">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2465-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2465-187">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2465-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2465-189">a.</span><span class="sxs-lookup"><span data-stu-id="a2465-189">a.</span></span> <span data-ttu-id="a2465-190">Em Olá **nome** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a2465-190">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="a2465-191">b.</span><span class="sxs-lookup"><span data-stu-id="a2465-191">b.</span></span> <span data-ttu-id="a2465-192">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2465-192">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="a2465-193">c.</span><span class="sxs-lookup"><span data-stu-id="a2465-193">c.</span></span> <span data-ttu-id="a2465-194">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="a2465-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a2465-195">d.</span><span class="sxs-lookup"><span data-stu-id="a2465-195">d.</span></span> <span data-ttu-id="a2465-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a2465-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="a2465-197">Criar um usuário de teste do Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="a2465-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="a2465-198">Nesta seção, você cria uma usuária chamada Brenda Fernandes no Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="a2465-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="a2465-199">Trabalhar com [Proofpoint da equipe de suporte de cliente de demanda](https://www.proofpoint.com/us/support-services) tooadd usuários Olá Proofpoint na plataforma de demanda.</span><span class="sxs-lookup"><span data-stu-id="a2465-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooadd users in hello Proofpoint on Demand platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a2465-200">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a2465-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a2465-201">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooProofpoint sob demanda.</span><span class="sxs-lookup"><span data-stu-id="a2465-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProofpoint on Demand.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a2465-203">**tooassign tooProofpoint Britta Simon sob demanda, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a2465-203">**tooassign Britta Simon tooProofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2465-204">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a2465-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a2465-206">Na lista de aplicativos hello, selecione **Proofpoint sob demanda**.</span><span class="sxs-lookup"><span data-stu-id="a2465-206">In hello applications list, select **Proofpoint on Demand**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="a2465-208">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a2465-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a2465-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a2465-210">Click **Add** button.</span></span> <span data-ttu-id="a2465-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a2465-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a2465-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2465-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a2465-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a2465-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2465-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a2465-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2465-216">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a2465-216">Testing single sign-on</span></span>

<span data-ttu-id="a2465-217">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2465-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a2465-218">Quando você clica em Olá **Proofpoint sob demanda** bloco Olá painel de acesso, você deve ser conectado automaticamente em tooyour Proofpoint no aplicativo de demanda.</span><span class="sxs-lookup"><span data-stu-id="a2465-218">When you click hello **Proofpoint on Demand** tile on hello Access Panel, you should be automatically signed on tooyour Proofpoint on Demand application.</span></span>
<span data-ttu-id="a2465-219">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a2465-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="a2465-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a2465-220">Additional resources</span></span>

* [<span data-ttu-id="a2465-221">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a2465-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2465-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2465-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

