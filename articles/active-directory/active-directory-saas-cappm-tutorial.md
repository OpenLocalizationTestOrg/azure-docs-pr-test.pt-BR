---
title: "Tutorial: Integração do Azure Active Directory com o CA PPM | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e PPM de autoridade de certificação."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 571130f3be0529c986aa0d8a08e4172015cd0b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a><span data-ttu-id="91733-103">Tutorial: Integração do Azure Active Directory ao CA PPM</span><span class="sxs-lookup"><span data-stu-id="91733-103">Tutorial: Azure Active Directory integration with CA PPM</span></span>

<span data-ttu-id="91733-104">Neste tutorial, você aprenderá como toointegrate PPM de autoridade de certificação com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="91733-104">In this tutorial, you learn how toointegrate CA PPM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91733-105">Integrando PPM de autoridade de certificação do AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="91733-105">Integrating CA PPM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="91733-106">Você pode controlar no AD do Azure que tenha acesso tooCA PPM</span><span class="sxs-lookup"><span data-stu-id="91733-106">You can control in Azure AD who has access tooCA PPM</span></span>
- <span data-ttu-id="91733-107">Você pode habilitar seu usuários tooautomatically get conectado tooCA PPM (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91733-107">You can enable your users tooautomatically get signed-on tooCA PPM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91733-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="91733-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="91733-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="91733-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91733-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="91733-110">Prerequisites</span></span>

<span data-ttu-id="91733-111">tooconfigure integração do AD do Azure com PPM de autoridade de certificação, é necessário Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="91733-111">tooconfigure Azure AD integration with CA PPM, you need hello following items:</span></span>

- <span data-ttu-id="91733-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91733-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91733-113">Uma assinatura habilitada para logon único do CA PPM</span><span class="sxs-lookup"><span data-stu-id="91733-113">A CA PPM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91733-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="91733-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91733-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="91733-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91733-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="91733-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91733-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91733-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91733-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="91733-118">Scenario description</span></span>
<span data-ttu-id="91733-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="91733-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91733-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="91733-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91733-121">Adicionar autoridade de certificação PPM da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="91733-121">Adding CA PPM from hello gallery</span></span>
2. <span data-ttu-id="91733-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91733-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ca-ppm-from-hello-gallery"></a><span data-ttu-id="91733-123">Adicionar autoridade de certificação PPM da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="91733-123">Adding CA PPM from hello gallery</span></span>
<span data-ttu-id="91733-124">integração de Olá tooconfigure da autoridade de certificação PPM no AD do Azure, você precisa tooadd PPM de autoridade de certificação na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="91733-124">tooconfigure hello integration of CA PPM into Azure AD, you need tooadd CA PPM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="91733-125">**tooadd PPM de autoridade de certificação da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="91733-125">**tooadd CA PPM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="91733-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="91733-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="91733-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="91733-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="91733-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="91733-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="91733-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="91733-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="91733-133">Na caixa de pesquisa hello, digite **AC PPM**.</span><span class="sxs-lookup"><span data-stu-id="91733-133">In hello search box, type **CA PPM**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_search.png)

5. <span data-ttu-id="91733-135">No painel de resultados de saudação, selecione **AC PPM**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="91733-135">In hello results panel, select **CA PPM**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91733-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91733-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91733-138">Nesta seção, você configura e testa o logon único do Azure AD com o CA PPM, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="91733-138">In this section, you configure and test Azure AD single sign-on with CA PPM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="91733-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na autoridade de certificação PPM é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="91733-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CA PPM is tooa user in Azure AD.</span></span> <span data-ttu-id="91733-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na autoridade de certificação PPM precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="91733-140">In other words, a link relationship between an Azure AD user and hello related user in CA PPM needs toobe established.</span></span>

<span data-ttu-id="91733-141">Na autoridade de certificação PPM, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="91733-141">In CA PPM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="91733-142">tooconfigure e teste de logon único do AD do Azure com PPM de autoridade de certificação, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="91733-142">tooconfigure and test Azure AD single sign-on with CA PPM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="91733-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="91733-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="91733-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91733-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91733-145">**[Criar um usuário de teste de autoridade de certificação PPM](#creating-a-ca-ppm-test-user)**  -toohave um equivalente do Britta Simon em PPM de autoridade de certificação que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="91733-145">**[Creating a CA PPM test user](#creating-a-ca-ppm-test-user)** - toohave a counterpart of Britta Simon in CA PPM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="91733-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="91733-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91733-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="91733-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91733-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="91733-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91733-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo PPM de autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="91733-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CA PPM application.</span></span>

<span data-ttu-id="91733-150">**tooconfigure AD do Azure-logon único com PPM de autoridade de certificação, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="91733-150">**tooconfigure Azure AD single sign-on with CA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="91733-151">Em Olá portal do Azure, Olá **AC PPM** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="91733-151">In hello Azure portal, on hello **CA PPM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="91733-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="91733-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_samlbase.png)

