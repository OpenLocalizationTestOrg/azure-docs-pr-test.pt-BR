---
title: "Tutorial: Integração do Azure Active Directory ao Halogen Software | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e alogênio Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="49ab9-103">Tutorial: Integração do Active Directory do Azure com o Halogen Software</span><span class="sxs-lookup"><span data-stu-id="49ab9-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="49ab9-104">Neste tutorial, você aprenderá como toointegrate alogênio Software com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="49ab9-104">In this tutorial, you learn how toointegrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49ab9-105">Integração do Software alogênio com o Azure AD fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="49ab9-105">Integrating Halogen Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="49ab9-106">Você pode controlar no AD do Azure que tenha acesso tooHalogen Software</span><span class="sxs-lookup"><span data-stu-id="49ab9-106">You can control in Azure AD who has access tooHalogen Software</span></span>
- <span data-ttu-id="49ab9-107">Você pode habilitar seu usuários tooautomatically get conectado tooHalogen Software (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="49ab9-107">You can enable your users tooautomatically get signed-on tooHalogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="49ab9-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="49ab9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="49ab9-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49ab9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49ab9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="49ab9-110">Prerequisites</span></span>

<span data-ttu-id="49ab9-111">tooconfigure integração do AD do Azure com halogênio Software, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="49ab9-111">tooconfigure Azure AD integration with Halogen Software, you need hello following items:</span></span>

- <span data-ttu-id="49ab9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="49ab9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49ab9-113">Uma assinatura do Halogen Software com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="49ab9-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="49ab9-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="49ab9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="49ab9-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="49ab9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49ab9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="49ab9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="49ab9-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49ab9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49ab9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="49ab9-118">Scenario description</span></span>

<span data-ttu-id="49ab9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="49ab9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49ab9-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="49ab9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49ab9-121">Adicionar Software alogênio da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="49ab9-121">Adding Halogen Software from hello gallery</span></span>
2. <span data-ttu-id="49ab9-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="49ab9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-hello-gallery"></a><span data-ttu-id="49ab9-123">Adicionar Software alogênio da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="49ab9-123">Adding Halogen Software from hello gallery</span></span>

<span data-ttu-id="49ab9-124">integração de saudação tooconfigure do Software alogênio no AD do Azure, você precisa tooadd alogênio Software na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="49ab9-124">tooconfigure hello integration of Halogen Software into Azure AD, you need tooadd Halogen Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="49ab9-125">**tooadd Software alogênio da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="49ab9-125">**tooadd Halogen Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="49ab9-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="49ab9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="49ab9-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="49ab9-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="49ab9-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="49ab9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="49ab9-133">Na caixa de pesquisa hello, digite **alogênio Software**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-133">In hello search box, type **Halogen Software**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="49ab9-135">No painel de resultados de saudação, selecione **alogênio Software**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="49ab9-135">In hello results panel, select **Halogen Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="49ab9-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="49ab9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="49ab9-138">Nesta seção, você configura e testa o logon único do Azure AD com o Halogen Software com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="49ab9-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="49ab9-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Software alogênio é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ab9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halogen Software is tooa user in Azure AD.</span></span> <span data-ttu-id="49ab9-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Software alogênio precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="49ab9-140">In other words, a link relationship between an Azure AD user and hello related user in Halogen Software needs toobe established.</span></span>

<span data-ttu-id="49ab9-141">No Software de alogênio, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="49ab9-141">In Halogen Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="49ab9-142">tooconfigure e teste de logon único do AD do Azure com halogênio Software, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="49ab9-142">tooconfigure and test Azure AD single sign-on with Halogen Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="49ab9-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="49ab9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="49ab9-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49ab9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49ab9-145">**[Criar um usuário de teste de Software alogênio](#creating-a-halogen-software-test-user)**  -toohave um equivalente do Britta Simon no Software alogênio toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="49ab9-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in Halogen Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="49ab9-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="49ab9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49ab9-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="49ab9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="49ab9-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="49ab9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="49ab9-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo alogênio.</span><span class="sxs-lookup"><span data-stu-id="49ab9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="49ab9-150">**tooconfigure AD do Azure-logon único com o Software de alogênio, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="49ab9-150">**tooconfigure Azure AD single sign-on with Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="49ab9-151">Em Olá portal do Azure, Olá **alogênio Software** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-151">In hello Azure portal, on hello **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="49ab9-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="49ab9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="49ab9-155">Em Olá **alogênio Software domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="49ab9-155">On hello **Halogen Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="49ab9-157">a.</span><span class="sxs-lookup"><span data-stu-id="49ab9-157">a.</span></span> <span data-ttu-id="49ab9-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="49ab9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="49ab9-159">b.</span><span class="sxs-lookup"><span data-stu-id="49ab9-159">b.</span></span> <span data-ttu-id="49ab9-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="49ab9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="49ab9-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="49ab9-161">These values are not real.</span></span> <span data-ttu-id="49ab9-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="49ab9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="49ab9-163">Entre em contato com [a equipe de suporte do cliente de Software alogênio](https://support.halogensoftware.com/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="49ab9-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="49ab9-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="49ab9-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="49ab9-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="49ab9-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="49ab9-168">Em uma janela de navegador diferente, logon tooyour **alogênio Software** aplicativo como um administrador.</span><span class="sxs-lookup"><span data-stu-id="49ab9-168">In a different browser window, sign-on tooyour **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="49ab9-169">Clique em Olá **opções** guia.</span><span class="sxs-lookup"><span data-stu-id="49ab9-169">Click hello **Options** tab.</span></span> 
   
    ![O que é o Azure AD Connect][12]

8. <span data-ttu-id="49ab9-171">No painel de navegação esquerdo hello, clique em **configuração SAML**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-171">In hello left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![O que é o Azure AD Connect][13]

9. <span data-ttu-id="49ab9-173">Em Olá **configuração SAML** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="49ab9-173">On hello **SAML Configuration** page, perform hello following steps:</span></span> 

    ![O que é o Azure AD Connect][14]

     <span data-ttu-id="49ab9-175">a.</span><span class="sxs-lookup"><span data-stu-id="49ab9-175">a.</span></span> <span data-ttu-id="49ab9-176">Como **Identificador exclusivo**, selecione **NameID**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="49ab9-177">b.</span><span class="sxs-lookup"><span data-stu-id="49ab9-177">b.</span></span> <span data-ttu-id="49ab9-178">Em **Identificador exclusivo mapeia para**, selecione **Nome de usuário**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="49ab9-179">c.</span><span class="sxs-lookup"><span data-stu-id="49ab9-179">c.</span></span> <span data-ttu-id="49ab9-180">tooupload seu arquivo de metadados baixado, clique em **procurar** tooselect arquivo de saudação e, em seguida, **carregar arquivo**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-180">tooupload your downloaded metadata file, click **Browse** tooselect hello file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="49ab9-181">d.</span><span class="sxs-lookup"><span data-stu-id="49ab9-181">d.</span></span> <span data-ttu-id="49ab9-182">configuração de saudação tootest, clique em **executar teste**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-182">tootest hello configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="49ab9-183">Você precisa toowait para mensagem de saudação "*Olá SAML teste for concluído. Feche esta janela*".</span><span class="sxs-lookup"><span data-stu-id="49ab9-183">You need toowait for hello message "*hello SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="49ab9-184">Em seguida, feche a janela de navegador aberta de saudação.</span><span class="sxs-lookup"><span data-stu-id="49ab9-184">Then, close hello opened browser window.</span></span> <span data-ttu-id="49ab9-185">Olá **habilitar SAML** caixa de seleção só estará habilitada se o teste de saudação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="49ab9-185">hello **Enable SAML** checkbox is only enabled if hello test has been completed.</span></span> 
     
     <span data-ttu-id="49ab9-186">e.</span><span class="sxs-lookup"><span data-stu-id="49ab9-186">e.</span></span> <span data-ttu-id="49ab9-187">Selecione **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="49ab9-188">f.</span><span class="sxs-lookup"><span data-stu-id="49ab9-188">f.</span></span> <span data-ttu-id="49ab9-189">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="49ab9-190">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="49ab9-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="49ab9-191">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="49ab9-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="49ab9-192">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="49ab9-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="49ab9-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="49ab9-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="49ab9-194">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ab9-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="49ab9-196">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="49ab9-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="49ab9-197">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="49ab9-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49ab9-199">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49ab9-201">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="49ab9-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49ab9-203">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="49ab9-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49ab9-205">a.</span><span class="sxs-lookup"><span data-stu-id="49ab9-205">a.</span></span> <span data-ttu-id="49ab9-206">Em Olá **nome** caixa de texto Nome do tipo como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-206">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="49ab9-207">b.</span><span class="sxs-lookup"><span data-stu-id="49ab9-207">b.</span></span> <span data-ttu-id="49ab9-208">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="49ab9-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="49ab9-209">c.</span><span class="sxs-lookup"><span data-stu-id="49ab9-209">c.</span></span> <span data-ttu-id="49ab9-210">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="49ab9-211">d.</span><span class="sxs-lookup"><span data-stu-id="49ab9-211">d.</span></span> <span data-ttu-id="49ab9-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="49ab9-213">Criação de um usuário de teste do Halogen Software</span><span class="sxs-lookup"><span data-stu-id="49ab9-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="49ab9-214">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon alogênio software.</span><span class="sxs-lookup"><span data-stu-id="49ab9-214">hello objective of this section is toocreate a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="49ab9-215">**toocreate um usuário chamado Britta Simon no Software de alogênio execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="49ab9-215">**toocreate a user called Britta Simon in Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="49ab9-216">Logon tooyour **alogênio Software** aplicativo como um administrador.</span><span class="sxs-lookup"><span data-stu-id="49ab9-216">Sign on tooyour **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="49ab9-217">Clique em Olá **usuário Center** guia e, em seguida, clique em **Create User**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-217">Click hello **User Center** tab, and then click **Create User**.</span></span>
   
    ![O que é o Azure AD Connect][300]  

3. <span data-ttu-id="49ab9-219">Em Olá **novo usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="49ab9-219">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    ![O que é o Azure AD Connect][301]

    <span data-ttu-id="49ab9-221">a.</span><span class="sxs-lookup"><span data-stu-id="49ab9-221">a.</span></span> <span data-ttu-id="49ab9-222">Em Olá **nome** caixa de texto, nome do primeiro tipo de usuário hello como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-222">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>
    
    <span data-ttu-id="49ab9-223">b.</span><span class="sxs-lookup"><span data-stu-id="49ab9-223">b.</span></span> <span data-ttu-id="49ab9-224">Em Olá **Sobrenome** caixa de texto, digite sobrenome do usuário hello como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-224">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span> 

    <span data-ttu-id="49ab9-225">c.</span><span class="sxs-lookup"><span data-stu-id="49ab9-225">c.</span></span> <span data-ttu-id="49ab9-226">Em Olá **Username** caixa de texto, tipo **Britta Simon**, nome de usuário hello como Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49ab9-226">In hello **Username** textbox, type **Britta Simon**, hello user name as in hello Azure portal.</span></span>

    <span data-ttu-id="49ab9-227">d.</span><span class="sxs-lookup"><span data-stu-id="49ab9-227">d.</span></span> <span data-ttu-id="49ab9-228">Em Olá **senha** caixa de texto, digite uma senha para Britta.</span><span class="sxs-lookup"><span data-stu-id="49ab9-228">In hello **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="49ab9-229">e.</span><span class="sxs-lookup"><span data-stu-id="49ab9-229">e.</span></span> <span data-ttu-id="49ab9-230">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-230">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="49ab9-231">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="49ab9-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="49ab9-232">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHalogen Software.</span><span class="sxs-lookup"><span data-stu-id="49ab9-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHalogen Software.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="49ab9-234">**tooassign Britta Simon tooHalogen Software, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="49ab9-234">**tooassign Britta Simon tooHalogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="49ab9-235">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="49ab9-237">Na lista de aplicativos hello, selecione **alogênio Software**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-237">In hello applications list, select **Halogen Software**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="49ab9-239">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="49ab9-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="49ab9-241">Click **Add** button.</span></span> <span data-ttu-id="49ab9-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="49ab9-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="49ab9-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="49ab9-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="49ab9-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="49ab9-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49ab9-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="49ab9-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="49ab9-247">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="49ab9-247">Testing single sign-on</span></span>

<span data-ttu-id="49ab9-248">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="49ab9-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="49ab9-249">Quando você clica em bloco alogênio Software Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Software alogênio.</span><span class="sxs-lookup"><span data-stu-id="49ab9-249">When you click hello Halogen Software tile in hello Access Panel, you should get automatically signed-on tooyour Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49ab9-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="49ab9-250">Additional resources</span></span>

* [<span data-ttu-id="49ab9-251">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="49ab9-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49ab9-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49ab9-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
