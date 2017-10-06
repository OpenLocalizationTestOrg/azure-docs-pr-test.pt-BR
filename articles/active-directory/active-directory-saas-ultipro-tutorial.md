---
title: "Tutorial: Integração do Azure Active Directory ao UltiPro | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e UltiPro."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: afc0f2b9-2eac-47ec-af04-65ed0fb0ca5a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 8cb613228893e8cbf997957452d55d0ab7939171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ultipro"></a><span data-ttu-id="e60aa-103">Tutorial: Integração do Azure Active Directory ao UltiPro</span><span class="sxs-lookup"><span data-stu-id="e60aa-103">Tutorial: Azure Active Directory integration with UltiPro</span></span>

<span data-ttu-id="e60aa-104">Neste tutorial, você aprenderá como toointegrate UltiPro com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="e60aa-104">In this tutorial, you learn how toointegrate UltiPro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e60aa-105">Integrando UltiPro com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="e60aa-105">Integrating UltiPro with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e60aa-106">Você pode controlar no AD do Azure que tenha acesso tooUltiPro</span><span class="sxs-lookup"><span data-stu-id="e60aa-106">You can control in Azure AD who has access tooUltiPro</span></span>
- <span data-ttu-id="e60aa-107">Você pode habilitar seu usuários tooautomatically get conectado tooUltiPro (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e60aa-107">You can enable your users tooautomatically get signed-on tooUltiPro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e60aa-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e60aa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e60aa-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e60aa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e60aa-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e60aa-110">Prerequisites</span></span>

<span data-ttu-id="e60aa-111">tooconfigure integração do AD do Azure com UltiPro, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="e60aa-111">tooconfigure Azure AD integration with UltiPro, you need hello following items:</span></span>

- <span data-ttu-id="e60aa-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e60aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e60aa-113">Uma assinatura do UltiPro habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="e60aa-113">A UltiPro single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e60aa-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e60aa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e60aa-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e60aa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e60aa-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e60aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e60aa-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e60aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e60aa-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e60aa-118">Scenario description</span></span>
<span data-ttu-id="e60aa-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e60aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e60aa-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="e60aa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e60aa-121">Adicionando UltiPro da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e60aa-121">Adding UltiPro from hello gallery</span></span>
2. <span data-ttu-id="e60aa-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e60aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ultipro-from-hello-gallery"></a><span data-ttu-id="e60aa-123">Adicionando UltiPro da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e60aa-123">Adding UltiPro from hello gallery</span></span>
<span data-ttu-id="e60aa-124">integração de saudação tooconfigure de UltiPro no AD do Azure, você precisa tooadd UltiPro da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e60aa-124">tooconfigure hello integration of UltiPro into Azure AD, you need tooadd UltiPro from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e60aa-125">**tooadd UltiPro da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e60aa-125">**tooadd UltiPro from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e60aa-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e60aa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e60aa-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e60aa-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e60aa-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e60aa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e60aa-133">Na caixa de pesquisa hello, digite **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-133">In hello search box, type **UltiPro**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_search.png)

5. <span data-ttu-id="e60aa-135">No painel de resultados de saudação, selecione **UltiPro**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e60aa-135">In hello results panel, select **UltiPro**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e60aa-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e60aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e60aa-138">Nesta seção, você configurará e testará o logon único do Azure AD com o UltiPro, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e60aa-138">In this section, you configure and test Azure AD single sign-on with UltiPro based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e60aa-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em UltiPro é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e60aa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UltiPro is tooa user in Azure AD.</span></span> <span data-ttu-id="e60aa-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em UltiPro precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e60aa-140">In other words, a link relationship between an Azure AD user and hello related user in UltiPro needs toobe established.</span></span>

<span data-ttu-id="e60aa-141">UltiPro, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="e60aa-141">In UltiPro, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e60aa-142">tooconfigure e teste de logon único do AD do Azure com UltiPro, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="e60aa-142">tooconfigure and test Azure AD single sign-on with UltiPro, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e60aa-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e60aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e60aa-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e60aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e60aa-145">**[Criar um usuário de teste UltiPro](#creating-a-ultipro-test-user)**  -toohave um equivalente do Britta Simon em UltiPro é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="e60aa-145">**[Creating a UltiPro test user](#creating-a-ultipro-test-user)** - toohave a counterpart of Britta Simon in UltiPro that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e60aa-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="e60aa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e60aa-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="e60aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e60aa-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e60aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e60aa-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo UltiPro.</span><span class="sxs-lookup"><span data-stu-id="e60aa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UltiPro application.</span></span>

<span data-ttu-id="e60aa-150">**tooconfigure AD do Azure-logon único com UltiPro, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e60aa-150">**tooconfigure Azure AD single sign-on with UltiPro, perform hello following steps:**</span></span>

1. <span data-ttu-id="e60aa-151">Em Olá portal do Azure, Olá **UltiPro** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-151">In hello Azure portal, on hello **UltiPro** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e60aa-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="e60aa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_samlbase.png)

3. <span data-ttu-id="e60aa-155">Em Olá **UltiPro domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e60aa-155">On hello **UltiPro Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_url.png)

    <span data-ttu-id="e60aa-157">a.</span><span class="sxs-lookup"><span data-stu-id="e60aa-157">a.</span></span> <span data-ttu-id="e60aa-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="e60aa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/`|
    | `https://<companyname>.ultiproworkplace.com?cpi=AZUREADISSSUERURL`|
    | ` https://<companyname>.ultipro.ca`|
    
    <span data-ttu-id="e60aa-159">b.</span><span class="sxs-lookup"><span data-stu-id="e60aa-159">b.</span></span> <span data-ttu-id="e60aa-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="e60aa-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/adfs/services/trust`|
    | `https://<companyname>.ultiproworkplace.com/adfs/services/trust`|
    | `https://<companyname>.ultipro.ca/adfs/services/trust`|
    
    <span data-ttu-id="e60aa-161">c.</span><span class="sxs-lookup"><span data-stu-id="e60aa-161">c.</span></span> <span data-ttu-id="e60aa-162">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="e60aa-162">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/<instancename>`|
    | `https://<companyname>.ultiproworkplace.com/<instancename>`|
    | `https://<companyname>.ultipro.ca/<instancename>`|
    
    > [!NOTE] 
    > <span data-ttu-id="e60aa-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e60aa-163">These values are not real.</span></span> <span data-ttu-id="e60aa-164">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="e60aa-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e60aa-165">Entre em contato com [equipe de suporte do cliente UltiPro](https://www.ultimatesoftware.com/ContactUs) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="e60aa-165">Contact [UltiPro Client support team](https://www.ultimatesoftware.com/ContactUs) tooget these values.</span></span> 

5. <span data-ttu-id="e60aa-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e60aa-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_certificate.png) 

6. <span data-ttu-id="e60aa-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e60aa-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ultipro-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="e60aa-170">Em Olá **UltiPro configuração** seção, clique em **configurar UltiPro** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="e60aa-170">On hello **UltiPro Configuration** section, click **Configure UltiPro** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e60aa-171">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="e60aa-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_configure.png) 

8. <span data-ttu-id="e60aa-173">tooconfigure logon único no **UltiPro** lado, você precisa toosend Olá baixado **Certificate(Base64), URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** muito[UltiPro equipe de suporte](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="e60aa-173">tooconfigure single sign-on on **UltiPro** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[UltiPro support team](https://www.ultimatesoftware.com/ContactUs).</span></span>

> [!TIP]
> <span data-ttu-id="e60aa-174">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="e60aa-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e60aa-175">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="e60aa-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e60aa-176">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e60aa-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e60aa-177">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e60aa-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="e60aa-178">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e60aa-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e60aa-180">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e60aa-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e60aa-181">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e60aa-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ultipro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e60aa-183">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ultipro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e60aa-185">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e60aa-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ultipro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e60aa-187">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e60aa-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ultipro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e60aa-189">a.</span><span class="sxs-lookup"><span data-stu-id="e60aa-189">a.</span></span> <span data-ttu-id="e60aa-190">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e60aa-191">b.</span><span class="sxs-lookup"><span data-stu-id="e60aa-191">b.</span></span> <span data-ttu-id="e60aa-192">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e60aa-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e60aa-193">c.</span><span class="sxs-lookup"><span data-stu-id="e60aa-193">c.</span></span> <span data-ttu-id="e60aa-194">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e60aa-195">d.</span><span class="sxs-lookup"><span data-stu-id="e60aa-195">d.</span></span> <span data-ttu-id="e60aa-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-196">Click **Create**.</span></span>
 
### <a name="creating-a-ultipro-test-user"></a><span data-ttu-id="e60aa-197">Criando um usuário de teste do UltiPro</span><span class="sxs-lookup"><span data-stu-id="e60aa-197">Creating a UltiPro test user</span></span>

<span data-ttu-id="e60aa-198">Nesta seção, você criará uma usuária chamada Brenda Fernandes no UltiPro.</span><span class="sxs-lookup"><span data-stu-id="e60aa-198">In this section, you create a user called Britta Simon in UltiPro.</span></span> <span data-ttu-id="e60aa-199">Trabalhar com [UltiPro a equipe de suporte](https://www.ultimatesoftware.com/ContactUs) para adicionar usuários de saudação na plataforma de UltiPro hello.</span><span class="sxs-lookup"><span data-stu-id="e60aa-199">Work with [UltiPro support team](https://www.ultimatesoftware.com/ContactUs) to add hello users in hello UltiPro platform.</span></span> <span data-ttu-id="e60aa-200">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e60aa-200">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e60aa-201">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e60aa-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e60aa-202">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooUltiPro.</span><span class="sxs-lookup"><span data-stu-id="e60aa-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUltiPro.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e60aa-204">**tooassign Britta Simon tooUltiPro, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e60aa-204">**tooassign Britta Simon tooUltiPro, perform hello following steps:**</span></span>

1. <span data-ttu-id="e60aa-205">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e60aa-207">Na lista de aplicativos hello, selecione **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-207">In hello applications list, select **UltiPro**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_app.png) 

3. <span data-ttu-id="e60aa-209">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e60aa-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e60aa-211">Click **Add** button.</span></span> <span data-ttu-id="e60aa-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e60aa-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e60aa-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="e60aa-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e60aa-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e60aa-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e60aa-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e60aa-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e60aa-217">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e60aa-217">Testing single sign-on</span></span>

<span data-ttu-id="e60aa-218">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e60aa-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="e60aa-219">Quando você clica em bloco UltiPro Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour UltiPro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e60aa-219">When you click hello UltiPro tile in hello Access Panel, you should get automatically signed-on tooyour UltiPro application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e60aa-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e60aa-220">Additional resources</span></span>

* [<span data-ttu-id="e60aa-221">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e60aa-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e60aa-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e60aa-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_203.png

