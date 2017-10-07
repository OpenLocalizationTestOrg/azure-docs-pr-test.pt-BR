---
title: "Tutorial: integração do Azure Active Directory com o Teamphoria | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="8663f-103">Tutorial: integração do Azure Active Directory ao Teamphoria</span><span class="sxs-lookup"><span data-stu-id="8663f-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="8663f-104">Neste tutorial, você aprenderá como toointegrate Teamphoria com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="8663f-104">In this tutorial, you learn how toointegrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8663f-105">Integrando Teamphoria com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="8663f-105">Integrating Teamphoria with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8663f-106">Você pode controlar no AD do Azure que tenha acesso tooTeamphoria</span><span class="sxs-lookup"><span data-stu-id="8663f-106">You can control in Azure AD who has access tooTeamphoria</span></span>
- <span data-ttu-id="8663f-107">Você pode habilitar seu usuários tooautomatically get conectado tooTeamphoria (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8663f-107">You can enable your users tooautomatically get signed-on tooTeamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8663f-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="8663f-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="8663f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8663f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="8663f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8663f-110">Prerequisites</span></span>

<span data-ttu-id="8663f-111">tooconfigure integração do AD do Azure com Teamphoria, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8663f-111">tooconfigure Azure AD integration with Teamphoria, you need hello following items:</span></span>

- <span data-ttu-id="8663f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8663f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8663f-113">Uma assinatura habilitada para logon único do Teamphoria</span><span class="sxs-lookup"><span data-stu-id="8663f-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8663f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8663f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8663f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8663f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8663f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8663f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8663f-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8663f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8663f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8663f-118">Scenario description</span></span>
<span data-ttu-id="8663f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8663f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8663f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="8663f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8663f-121">Adicionando Teamphoria da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8663f-121">Adding Teamphoria from hello gallery</span></span>
2. <span data-ttu-id="8663f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8663f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-hello-gallery"></a><span data-ttu-id="8663f-123">Adicionando Teamphoria da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8663f-123">Adding Teamphoria from hello gallery</span></span>
<span data-ttu-id="8663f-124">integração de saudação tooconfigure de Teamphoria no AD do Azure, você precisa tooadd Teamphoria da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8663f-124">tooconfigure hello integration of Teamphoria into Azure AD, you need tooadd Teamphoria from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8663f-125">**tooadd Teamphoria da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8663f-125">**tooadd Teamphoria from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8663f-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8663f-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8663f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8663f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8663f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8663f-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8663f-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8663f-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8663f-133">Na caixa de pesquisa hello, digite **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="8663f-133">In hello search box, type **Teamphoria**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="8663f-135">No painel de resultados de saudação, selecione **Teamphoria**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8663f-135">In hello results panel, select **Teamphoria**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8663f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8663f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8663f-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Teamphoria, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8663f-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8663f-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Teamphoria é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8663f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamphoria is tooa user in Azure AD.</span></span> <span data-ttu-id="8663f-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Teamphoria precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="8663f-140">In other words, a link relationship between an Azure AD user and hello related user in Teamphoria needs toobe established.</span></span>

<span data-ttu-id="8663f-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="8663f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamphoria.</span></span>

<span data-ttu-id="8663f-142">tooconfigure e teste de logon único do AD do Azure com Teamphoria, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="8663f-142">tooconfigure and test Azure AD single sign-on with Teamphoria, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8663f-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8663f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8663f-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8663f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8663f-145">**[Criar um usuário de teste Teamphoria](#creating-a-teamphoria-test-user)**  -toohave um equivalente do Britta Simon em Teamphoria é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="8663f-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - toohave a counterpart of Britta Simon in Teamphoria that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="8663f-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="8663f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8663f-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="8663f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8663f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8663f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8663f-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="8663f-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="8663f-150">**tooconfigure AD do Azure-logon único com Teamphoria, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8663f-150">**tooconfigure Azure AD single sign-on with Teamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="8663f-151">No portal de gerenciamento do Azure do hello, no hello **Teamphoria** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="8663f-151">In hello Azure Management portal, on hello **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8663f-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="8663f-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="8663f-155">Em Olá **Teamphoria domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8663f-155">On hello **Teamphoria Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="8663f-157">a.</span><span class="sxs-lookup"><span data-stu-id="8663f-157">a.</span></span> <span data-ttu-id="8663f-158">Em Olá **URL de logon** caixa de texto, digite a URL do hello usando saudação padrão a seguir:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="8663f-158">In hello **Sign-on URL** textbox, type hello URL using hello following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="8663f-159">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="8663f-159">Please note that these are not hello real values.</span></span> <span data-ttu-id="8663f-160">Você tem tooupdate esses valores com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="8663f-160">You have tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="8663f-161">Entre em contato com [equipe de suporte do cliente Teamphoria](https://www.teamphoria.com/) tooget Olá logon na URL.</span><span class="sxs-lookup"><span data-stu-id="8663f-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) tooget hello Sign-on URL.</span></span> 

