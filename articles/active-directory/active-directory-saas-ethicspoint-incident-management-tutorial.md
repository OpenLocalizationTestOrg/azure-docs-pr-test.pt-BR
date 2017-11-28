---
title: "Tutorial: integração do Azure Active Directory ao EthicsPoint Incident Management (EPIM) | Microsoft Azure"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o gerenciamento de incidentes de EthicsPoint (EPIM)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 73ef5fab815cddb3728f4b23173f99e62aec5bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="56c96-103">Tutorial: integração do Azure Active Directory ao EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="56c96-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="56c96-104">Neste tutorial, você aprenderá como toointegrate gerenciamento de incidentes de EthicsPoint (EPIM) com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="56c96-104">In this tutorial, you learn how toointegrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56c96-105">Integração do gerenciamento de incidentes de EthicsPoint (EPIM) com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="56c96-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="56c96-106">Você pode controlar no AD do Azure que tenha acesso tooEthicsPoint gerenciamento de incidentes (EPIM)</span><span class="sxs-lookup"><span data-stu-id="56c96-106">You can control in Azure AD who has access tooEthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="56c96-107">Você pode habilitar seu usuários tooautomatically get conectado tooEthicsPoint gerenciamento de incidentes (EPIM) (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="56c96-107">You can enable your users tooautomatically get signed-on tooEthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56c96-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="56c96-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="56c96-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56c96-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56c96-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="56c96-110">Prerequisites</span></span>

<span data-ttu-id="56c96-111">tooconfigure integração do AD do Azure com o gerenciamento de incidentes de EthicsPoint (EPIM), você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="56c96-111">tooconfigure Azure AD integration with EthicsPoint Incident Management (EPIM), you need hello following items:</span></span>

- <span data-ttu-id="56c96-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="56c96-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56c96-113">Uma assinatura habilitada para logon único do EPIM (EthicsPoint Incident Management)</span><span class="sxs-lookup"><span data-stu-id="56c96-113">A EthicsPoint Incident Management (EPIM) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56c96-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="56c96-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56c96-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="56c96-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56c96-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="56c96-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56c96-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56c96-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56c96-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="56c96-118">Scenario description</span></span>
<span data-ttu-id="56c96-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="56c96-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56c96-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="56c96-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56c96-121">Adicionando o gerenciamento de incidentes de EthicsPoint (EPIM) da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="56c96-121">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
2. <span data-ttu-id="56c96-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="56c96-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ethicspoint-incident-management-epim-from-hello-gallery"></a><span data-ttu-id="56c96-123">Adicionando o gerenciamento de incidentes de EthicsPoint (EPIM) da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="56c96-123">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
<span data-ttu-id="56c96-124">integração de saudação do tooconfigure do gerenciamento de incidentes EthicsPoint (EPIM) no AD do Azure, você precisa tooadd gerenciamento de incidentes de EthicsPoint (EPIM) na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="56c96-124">tooconfigure hello integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need tooadd EthicsPoint Incident Management (EPIM) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="56c96-125">**tooadd gerenciamento de incidentes de EthicsPoint (EPIM) da Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="56c96-125">**tooadd EthicsPoint Incident Management (EPIM) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="56c96-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="56c96-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="56c96-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="56c96-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="56c96-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="56c96-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="56c96-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56c96-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="56c96-133">Na caixa de pesquisa hello, digite **EthicsPoint incidente gerenciamento (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="56c96-133">In hello search box, type **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

5. <span data-ttu-id="56c96-135">No painel de resultados de saudação, selecione **EthicsPoint incidente gerenciamento (EPIM)**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="56c96-135">In hello results panel, select **EthicsPoint Incident Management (EPIM)**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56c96-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="56c96-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56c96-138">Nesta seção, você configura e testa o logon único do Azure AD com o EPIM (EthicsPoint Incident Management), com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="56c96-138">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="56c96-139">Para toowork de logon único, o AD do Azure precisa tooknow que o usuário de contraparte Olá no gerenciamento de incidentes EthicsPoint (EPIM) é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="56c96-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EthicsPoint Incident Management (EPIM) is tooa user in Azure AD.</span></span> <span data-ttu-id="56c96-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado da saudação no gerenciamento de incidentes EthicsPoint (EPIM) precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="56c96-140">In other words, a link relationship between an Azure AD user and hello related user in EthicsPoint Incident Management (EPIM) needs toobe established.</span></span>

