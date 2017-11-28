---
title: "Tutorial: Integração do Azure Active Directory ao Evernote | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="6a986-103">Tutorial: Integração do Azure Active Directory ao Evernote</span><span class="sxs-lookup"><span data-stu-id="6a986-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="6a986-104">Neste tutorial, você aprenderá como toointegrate Evernote com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="6a986-104">In this tutorial, you learn how toointegrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a986-105">Integrando Evernote com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a986-105">Integrating Evernote with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6a986-106">Você pode controlar no AD do Azure que tenha acesso tooEvernote.</span><span class="sxs-lookup"><span data-stu-id="6a986-106">You can control in Azure AD who has access tooEvernote.</span></span>
- <span data-ttu-id="6a986-107">Você pode habilitar seu usuários tooautomatically get conectado tooEvernote (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a986-107">You can enable your users tooautomatically get signed-on tooEvernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6a986-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a986-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6a986-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a986-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a986-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6a986-110">Prerequisites</span></span>

<span data-ttu-id="6a986-111">tooconfigure integração do AD do Azure com Evernote, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a986-111">tooconfigure Azure AD integration with Evernote, you need hello following items:</span></span>

- <span data-ttu-id="6a986-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6a986-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a986-113">Uma assinatura do Evernote habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="6a986-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a986-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6a986-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a986-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6a986-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a986-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6a986-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a986-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a986-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a986-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6a986-118">Scenario description</span></span>
<span data-ttu-id="6a986-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6a986-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a986-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="6a986-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a986-121">Adicionando Evernote da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="6a986-121">Adding Evernote from hello gallery</span></span>
2. <span data-ttu-id="6a986-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6a986-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-hello-gallery"></a><span data-ttu-id="6a986-123">Adicionando Evernote da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="6a986-123">Adding Evernote from hello gallery</span></span>
<span data-ttu-id="6a986-124">integração de saudação tooconfigure de Evernote no AD do Azure, você precisa tooadd Evernote da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6a986-124">tooconfigure hello integration of Evernote into Azure AD, you need tooadd Evernote from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6a986-125">**tooadd Evernote da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6a986-125">**tooadd Evernote from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a986-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="6a986-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="6a986-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6a986-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6a986-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6a986-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="6a986-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a986-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="6a986-133">Na caixa de pesquisa hello, digite **Evernote**, selecione **Evernote** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6a986-133">In hello search box, type **Evernote**, select **Evernote** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evernote na lista de resultados de saudação](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6a986-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a986-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6a986-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Evernote, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="6a986-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6a986-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Evernote é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a986-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evernote is tooa user in Azure AD.</span></span> <span data-ttu-id="6a986-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Evernote precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="6a986-138">In other words, a link relationship between an Azure AD user and hello related user in Evernote needs toobe established.</span></span>

<span data-ttu-id="6a986-139">Evernote, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a986-139">In Evernote, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6a986-140">tooconfigure e teste de logon único do AD do Azure com Evernote, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a986-140">tooconfigure and test Azure AD single sign-on with Evernote, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6a986-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6a986-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6a986-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a986-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a986-143">**[Criar um usuário de teste Evernote](#create-an-evernote-test-user)**  -toohave um equivalente do Britta Simon em Evernote é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="6a986-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - toohave a counterpart of Britta Simon in Evernote that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a986-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="6a986-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a986-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="6a986-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6a986-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a986-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6a986-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Evernote.</span><span class="sxs-lookup"><span data-stu-id="6a986-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="6a986-148">**tooconfigure AD do Azure-logon único com Evernote, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6a986-148">**tooconfigure Azure AD single sign-on with Evernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a986-149">Em Olá portal do Azure, Olá **Evernote** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="6a986-149">In hello Azure portal, on hello **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="6a986-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="6a986-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="6a986-153">Em Olá **Evernote domínio e URLs** , execute Olá etapas a seguir se desejar que o modo de aplicativo de hello tooconfigure IDP iniciado:</span><span class="sxs-lookup"><span data-stu-id="6a986-153">On hello **Evernote Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Informações de logon único de URLs e Domínio do Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="6a986-155">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="6a986-155">In hello **Identifier** textbox, type hello URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="6a986-156">Verificar **Mostrar configurações de URL avançadas** e executar Olá etapa a seguir se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="6a986-156">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informações de logon único de URLs e Domínio do Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="6a986-158">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="6a986-158">In hello **Sign on URL** textbox, type hello URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="6a986-159">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="6a986-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="6a986-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6a986-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6a986-163">Em Olá **Evernote configuração** seção, clique em **configurar Evernote** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="6a986-163">On hello **Evernote Configuration** section, click **Configure Evernote** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6a986-164">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="6a986-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração de Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="6a986-166">Em outra janela do navegador da Web, faça logon em seu site de empresa do Evernote como administrador.</span><span class="sxs-lookup"><span data-stu-id="6a986-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="6a986-167">Vá muito**Console do administrador**</span><span class="sxs-lookup"><span data-stu-id="6a986-167">Go too**'Admin Console'**</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="6a986-169">De saudação **'Admin Console'**, ir muito**'Security'** e selecione **' Single Sign-On'**</span><span class="sxs-lookup"><span data-stu-id="6a986-169">From hello **'Admin Console'**, go too**‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="6a986-171">Configure Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a986-171">Configure hello following values:</span></span>

    ![Certificate-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="6a986-173">a.</span><span class="sxs-lookup"><span data-stu-id="6a986-173">a.</span></span>  <span data-ttu-id="6a986-174">**Habilitar SSO:** SSO é habilitado por padrão (clique **desabilitar Single Sign-on** requisito de SSO Olá tooremove)</span><span class="sxs-lookup"><span data-stu-id="6a986-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** tooremove hello SSO requirement)</span></span>

    <span data-ttu-id="6a986-175">b.</span><span class="sxs-lookup"><span data-stu-id="6a986-175">b.</span></span> <span data-ttu-id="6a986-176">Colar **SAML logon único na URL do serviço** valor que você copiou de saudação portal do Azure em hello **URL de solicitação de HTTP de SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6a986-176">Paste **SAML Single sign-on Service URL** value, which you have copied from hello Azure portal into hello **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="6a986-177">c.</span><span class="sxs-lookup"><span data-stu-id="6a986-177">c.</span></span> <span data-ttu-id="6a986-178">Abra o certificado baixado de saudação do Azure AD em um bloco de notas e copie Olá de conteúdo incluindo "Iniciar certificado" e "END" e colá-la no hello **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6a986-178">Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into hello **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="6a986-179">d.Clique em **Salvar Alterações**</span><span class="sxs-lookup"><span data-stu-id="6a986-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="6a986-180">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="6a986-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6a986-181">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="6a986-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6a986-182">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a986-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6a986-183">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a986-183">Create an Azure AD test user</span></span>

<span data-ttu-id="6a986-184">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a986-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="6a986-186">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6a986-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a986-187">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="6a986-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6a986-189">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="6a986-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6a986-191">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a986-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6a986-193">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a986-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6a986-195">a.</span><span class="sxs-lookup"><span data-stu-id="6a986-195">a.</span></span> <span data-ttu-id="6a986-196">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a986-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a986-197">b.</span><span class="sxs-lookup"><span data-stu-id="6a986-197">b.</span></span> <span data-ttu-id="6a986-198">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a986-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6a986-199">c.</span><span class="sxs-lookup"><span data-stu-id="6a986-199">c.</span></span> <span data-ttu-id="6a986-200">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="6a986-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6a986-201">d.</span><span class="sxs-lookup"><span data-stu-id="6a986-201">d.</span></span> <span data-ttu-id="6a986-202">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6a986-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="6a986-203">Criar um usuário de teste do Evernote</span><span class="sxs-lookup"><span data-stu-id="6a986-203">Create an Evernote test user</span></span>

<span data-ttu-id="6a986-204">Em ordem tooenable AD do Azure usuários toolog em Evernote, eles devem ser provisionados no Evernote.</span><span class="sxs-lookup"><span data-stu-id="6a986-204">In order tooenable Azure AD users toolog into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="6a986-205">No caso de saudação de Evernote, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="6a986-205">In hello case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="6a986-206">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6a986-206">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a986-207">Faça logon no tooyour Evernote site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="6a986-207">Log in tooyour Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="6a986-208">Clique em Olá **Console do administrador**.</span><span class="sxs-lookup"><span data-stu-id="6a986-208">Click hello **'Admin Console'**.</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="6a986-210">De saudação **'Admin Console'**, ir muito**'Adicionar usuários'**.</span><span class="sxs-lookup"><span data-stu-id="6a986-210">From hello **'Admin Console'**, go too**‘Add users’**.</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="6a986-212">**Adicionar membros da equipe** em Olá **Email** caixa de texto, digite o endereço de email de saudação da conta de usuário e clique em **convidar.**</span><span class="sxs-lookup"><span data-stu-id="6a986-212">**Add team members** in hello **Email** textbox, type hello email address of user account and click **Invite.**</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="6a986-214">Depois que o convite é enviado, proprietário de conta do Active Directory do Azure Olá receberão um convite por email tooaccept hello.</span><span class="sxs-lookup"><span data-stu-id="6a986-214">After invitation is sent, hello Azure Active Directory account holder will receive an email tooaccept hello invitation.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6a986-215">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6a986-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6a986-216">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooEvernote.</span><span class="sxs-lookup"><span data-stu-id="6a986-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvernote.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="6a986-218">**tooassign Britta Simon tooEvernote, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6a986-218">**tooassign Britta Simon tooEvernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a986-219">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6a986-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="6a986-221">Na lista de aplicativos hello, selecione **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="6a986-221">In hello applications list, select **Evernote**.</span></span>

    ![link de Evernote Olá na lista de aplicativos Olá](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="6a986-223">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6a986-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="6a986-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6a986-225">Click **Add** button.</span></span> <span data-ttu-id="6a986-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a986-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="6a986-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a986-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6a986-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a986-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a986-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a986-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6a986-231">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="6a986-231">Test single sign-on</span></span>

<span data-ttu-id="6a986-232">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a986-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6a986-233">Quando você clica em bloco Evernote Olá Olá painel de acesso, você deve obter conectado tooyour Evernote aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a986-233">When you click hello Evernote tile in hello Access Panel, you should get signed-on tooyour Evernote application.</span></span> <span data-ttu-id="6a986-234">Você vai ser logon como uma conta de organização mas toolog necessidade com sua conta pessoal.</span><span class="sxs-lookup"><span data-stu-id="6a986-234">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6a986-235">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6a986-235">Additional resources</span></span>

* [<span data-ttu-id="6a986-236">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6a986-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a986-237">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6a986-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

