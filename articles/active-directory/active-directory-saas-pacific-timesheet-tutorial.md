---
title: "Tutorial: integração do Azure Active Directory com o Pacific Timesheet | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e os horários do Pacífico."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e546e8ba-821a-4942-9545-c84b0670beab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 5fd57ff78a3a64c135f2de9895f4643b39e33bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pacific-timesheet"></a><span data-ttu-id="45d39-103">Tutorial: integração do Azure Active Directory com o Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="45d39-103">Tutorial: Azure Active Directory integration with Pacific Timesheet</span></span>

<span data-ttu-id="45d39-104">Neste tutorial, você aprenderá como toointegrate Pacífico horários com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="45d39-104">In this tutorial, you learn how toointegrate Pacific Timesheet with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="45d39-105">Integração do Pacífico horários com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="45d39-105">Integrating Pacific Timesheet with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="45d39-106">Você pode controlar no AD do Azure que tenha acesso tooPacific horários</span><span class="sxs-lookup"><span data-stu-id="45d39-106">You can control in Azure AD who has access tooPacific Timesheet</span></span>
- <span data-ttu-id="45d39-107">Você pode habilitar seu usuários tooautomatically get conectado tooPacific horários (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="45d39-107">You can enable your users tooautomatically get signed-on tooPacific Timesheet (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="45d39-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="45d39-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="45d39-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="45d39-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45d39-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="45d39-110">Prerequisites</span></span>

<span data-ttu-id="45d39-111">tooconfigure integração do AD do Azure com o quadro de horários do Pacífico, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="45d39-111">tooconfigure Azure AD integration with Pacific Timesheet, you need hello following items:</span></span>

- <span data-ttu-id="45d39-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="45d39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="45d39-113">Uma assinatura habilitada para logon único do Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="45d39-113">A Pacific Timesheet single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="45d39-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="45d39-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="45d39-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="45d39-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="45d39-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="45d39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="45d39-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45d39-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="45d39-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="45d39-118">Scenario description</span></span>
<span data-ttu-id="45d39-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="45d39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="45d39-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="45d39-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="45d39-121">Adicionando Pacífico horários da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="45d39-121">Adding Pacific Timesheet from hello gallery</span></span>
2. <span data-ttu-id="45d39-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="45d39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pacific-timesheet-from-hello-gallery"></a><span data-ttu-id="45d39-123">Adicionando Pacífico horários da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="45d39-123">Adding Pacific Timesheet from hello gallery</span></span>
<span data-ttu-id="45d39-124">integração de Olá tooconfigure do quadro de horários Pacífico no AD do Azure, você precisa tooadd horários Pacífico na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="45d39-124">tooconfigure hello integration of Pacific Timesheet into Azure AD, you need tooadd Pacific Timesheet from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="45d39-125">**tooadd Pacific horários da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="45d39-125">**tooadd Pacific Timesheet from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="45d39-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="45d39-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="45d39-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="45d39-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="45d39-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="45d39-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="45d39-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="45d39-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="45d39-133">Na caixa de pesquisa hello, digite **Pacífico horários**.</span><span class="sxs-lookup"><span data-stu-id="45d39-133">In hello search box, type **Pacific Timesheet**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_search.png)

5. <span data-ttu-id="45d39-135">No painel de resultados de saudação, selecione **Pacífico horários**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="45d39-135">In hello results panel, select **Pacific Timesheet**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="45d39-137">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="45d39-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="45d39-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Pacific Timesheet, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="45d39-138">In this section, you configure and test Azure AD single sign-on with Pacific Timesheet based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="45d39-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no quadro de horários Pacífico é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="45d39-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pacific Timesheet is tooa user in Azure AD.</span></span> <span data-ttu-id="45d39-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no quadro de horários Pacífico precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="45d39-140">In other words, a link relationship between an Azure AD user and hello related user in Pacific Timesheet needs toobe established.</span></span>

<span data-ttu-id="45d39-141">No quadro de horários do Pacífico, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="45d39-141">In Pacific Timesheet, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="45d39-142">tooconfigure e teste de logon único do AD do Azure com os horários do Pacífico, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="45d39-142">tooconfigure and test Azure AD single sign-on with Pacific Timesheet, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="45d39-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="45d39-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="45d39-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="45d39-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="45d39-145">**[Criar um usuário de teste do quadro de horários Pacífico](#creating-a-pacific-timesheet-test-user)**  -toohave um equivalente do Britta Simon no quadro de horários Pacífico que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="45d39-145">**[Creating a Pacific Timesheet test user](#creating-a-pacific-timesheet-test-user)** - toohave a counterpart of Britta Simon in Pacific Timesheet that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="45d39-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="45d39-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="45d39-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="45d39-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="45d39-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="45d39-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="45d39-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de quadro de horários do Pacífico.</span><span class="sxs-lookup"><span data-stu-id="45d39-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pacific Timesheet application.</span></span>

<span data-ttu-id="45d39-150">**tooconfigure AD do Azure-logon único com o quadro de horários do Pacífico, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="45d39-150">**tooconfigure Azure AD single sign-on with Pacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="45d39-151">Em Olá portal do Azure, Olá **Pacífico horários** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="45d39-151">In hello Azure portal, on hello **Pacific Timesheet** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="45d39-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="45d39-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_samlbase.png)

3. <span data-ttu-id="45d39-155">Em Olá **URLs e domínio de quadro de horários Pacífico** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="45d39-155">On hello **Pacific Timesheet Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_url.png)

    <span data-ttu-id="45d39-157">a.</span><span class="sxs-lookup"><span data-stu-id="45d39-157">a.</span></span> <span data-ttu-id="45d39-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="45d39-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    <span data-ttu-id="45d39-159">b.</span><span class="sxs-lookup"><span data-stu-id="45d39-159">b.</span></span> <span data-ttu-id="45d39-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="45d39-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="45d39-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="45d39-161">These values are not real.</span></span> <span data-ttu-id="45d39-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="45d39-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="45d39-163">Entre em contato com [equipe de suporte do quadro de horários Pacífico](http://www.pacifictimesheet.com/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="45d39-163">Contact [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) tooget these values.</span></span>
 
