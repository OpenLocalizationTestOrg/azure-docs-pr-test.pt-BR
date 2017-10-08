---
title: "Tutorial: Integração do Azure Active Directory ao UNIFI | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e UNIFI."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: af7cc1167b5c0cff2a1f4cdaa8a2b93f5a718f81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="d3775-103">Tutorial: Integração do Azure Active Directory ao UNIFI</span><span class="sxs-lookup"><span data-stu-id="d3775-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="d3775-104">Neste tutorial, você aprenderá como toointegrate UNIFI com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d3775-104">In this tutorial, you learn how toointegrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3775-105">Integrando UNIFI com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3775-105">Integrating UNIFI with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d3775-106">Você pode controlar no AD do Azure que tenha acesso tooUNIFI</span><span class="sxs-lookup"><span data-stu-id="d3775-106">You can control in Azure AD who has access tooUNIFI</span></span>
- <span data-ttu-id="d3775-107">Você pode habilitar seu usuários tooautomatically get conectado tooUNIFI (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3775-107">You can enable your users tooautomatically get signed-on tooUNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3775-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d3775-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d3775-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d3775-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3775-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d3775-110">Prerequisites</span></span>

<span data-ttu-id="d3775-111">tooconfigure integração do AD do Azure com UNIFI, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3775-111">tooconfigure Azure AD integration with UNIFI, you need hello following items:</span></span>

- <span data-ttu-id="d3775-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3775-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3775-113">Uma assinatura habilitada para logon único do UNIFI</span><span class="sxs-lookup"><span data-stu-id="d3775-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3775-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d3775-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3775-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d3775-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3775-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d3775-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3775-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3775-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3775-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d3775-118">Scenario description</span></span>
<span data-ttu-id="d3775-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d3775-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3775-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="d3775-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3775-121">Adicionando UNIFI da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d3775-121">Adding UNIFI from hello gallery</span></span>
2. <span data-ttu-id="d3775-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3775-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-hello-gallery"></a><span data-ttu-id="d3775-123">Adicionando UNIFI da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d3775-123">Adding UNIFI from hello gallery</span></span>
<span data-ttu-id="d3775-124">integração de saudação tooconfigure de UNIFI no AD do Azure, você precisa tooadd UNIFI da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d3775-124">tooconfigure hello integration of UNIFI into Azure AD, you need tooadd UNIFI from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d3775-125">**tooadd UNIFI da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d3775-125">**tooadd UNIFI from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3775-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d3775-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3775-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d3775-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d3775-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d3775-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d3775-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d3775-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d3775-133">Na caixa de pesquisa hello, digite **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="d3775-133">In hello search box, type **UNIFI**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="d3775-135">No painel de resultados de saudação, selecione **UNIFI**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d3775-135">In hello results panel, select **UNIFI**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3775-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3775-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3775-138">Nesta seção, você configurará e testará o logon único do Azure AD com o UNIFI, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d3775-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d3775-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em UNIFI é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3775-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UNIFI is tooa user in Azure AD.</span></span> <span data-ttu-id="d3775-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em UNIFI precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d3775-140">In other words, a link relationship between an Azure AD user and hello related user in UNIFI needs toobe established.</span></span>

<span data-ttu-id="d3775-141">UNIFI, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3775-141">In UNIFI, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d3775-142">tooconfigure e teste de logon único do AD do Azure com UNIFI, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3775-142">tooconfigure and test Azure AD single sign-on with UNIFI, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d3775-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d3775-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d3775-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3775-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3775-145">**[Criando um UNIFI testar usuário](#creating-a-unifi-test-user)**  -toohave um equivalente do Britta Simon em UNIFI é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="d3775-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - toohave a counterpart of Britta Simon in UNIFI that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3775-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="d3775-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3775-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="d3775-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3775-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3775-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3775-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo UNIFI.</span><span class="sxs-lookup"><span data-stu-id="d3775-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="d3775-150">**tooconfigure AD do Azure-logon único com UNIFI, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d3775-150">**tooconfigure Azure AD single sign-on with UNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3775-151">Em Olá portal do Azure, Olá **UNIFI** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="d3775-151">In hello Azure portal, on hello **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d3775-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="d3775-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="d3775-155">Em Olá **UNIFI domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="d3775-155">On hello **UNIFI Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="d3775-157">Em Olá **identificador** caixa de texto, o valor de saudação do tipo:`INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="d3775-157">In hello **Identifier** textbox, type hello value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="d3775-158">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="d3775-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="d3775-160">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="d3775-160">In hello **Sign-on URL** textbox, type hello URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="d3775-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d3775-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="d3775-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d3775-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="d3775-165">Em Olá **UNIFI configuração** seção, clique em **configurar UNIFI** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="d3775-165">On hello **UNIFI Configuration** section, click **Configure UNIFI** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d3775-166">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="d3775-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="d3775-168">Em uma janela de navegador web diferente, logon tooyour **UNIFI** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="d3775-168">In a different web browser window, sign on tooyour **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="d3775-169">Clique em Olá **usuários**.</span><span class="sxs-lookup"><span data-stu-id="d3775-169">Click on hello **Users**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="d3775-171">Clique em Olá **adicionar novo provedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="d3775-171">Click on hello **Add New Identity Provider**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="d3775-173">Em Olá **Adicionar provedor de identidade** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3775-173">In hello **Add Identity Provider** section, perform hello following steps:</span></span>   

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="d3775-175">a.</span><span class="sxs-lookup"><span data-stu-id="d3775-175">a.</span></span> <span data-ttu-id="d3775-176">Em Olá **nome do provedor** caixa de texto Nome do tipo hello de saudação provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="d3775-176">In hello **Provider Name** textbox, type hello name of hello Identity Provider..</span></span>

    <span data-ttu-id="d3775-177">b.</span><span class="sxs-lookup"><span data-stu-id="d3775-177">b.</span></span> <span data-ttu-id="d3775-178">Em Olá Olá **URL do provedor** textbox colar Olá **Single Sign-On URL do serviço SAML** valor que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3775-178">In hello hello **Provider URL** textbox paste hello **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d3775-179">c.</span><span class="sxs-lookup"><span data-stu-id="d3775-179">c.</span></span> <span data-ttu-id="d3775-180">Abra Olá certificado que você baixou do hello portal do Azure no bloco de notas, remova Olá **---iniciar certificado---** e **---concluir certificado---** marca e cole Olá restantes conteúdo Olá **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="d3775-180">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Certificate** textbox.</span></span>

    <span data-ttu-id="d3775-181">d.</span><span class="sxs-lookup"><span data-stu-id="d3775-181">d.</span></span> <span data-ttu-id="d3775-182">Selecione Olá **é o provedor padrão** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="d3775-182">Select hello **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="d3775-183">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="d3775-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d3775-184">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="d3775-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d3775-185">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d3775-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3775-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3775-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3775-187">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3775-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d3775-189">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d3775-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3775-190">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d3775-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3775-192">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="d3775-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3775-194">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3775-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3775-196">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3775-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3775-198">a.</span><span class="sxs-lookup"><span data-stu-id="d3775-198">a.</span></span> <span data-ttu-id="d3775-199">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3775-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3775-200">b.</span><span class="sxs-lookup"><span data-stu-id="d3775-200">b.</span></span> <span data-ttu-id="d3775-201">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d3775-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3775-202">c.</span><span class="sxs-lookup"><span data-stu-id="d3775-202">c.</span></span> <span data-ttu-id="d3775-203">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="d3775-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d3775-204">d.</span><span class="sxs-lookup"><span data-stu-id="d3775-204">d.</span></span> <span data-ttu-id="d3775-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d3775-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="d3775-206">Criação um usuário de teste do UNIFI</span><span class="sxs-lookup"><span data-stu-id="d3775-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="d3775-207">Nesta seção, você criará uma usuária chamada Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d3775-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="d3775-208">O **UNIFI** dá suporte ao provisionamento de usuário automático para que não seja necessária nenhuma etapa manual.</span><span class="sxs-lookup"><span data-stu-id="d3775-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="d3775-209">Os usuários são criados automaticamente após a autenticação bem-sucedida de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3775-209">Users are created automatically after successful authentication from hello Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d3775-210">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3775-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d3775-211">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooUNIFI.</span><span class="sxs-lookup"><span data-stu-id="d3775-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUNIFI.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d3775-213">**tooassign Britta Simon tooUNIFI, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d3775-213">**tooassign Britta Simon tooUNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3775-214">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d3775-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d3775-216">Na lista de aplicativos hello, selecione **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="d3775-216">In hello applications list, select **UNIFI**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="d3775-218">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d3775-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d3775-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d3775-220">Click **Add** button.</span></span> <span data-ttu-id="d3775-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d3775-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d3775-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3775-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d3775-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d3775-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3775-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d3775-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3775-226">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d3775-226">Testing single sign-on</span></span>

<span data-ttu-id="d3775-227">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3775-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d3775-228">Quando você clica em Olá UNIFI bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de UNIFI.</span><span class="sxs-lookup"><span data-stu-id="d3775-228">When you click hello UNIFI tile in hello Access Panel, you should get automatically signed-on tooyour UNIFI application.</span></span>
<span data-ttu-id="d3775-229">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d3775-229">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d3775-230">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d3775-230">Additional resources</span></span>

* [<span data-ttu-id="d3775-231">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d3775-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3775-232">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d3775-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

