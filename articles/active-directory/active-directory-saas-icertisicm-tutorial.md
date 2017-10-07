---
title: "Tutorial: integração do Azure Active Directory com o Icertis Contract Management Platform | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e plataforma de gerenciamento de contrato de Icertis."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 6eb99553ef9df732512a38fb0489e66b41ba94a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icertis-contract-management-platform"></a><span data-ttu-id="c4558-103">Tutorial: integração do Azure Active Directory com o Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="c4558-103">Tutorial: Azure Active Directory integration with Icertis Contract Management Platform</span></span>

<span data-ttu-id="c4558-104">Neste tutorial, você aprenderá como toointegrate Icertis plataforma de gerenciamento de contrato com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c4558-104">In this tutorial, you learn how toointegrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4558-105">Integrando Icertis plataforma de gerenciamento de contrato com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4558-105">Integrating Icertis Contract Management Platform with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c4558-106">Você pode controlar no AD do Azure que tenha acesso tooIcertis plataforma de gerenciamento de contrato</span><span class="sxs-lookup"><span data-stu-id="c4558-106">You can control in Azure AD who has access tooIcertis Contract Management Platform</span></span>
- <span data-ttu-id="c4558-107">Você pode habilitar seus usuários tooautomatically get conectado tooIcertis plataforma de gerenciamento de contrato (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4558-107">You can enable your users tooautomatically get signed-on tooIcertis Contract Management Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4558-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c4558-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c4558-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4558-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4558-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c4558-110">Prerequisites</span></span>

<span data-ttu-id="c4558-111">tooconfigure integração do AD do Azure com a plataforma de gerenciamento de contrato Icertis, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4558-111">tooconfigure Azure AD integration with Icertis Contract Management Platform, you need hello following items:</span></span>

- <span data-ttu-id="c4558-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4558-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4558-113">Uma assinatura com logon único habilitado da Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="c4558-113">An Icertis Contract Management Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4558-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c4558-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4558-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c4558-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4558-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c4558-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4558-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4558-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4558-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c4558-118">Scenario description</span></span>
<span data-ttu-id="c4558-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c4558-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4558-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c4558-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4558-121">Adicionando Icertis plataforma de gerenciamento de contrato da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c4558-121">Adding Icertis Contract Management Platform from hello gallery</span></span>
2. <span data-ttu-id="c4558-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4558-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icertis-contract-management-platform-from-hello-gallery"></a><span data-ttu-id="c4558-123">Adicionando Icertis plataforma de gerenciamento de contrato da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c4558-123">Adding Icertis Contract Management Platform from hello gallery</span></span>
<span data-ttu-id="c4558-124">integração de Olá tooconfigure da plataforma de gerenciamento de contrato Icertis no AD do Azure, você precisa tooadd Icertis plataforma de gerenciamento de contrato na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c4558-124">tooconfigure hello integration of Icertis Contract Management Platform into Azure AD, you need tooadd Icertis Contract Management Platform from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c4558-125">**tooadd Icertis plataforma de gerenciamento de contrato da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4558-125">**tooadd Icertis Contract Management Platform from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4558-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c4558-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4558-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c4558-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c4558-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c4558-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c4558-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4558-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c4558-133">Na caixa de pesquisa hello, digite **plataforma de gerenciamento de contrato Icertis**.</span><span class="sxs-lookup"><span data-stu-id="c4558-133">In hello search box, type **Icertis Contract Management Platform**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_search.png)

5. <span data-ttu-id="c4558-135">No painel de resultados de saudação, selecione **plataforma de gerenciamento de contrato Icertis**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c4558-135">In hello results panel, select **Icertis Contract Management Platform**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4558-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4558-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4558-138">Nesta seção, você configurará e testará o logon único do Azure AD com a Icertis Contract Management Platform com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c4558-138">In this section, you configure and test Azure AD single sign-on with Icertis Contract Management Platform based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c4558-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na plataforma de gerenciamento de contrato Icertis é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4558-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Icertis Contract Management Platform is tooa user in Azure AD.</span></span> <span data-ttu-id="c4558-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na plataforma de gerenciamento de contrato Icertis precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c4558-140">In other words, a link relationship between an Azure AD user and hello related user in Icertis Contract Management Platform needs toobe established.</span></span>