4. <span data-ttu-id="8663f-162">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8663f-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="8663f-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8663f-164">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8663f-166">Em Olá **Teamphoria configuração** seção, clique em **configurar Teamphoria** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="8663f-166">On hello **Teamphoria Configuration** section, click **Configure Teamphoria** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8663f-167">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="8663f-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="8663f-169">tooconfigure logon único no **Teamphoria** lado, o aplicativo de Teamphoria tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="8663f-169">tooconfigure single sign-on on **Teamphoria** side, Login tooyour Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="8663f-170">Vá muito**as configurações de administração** opção em ferramentas de saudação à esquerda e sob Olá Olá guia Configurar clique em **logon único** tooopen janela de configuração de SSO de saudação.</span><span class="sxs-lookup"><span data-stu-id="8663f-170">Go too**ADMIN SETTINGS** option in hello left toolbar and under hello hello Configure Tab click on **SINGLE SIGN-ON** tooopen hello SSO configuration window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="8663f-172">Clique em **adicionar novo provedor de identidade** opção no formulário de saudação de tooopen Olá canto superior direito para adicionar configurações de saudação do SSO.</span><span class="sxs-lookup"><span data-stu-id="8663f-172">Click on **ADD NEW IDENTITY PROVIDER** option in hello top right corner tooopen hello form for adding hello settings for SSO.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="8663f-174">Insira detalhes de saudação nos campos Olá conforme descrito abaixo-</span><span class="sxs-lookup"><span data-stu-id="8663f-174">Enter hello details in hello fields as described below-</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="8663f-176">a.</span><span class="sxs-lookup"><span data-stu-id="8663f-176">a.</span></span> <span data-ttu-id="8663f-177">**NOME de exibição** : digite o nome de exibição de saudação do hello plug-in na página de administração de saudação.</span><span class="sxs-lookup"><span data-stu-id="8663f-177">**DISPLAY NAME** : Enter hello display name of hello plugin on hello admin page.</span></span>

    <span data-ttu-id="8663f-178">b.</span><span class="sxs-lookup"><span data-stu-id="8663f-178">b.</span></span> <span data-ttu-id="8663f-179">**NOME do botão** : nome de saudação de guia de saudação que será exibido na página de logon Olá para registrar em log por meio do SSO.</span><span class="sxs-lookup"><span data-stu-id="8663f-179">**BUTTON NAME** : hello name of hello tab which will display on hello login page for logging in via SSO.</span></span>

    <span data-ttu-id="8663f-180">c.</span><span class="sxs-lookup"><span data-stu-id="8663f-180">c.</span></span> <span data-ttu-id="8663f-181">**CERTIFICADO** : Abra Olá certificado obtido anteriormente Olá portal do Azure no bloco de notas, copia o conteúdo de saudação do hello mesmo e cole-o aqui na caixa de hello.</span><span class="sxs-lookup"><span data-stu-id="8663f-181">**CERTIFICATE** : Open hello Certificate downloaded earlier from hello Azure portal in notepad, copy hello contents of hello same and paste it here in hello box.</span></span>

    <span data-ttu-id="8663f-182">d.</span><span class="sxs-lookup"><span data-stu-id="8663f-182">d.</span></span> <span data-ttu-id="8663f-183">**PONTO de entrada** : Olá colar **Single Sign-On URL do serviço SAML** copiados Olá anterior de formulário portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8663f-183">**ENTRY POINT** : Paste hello **SAML Single Sign-On Service URL** copied earlier form hello Azure portal.</span></span>

    <span data-ttu-id="8663f-184">e.</span><span class="sxs-lookup"><span data-stu-id="8663f-184">e.</span></span> <span data-ttu-id="8663f-185">Alternar a opção de saudação muito**ON** e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="8663f-185">Switch hello option too**ON** and click on **SAVE**.</span></span> 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8663f-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8663f-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="8663f-187">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8663f-187">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8663f-189">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8663f-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8663f-190">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8663f-190">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8663f-192">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="8663f-192">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8663f-194">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8663f-194">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8663f-196">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8663f-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8663f-198">a.</span><span class="sxs-lookup"><span data-stu-id="8663f-198">a.</span></span> <span data-ttu-id="8663f-199">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8663f-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8663f-200">b.</span><span class="sxs-lookup"><span data-stu-id="8663f-200">b.</span></span> <span data-ttu-id="8663f-201">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8663f-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8663f-202">c.</span><span class="sxs-lookup"><span data-stu-id="8663f-202">c.</span></span> <span data-ttu-id="8663f-203">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="8663f-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8663f-204">d.</span><span class="sxs-lookup"><span data-stu-id="8663f-204">d.</span></span> <span data-ttu-id="8663f-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8663f-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="8663f-206">Criar um usuário de teste do Teamphoria</span><span class="sxs-lookup"><span data-stu-id="8663f-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="8663f-207">Em ordem tooenable AD do Azure usuários toolog em Teamphoria, eles devem ser provisionados no Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="8663f-207">In order tooenable Azure AD users toolog into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="8663f-208">No caso de saudação de Teamphoria, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="8663f-208">In hello case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="8663f-209">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8663f-209">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="8663f-210">Faça logon no tooyour Teamphoria site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="8663f-210">Log in tooyour Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="8663f-211">Clique em **ADMIN** configurações na barra de ferramentas à esquerda do hello e em Olá **gerenciar** guia clique **usuários** tooopen página de administrador Olá para usuários.</span><span class="sxs-lookup"><span data-stu-id="8663f-211">Click on **ADMIN** settings on hello left toolbar and under hello **MANAGE** tab Click on **USERS** tooopen hello admin page for users.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="8663f-213">Clique em Olá **MANUAL CONVIDAR** opção.</span><span class="sxs-lookup"><span data-stu-id="8663f-213">Click on hello **MANUAL INVITE** option.</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="8663f-215">Nessa página, realize a ação a seguir.</span><span class="sxs-lookup"><span data-stu-id="8663f-215">On this page, perform following action.</span></span> 
    
    ![Convidar Pessoas](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="8663f-217">a.</span><span class="sxs-lookup"><span data-stu-id="8663f-217">a.</span></span> <span data-ttu-id="8663f-218">Em Olá **endereço de EMAIL** caixa de texto, Olá **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8663f-218">In hello **EMAIL ADDRESS** textbox, hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8663f-219">b.</span><span class="sxs-lookup"><span data-stu-id="8663f-219">b.</span></span> <span data-ttu-id="8663f-220">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8663f-220">In hello **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="8663f-221">c.</span><span class="sxs-lookup"><span data-stu-id="8663f-221">c.</span></span> <span data-ttu-id="8663f-222">Em Olá **Sobrenome** caixa de texto, tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8663f-222">In hello **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="8663f-223">d.</span><span class="sxs-lookup"><span data-stu-id="8663f-223">d.</span></span> <span data-ttu-id="8663f-224">Clique em **CONVIDAR 1 USUÁRIO**.</span><span class="sxs-lookup"><span data-stu-id="8663f-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="8663f-225">Os usuários precisam tooaccept Olá convite tooget criado no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="8663f-225">User needs tooaccept hello invite tooget created in hello system.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8663f-226">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8663f-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8663f-227">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooTeamphoria seu acesso.</span><span class="sxs-lookup"><span data-stu-id="8663f-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamphoria.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8663f-229">**tooassign Britta Simon tooTeamphoria, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8663f-229">**tooassign Britta Simon tooTeamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="8663f-230">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8663f-230">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8663f-232">Na lista de aplicativos hello, selecione **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="8663f-232">In hello applications list, select **Teamphoria**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="8663f-234">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8663f-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8663f-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8663f-236">Click **Add** button.</span></span> <span data-ttu-id="8663f-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8663f-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8663f-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="8663f-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8663f-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8663f-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8663f-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8663f-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8663f-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8663f-242">Testing single sign-on</span></span>

<span data-ttu-id="8663f-243">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="8663f-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8663f-244">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="8663f-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="8663f-245">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="8663f-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8663f-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8663f-246">Additional resources</span></span>

* [<span data-ttu-id="8663f-247">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8663f-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8663f-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8663f-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

