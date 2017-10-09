---
title: "Tutorial: Integração do Azure Active Directory ao Five9 Plus Adapter (CTI, Contact Center Agents) | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Five9 mais adaptador (CTI, entre em contato com os agentes Center)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="b9f0f-103">Tutorial: Integração do Azure Active Directory ao Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="b9f0f-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="b9f0f-104">Neste tutorial, você aprenderá como toointegrate Five9 Plus adaptador (CTI, entre em contato com os agentes Center) com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="b9f0f-104">In this tutorial, you learn how toointegrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9f0f-105">Integrar Five9 Plus adaptador (CTI, entre em contato com os agentes Center) com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9f0f-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9f0f-106">Você pode controlar no AD do Azure que tenha acesso tooFive9 mais adaptador (CTI, entre em contato com os agentes Center)</span><span class="sxs-lookup"><span data-stu-id="b9f0f-106">You can control in Azure AD who has access tooFive9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="b9f0f-107">Você pode habilitar seus usuários tooautomatically get conectado tooFive9 mais adaptador (CTI, entre em contato com Center agentes) (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9f0f-107">You can enable your users tooautomatically get signed-on tooFive9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9f0f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b9f0f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b9f0f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9f0f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9f0f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b9f0f-110">Prerequisites</span></span>

<span data-ttu-id="b9f0f-111">integração de tooconfigure AD do Azure com Five9 Plus adaptador (CTI, contato Center agentes), você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9f0f-111">tooconfigure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need hello following items:</span></span>

- <span data-ttu-id="b9f0f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9f0f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9f0f-113">Uma assinatura habilitada para logon único do Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="b9f0f-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9f0f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9f0f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b9f0f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9f0f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9f0f-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9f0f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9f0f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b9f0f-118">Scenario description</span></span>
<span data-ttu-id="b9f0f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9f0f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="b9f0f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9f0f-121">Adicionando Five9 Plus adaptador (CTI, entre em contato com os agentes Center) da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b9f0f-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
2. <span data-ttu-id="b9f0f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9f0f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a><span data-ttu-id="b9f0f-123">Adicionando Five9 Plus adaptador (CTI, entre em contato com os agentes Center) da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b9f0f-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
<span data-ttu-id="b9f0f-124">integração de saudação tooconfigure do Five9 mais adaptador (CTI, entre em contato com os agentes Center) no AD do Azure, você precisa tooadd Five9 Plus adaptador (CTI, entre em contato com os agentes Center) na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-124">tooconfigure hello integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9f0f-125">**tooadd Five9 Plus adaptador (CTI, entre em contato com os agentes Center) da Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b9f0f-125">**tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9f0f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9f0f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9f0f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="b9f0f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="b9f0f-133">Na caixa de pesquisa hello, digite **Five9 Plus adaptador (CTI, entre em contato com os agentes Center)**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-133">In hello search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="b9f0f-135">No painel de resultados de saudação, selecione **Five9 Plus adaptador (CTI, entre em contato com os agentes Center)**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-135">In hello results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9f0f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9f0f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9f0f-138">Nesta seção, você configura e testa o logon único do Azure AD com o Five9 Plus Adapter (CTI, Contact Center Agents), com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9f0f-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá Five9 Plus adaptador (CTI, entre em contato com os agentes Center) é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is tooa user in Azure AD.</span></span> <span data-ttu-id="b9f0f-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação Five9 Plus adaptador (CTI, entre em contato com Center agentes) deve toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-140">In other words, a link relationship between an Azure AD user and hello related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs toobe established.</span></span>

<span data-ttu-id="b9f0f-141">Five9 mais adaptador (CTI, entre em contato com os agentes Center), atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b9f0f-142">tooconfigure e teste de logon único do AD do Azure com Five9 Plus adaptador (CTI, contato Center agentes), precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9f0f-142">tooconfigure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9f0f-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9f0f-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9f0f-145">**[Criar um usuário de teste Five9 Plus adaptador (CTI, entre em contato com os agentes Center)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave um equivalente de Britta Simon Five9 Plus adaptador (CTI, entre em contato com os agentes Center) que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - toohave a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9f0f-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9f0f-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9f0f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9f0f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9f0f-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Five9 Plus adaptador (CTI, entre em contato com os agentes Center).</span><span class="sxs-lookup"><span data-stu-id="b9f0f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="b9f0f-150">**tooconfigure logon único do AD do Azure com Five9 Plus adaptador (CTI, entre em contato com os agentes Center), execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b9f0f-150">**tooconfigure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="b9f0f-151">Em Olá portal do Azure, Olá **Five9 Plus adaptador (CTI, entre em contato com os agentes Center)** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-151">In hello Azure portal, on hello **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="b9f0f-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="b9f0f-155">Em Olá **Five9 Plus adaptador (CTI, entre em contato com os agentes Center) de domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9f0f-155">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="b9f0f-157">a.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-157">a.</span></span> <span data-ttu-id="b9f0f-158">Em Olá **identificador** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="b9f0f-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>

    |    <span data-ttu-id="b9f0f-159">Ambiente</span><span class="sxs-lookup"><span data-stu-id="b9f0f-159">Environment</span></span>      |       <span data-ttu-id="b9f0f-160">URL</span><span class="sxs-lookup"><span data-stu-id="b9f0f-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="b9f0f-161">Para o “Five9 Plus Adapter for Microsoft Dynamics CRM”</span><span class="sxs-lookup"><span data-stu-id="b9f0f-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="b9f0f-162">Para o “Five9 Plus Adapter for Zendesk”</span><span class="sxs-lookup"><span data-stu-id="b9f0f-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="b9f0f-163">Para o “Five9 Plus Adapter for Agent Desktop Toolkit”</span><span class="sxs-lookup"><span data-stu-id="b9f0f-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="b9f0f-164">b.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-164">b.</span></span> <span data-ttu-id="b9f0f-165">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9f0f-165">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    |      <span data-ttu-id="b9f0f-166">Ambiente</span><span class="sxs-lookup"><span data-stu-id="b9f0f-166">Environment</span></span>     |      <span data-ttu-id="b9f0f-167">URL</span><span class="sxs-lookup"><span data-stu-id="b9f0f-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="b9f0f-168">Para o “Five9 Plus Adapter for Microsoft Dynamics CRM”</span><span class="sxs-lookup"><span data-stu-id="b9f0f-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="b9f0f-169">Para o “Five9 Plus Adapter for Zendesk”</span><span class="sxs-lookup"><span data-stu-id="b9f0f-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="b9f0f-170">Para o “Five9 Plus Adapter for Agent Desktop Toolkit”</span><span class="sxs-lookup"><span data-stu-id="b9f0f-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="b9f0f-171">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-171">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="b9f0f-173">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b9f0f-173">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9f0f-175">Em Olá **Five9 Plus adaptador (CTI, entre em contato com os agentes Center) configuração** seção, clique em **configurar Five9 Plus adaptador (CTI, entre em contato com os agentes Center)** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-175">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b9f0f-176">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="b9f0f-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="b9f0f-178">tooconfigure logon único no **Five9 Plus adaptador (CTI, entre em contato com os agentes Center)** lado, você precisa toosend Olá baixado **Certificate(Base64), URL de logout, ID de entidade de SAML e SAML Single Sign-On URL do serviço** muito[Five9 Plus (CTI, entre em contato com os agentes Center) suporte adaptadoras](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="b9f0f-178">tooconfigure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="b9f0f-179">Também Além disso, para configurar SSO adicional, siga Olá etapas de acordo com o adaptador de toohello abaixo:</span><span class="sxs-lookup"><span data-stu-id="b9f0f-179">Also additionally, for configuring SSO further please follow hello below steps according toohello adapter:</span></span>

    <span data-ttu-id="b9f0f-180">a.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-180">a.</span></span> <span data-ttu-id="b9f0f-181">Guia do Administrador do “Five9 Plus Adapter for Agent Desktop Toolkit”: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="b9f0f-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="b9f0f-182">b.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-182">b.</span></span> <span data-ttu-id="b9f0f-183">Guia do Administrador do “Five9 Plus Adapter for Microsoft Dynamics CRM”: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="b9f0f-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="b9f0f-184">c.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-184">c.</span></span> <span data-ttu-id="b9f0f-185">Guia do Administrador do “Five9 Plus Adapter for Zendesk”: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="b9f0f-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="b9f0f-186">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="b9f0f-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b9f0f-187">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b9f0f-188">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9f0f-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9f0f-189">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9f0f-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9f0f-190">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="b9f0f-192">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b9f0f-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9f0f-193">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9f0f-195">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9f0f-197">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9f0f-199">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9f0f-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9f0f-201">a.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-201">a.</span></span> <span data-ttu-id="b9f0f-202">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9f0f-203">b.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-203">b.</span></span> <span data-ttu-id="b9f0f-204">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9f0f-205">c.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-205">c.</span></span> <span data-ttu-id="b9f0f-206">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b9f0f-207">d.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-207">d.</span></span> <span data-ttu-id="b9f0f-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="b9f0f-209">Criando um usuário de teste do Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="b9f0f-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="b9f0f-210">Nesta seção, você cria um usuário chamado Brenda Fernandes no Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="b9f0f-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="b9f0f-211">Trabalhar com [Five9 Plus (CTI, entre em contato com os agentes Center) suporte adaptadoras](https://www.five9.com/about/contact) para adicionar usuários de saudação na plataforma do hello Five9 Plus adaptador (CTI, entre em contato com os agentes Center).</span><span class="sxs-lookup"><span data-stu-id="b9f0f-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add hello users in hello Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="b9f0f-212">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b9f0f-213">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9f0f-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b9f0f-214">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooFive9 além do adaptador (CTI, entre em contato com os agentes Center).</span><span class="sxs-lookup"><span data-stu-id="b9f0f-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFive9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="b9f0f-216">**tooassign Britta Simon tooFive9 Plus adaptador (CTI, entre em contato com os agentes Center), execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b9f0f-216">**tooassign Britta Simon tooFive9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="b9f0f-217">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b9f0f-219">Na lista de aplicativos hello, selecione **Five9 Plus adaptador (CTI, entre em contato com os agentes Center)**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-219">In hello applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="b9f0f-221">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="b9f0f-223">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-223">Click **Add** button.</span></span> <span data-ttu-id="b9f0f-224">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="b9f0f-226">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b9f0f-227">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9f0f-228">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9f0f-229">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="b9f0f-229">Testing single sign-on</span></span>

<span data-ttu-id="b9f0f-230">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9f0f-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b9f0f-231">Quando você clica em bloco Five9 Plus adaptador (CTI, entre em contato com os agentes Center) Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Five9 mais adaptador (CTI, entre em contato com os agentes Center).</span><span class="sxs-lookup"><span data-stu-id="b9f0f-231">When you click hello Five9 Plus Adapter (CTI, Contact Center Agents) tile in hello Access Panel, you should get automatically signed-on tooyour Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="b9f0f-232">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9f0f-232">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9f0f-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b9f0f-233">Additional resources</span></span>

* [<span data-ttu-id="b9f0f-234">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b9f0f-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9f0f-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9f0f-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

