---
title: "Tutorial: integração do Azure Active Directory com o Workfront | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Workfront."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: e7249b9ec769f19cf5aa7d44ff6f58705df4020a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="576b6-103">Tutorial: integração do Azure Active Directory com o Workfront</span><span class="sxs-lookup"><span data-stu-id="576b6-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="576b6-104">Neste tutorial, você aprenderá como toointegrate Workfront com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="576b6-104">In this tutorial, you learn how toointegrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="576b6-105">Integrando Workfront com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="576b6-105">Integrating Workfront with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="576b6-106">Você pode controlar no AD do Azure que tenha acesso tooWorkfront</span><span class="sxs-lookup"><span data-stu-id="576b6-106">You can control in Azure AD who has access tooWorkfront</span></span>
- <span data-ttu-id="576b6-107">Você pode habilitar seu usuários tooautomatically get conectado tooWorkfront (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="576b6-107">You can enable your users tooautomatically get signed-on tooWorkfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="576b6-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="576b6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="576b6-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="576b6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="576b6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="576b6-110">Prerequisites</span></span>

<span data-ttu-id="576b6-111">tooconfigure integração do AD do Azure com Workfront, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="576b6-111">tooconfigure Azure AD integration with Workfront, you need hello following items:</span></span>

- <span data-ttu-id="576b6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="576b6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="576b6-113">Uma assinatura do Workfront com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="576b6-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="576b6-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="576b6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="576b6-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="576b6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="576b6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="576b6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="576b6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="576b6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="576b6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="576b6-118">Scenario description</span></span>
<span data-ttu-id="576b6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="576b6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="576b6-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="576b6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="576b6-121">Adicionando Workfront da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="576b6-121">Adding Workfront from hello gallery</span></span>
2. <span data-ttu-id="576b6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="576b6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-hello-gallery"></a><span data-ttu-id="576b6-123">Adicionando Workfront da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="576b6-123">Adding Workfront from hello gallery</span></span>
<span data-ttu-id="576b6-124">integração de saudação tooconfigure de Workfront no AD do Azure, você precisa tooadd Workfront da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="576b6-124">tooconfigure hello integration of Workfront into Azure AD, you need tooadd Workfront from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="576b6-125">**tooadd Workfront da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="576b6-125">**tooadd Workfront from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="576b6-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="576b6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="576b6-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="576b6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="576b6-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="576b6-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="576b6-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="576b6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="576b6-133">Na caixa de pesquisa hello, digite **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="576b6-133">In hello search box, type **Workfront**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="576b6-135">No painel de resultados de saudação, selecione **Workfront**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="576b6-135">In hello results panel, select **Workfront**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="576b6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="576b6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="576b6-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o Workfront com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="576b6-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="576b6-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Workfront é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="576b6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workfront is tooa user in Azure AD.</span></span> <span data-ttu-id="576b6-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Workfront precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="576b6-140">In other words, a link relationship between an Azure AD user and hello related user in Workfront needs toobe established.</span></span>

<span data-ttu-id="576b6-141">Workfront, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="576b6-141">In Workfront, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="576b6-142">tooconfigure e teste de logon único do AD do Azure com Workfront, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="576b6-142">tooconfigure and test Azure AD single sign-on with Workfront, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="576b6-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="576b6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="576b6-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="576b6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="576b6-145">**[Criar um usuário de teste Workfront](#creating-a-workfront-test-user)**  -toohave um equivalente do Britta Simon em Workfront é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="576b6-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - toohave a counterpart of Britta Simon in Workfront that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="576b6-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="576b6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="576b6-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="576b6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="576b6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="576b6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="576b6-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Workfront.</span><span class="sxs-lookup"><span data-stu-id="576b6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="576b6-150">**tooconfigure AD do Azure-logon único com Workfront, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="576b6-150">**tooconfigure Azure AD single sign-on with Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="576b6-151">Em Olá portal do Azure, Olá **Workfront** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="576b6-151">In hello Azure portal, on hello **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="576b6-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="576b6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="576b6-155">Em Olá **Workfront domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="576b6-155">On hello **Workfront Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="576b6-157">a.</span><span class="sxs-lookup"><span data-stu-id="576b6-157">a.</span></span> <span data-ttu-id="576b6-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="576b6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="576b6-159">b.</span><span class="sxs-lookup"><span data-stu-id="576b6-159">b.</span></span> <span data-ttu-id="576b6-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="576b6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="576b6-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="576b6-161">These values are not real.</span></span> <span data-ttu-id="576b6-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="576b6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="576b6-163">Entre em contato com [equipe de suporte do cliente Workfront](https://www.workfront.com/contact-us/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="576b6-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="576b6-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="576b6-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="576b6-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="576b6-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="576b6-168">Em Olá **Workfront configuração** seção, clique em **configurar Workfront** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="576b6-168">On hello **Workfront Configuration** section, click **Configure Workfront** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="576b6-169">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="576b6-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="576b6-171">Site de empresa de Workfront tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="576b6-171">Sign-on tooyour Workfront company site as administrator.</span></span>

8. <span data-ttu-id="576b6-172">Vá muito**logon único na configuração**.</span><span class="sxs-lookup"><span data-stu-id="576b6-172">Go too**Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="576b6-173">Em Olá **Single Sign-On** caixa de diálogo, executar Olá etapas</span><span class="sxs-lookup"><span data-stu-id="576b6-173">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
    
    ![Configurar Logon Único][23]
   
    <span data-ttu-id="576b6-175">a.</span><span class="sxs-lookup"><span data-stu-id="576b6-175">a.</span></span> <span data-ttu-id="576b6-176">Como **Tipo**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="576b6-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="576b6-177">b.</span><span class="sxs-lookup"><span data-stu-id="576b6-177">b.</span></span> <span data-ttu-id="576b6-178">Selecione **ID do Provedor de Serviços**.</span><span class="sxs-lookup"><span data-stu-id="576b6-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="576b6-179">c.</span><span class="sxs-lookup"><span data-stu-id="576b6-179">c.</span></span> <span data-ttu-id="576b6-180">Saudação de colar **Single Sign-On URL do serviço SAML** em Olá **URL de logon do Portal** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="576b6-180">Paste hello **SAML Single Sign-On Service URL** into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="576b6-181">d.</span><span class="sxs-lookup"><span data-stu-id="576b6-181">d.</span></span> <span data-ttu-id="576b6-182">Colar **URL do serviço de logon único** em Olá **URL de logout** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="576b6-182">Paste **Single Sign-Out Service URL** into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="576b6-183">e.</span><span class="sxs-lookup"><span data-stu-id="576b6-183">e.</span></span> <span data-ttu-id="576b6-184">Colar **alterar a URL da senha** em Olá **alterar a URL da senha** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="576b6-184">Paste **Change Password URL** into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="576b6-185">f.</span><span class="sxs-lookup"><span data-stu-id="576b6-185">f.</span></span> <span data-ttu-id="576b6-186">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="576b6-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="576b6-187">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="576b6-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="576b6-188">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="576b6-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="576b6-189">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="576b6-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="576b6-190">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="576b6-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="576b6-191">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="576b6-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="576b6-193">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="576b6-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="576b6-194">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="576b6-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="576b6-196">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="576b6-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="576b6-198">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="576b6-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="576b6-200">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="576b6-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="576b6-202">a.</span><span class="sxs-lookup"><span data-stu-id="576b6-202">a.</span></span> <span data-ttu-id="576b6-203">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="576b6-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="576b6-204">b.</span><span class="sxs-lookup"><span data-stu-id="576b6-204">b.</span></span> <span data-ttu-id="576b6-205">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="576b6-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="576b6-206">c.</span><span class="sxs-lookup"><span data-stu-id="576b6-206">c.</span></span> <span data-ttu-id="576b6-207">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="576b6-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="576b6-208">d.</span><span class="sxs-lookup"><span data-stu-id="576b6-208">d.</span></span> <span data-ttu-id="576b6-209">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="576b6-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="576b6-210">Criar um usuário de teste do Workfront</span><span class="sxs-lookup"><span data-stu-id="576b6-210">Creating a Workfront test user</span></span>

<span data-ttu-id="576b6-211">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Workfront.</span><span class="sxs-lookup"><span data-stu-id="576b6-211">hello objective of this section is toocreate a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="576b6-212">**toocreate um usuário chamado Britta Simon no Workfront, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="576b6-212">**toocreate a user called Britta Simon in Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="576b6-213">Faça logon no tooyour Workfront site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="576b6-213">Sign on tooyour Workfront company site as administrator.</span></span>
2. <span data-ttu-id="576b6-214">No menu de saudação na parte superior de saudação, clique em **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="576b6-214">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="576b6-215">Clique em **Nova Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="576b6-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="576b6-216">Na caixa de diálogo de nova pessoa hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="576b6-216">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Criar um usuário de teste do Workfront][21] 
   
    <span data-ttu-id="576b6-218">a.</span><span class="sxs-lookup"><span data-stu-id="576b6-218">a.</span></span> <span data-ttu-id="576b6-219">Em Olá **nome** caixa de texto, digite "Britta".</span><span class="sxs-lookup"><span data-stu-id="576b6-219">In hello **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="576b6-220">b.</span><span class="sxs-lookup"><span data-stu-id="576b6-220">b.</span></span> <span data-ttu-id="576b6-221">Em Olá **Sobrenome** caixa de texto, digite "Simon".</span><span class="sxs-lookup"><span data-stu-id="576b6-221">In hello **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="576b6-222">c.</span><span class="sxs-lookup"><span data-stu-id="576b6-222">c.</span></span> <span data-ttu-id="576b6-223">Em Olá **endereço de Email** caixa de texto, digite o endereço de email Britta Simon no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="576b6-223">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="576b6-224">d.</span><span class="sxs-lookup"><span data-stu-id="576b6-224">d.</span></span> <span data-ttu-id="576b6-225">Clique em **Adicionar Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="576b6-225">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="576b6-226">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="576b6-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="576b6-227">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWorkfront.</span><span class="sxs-lookup"><span data-stu-id="576b6-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkfront.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="576b6-229">**tooassign Britta Simon tooWorkfront, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="576b6-229">**tooassign Britta Simon tooWorkfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="576b6-230">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="576b6-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="576b6-232">Na lista de aplicativos hello, selecione **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="576b6-232">In hello applications list, select **Workfront**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="576b6-234">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="576b6-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="576b6-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="576b6-236">Click **Add** button.</span></span> <span data-ttu-id="576b6-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="576b6-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="576b6-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="576b6-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="576b6-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="576b6-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="576b6-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="576b6-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="576b6-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="576b6-242">Testing single sign-on</span></span>

<span data-ttu-id="576b6-243">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="576b6-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="576b6-244">Quando você clica em bloco Workfront Olá Olá painel de acesso, você deve obter a página de logon do aplicativo Workfront.</span><span class="sxs-lookup"><span data-stu-id="576b6-244">When you click hello Workfront tile in hello Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="576b6-245">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="576b6-245">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="576b6-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="576b6-246">Additional resources</span></span>

* [<span data-ttu-id="576b6-247">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="576b6-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="576b6-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="576b6-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

