---
title: "Tutorial: Integração do Azure Active Directory ao Google Apps no Azure | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="ae6dc-103">Tutorial: integração do Azure Active Directory ao Google Apps</span><span class="sxs-lookup"><span data-stu-id="ae6dc-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="ae6dc-104">Neste tutorial, você aprenderá como toointegrate Google Apps com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="ae6dc-104">In this tutorial, you learn how toointegrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae6dc-105">Integração do Google Apps com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="ae6dc-105">Integrating Google Apps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ae6dc-106">Você pode controlar no AD do Azure que tenha acesso tooGoogle aplicativos</span><span class="sxs-lookup"><span data-stu-id="ae6dc-106">You can control in Azure AD who has access tooGoogle Apps</span></span>
- <span data-ttu-id="ae6dc-107">Você pode habilitar seu usuários tooautomatically get conectado tooGoogle aplicativos (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ae6dc-107">You can enable your users tooautomatically get signed-on tooGoogle Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae6dc-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ae6dc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ae6dc-109">Se você quiser tooknow para obter mais informações sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae6dc-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae6dc-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ae6dc-110">Prerequisites</span></span>

<span data-ttu-id="ae6dc-111">tooconfigure integração do AD do Azure com o Google Apps, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ae6dc-111">tooconfigure Azure AD integration with Google Apps, you need hello following items:</span></span>

- <span data-ttu-id="ae6dc-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ae6dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae6dc-113">Uma assinatura habilitada para logon único do Google Apps</span><span class="sxs-lookup"><span data-stu-id="ae6dc-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae6dc-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae6dc-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ae6dc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae6dc-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae6dc-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae6dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="ae6dc-118">Tutorial em vídeo</span><span class="sxs-lookup"><span data-stu-id="ae6dc-118">Video tutorial</span></span>
<span data-ttu-id="ae6dc-119">Como tooEnable Single Sign-On tooGoogle aplicativos em 2 minutos:</span><span class="sxs-lookup"><span data-stu-id="ae6dc-119">How tooEnable Single Sign-On tooGoogle Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="ae6dc-120">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="ae6dc-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="ae6dc-121">**P: Os Chromebooks e outros dispositivos Chrome são compatíveis com o logon único do AD do AD do Azure?**</span><span class="sxs-lookup"><span data-stu-id="ae6dc-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="ae6dc-122">R: Sim, os usuários são toosign capaz em seus dispositivos Chromebook usando suas credenciais do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-122">A: Yes, users are able toosign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="ae6dc-123">Confira este [artigo de suporte do Google Apps](https://support.google.com/chrome/a/answer/6060880) para saber mais sobre o motivo de os usuários receberem uma solicitação por credenciais duas vezes.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="ae6dc-124">**P: se habilitar o logon único, será usuários ser capaz de toouse seu toosign de credenciais do AD do Azure em qualquer produto do Google, como Google sala de aula, GMail, Google Drive, YouTube e assim por diante?**</span><span class="sxs-lookup"><span data-stu-id="ae6dc-124">**Q: If I enable single sign-on, will users be able toouse their Azure AD credentials toosign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="ae6dc-125">R: Sim, dependendo da [quais aplicativos do Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) escolha tooenable ou desabilitar para sua organização.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose tooenable or disable for your organization.</span></span>

3. <span data-ttu-id="ae6dc-126">**P: Posso habilitar o logon único apenas para um subconjunto de meus usuários do Google Apps?**</span><span class="sxs-lookup"><span data-stu-id="ae6dc-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="ae6dc-127">R: não, ativar o logon único imediatamente requer que todos os seu tooauthenticate de usuários do Google Apps com suas credenciais do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-127">A: No, turning on single sign-on immediately requires all your Google Apps users tooauthenticate with their Azure AD credentials.</span></span> <span data-ttu-id="ae6dc-128">Porque o Google Apps não oferece suporte para vários provedores de identidade, provedor de identidade Olá para o seu ambiente do Google Apps pode ser AD do Azure ou Google – mas não ambos ao Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-128">Because Google Apps doesn't support having multiple identity providers, hello identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at hello same time.</span></span>

4. <span data-ttu-id="ae6dc-129">**P: se um usuário está conectado por meio do Windows, são que automaticamente eles autenticam os aplicativos tooGoogle sem obtendo for solicitada uma senha?**</span><span class="sxs-lookup"><span data-stu-id="ae6dc-129">**Q: If a user is signed in through Windows, are they automatically authenticate tooGoogle Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="ae6dc-130">R: Há duas opções para este cenário.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="ae6dc-131">Primeiro, os usuários podem entrar em dispositivos com Windows 10 por meio do [Ingresso no Active Directory do Azure](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae6dc-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="ae6dc-132">Como alternativa, os usuários podem entrar dispositivos Windows que estão tooan ingressado no domínio do Active Directory que tenha sido habilitado para um único logon tooAzure AD por meio do local um [os serviços de Federação do Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) implantação.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-132">Alternatively, users could sign into Windows devices that are domain-joined tooan on-premises Active Directory that has been enabled for single sign-on tooAzure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="ae6dc-133">Ambas as opções exigem etapas tooperform Olá Olá após tooenable tutorial logon único entre o Azure AD e Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-133">Both options require you tooperform hello steps in hello following tutorial tooenable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae6dc-134">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ae6dc-134">Scenario description</span></span>
<span data-ttu-id="ae6dc-135">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae6dc-136">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="ae6dc-136">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae6dc-137">Adicionar o Google Apps da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ae6dc-137">Adding Google Apps from hello gallery</span></span>
2. <span data-ttu-id="ae6dc-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ae6dc-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-hello-gallery"></a><span data-ttu-id="ae6dc-139">Adicionar o Google Apps da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ae6dc-139">Adding Google Apps from hello gallery</span></span>
<span data-ttu-id="ae6dc-140">integração de Olá tooconfigure do Google Apps para o AD do Azure, você precisa tooadd Google Apps na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-140">tooconfigure hello integration of Google Apps into Azure AD, you need tooadd Google Apps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ae6dc-141">**tooadd da Galeria de saudação do Google Apps execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ae6dc-141">**tooadd Google Apps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae6dc-142">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-142">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae6dc-144">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-144">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ae6dc-145">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-145">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ae6dc-147">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-147">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ae6dc-149">Na caixa de pesquisa hello, digite **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-149">In hello search box, type **Google Apps**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="ae6dc-151">No painel de resultados de saudação, selecione **Google Apps**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-151">In hello results panel, select **Google Apps**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae6dc-153">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ae6dc-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae6dc-154">Nesta seção, você configura e testa o logon único do Azure AD com o Google Apps, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ae6dc-155">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Google Apps é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-155">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Google Apps is tooa user in Azure AD.</span></span> <span data-ttu-id="ae6dc-156">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Google Apps precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-156">In other words, a link relationship between an Azure AD user and hello related user in Google Apps needs toobe established.</span></span>

<span data-ttu-id="ae6dc-157">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-157">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Google Apps.</span></span>

<span data-ttu-id="ae6dc-158">tooconfigure e teste de logon único do AD do Azure com o Google Apps, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="ae6dc-158">tooconfigure and test Azure AD single sign-on with Google Apps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ae6dc-159">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ae6dc-160">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae6dc-161">**[Criar um usuário de teste do Google Apps](#creating-a-google-apps-test-user)**  -toohave um equivalente do Britta Simon no Google Apps é a representação toohello vinculado AD do Azure do usuário.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - toohave a counterpart of Britta Simon in Google Apps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae6dc-162">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-162">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae6dc-163">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-163">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae6dc-164">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae6dc-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae6dc-165">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-165">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="ae6dc-166">**tooconfigure AD do Azure-logon único com o Google Apps, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ae6dc-166">**tooconfigure Azure AD single sign-on with Google Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae6dc-167">Em Olá portal do Azure, Olá **Google Apps** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-167">In hello Azure portal, on hello **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ae6dc-169">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-169">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="ae6dc-171">Em Olá **URLs e domínio do Google Apps** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ae6dc-171">On hello **Google Apps Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="ae6dc-173">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="ae6dc-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae6dc-174">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-174">This value is not real.</span></span> <span data-ttu-id="ae6dc-175">Atualize o valor de saudação com URL de logon real hello.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-175">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="ae6dc-176">entre em contato com o hello [equipe de suporte do Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="ae6dc-176">contact hello [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="ae6dc-177">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado** e, em seguida, salve o certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-177">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="ae6dc-179">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ae6dc-179">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ae6dc-181">Em Olá **configuração do Google Apps** seção, clique em **configurar o Google Apps** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-181">On hello **Google Apps Configuration** section, click **Configure Google Apps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ae6dc-182">Saudação de cópia **URL de URL de logout, Single Sign-On URL do serviço SAML e alteração de senha** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ae6dc-182">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="ae6dc-184">Abra uma nova guia no seu navegador e entrar Olá [Console de administração do Google Apps](http://admin.google.com/) usando sua conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-184">Open a new tab in your browser, and sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="ae6dc-185">Clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-185">Click **Security**.</span></span> <span data-ttu-id="ae6dc-186">Se você não vir o link hello, podem estar ocultos em Olá **mais controles** menu na parte inferior de saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-186">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Clique em Segurança.][10]

9. <span data-ttu-id="ae6dc-188">Em Olá **segurança** , clique em **configurar logon único (SSO).**</span><span class="sxs-lookup"><span data-stu-id="ae6dc-188">On hello **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Clique em SSO.][11]

10. <span data-ttu-id="ae6dc-190">Execute Olá alterações de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="ae6dc-190">Perform hello following configuration changes:</span></span>
   
    ![Configure o SSO][12]
   
    <span data-ttu-id="ae6dc-192">a.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-192">a.</span></span> <span data-ttu-id="ae6dc-193">Selecione **Configurar SSO com um provedor de identidade de terceiros**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="ae6dc-194">b.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-194">b.</span></span> <span data-ttu-id="ae6dc-195">No **URL da página de entrada** campo no Google Apps, cole o valor de saudação do **o URL de serviço de logon único**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-195">In the **Sign-in page URL** field in Google Apps, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ae6dc-196">c.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-196">c.</span></span> <span data-ttu-id="ae6dc-197">Em Olá **URL da página de logout** campo no Google Apps, cole o valor de saudação do **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-197">In hello **Sign-out page URL** field in Google Apps, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ae6dc-198">d.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-198">d.</span></span> <span data-ttu-id="ae6dc-199">Em Olá **alterar senha URL** campo no Google Apps, cole o valor de saudação do **alterar senha URL**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-199">In hello **Change password URL** field in Google Apps, paste hello value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ae6dc-200">e.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-200">e.</span></span> <span data-ttu-id="ae6dc-201">No Google Apps para Olá **certificado de verificação**, upload do certificado Olá que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-201">In Google Apps, for hello **Verification certificate**, upload hello certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="ae6dc-202">f.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-202">f.</span></span> <span data-ttu-id="ae6dc-203">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="ae6dc-204">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="ae6dc-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ae6dc-205">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-205">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ae6dc-206">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae6dc-206">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae6dc-207">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ae6dc-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae6dc-208">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ae6dc-210">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ae6dc-210">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae6dc-211">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-211">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae6dc-213">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-213">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae6dc-215">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-215">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae6dc-217">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ae6dc-217">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae6dc-219">a.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-219">a.</span></span> <span data-ttu-id="ae6dc-220">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-220">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae6dc-221">b.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-221">b.</span></span> <span data-ttu-id="ae6dc-222">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-222">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae6dc-223">c.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-223">c.</span></span> <span data-ttu-id="ae6dc-224">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-224">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ae6dc-225">d.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-225">d.</span></span> <span data-ttu-id="ae6dc-226">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="ae6dc-227">Criando um usuário de teste do Google Apps</span><span class="sxs-lookup"><span data-stu-id="ae6dc-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="ae6dc-228">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no Software de aplicativos do Google.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-228">hello objective of this section is toocreate a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="ae6dc-229">O Google Apps dá suporte ao provisionamento automático, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="ae6dc-230">Não há nenhuma ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-230">There is no action for you in this section.</span></span> <span data-ttu-id="ae6dc-231">Se um usuário não existir no Software de aplicativos do Google, um novo é criado quando você tenta tooaccess Software de aplicativos do Google.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt tooaccess Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="ae6dc-232">Se você precisar toocreate um usuário manualmente, entre em contato com o hello [equipe de suporte do Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="ae6dc-232">If you need toocreate a user manually, contact hello [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ae6dc-233">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ae6dc-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ae6dc-234">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooGoogle aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGoogle Apps.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ae6dc-236">**tooassign Britta Simon tooGoogle aplicativos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ae6dc-236">**tooassign Britta Simon tooGoogle Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae6dc-237">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ae6dc-239">Na lista de aplicativos hello, selecione **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-239">In hello applications list, select **Google Apps**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="ae6dc-241">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ae6dc-243">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-243">Click **Add** button.</span></span> <span data-ttu-id="ae6dc-244">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ae6dc-246">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ae6dc-247">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae6dc-248">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae6dc-249">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ae6dc-249">Testing single sign-on</span></span>

<span data-ttu-id="ae6dc-250">Nesta seção, tootest seu único-configurações de logon, abra Olá painel de acesso em [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), faça logon na conta de teste hello e clique em **Google Apps** bloco no painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae6dc-250">In this section, tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into hello test account, and click **Google Apps** tile in hello Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae6dc-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ae6dc-251">Additional resources</span></span>

* [<span data-ttu-id="ae6dc-252">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ae6dc-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae6dc-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae6dc-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ae6dc-254">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="ae6dc-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png