4. <span data-ttu-id="45d39-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="45d39-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_certificate.png) 

5. <span data-ttu-id="45d39-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="45d39-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="45d39-168">Em Olá **Pacífico horários configuração** seção, clique em **configurar horários de Pacífico** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="45d39-168">On hello **Pacific Timesheet Configuration** section, click **Configure Pacific Timesheet** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="45d39-169">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="45d39-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_configure.png) 

7. <span data-ttu-id="45d39-171">tooconfigure logon único no **Pacífico horários** lado, você precisa toosend Olá baixado **certificado (Base64)**, **Single Sign-On URL do serviço SAML**e  **ID da entidade SAML** muito[equipe de suporte do quadro de horários Pacífico](http://www.pacifictimesheet.com/support).</span><span class="sxs-lookup"><span data-stu-id="45d39-171">tooconfigure single sign-on on **Pacific Timesheet** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Pacific Timesheet support team](http://www.pacifictimesheet.com/support).</span></span> <span data-ttu-id="45d39-172">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="45d39-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="45d39-173">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="45d39-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="45d39-174">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="45d39-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="45d39-175">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="45d39-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="45d39-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="45d39-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="45d39-177">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="45d39-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="45d39-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="45d39-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="45d39-180">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="45d39-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="45d39-182">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="45d39-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="45d39-184">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="45d39-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="45d39-186">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="45d39-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="45d39-188">a.</span><span class="sxs-lookup"><span data-stu-id="45d39-188">a.</span></span> <span data-ttu-id="45d39-189">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="45d39-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="45d39-190">b.</span><span class="sxs-lookup"><span data-stu-id="45d39-190">b.</span></span> <span data-ttu-id="45d39-191">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="45d39-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="45d39-192">c.</span><span class="sxs-lookup"><span data-stu-id="45d39-192">c.</span></span> <span data-ttu-id="45d39-193">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="45d39-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="45d39-194">d.</span><span class="sxs-lookup"><span data-stu-id="45d39-194">d.</span></span> <span data-ttu-id="45d39-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="45d39-195">Click **Create**.</span></span>
 
### <a name="creating-a-pacific-timesheet-test-user"></a><span data-ttu-id="45d39-196">Criando um usuário de teste do Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="45d39-196">Creating a Pacific Timesheet test user</span></span>

<span data-ttu-id="45d39-197">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Pacific Timesheet.</span><span class="sxs-lookup"><span data-stu-id="45d39-197">In this section, you create a user called Britta Simon in Pacific Timesheet.</span></span> <span data-ttu-id="45d39-198">Trabalhar com [equipe de suporte do quadro de horários Pacífico](http://www.pacifictimesheet.com/support) toocreate um usuário no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="45d39-198">Work with [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) toocreate a user in hello application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="45d39-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="45d39-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="45d39-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPacific horários.</span><span class="sxs-lookup"><span data-stu-id="45d39-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPacific Timesheet.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="45d39-202">**tooassign Britta Simon tooPacific horários, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="45d39-202">**tooassign Britta Simon tooPacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="45d39-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="45d39-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="45d39-205">Na lista de aplicativos hello, selecione **Pacífico horários**.</span><span class="sxs-lookup"><span data-stu-id="45d39-205">In hello applications list, select **Pacific Timesheet**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_app.png) 

3. <span data-ttu-id="45d39-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="45d39-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="45d39-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="45d39-209">Click **Add** button.</span></span> <span data-ttu-id="45d39-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="45d39-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="45d39-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="45d39-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="45d39-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="45d39-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="45d39-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="45d39-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="45d39-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="45d39-215">Testing single sign-on</span></span>

<span data-ttu-id="45d39-216">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="45d39-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="45d39-217">Quando você clica em um bloco de horários Pacífico Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de quadro de horários do Pacífico.</span><span class="sxs-lookup"><span data-stu-id="45d39-217">When you click hello Pacific Timesheet tile in hello Access Panel, you should get automatically signed-on tooyour Pacific Timesheet application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="45d39-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="45d39-218">Additional resources</span></span>

* [<span data-ttu-id="45d39-219">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="45d39-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="45d39-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="45d39-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_203.png

