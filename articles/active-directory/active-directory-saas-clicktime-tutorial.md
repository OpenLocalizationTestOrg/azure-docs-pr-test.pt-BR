---
title: "Tutorial: integração do Azure Active Directory com o ClickTime | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="d6acf-103">Tutorial: integração do Active Directory do Azure ao ClickTime</span><span class="sxs-lookup"><span data-stu-id="d6acf-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="d6acf-104">Neste tutorial, você aprenderá como toointegrate ClickTime com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d6acf-104">In this tutorial, you learn how toointegrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6acf-105">Integrando o ClickTime com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6acf-105">Integrating ClickTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d6acf-106">Você pode controlar no AD do Azure que tenha acesso tooClickTime</span><span class="sxs-lookup"><span data-stu-id="d6acf-106">You can control in Azure AD who has access tooClickTime</span></span>
- <span data-ttu-id="d6acf-107">Você pode habilitar seu usuários tooautomatically get conectado tooClickTime (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d6acf-107">You can enable your users tooautomatically get signed-on tooClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6acf-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d6acf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d6acf-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6acf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6acf-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d6acf-110">Prerequisites</span></span>

<span data-ttu-id="d6acf-111">tooconfigure integração do AD do Azure com o ClickTime, é necessário Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6acf-111">tooconfigure Azure AD integration with ClickTime, you need hello following items:</span></span>

- <span data-ttu-id="d6acf-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d6acf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6acf-113">Uma assinatura do ClickTime habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="d6acf-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6acf-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d6acf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6acf-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d6acf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6acf-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d6acf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6acf-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6acf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6acf-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d6acf-118">Scenario description</span></span>
<span data-ttu-id="d6acf-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d6acf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6acf-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="d6acf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6acf-121">Adicionando ClickTime da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d6acf-121">Adding ClickTime from hello gallery</span></span>
2. <span data-ttu-id="d6acf-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d6acf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-hello-gallery"></a><span data-ttu-id="d6acf-123">Adicionando ClickTime da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d6acf-123">Adding ClickTime from hello gallery</span></span>
<span data-ttu-id="d6acf-124">integração de saudação tooconfigure do ClickTime no AD do Azure, você precisa tooadd ClickTime da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d6acf-124">tooconfigure hello integration of ClickTime into Azure AD, you need tooadd ClickTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d6acf-125">**tooadd ClickTime da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d6acf-125">**tooadd ClickTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6acf-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d6acf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="d6acf-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d6acf-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="d6acf-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d6acf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="d6acf-133">Na caixa de pesquisa hello, digite **ClickTime**, selecione **ClickTime** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d6acf-133">In hello search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ClickTime na lista de resultados de saudação](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d6acf-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6acf-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d6acf-136">Nesta seção, você configurará e testará o logon único do Azure AD com o ClickTime, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d6acf-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d6acf-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ClickTime é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6acf-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ClickTime is tooa user in Azure AD.</span></span> <span data-ttu-id="d6acf-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no ClickTime precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d6acf-138">In other words, a link relationship between an Azure AD user and hello related user in ClickTime needs toobe established.</span></span>

<span data-ttu-id="d6acf-139">No ClickTime, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6acf-139">In ClickTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d6acf-140">tooconfigure e teste de logon único do AD do Azure com o ClickTime, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6acf-140">tooconfigure and test Azure AD single sign-on with ClickTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d6acf-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d6acf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d6acf-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6acf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6acf-143">**[Criar um usuário de teste do ClickTime](#create-a-clicktime-test-user)**  -toohave um equivalente do Britta Simon no ClickTime é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="d6acf-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - toohave a counterpart of Britta Simon in ClickTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6acf-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="d6acf-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6acf-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="d6acf-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d6acf-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6acf-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d6acf-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ClickTime.</span><span class="sxs-lookup"><span data-stu-id="d6acf-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="d6acf-148">**tooconfigure AD do Azure-logon único com o ClickTime, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d6acf-148">**tooconfigure Azure AD single sign-on with ClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6acf-149">Em Olá portal do Azure, Olá **ClickTime** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-149">In hello Azure portal, on hello **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="d6acf-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="d6acf-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="d6acf-153">Em Olá **ClickTime domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6acf-153">On hello **ClickTime Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="d6acf-155">a.</span><span class="sxs-lookup"><span data-stu-id="d6acf-155">a.</span></span> <span data-ttu-id="d6acf-156">Em Olá **identificador** caixa de texto, digite um URL como:`https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="d6acf-156">In hello **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="d6acf-157">b.</span><span class="sxs-lookup"><span data-stu-id="d6acf-157">b.</span></span> <span data-ttu-id="d6acf-158">Em Olá **URL de resposta** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="d6acf-158">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="d6acf-159">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d6acf-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="d6acf-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d6acf-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d6acf-163">Em Olá **ClickTime configuração** seção, clique em **configurar ClickTime** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="d6acf-163">On hello **ClickTime Configuration** section, click **Configure ClickTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d6acf-164">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="d6acf-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="d6acf-166">Em outra janela do navegador da Web, faça logon em seu site de empresa do ClickTime como administrador.</span><span class="sxs-lookup"><span data-stu-id="d6acf-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="d6acf-167">Na barra de ferramentas de saudação na parte superior do hello, clique em **preferências**e, em seguida, clique em **as configurações de segurança**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-167">In hello toolbar on hello top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="d6acf-168">Em Olá **preferências de logon único** configuração, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6acf-168">In hello **Single Sign-On Preferences** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d6acf-169">![Configurações de segurança](./media/active-directory-saas-clicktime-tutorial/tic777280.png "as configurações de segurança")</span><span class="sxs-lookup"><span data-stu-id="d6acf-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="d6acf-170">a.</span><span class="sxs-lookup"><span data-stu-id="d6acf-170">a.</span></span>  <span data-ttu-id="d6acf-171">Selecione **Permitir** a entrada usando o SSO (Logon Único) com **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="d6acf-172">b.</span><span class="sxs-lookup"><span data-stu-id="d6acf-172">b.</span></span> <span data-ttu-id="d6acf-173">Em Olá **ponto de extremidade de provedor de identidade** caixa de texto, colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6acf-173">In hello **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="d6acf-174">c.</span><span class="sxs-lookup"><span data-stu-id="d6acf-174">c.</span></span>  <span data-ttu-id="d6acf-175">Olá abrir **certificado codificado na base 64** baixado do portal do Azure em **o bloco de notas**, copie o conteúdo de saudação e, em seguida, cole-o em hello **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="d6acf-175">Open hello **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="d6acf-176">d.</span><span class="sxs-lookup"><span data-stu-id="d6acf-176">d.</span></span>  <span data-ttu-id="d6acf-177">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d6acf-178">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="d6acf-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d6acf-179">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="d6acf-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d6acf-180">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6acf-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d6acf-181">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6acf-181">Create an Azure AD test user</span></span>
<span data-ttu-id="d6acf-182">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6acf-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="d6acf-184">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d6acf-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6acf-185">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="d6acf-185">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6acf-187">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-187">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6acf-189">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d6acf-189">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6acf-191">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6acf-191">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6acf-193">a.</span><span class="sxs-lookup"><span data-stu-id="d6acf-193">a.</span></span> <span data-ttu-id="d6acf-194">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6acf-195">b.</span><span class="sxs-lookup"><span data-stu-id="d6acf-195">b.</span></span> <span data-ttu-id="d6acf-196">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d6acf-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6acf-197">c.</span><span class="sxs-lookup"><span data-stu-id="d6acf-197">c.</span></span> <span data-ttu-id="d6acf-198">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d6acf-199">d.</span><span class="sxs-lookup"><span data-stu-id="d6acf-199">d.</span></span> <span data-ttu-id="d6acf-200">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="d6acf-201">Criar um usuário de teste do ClickTime</span><span class="sxs-lookup"><span data-stu-id="d6acf-201">Create a ClickTime test user</span></span>

<span data-ttu-id="d6acf-202">Em ordem tooenable AD do Azure usuários toolog no ClickTime, eles devem ser provisionados no ClickTime.</span><span class="sxs-lookup"><span data-stu-id="d6acf-202">In order tooenable Azure AD users toolog into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="d6acf-203">No caso de saudação do ClickTime, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="d6acf-203">In hello case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="d6acf-204">Você pode usar qualquer ferramenta de criação outros ClickTime usuário conta ou APIs fornecidas pelo ClickTime tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6acf-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime tooprovision Azure AD user accounts.</span></span>

<span data-ttu-id="d6acf-205">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d6acf-205">**tooprovision a user account, perform hello following steps:**</span></span>
1. <span data-ttu-id="d6acf-206">Faça logon no tooyour **ClickTime** locatário.</span><span class="sxs-lookup"><span data-stu-id="d6acf-206">Log in tooyour **ClickTime** tenant.</span></span>
2. <span data-ttu-id="d6acf-207">Na barra de ferramentas de saudação na parte superior do hello, clique em **empresa**e, em seguida, clique em **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-207">In hello toolbar on hello top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="d6acf-208">![Pessoas](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="d6acf-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="d6acf-209">Clique em **Adicionar Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="d6acf-210">![Adicionar pessoa](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Adicionar pessoa")</span><span class="sxs-lookup"><span data-stu-id="d6acf-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="d6acf-211">Olá seção nova pessoa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6acf-211">In hello New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d6acf-212">![Pessoas](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="d6acf-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="d6acf-213">a.</span><span class="sxs-lookup"><span data-stu-id="d6acf-213">a.</span></span>  <span data-ttu-id="d6acf-214">Em Olá **nome completo** caixa de texto, digite nome completo de usuário como **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-214">In hello **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="d6acf-215">b.</span><span class="sxs-lookup"><span data-stu-id="d6acf-215">b.</span></span>  <span data-ttu-id="d6acf-216">Em Olá **endereço de email** caixa de texto, como o email de saudação do tipo de usuário  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="d6acf-216">In hello **email address** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="d6acf-217">Se desejar, você pode definir propriedades adicionais do novo objeto de pessoa hello.</span><span class="sxs-lookup"><span data-stu-id="d6acf-217">If you want to, you can set additional properties of hello new person object.</span></span>
   
    <span data-ttu-id="d6acf-218">c.</span><span class="sxs-lookup"><span data-stu-id="d6acf-218">c.</span></span>  <span data-ttu-id="d6acf-219">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-219">Click **Save**.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d6acf-220">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d6acf-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d6acf-221">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooClickTime.</span><span class="sxs-lookup"><span data-stu-id="d6acf-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClickTime.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="d6acf-223">**tooassign Britta Simon tooClickTime, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d6acf-223">**tooassign Britta Simon tooClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6acf-224">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d6acf-226">Na lista de aplicativos hello, selecione **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-226">In hello applications list, select **ClickTime**.</span></span>

    ![Link de ClickTimne na lista de aplicativos de saudação](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="d6acf-228">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202] 

4. <span data-ttu-id="d6acf-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d6acf-230">Click **Add** button.</span></span> <span data-ttu-id="d6acf-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d6acf-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="d6acf-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6acf-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d6acf-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d6acf-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6acf-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d6acf-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d6acf-236">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="d6acf-236">Test single sign-on</span></span>

<span data-ttu-id="d6acf-237">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6acf-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d6acf-238">Quando você clica em bloco ClickTime Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour ClickTime aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6acf-238">When you click hello ClickTime tile in hello Access Panel, you should get automatically signed-on tooyour ClickTime application.</span></span>
<span data-ttu-id="d6acf-239">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d6acf-239">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6acf-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d6acf-240">Additional resources</span></span>

* [<span data-ttu-id="d6acf-241">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d6acf-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6acf-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d6acf-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

