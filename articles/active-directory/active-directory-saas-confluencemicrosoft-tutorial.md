---
title: "Tutorial: Integração do Azure Active Directory ao SSO do SAML para o Confluence da Microsoft | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SSO do SAML confluência pela Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ace23800e3908c8125052b4a2edcaae71f19935d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a><span data-ttu-id="eff15-103">Tutorial: Integração do Azure Active Directory ao SSO do SAML para o Confluence da Microsoft</span><span class="sxs-lookup"><span data-stu-id="eff15-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span></span>

<span data-ttu-id="eff15-104">Neste tutorial, você aprenderá como toointegrate SSO do SAML confluência pela Microsoft no Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="eff15-104">In this tutorial, you learn how toointegrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eff15-105">Integração de SSO do SAML confluência pela Microsoft com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="eff15-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eff15-106">Você pode controlar no AD do Azure que tenha acesso tooConfluence SSO do SAML pela Microsoft</span><span class="sxs-lookup"><span data-stu-id="eff15-106">You can control in Azure AD who has access tooConfluence SAML SSO by Microsoft</span></span>
- <span data-ttu-id="eff15-107">Você pode habilitar seu usuários tooautomatically get conectado tooConfluence SSO do SAML pela Microsoft (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eff15-107">You can enable your users tooautomatically get signed-on tooConfluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eff15-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="eff15-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eff15-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eff15-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eff15-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eff15-110">Prerequisites</span></span>

<span data-ttu-id="eff15-111">tooconfigure integração do AD do Azure com o SSO do SAML confluência pela Microsoft, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="eff15-111">tooconfigure Azure AD integration with Confluence SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="eff15-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eff15-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eff15-113">Aplicativo de servidor confluência instalado em um servidor do Windows de 64 bits (no local ou na nuvem Olá infraestrutura IaaS)</span><span class="sxs-lookup"><span data-stu-id="eff15-113">Confluence server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="eff15-114">O servidor do Confluence é habilitado para HTTPS</span><span class="sxs-lookup"><span data-stu-id="eff15-114">Confluence server is HTTPS enabled</span></span>
- <span data-ttu-id="eff15-115">Observação Olá suporte para versões confluência plug-in são mencionadas na seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="eff15-115">Note hello supported versions for Confluence Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="eff15-116">Servidor confluência está acessível na internet particularmente tooAzure página de logon do AD para autenticação e deve tooreceive capaz de Olá token do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eff15-116">Confluence server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="eff15-117">As credenciais do administrador são configuradas no Confluence</span><span class="sxs-lookup"><span data-stu-id="eff15-117">Admin credentials are set up in Confluence</span></span>
- <span data-ttu-id="eff15-118">O WebSudo está desabilitado no Confluence</span><span class="sxs-lookup"><span data-stu-id="eff15-118">WebSudo is disabled in Confluence</span></span>
- <span data-ttu-id="eff15-119">Testar usuário criado na Olá aplicativo de servidor confluência</span><span class="sxs-lookup"><span data-stu-id="eff15-119">Test user created in hello Confluence server application</span></span>

> [!NOTE]
> <span data-ttu-id="eff15-120">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção de confluência.</span><span class="sxs-lookup"><span data-stu-id="eff15-120">tootest hello steps in this tutorial, we do not recommend using a production environment of Confluence.</span></span> <span data-ttu-id="eff15-121">Teste a integração de saudação primeiro em desenvolvimento ou ambiente de aplicativo hello e, em seguida, ambiente de produção de hello do uso de preparo.</span><span class="sxs-lookup"><span data-stu-id="eff15-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="eff15-122">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="eff15-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eff15-123">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="eff15-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eff15-124">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eff15-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-confluence"></a><span data-ttu-id="eff15-125">Versões com suporte do Confluence</span><span class="sxs-lookup"><span data-stu-id="eff15-125">Supported versions of Confluence</span></span> 

<span data-ttu-id="eff15-126">A partir de agora, há suporte para as seguintes versões do Confluence:</span><span class="sxs-lookup"><span data-stu-id="eff15-126">As of now, following versions of Confluence are supported:</span></span>

- <span data-ttu-id="eff15-127">Confluência: too5.10 5.0</span><span class="sxs-lookup"><span data-stu-id="eff15-127">Confluence: 5.0 too5.10</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eff15-128">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="eff15-128">Scenario description</span></span>
<span data-ttu-id="eff15-129">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="eff15-129">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eff15-130">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="eff15-130">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eff15-131">Adicionando o SSO do SAML confluência pela Microsoft na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="eff15-131">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="eff15-132">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eff15-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-confluence-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="eff15-133">Adicionando o SSO do SAML confluência pela Microsoft na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="eff15-133">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="eff15-134">integração de saudação tooconfigure do SSO do SAML confluência pela Microsoft no Azure AD, é necessário tooadd SSO do SAML confluência pela Microsoft na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="eff15-134">tooconfigure hello integration of Confluence SAML SSO by Microsoft into Azure AD, you need tooadd Confluence SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eff15-135">**tooadd SSO do SAML confluência pela Microsoft na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eff15-135">**tooadd Confluence SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eff15-136">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="eff15-136">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eff15-138">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="eff15-138">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eff15-139">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="eff15-139">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="eff15-141">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eff15-141">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="eff15-143">Na caixa de pesquisa hello, digite **SSO do SAML confluência pela Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="eff15-143">In hello search box, type **Confluence SAML SSO by Microsoft**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. <span data-ttu-id="eff15-145">No painel de resultados de saudação, selecione **SSO do SAML confluência pela Microsoft**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="eff15-145">In hello results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eff15-147">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eff15-147">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eff15-148">Nesta seção, você configura e testa o logon único do Azure AD com o SSO do SAML para o Confluence da Microsoft, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="eff15-148">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eff15-149">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SSO do SAML confluência pela Microsoft é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="eff15-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Confluence SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="eff15-150">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em SSO do SAML confluência pela Microsoft precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="eff15-150">In other words, a link relationship between an Azure AD user and hello related user in Confluence SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="eff15-151">SSO do SAML confluência pela Microsoft, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="eff15-151">In Confluence SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eff15-152">tooconfigure e teste de logon único do AD do Azure com o SSO do SAML confluência pela Microsoft, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="eff15-152">tooconfigure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eff15-153">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="eff15-153">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eff15-154">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eff15-154">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eff15-155">**[Criando um SSO do SAML confluência pelo usuário de teste do Microsoft](#creating-a-confluence-saml-sso-by-microsoft-test-user)**  -toohave um equivalente do Britta Simon no SSO do SAML confluência pela Microsoft que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="eff15-155">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eff15-156">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="eff15-156">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eff15-157">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="eff15-157">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eff15-158">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="eff15-158">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eff15-159">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu SSO do SAML confluência pelo aplicativo Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eff15-159">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="eff15-160">**tooconfigure logon único do AD do Azure com o SSO do SAML confluência pela Microsoft, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eff15-160">**tooconfigure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="eff15-161">Em Olá portal do Azure, Olá **SSO do SAML confluência pela Microsoft** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="eff15-161">In hello Azure portal, on hello **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="eff15-163">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="eff15-163">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. <span data-ttu-id="eff15-165">Em Olá **SSO do SAML confluência Domain da Microsoft e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="eff15-165">On hello **Confluence SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    <span data-ttu-id="eff15-167">a.</span><span class="sxs-lookup"><span data-stu-id="eff15-167">a.</span></span> <span data-ttu-id="eff15-168">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="eff15-168">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="eff15-169">b.</span><span class="sxs-lookup"><span data-stu-id="eff15-169">b.</span></span> <span data-ttu-id="eff15-170">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="eff15-170">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="eff15-171">c.</span><span class="sxs-lookup"><span data-stu-id="eff15-171">c.</span></span> <span data-ttu-id="eff15-172">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="eff15-172">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eff15-173">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="eff15-173">These values are not real.</span></span> <span data-ttu-id="eff15-174">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="eff15-174">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="eff15-175">A porta é opcional, caso seja uma URL nomeada.</span><span class="sxs-lookup"><span data-stu-id="eff15-175">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="eff15-176">Esses valores são recebidos durante a configuração de saudação do plugin confluência, que é explicada posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="eff15-176">These values are received during hello configuration of Confluence plugin, which is explained later in hello tutorial.</span></span>
 

4. <span data-ttu-id="eff15-177">Olá toogenerate **metadados** url, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="eff15-177">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="eff15-178">a.</span><span class="sxs-lookup"><span data-stu-id="eff15-178">a.</span></span> <span data-ttu-id="eff15-179">Clique em **Registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="eff15-179">Click **App registrations**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="eff15-181">b.</span><span class="sxs-lookup"><span data-stu-id="eff15-181">b.</span></span> <span data-ttu-id="eff15-182">Clique em **pontos de extremidade** tooopen **pontos de extremidade** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eff15-182">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar Logon Único](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="eff15-184">c.</span><span class="sxs-lookup"><span data-stu-id="eff15-184">c.</span></span> <span data-ttu-id="eff15-185">Clique em Olá cópia botão toocopy **documento de METADADOS de Federação** url e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="eff15-185">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="eff15-187">d.</span><span class="sxs-lookup"><span data-stu-id="eff15-187">d.</span></span> <span data-ttu-id="eff15-188">Agora vá toohello a página de propriedades de **SSO do SAML confluência pela Microsoft** e cópia hello **Id do aplicativo** usando **cópia** botão e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="eff15-188">Now go toohello property page of **Confluence SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    <span data-ttu-id="eff15-190">e.</span><span class="sxs-lookup"><span data-stu-id="eff15-190">e.</span></span> <span data-ttu-id="eff15-191">Gerar Olá **URL de metadados** usando saudação padrão a seguir: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` e copie esse valor no bloco de notas, como ele é usado posteriormente para configuração de saudação do plug-in de saudação.</span><span class="sxs-lookup"><span data-stu-id="eff15-191">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="eff15-192">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="eff15-192">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eff15-194">Entre em contato com [Microsoft](mailto:waadpartners@microsoft.com) com hello informações para o plug-in do hello confluência a seguir.</span><span class="sxs-lookup"><span data-stu-id="eff15-194">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello Confluence plugin.</span></span>
    
    *   <span data-ttu-id="eff15-195">Nome do cliente:</span><span class="sxs-lookup"><span data-stu-id="eff15-195">Customer Name:</span></span>
    *   <span data-ttu-id="eff15-196">Nome de domínio primário:</span><span class="sxs-lookup"><span data-stu-id="eff15-196">Primary domain name:</span></span>
    *   <span data-ttu-id="eff15-197">O Azure AD Premium: Sim/não (o plug-in será tooall disponível Prezado cliente gratuito, básico e SKU Premium)</span><span class="sxs-lookup"><span data-stu-id="eff15-197">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="eff15-198">Número de usuários que usarão essa integração:</span><span class="sxs-lookup"><span data-stu-id="eff15-198">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="eff15-199">Versão do Confluence:</span><span class="sxs-lookup"><span data-stu-id="eff15-199">Confluence Version:</span></span>
    *   <span data-ttu-id="eff15-200">Comentários:</span><span class="sxs-lookup"><span data-stu-id="eff15-200">Comments:</span></span>

7. <span data-ttu-id="eff15-201">Em uma janela de navegador web diferente, faça logon na instância de confluência tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="eff15-201">In a different web browser window, log in tooyour Confluence instance as an administrator.</span></span>

8. <span data-ttu-id="eff15-202">Passe o mouse sobre engrenagem e clique em Olá **complementos**.</span><span class="sxs-lookup"><span data-stu-id="eff15-202">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="eff15-204">Na seção da guia Complementos, clique em **Gerenciar complementos**.</span><span class="sxs-lookup"><span data-stu-id="eff15-204">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. <span data-ttu-id="eff15-206">Carregar manualmente o plug-in de saudação fornecido pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eff15-206">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="eff15-207">Depois de instalar o plug-in do hello, ele aparece na **usuário instalado** seção complementos **gerenciar complementos** seção.</span><span class="sxs-lookup"><span data-stu-id="eff15-207">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="eff15-208">Clique em **configurar** tooconfigure Olá novo plug-in.</span><span class="sxs-lookup"><span data-stu-id="eff15-208">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="eff15-209">Realize as seguintes etapas na página de configuração:</span><span class="sxs-lookup"><span data-stu-id="eff15-209">Perform following steps on configuration page:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="eff15-211">a.</span><span class="sxs-lookup"><span data-stu-id="eff15-211">a.</span></span> <span data-ttu-id="eff15-212">Em **URL de metadados** colar Olá **URL de metadados** gerado a partir do AD do Azure e clique em Olá **resolver** botão.</span><span class="sxs-lookup"><span data-stu-id="eff15-212">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="eff15-213">Ele lê a URL de metadados IdP hello e preenche todas as informações de campos de saudação.</span><span class="sxs-lookup"><span data-stu-id="eff15-213">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="eff15-214">O local padrão da ID de Usuário SAML é o Identificador de Nome.</span><span class="sxs-lookup"><span data-stu-id="eff15-214">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="eff15-215">Você pode alterar essa opção de atributo tooan e inserir nome do atributo apropriado hello.</span><span class="sxs-lookup"><span data-stu-id="eff15-215">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="eff15-216">Certifique-se de que há apenas um certificado mapeado em relação a saudação aplicativo para que não haja nenhum erro na resolução de metadados de saudação.</span><span class="sxs-lookup"><span data-stu-id="eff15-216">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="eff15-217">Se houver vários certificados, após a resolução de metadados hello, o administrador recebe um erro.</span><span class="sxs-lookup"><span data-stu-id="eff15-217">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="eff15-218">b.</span><span class="sxs-lookup"><span data-stu-id="eff15-218">b.</span></span> <span data-ttu-id="eff15-219">Saudação de cópia **identificador, a URL de resposta e a URL de logon** valores e colá-los em **identificador, a URL de resposta e a URL de logon** caixas de texto em respectivamente **SSO do SAML confluência Domain da Microsoft e URLs**  seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eff15-219">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="eff15-220">c.</span><span class="sxs-lookup"><span data-stu-id="eff15-220">c.</span></span> <span data-ttu-id="eff15-221">Em **nome do botão de logon** nome do tipo de saudação do botão de sua organização deseja Olá toosee de usuários na tela de logon.</span><span class="sxs-lookup"><span data-stu-id="eff15-221">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="eff15-222">d.</span><span class="sxs-lookup"><span data-stu-id="eff15-222">d.</span></span> <span data-ttu-id="eff15-223">Em **locais de ID de usuário SAML** selecione **ID de usuário está no elemento NameIdentifier Olá Olá declaração assunto** ou **ID de usuário está em um elemento de atributo**.</span><span class="sxs-lookup"><span data-stu-id="eff15-223">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="eff15-224">Essa ID tem a id de usuário do toobe Olá confluência. Se a id de usuário de saudação não for atendida, sistema não permitirá que usuários toolog no.</span><span class="sxs-lookup"><span data-stu-id="eff15-224">This ID has toobe hello Confluence user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="eff15-225">e.</span><span class="sxs-lookup"><span data-stu-id="eff15-225">e.</span></span> <span data-ttu-id="eff15-226">Se você selecionar **ID de usuário está em um elemento de atributo** opção, em seguida, em **nome do atributo** caixa de texto nome de saudação do tipo do atributo Olá onde a Id de usuário é esperada.</span><span class="sxs-lookup"><span data-stu-id="eff15-226">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="eff15-227">f.</span><span class="sxs-lookup"><span data-stu-id="eff15-227">f.</span></span> <span data-ttu-id="eff15-228">Se você estiver usando o domínio federado de saudação (como o ADFS etc) com o AD do Azure, em seguida, clique em Olá **habilitar Home Realm Discovery** opção e configurar Olá **nome de domínio**.</span><span class="sxs-lookup"><span data-stu-id="eff15-228">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="eff15-229">g.</span><span class="sxs-lookup"><span data-stu-id="eff15-229">g.</span></span> <span data-ttu-id="eff15-230">Em **nome de domínio** Olá domínio nome do tipo aqui em caso de logon baseada no AD FS do hello.</span><span class="sxs-lookup"><span data-stu-id="eff15-230">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="eff15-231">h.</span><span class="sxs-lookup"><span data-stu-id="eff15-231">h.</span></span> <span data-ttu-id="eff15-232">Verificar **habilitar o logout único** se desejar toolog fora do AD do Azure, quando um usuário faz logoff de confluência.</span><span class="sxs-lookup"><span data-stu-id="eff15-232">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from Confluence.</span></span> 

    <span data-ttu-id="eff15-233">i.</span><span class="sxs-lookup"><span data-stu-id="eff15-233">i.</span></span> <span data-ttu-id="eff15-234">Clique em **salvar** botão Configurações de saudação toosave.</span><span class="sxs-lookup"><span data-stu-id="eff15-234">Click **Save** button toosave hello settings.</span></span>


> [!TIP]
> <span data-ttu-id="eff15-235">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="eff15-235">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eff15-236">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="eff15-236">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eff15-237">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eff15-237">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eff15-238">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eff15-238">Creating an Azure AD test user</span></span>
<span data-ttu-id="eff15-239">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eff15-239">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="eff15-241">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eff15-241">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eff15-242">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="eff15-242">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eff15-244">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="eff15-244">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eff15-246">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="eff15-246">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eff15-248">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="eff15-248">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eff15-250">a.</span><span class="sxs-lookup"><span data-stu-id="eff15-250">a.</span></span> <span data-ttu-id="eff15-251">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eff15-251">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eff15-252">b.</span><span class="sxs-lookup"><span data-stu-id="eff15-252">b.</span></span> <span data-ttu-id="eff15-253">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eff15-253">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eff15-254">c.</span><span class="sxs-lookup"><span data-stu-id="eff15-254">c.</span></span> <span data-ttu-id="eff15-255">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="eff15-255">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eff15-256">d.</span><span class="sxs-lookup"><span data-stu-id="eff15-256">d.</span></span> <span data-ttu-id="eff15-257">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="eff15-257">Click **Create**.</span></span>
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="eff15-258">Criando um usuário de teste do SSO do SAML para o Confluence da Microsoft</span><span class="sxs-lookup"><span data-stu-id="eff15-258">Creating a Confluence SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="eff15-259">tooenable AD do Azure usuários toolog em tooConfluence no servidor local, eles devem ser provisionados no SSO do SAML confluência pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eff15-259">tooenable Azure AD users toolog in tooConfluence on premise server, they must be provisioned into Confluence SAML SSO by Microsoft.</span></span> <span data-ttu-id="eff15-260">Para o SSO do SAML para o Confluence da Microsoft, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="eff15-260">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="eff15-261">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eff15-261">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="eff15-262">Faça logon tooyour confluência no servidor local como um administrador.</span><span class="sxs-lookup"><span data-stu-id="eff15-262">Log in tooyour Confluence on premise server as an administrator.</span></span>

2. <span data-ttu-id="eff15-263">Passe o mouse sobre engrenagem e clique em Olá **gerenciamento de usuário**.</span><span class="sxs-lookup"><span data-stu-id="eff15-263">Hover on cog and click hello **User management**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="eff15-265">Na seção usuários, clique na guia **Adicionar usuários**. Em Olá **"Adicionar um usuário"** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="eff15-265">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    <span data-ttu-id="eff15-267">a.</span><span class="sxs-lookup"><span data-stu-id="eff15-267">a.</span></span> <span data-ttu-id="eff15-268">Em Olá **Username** caixa de texto, tipo hello email do usuário como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eff15-268">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="eff15-269">b.</span><span class="sxs-lookup"><span data-stu-id="eff15-269">b.</span></span> <span data-ttu-id="eff15-270">Em Olá **nome completo** caixa de texto, nome completo do tipo saudação do usuário como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eff15-270">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="eff15-271">c.</span><span class="sxs-lookup"><span data-stu-id="eff15-271">c.</span></span> <span data-ttu-id="eff15-272">Em Olá **Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="eff15-272">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="eff15-273">d.</span><span class="sxs-lookup"><span data-stu-id="eff15-273">d.</span></span> <span data-ttu-id="eff15-274">Em Olá **senha** caixa de texto, digite a senha para Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="eff15-274">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="eff15-275">e.</span><span class="sxs-lookup"><span data-stu-id="eff15-275">e.</span></span> <span data-ttu-id="eff15-276">Clique em **Confirmar senha** Redigite a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="eff15-276">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="eff15-277">f.</span><span class="sxs-lookup"><span data-stu-id="eff15-277">f.</span></span> <span data-ttu-id="eff15-278">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="eff15-278">Click **Add** button.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eff15-279">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eff15-279">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eff15-280">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooConfluence SSO do SAML pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eff15-280">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConfluence SAML SSO by Microsoft.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="eff15-282">**tooassign Britta Simon tooConfluence SSO do SAML pela Microsoft, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eff15-282">**tooassign Britta Simon tooConfluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="eff15-283">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="eff15-283">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="eff15-285">Na lista de aplicativos hello, selecione **SSO do SAML confluência pela Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="eff15-285">In hello applications list, select **Confluence SAML SSO by Microsoft**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. <span data-ttu-id="eff15-287">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="eff15-287">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="eff15-289">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="eff15-289">Click **Add** button.</span></span> <span data-ttu-id="eff15-290">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eff15-290">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="eff15-292">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="eff15-292">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eff15-293">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eff15-293">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eff15-294">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eff15-294">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eff15-295">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="eff15-295">Testing single sign-on</span></span>

<span data-ttu-id="eff15-296">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="eff15-296">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eff15-297">Quando você clica em Olá SSO do SAML confluência pelo bloco Microsoft hello painel de acesso, você deve obter automaticamente assinado em tooyour SSO do SAML confluência pelo aplicativo da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eff15-297">When you click hello Confluence SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour Confluence SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="eff15-298">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eff15-298">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eff15-299">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="eff15-299">Additional resources</span></span>

* [<span data-ttu-id="eff15-300">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="eff15-300">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eff15-301">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eff15-301">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