3. <span data-ttu-id="91733-155">Em Olá **URLs e autoridade de certificação PPM domínio** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="91733-155">On hello **CA PPM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_url.png)

    <span data-ttu-id="91733-157">a.</span><span class="sxs-lookup"><span data-stu-id="91733-157">a.</span></span> <span data-ttu-id="91733-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://ca.ondemand.saml.20.post.<companyname>`</span><span class="sxs-lookup"><span data-stu-id="91733-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://ca.ondemand.saml.20.post.<companyname>`</span></span>
    
    <span data-ttu-id="91733-159">b.</span><span class="sxs-lookup"><span data-stu-id="91733-159">b.</span></span> <span data-ttu-id="91733-160">Em Olá **URL de resposta** caixa de texto, tipo:`https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="91733-160">In hello **Reply URL** textbox, type as: `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91733-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="91733-161">This value is not real.</span></span> <span data-ttu-id="91733-162">Atualize esse valor com hello identificador real.</span><span class="sxs-lookup"><span data-stu-id="91733-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="91733-163">Entre em contato com [equipe de suporte de autoridade de certificação PPM](mailto:catechnicalsupport@ca.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="91733-163">Contact [CA PPM support team](mailto:catechnicalsupport@ca.com) tooget this value.</span></span>
 
4. <span data-ttu-id="91733-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="91733-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_certificate.png) 

5. <span data-ttu-id="91733-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="91733-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cappm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91733-168">Em Olá **AC PPM configuração** seção, clique em **configurar autoridade de certificação PPM** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="91733-168">On hello **CA PPM Configuration** section, click **Configure CA PPM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="91733-169">Saudação de cópia **ID da entidade SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="91733-169">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_configure.png) 

7. <span data-ttu-id="91733-171">tooconfigure logon único no **PPM de autoridade de certificação** lado, você precisa toosend Olá baixado **Certificate(Base64)** e **ID da entidade SAML** muito[a equipe de suporte PPM de autoridade de certificação ](mailto:catechnicalsupport@ca.com).</span><span class="sxs-lookup"><span data-stu-id="91733-171">tooconfigure single sign-on on **CA PPM** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Entity ID** too[CA PPM support team](mailto:catechnicalsupport@ca.com).</span></span>

> [!TIP]
> <span data-ttu-id="91733-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="91733-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="91733-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="91733-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="91733-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91733-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91733-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91733-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="91733-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="91733-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="91733-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="91733-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="91733-179">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="91733-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cappm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91733-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="91733-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cappm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91733-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="91733-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91733-185">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="91733-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91733-187">a.</span><span class="sxs-lookup"><span data-stu-id="91733-187">a.</span></span> <span data-ttu-id="91733-188">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91733-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91733-189">b.</span><span class="sxs-lookup"><span data-stu-id="91733-189">b.</span></span> <span data-ttu-id="91733-190">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="91733-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91733-191">c.</span><span class="sxs-lookup"><span data-stu-id="91733-191">c.</span></span> <span data-ttu-id="91733-192">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="91733-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="91733-193">d.</span><span class="sxs-lookup"><span data-stu-id="91733-193">d.</span></span> <span data-ttu-id="91733-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="91733-194">Click **Create**.</span></span>
 
### <a name="creating-a-ca-ppm-test-user"></a><span data-ttu-id="91733-195">Criando um usuário de teste do CA PPM</span><span class="sxs-lookup"><span data-stu-id="91733-195">Creating a CA PPM test user</span></span>

<span data-ttu-id="91733-196">Nesta seção, você criará um usuário chamado Brenda Fernandes no CA PPM.</span><span class="sxs-lookup"><span data-stu-id="91733-196">In this section, you create a user called Britta Simon in CA PPM.</span></span> <span data-ttu-id="91733-197">Trabalhar com [equipe de suporte de autoridade de certificação PPM](mailto:catechnicalsupport@ca.com) tooadd usuários de saudação na plataforma de autoridade de certificação PPM hello.</span><span class="sxs-lookup"><span data-stu-id="91733-197">Work with [CA PPM support team](mailto:catechnicalsupport@ca.com) tooadd hello users in hello CA PPM platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="91733-198">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="91733-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="91733-199">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCA PPM.</span><span class="sxs-lookup"><span data-stu-id="91733-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCA PPM.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="91733-201">**tooassign Britta Simon tooCA PPM, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="91733-201">**tooassign Britta Simon tooCA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="91733-202">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="91733-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="91733-204">Na lista de aplicativos hello, selecione **AC PPM**.</span><span class="sxs-lookup"><span data-stu-id="91733-204">In hello applications list, select **CA PPM**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_app.png) 

3. <span data-ttu-id="91733-206">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="91733-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="91733-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="91733-208">Click **Add** button.</span></span> <span data-ttu-id="91733-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="91733-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="91733-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="91733-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="91733-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="91733-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91733-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="91733-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91733-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="91733-214">Testing single sign-on</span></span>

<span data-ttu-id="91733-215">Nesta seção, você deve testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="91733-215">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="91733-216">Quando você clica em bloco CA PPM Olá Olá painel de acesso, você deve obter um aplicativo de autoridade de certificação PPM tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="91733-216">When you click hello CA PPM tile in hello Access Panel, you should get automatically signed-on tooyour CA PPM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91733-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="91733-217">Additional resources</span></span>

* [<span data-ttu-id="91733-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="91733-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91733-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91733-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_203.png

