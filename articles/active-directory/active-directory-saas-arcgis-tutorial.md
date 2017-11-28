---
title: "Tutorial: Integração do Azure Active Directory ao ArcGIS Online | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ArcGIS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="f50f6-103">Tutorial: Integração do Azure Active Directory ao ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="f50f6-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="f50f6-104">Neste tutorial, você aprenderá como toointegrate ArcGIS Online com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f50f6-104">In this tutorial, you learn how toointegrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f50f6-105">Integrando ArcGIS Online com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f50f6-105">Integrating ArcGIS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f50f6-106">Você pode controlar no AD do Azure que tenha acesso tooArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="f50f6-106">You can control in Azure AD who has access tooArcGIS Online</span></span>
- <span data-ttu-id="f50f6-107">Você pode habilitar seus usuários tooautomatically get conectado tooArcGIS on-line (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f50f6-107">You can enable your users tooautomatically get signed-on tooArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f50f6-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f50f6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f50f6-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f50f6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="f50f6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f50f6-110">Prerequisites</span></span>

<span data-ttu-id="f50f6-111">tooconfigure integração do AD do Azure com o ArcGIS Online, você precisará Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f50f6-111">tooconfigure Azure AD integration with ArcGIS Online, you need hello following items:</span></span>

- <span data-ttu-id="f50f6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f50f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f50f6-113">Uma assinatura habilitada para logon único do ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="f50f6-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f50f6-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f50f6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f50f6-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f50f6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f50f6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f50f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f50f6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f50f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f50f6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f50f6-118">Scenario description</span></span>
<span data-ttu-id="f50f6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f50f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f50f6-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="f50f6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f50f6-121">Adicionando ArcGIS Online da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f50f6-121">Adding ArcGIS Online from hello gallery</span></span>
2. <span data-ttu-id="f50f6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f50f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-hello-gallery"></a><span data-ttu-id="f50f6-123">Adicionando ArcGIS Online da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f50f6-123">Adding ArcGIS Online from hello gallery</span></span>
<span data-ttu-id="f50f6-124">integração de saudação tooconfigure do ArcGIS Online no AD do Azure, você precisa tooadd ArcGIS Online na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f50f6-124">tooconfigure hello integration of ArcGIS Online into Azure AD, you need tooadd ArcGIS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f50f6-125">**tooadd ArcGIS Online da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f50f6-125">**tooadd ArcGIS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f50f6-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f50f6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f50f6-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f50f6-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f50f6-131">Clique em **novo aplicativo** botão na parte superior de saudação do novo aplicativo do hello diálogo tooadd.</span><span class="sxs-lookup"><span data-stu-id="f50f6-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f50f6-133">Na caixa de pesquisa hello, digite **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-133">In hello search box, type **ArcGIS Online**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="f50f6-135">No painel de resultados de saudação, selecione **ArcGIS Online**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f50f6-135">In hello results panel, select **ArcGIS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f50f6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f50f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f50f6-138">Nesta seção, você configura e testa o logon único do Azure AD com o ArcGIS Online, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f50f6-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f50f6-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ArcGIS Online é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f50f6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ArcGIS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="f50f6-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no ArcGIS Online precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f50f6-140">In other words, a link relationship between an Azure AD user and hello related user in ArcGIS Online needs toobe established.</span></span>

<span data-ttu-id="f50f6-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="f50f6-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="f50f6-142">tooconfigure e teste de logon único do AD do Azure com o ArcGIS Online, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f50f6-142">tooconfigure and test Azure AD single sign-on with ArcGIS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f50f6-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f50f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f50f6-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f50f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f50f6-145">**[Criar um usuário de teste ArcGIS Online](#creating-an-arcgis-online-test-user)**  -toohave um equivalente do Britta Simon no ArcGIS Online que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f50f6-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - toohave a counterpart of Britta Simon in ArcGIS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f50f6-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="f50f6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f50f6-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="f50f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f50f6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f50f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f50f6-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="f50f6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="f50f6-150">**tooconfigure AD do Azure-logon único do ArcGIS Online, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f50f6-150">**tooconfigure Azure AD single sign-on with ArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="f50f6-151">Em Olá portal do Azure, Olá **ArcGIS Online** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-151">In hello Azure portal, on hello **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f50f6-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="f50f6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="f50f6-155">Em Olá **URLs e domínio Online ArcGIS** , execute Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="f50f6-155">On hello **ArcGIS Online Domain and URLs** section, perform hello following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="f50f6-157">Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="f50f6-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f50f6-158">Esse valor não é hello real.</span><span class="sxs-lookup"><span data-stu-id="f50f6-158">This value is not hello real.</span></span> <span data-ttu-id="f50f6-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="f50f6-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f50f6-160">Entre em contato com [equipe de suporte do cliente Online ArcGIS](http://support.esri.com/) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="f50f6-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) tooget this value.</span></span> 

4. <span data-ttu-id="f50f6-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f50f6-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="f50f6-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f50f6-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f50f6-165">Em outra janela do navegador da Web, faça logon em seu site de empresa ArcGIS como um administrador.</span><span class="sxs-lookup"><span data-stu-id="f50f6-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="f50f6-166">Clique em **EDITAR CONFIGURAÇÕES**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="f50f6-167">![Editar Configurações](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Editar Configurações")</span><span class="sxs-lookup"><span data-stu-id="f50f6-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="f50f6-168">Clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-168">Click **Security**.</span></span>

    <span data-ttu-id="f50f6-169">![Segurança](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="f50f6-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="f50f6-170">Em **Logons Corporativos**, clique em **DEFINIR PROVEDOR DE IDENTIDADE**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="f50f6-171">![Logons Corporativos](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Logons Corporativos")</span><span class="sxs-lookup"><span data-stu-id="f50f6-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="f50f6-172">Em Olá **definir provedor de identidade** configuração de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f50f6-172">On hello **Set Identity Provider** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="f50f6-173">![Definir Provedor de Identidade](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Definir Provedor de Identidade")</span><span class="sxs-lookup"><span data-stu-id="f50f6-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="f50f6-174">a.</span><span class="sxs-lookup"><span data-stu-id="f50f6-174">a.</span></span> <span data-ttu-id="f50f6-175">Em Olá **nome** caixa de texto, digite o nome da sua organização.</span><span class="sxs-lookup"><span data-stu-id="f50f6-175">In hello **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="f50f6-176">b.</span><span class="sxs-lookup"><span data-stu-id="f50f6-176">b.</span></span> <span data-ttu-id="f50f6-177">Para **metadados para Olá provedor de identidade da empresa serão fornecidos usando**, selecione **um arquivo**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-177">For **Metadata for hello Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="f50f6-178">c.</span><span class="sxs-lookup"><span data-stu-id="f50f6-178">c.</span></span> <span data-ttu-id="f50f6-179">tooupload seu arquivo de metadados baixado, clique em **Escolher arquivo**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-179">tooupload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="f50f6-180">d.</span><span class="sxs-lookup"><span data-stu-id="f50f6-180">d.</span></span> <span data-ttu-id="f50f6-181">Clique em **DEFINIR PROVEDOR DE IDENTIDADE**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="f50f6-182">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="f50f6-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f50f6-183">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="f50f6-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f50f6-184">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f50f6-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f50f6-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f50f6-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="f50f6-186">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f50f6-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f50f6-188">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f50f6-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f50f6-189">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f50f6-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f50f6-191">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="f50f6-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f50f6-193">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f50f6-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f50f6-195">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f50f6-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f50f6-197">a.</span><span class="sxs-lookup"><span data-stu-id="f50f6-197">a.</span></span> <span data-ttu-id="f50f6-198">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f50f6-199">b.</span><span class="sxs-lookup"><span data-stu-id="f50f6-199">b.</span></span> <span data-ttu-id="f50f6-200">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f50f6-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="f50f6-201">c.</span><span class="sxs-lookup"><span data-stu-id="f50f6-201">c.</span></span> <span data-ttu-id="f50f6-202">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f50f6-203">d.</span><span class="sxs-lookup"><span data-stu-id="f50f6-203">d.</span></span> <span data-ttu-id="f50f6-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="f50f6-205">Criando um usuário de teste do ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="f50f6-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="f50f6-206">Ordem tooenable AD do Azure usuários toolog no ArcGIS Online, eles devem ser provisionados no ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="f50f6-206">In order tooenable Azure AD users toolog into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="f50f6-207">No caso de saudação do ArcGIS Online, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="f50f6-207">In hello case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="f50f6-208">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f50f6-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="f50f6-209">Faça logon no tooyour **ArcGIS** locatário.</span><span class="sxs-lookup"><span data-stu-id="f50f6-209">Log in tooyour **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="f50f6-210">Clique em **CONVIDAR MEMBROS**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="f50f6-211">![Convidar Membros](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Convidar Membros")</span><span class="sxs-lookup"><span data-stu-id="f50f6-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="f50f6-212">Selecione **Adicionar membros automaticamente sem enviar um email** e, depois, clique em **AVANÇAR**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="f50f6-213">![Adicionar Membros Automaticamente](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Adicionar Membros Automaticamente")</span><span class="sxs-lookup"><span data-stu-id="f50f6-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="f50f6-214">Em Olá **membros** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f50f6-214">On hello **Members** dialog page, perform hello following steps:</span></span>
   
     <span data-ttu-id="f50f6-215">![Adicionar e examinar](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Adicionar e examinar")</span><span class="sxs-lookup"><span data-stu-id="f50f6-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="f50f6-216">a.</span><span class="sxs-lookup"><span data-stu-id="f50f6-216">a.</span></span> <span data-ttu-id="f50f6-217">Digite hello **Email**, **nome**, e **Sobrenome** de uma conta válida do AAD você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="f50f6-217">Enter hello **Email**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision.</span></span>
  
     <span data-ttu-id="f50f6-218">b.</span><span class="sxs-lookup"><span data-stu-id="f50f6-218">b.</span></span> <span data-ttu-id="f50f6-219">Clique em **ADICIONAR E EXAMINAR**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="f50f6-220">Examinar os dados de saudação você digitou e, em seguida, clique em **adicionar MEMBROS**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-220">Review hello data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="f50f6-221">![Adicionar membro](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Adicionar membro")</span><span class="sxs-lookup"><span data-stu-id="f50f6-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="f50f6-222">proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="f50f6-222">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f50f6-223">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f50f6-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f50f6-224">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooArcGIS on-line.</span><span class="sxs-lookup"><span data-stu-id="f50f6-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooArcGIS Online.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f50f6-226">**tooassign Britta Simon tooArcGIS Online, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f50f6-226">**tooassign Britta Simon tooArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="f50f6-227">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f50f6-229">Na lista de aplicativos hello, selecione **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-229">In hello applications list, select **ArcGIS Online**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="f50f6-231">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f50f6-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f50f6-233">Click **Add** button.</span></span> <span data-ttu-id="f50f6-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f50f6-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f50f6-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f50f6-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f50f6-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f50f6-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f50f6-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f50f6-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f50f6-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f50f6-239">Testing single sign-on</span></span>

<span data-ttu-id="f50f6-240">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f50f6-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f50f6-241">Quando você clica em bloco ArcGIS Online Olá Olá painel de acesso, você deve obter aplicativo ArcGIS Online automaticamente assinado em tooyour.</span><span class="sxs-lookup"><span data-stu-id="f50f6-241">When you click hello ArcGIS Online tile in hello Access Panel, you should get automatically signed-on tooyour ArcGIS Online application.</span></span>
<span data-ttu-id="f50f6-242">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f50f6-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f50f6-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f50f6-243">Additional resources</span></span>

* [<span data-ttu-id="f50f6-244">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f50f6-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f50f6-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f50f6-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