<span data-ttu-id="c4558-141">Na plataforma de gerenciamento de contrato Icertis, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4558-141">In Icertis Contract Management Platform, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c4558-142">tooconfigure e teste de logon único do AD do Azure com a plataforma de gerenciamento de contrato Icertis, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4558-142">tooconfigure and test Azure AD single sign-on with Icertis Contract Management Platform, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c4558-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c4558-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c4558-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4558-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4558-145">**[Criar um usuário de teste de plataforma de gerenciamento de contrato Icertis](#creating-an-icertis-contract-management-platform-test-user)**  -toohave um equivalente do Britta Simon na plataforma de gerenciamento do contrato Icertis é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c4558-145">**[Creating an Icertis Contract Management Platform test user](#creating-an-icertis-contract-management-platform-test-user)** - toohave a counterpart of Britta Simon in Icertis Contract Management Platform that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4558-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c4558-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4558-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c4558-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4558-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4558-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4558-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de plataforma de gerenciamento Icertis contrato.</span><span class="sxs-lookup"><span data-stu-id="c4558-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Icertis Contract Management Platform application.</span></span>

<span data-ttu-id="c4558-150">**tooconfigure logon único do AD do Azure com a plataforma de gerenciamento de contrato Icertis execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4558-150">**tooconfigure Azure AD single sign-on with Icertis Contract Management Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4558-151">Em Olá portal do Azure, Olá **plataforma de gerenciamento de contrato Icertis** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c4558-151">In hello Azure portal, on hello **Icertis Contract Management Platform** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c4558-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c4558-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_samlbase.png)

3. <span data-ttu-id="c4558-155">Em Olá **Icertis domínio de plataforma de gerenciamento de contrato e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4558-155">On hello **Icertis Contract Management Platform Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_url.png)

    <span data-ttu-id="c4558-157">a.</span><span class="sxs-lookup"><span data-stu-id="c4558-157">a.</span></span> <span data-ttu-id="c4558-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="c4558-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.icertis.com`</span></span>

    <span data-ttu-id="c4558-159">b.</span><span class="sxs-lookup"><span data-stu-id="c4558-159">b.</span></span> <span data-ttu-id="c4558-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="c4558-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.icertis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4558-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c4558-161">These values are not real.</span></span> <span data-ttu-id="c4558-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="c4558-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c4558-163">Entre em contato com [equipe de suporte do cliente de plataforma de gerenciamento de contrato Icertis](https://www.icertis.com/company/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="c4558-163">Contact [Icertis Contract Management Platform Client support team](https://www.icertis.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="c4558-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c4558-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_certificate.png) 

5. <span data-ttu-id="c4558-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c4558-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-icertisicm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4558-168">Em Olá **configuração de plataforma de gerenciamento de contrato Icertis** seção, clique em **configurar a plataforma de gerenciamento de contrato Icertis** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="c4558-168">On hello **Icertis Contract Management Platform Configuration** section, click **Configure Icertis Contract Management Platform** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c4558-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c4558-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_configure.png) 

7. <span data-ttu-id="c4558-171">tooconfigure logon único no **plataforma de gerenciamento de contrato Icertis** lado, você precisa toosend Olá baixado **Metadata XML** e **URL de logout, ID de entidade de SAML e logon único SAML URL do serviço** muito[equipe de suporte de plataforma de gerenciamento de contrato Icertis](https://www.icertis.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="c4558-171">tooconfigure single sign-on on **Icertis Contract Management Platform** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="c4558-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c4558-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c4558-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c4558-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c4558-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4558-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4558-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4558-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4558-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4558-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c4558-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4558-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4558-179">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c4558-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4558-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c4558-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4558-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4558-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4558-185">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4558-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4558-187">a.</span><span class="sxs-lookup"><span data-stu-id="c4558-187">a.</span></span> <span data-ttu-id="c4558-188">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4558-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4558-189">b.</span><span class="sxs-lookup"><span data-stu-id="c4558-189">b.</span></span> <span data-ttu-id="c4558-190">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c4558-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4558-191">c.</span><span class="sxs-lookup"><span data-stu-id="c4558-191">c.</span></span> <span data-ttu-id="c4558-192">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c4558-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c4558-193">d.</span><span class="sxs-lookup"><span data-stu-id="c4558-193">d.</span></span> <span data-ttu-id="c4558-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c4558-194">Click **Create**.</span></span>
 
### <a name="creating-an-icertis-contract-management-platform-test-user"></a><span data-ttu-id="c4558-195">Como criar um usuário de teste da Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="c4558-195">Creating an Icertis Contract Management Platform test user</span></span>

<span data-ttu-id="c4558-196">Nesta seção, você deve criar uma usuária chamada Brenda Fernandes no Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="c4558-196">In this section, you create a user called Britta Simon in Icertis Contract Management Platform.</span></span> <span data-ttu-id="c4558-197">Trabalhe com [equipe de suporte de plataforma de gerenciamento de contrato Icertis](https://www.icertis.com/company/contact/) tooadd usuários Olá Olá Icertis plataforma de gerenciamento de contrato.</span><span class="sxs-lookup"><span data-stu-id="c4558-197">Please work with [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/) tooadd hello users in hello Icertis Contract Management Platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c4558-198">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4558-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c4558-199">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooIcertis plataforma de gerenciamento de contrato.</span><span class="sxs-lookup"><span data-stu-id="c4558-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIcertis Contract Management Platform.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c4558-201">**tooassign Britta Simon tooIcertis plataforma de gerenciamento de contrato, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4558-201">**tooassign Britta Simon tooIcertis Contract Management Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4558-202">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c4558-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c4558-204">Na lista de aplicativos hello, selecione **plataforma de gerenciamento de contrato Icertis**.</span><span class="sxs-lookup"><span data-stu-id="c4558-204">In hello applications list, select **Icertis Contract Management Platform**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_app.png) 

3. <span data-ttu-id="c4558-206">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c4558-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c4558-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c4558-208">Click **Add** button.</span></span> <span data-ttu-id="c4558-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4558-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c4558-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4558-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c4558-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4558-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4558-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4558-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4558-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c4558-214">Testing single sign-on</span></span>

<span data-ttu-id="c4558-215">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="c4558-215">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c4558-216">Quando você clica em um bloco de plataforma de gerenciamento de contrato Icertis Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo da plataforma de gerenciamento Icertis contrato.</span><span class="sxs-lookup"><span data-stu-id="c4558-216">When you click hello Icertis Contract Management Platform tile in hello Access Panel, you should get automatically signed-on tooyour Icertis Contract Management Platform application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4558-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c4558-217">Additional resources</span></span>

* [<span data-ttu-id="c4558-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c4558-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4558-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c4558-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_203.png