<span data-ttu-id="56c96-141">No gerenciamento de incidentes de EthicsPoint (EPIM), atribua o valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="56c96-141">In EthicsPoint Incident Management (EPIM), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="56c96-142">tooconfigure e teste de logon único do AD do Azure com o gerenciamento de incidentes de EthicsPoint (EPIM), você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="56c96-142">tooconfigure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="56c96-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="56c96-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="56c96-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56c96-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56c96-145">**[Criar um usuário de teste do gerenciamento de incidentes de EthicsPoint (EPIM)](#creating-a-ethicspoint-incident-management-epim-test-user)**  -toohave um equivalente de Britta Simon no gerenciamento de incidentes EthicsPoint (EPIM) que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="56c96-145">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-epim-test-user)** - toohave a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="56c96-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="56c96-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56c96-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="56c96-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56c96-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="56c96-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="56c96-149">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de gerenciamento de incidentes de EthicsPoint (EPIM).</span><span class="sxs-lookup"><span data-stu-id="56c96-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>

<span data-ttu-id="56c96-150">**tooconfigure logon único do AD do Azure com o gerenciamento de incidentes de EthicsPoint (EPIM), execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="56c96-150">**tooconfigure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="56c96-151">Em Olá portal do Azure, Olá **EthicsPoint incidente gerenciamento (EPIM)** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="56c96-151">In hello Azure portal, on hello **EthicsPoint Incident Management (EPIM)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="56c96-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="56c96-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

3. <span data-ttu-id="56c96-155">Em Olá **URLs e domínio de gerenciamento de incidentes de EthicsPoint (EPIM)** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="56c96-155">On hello **EthicsPoint Incident Management (EPIM) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    <span data-ttu-id="56c96-157">a.</span><span class="sxs-lookup"><span data-stu-id="56c96-157">a.</span></span> <span data-ttu-id="56c96-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="56c96-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    <span data-ttu-id="56c96-159">b.</span><span class="sxs-lookup"><span data-stu-id="56c96-159">b.</span></span> <span data-ttu-id="56c96-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.navexglobal.com/adfs/services/trust`</span><span class="sxs-lookup"><span data-stu-id="56c96-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.navexglobal.com/adfs/services/trust`</span></span>

    <span data-ttu-id="56c96-161">c.</span><span class="sxs-lookup"><span data-stu-id="56c96-161">c.</span></span> <span data-ttu-id="56c96-162">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<servername>.navexglobal.com/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="56c96-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56c96-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="56c96-163">These values are not real.</span></span> <span data-ttu-id="56c96-164">Atualize esses valores com URL de resposta real hello, identificador e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="56c96-164">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="56c96-165">Entre em contato com [equipe de suporte do cliente de gerenciamento de incidentes de EthicsPoint (EPIM)](http://www.navexglobal.com/company/contact-us) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="56c96-165">Contact [EthicsPoint Incident Management (EPIM) Client support team](http://www.navexglobal.com/company/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="56c96-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="56c96-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

5. <span data-ttu-id="56c96-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="56c96-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="56c96-170">tooconfigure logon único no **EthicsPoint incidente gerenciamento (EPIM)** lado, você precisa toosend Olá baixado **Metadata XML** muito[suporte de gerenciamento de incidentes de EthicsPoint (EPIM) equipe](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="56c96-170">tooconfigure single sign-on on **EthicsPoint Incident Management (EPIM)** side, you need toosend hello downloaded **Metadata XML** too[EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="56c96-171">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="56c96-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="56c96-172">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="56c96-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="56c96-173">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56c96-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56c96-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="56c96-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="56c96-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="56c96-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="56c96-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="56c96-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="56c96-178">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="56c96-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="56c96-180">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="56c96-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="56c96-182">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="56c96-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="56c96-184">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="56c96-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56c96-186">a.</span><span class="sxs-lookup"><span data-stu-id="56c96-186">a.</span></span> <span data-ttu-id="56c96-187">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56c96-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56c96-188">b.</span><span class="sxs-lookup"><span data-stu-id="56c96-188">b.</span></span> <span data-ttu-id="56c96-189">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="56c96-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56c96-190">c.</span><span class="sxs-lookup"><span data-stu-id="56c96-190">c.</span></span> <span data-ttu-id="56c96-191">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="56c96-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="56c96-192">d.</span><span class="sxs-lookup"><span data-stu-id="56c96-192">d.</span></span> <span data-ttu-id="56c96-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="56c96-193">Click **Create**.</span></span>
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="56c96-194">Criando um usuário de teste do EPIM (EthicsPoint Incident Management)</span><span class="sxs-lookup"><span data-stu-id="56c96-194">Creating a EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="56c96-195">Nesta seção, você deve criar uma usuária chamada Brenda Fernandes no EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="56c96-195">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="56c96-196">Trabalhe com [equipe de suporte de gerenciamento de incidentes de EthicsPoint (EPIM)](http://www.navexglobal.com/company/contact-us) tooadd usuários de saudação na plataforma de gerenciamento de incidentes de EthicsPoint (EPIM) hello.</span><span class="sxs-lookup"><span data-stu-id="56c96-196">Please work with [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us) tooadd hello users in hello EthicsPoint Incident Management (EPIM) platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="56c96-197">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="56c96-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="56c96-198">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooEthicsPoint gerenciamento de incidentes (EPIM).</span><span class="sxs-lookup"><span data-stu-id="56c96-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEthicsPoint Incident Management (EPIM).</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="56c96-200">**tooassign Britta Simon tooEthicsPoint incidente gerenciamento (EPIM), execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="56c96-200">**tooassign Britta Simon tooEthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="56c96-201">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="56c96-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="56c96-203">Na lista de aplicativos hello, selecione **EthicsPoint incidente gerenciamento (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="56c96-203">In hello applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

3. <span data-ttu-id="56c96-205">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="56c96-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="56c96-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="56c96-207">Click **Add** button.</span></span> <span data-ttu-id="56c96-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56c96-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="56c96-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="56c96-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="56c96-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56c96-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56c96-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56c96-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="56c96-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="56c96-213">Testing single sign-on</span></span>

<span data-ttu-id="56c96-214">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="56c96-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="56c96-215">Quando você clica em um bloco de gerenciamento de incidentes de EthicsPoint (EPIM) Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de gerenciamento de incidentes de EthicsPoint (EPIM).</span><span class="sxs-lookup"><span data-stu-id="56c96-215">When you click hello EthicsPoint Incident Management (EPIM) tile in hello Access Panel, you should get automatically signed-on tooyour EthicsPoint Incident Management (EPIM) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="56c96-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="56c96-216">Additional resources</span></span>

* [<span data-ttu-id="56c96-217">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="56c96-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56c96-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56c96-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png

