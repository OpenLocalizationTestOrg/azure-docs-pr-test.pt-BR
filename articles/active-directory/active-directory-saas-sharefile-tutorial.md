---
title: "Tutorial: integração do Azure Active Directory com o Citrix ShareFile | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="4f9dd-103">Tutorial: integração do Azure Active Directory ao Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="4f9dd-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="4f9dd-104">Neste tutorial, você aprenderá como toointegrate Citrix ShareFile com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4f9dd-104">In this tutorial, you learn how toointegrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f9dd-105">Integração do Citrix ShareFile com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9dd-105">Integrating Citrix ShareFile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4f9dd-106">Você pode controlar no AD do Azure que tenha acesso tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-106">You can control in Azure AD who has access tooCitrix ShareFile.</span></span>
- <span data-ttu-id="4f9dd-107">Você pode habilitar seu usuários tooautomatically get conectado tooCitrix ShareFile (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-107">You can enable your users tooautomatically get signed-on tooCitrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4f9dd-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4f9dd-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f9dd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f9dd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4f9dd-110">Prerequisites</span></span>

<span data-ttu-id="4f9dd-111">tooconfigure integração do Azure AD com Citrix ShareFile, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9dd-111">tooconfigure Azure AD integration with Citrix ShareFile, you need hello following items:</span></span>

- <span data-ttu-id="4f9dd-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4f9dd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f9dd-113">Uma assinatura habilitada para logon único do Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="4f9dd-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4f9dd-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4f9dd-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4f9dd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f9dd-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f9dd-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f9dd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4f9dd-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4f9dd-118">Scenario description</span></span>
<span data-ttu-id="4f9dd-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f9dd-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="4f9dd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f9dd-121">Adicionar Citrix ShareFile da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4f9dd-121">Add Citrix ShareFile from hello gallery</span></span>
2. <span data-ttu-id="4f9dd-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f9dd-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-hello-gallery"></a><span data-ttu-id="4f9dd-123">Adicionar Citrix ShareFile da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4f9dd-123">Add Citrix ShareFile from hello gallery</span></span>
<span data-ttu-id="4f9dd-124">integração de saudação tooconfigure do Citrix ShareFile no AD do Azure, você precisa tooadd Citrix ShareFile da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-124">tooconfigure hello integration of Citrix ShareFile into Azure AD, you need tooadd Citrix ShareFile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4f9dd-125">**tooadd Citrix ShareFile da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4f9dd-125">**tooadd Citrix ShareFile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f9dd-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="4f9dd-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4f9dd-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="4f9dd-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="4f9dd-133">Na caixa de pesquisa hello, digite **Citrix ShareFile**, selecione **Citrix ShareFile** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-133">In hello search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados do Citrix ShareFile em Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4f9dd-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f9dd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4f9dd-136">Nesta seção, você vai configurar e testar o logon único do Azure AD com o Citrix ShareFile, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="4f9dd-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4f9dd-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Citrix ShareFile é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix ShareFile is tooa user in Azure AD.</span></span> <span data-ttu-id="4f9dd-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Citrix ShareFile precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-138">In other words, a link relationship between an Azure AD user and hello related user in Citrix ShareFile needs toobe established.</span></span>

<span data-ttu-id="4f9dd-139">No Citrix ShareFile, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-139">In Citrix ShareFile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4f9dd-140">tooconfigure e teste de logon único do AD do Azure com o Citrix ShareFile, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9dd-140">tooconfigure and test Azure AD single sign-on with Citrix ShareFile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4f9dd-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4f9dd-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f9dd-143">**[Criar um usuário de teste do Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave um equivalente do Britta Simon no Citrix ShareFile é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - toohave a counterpart of Britta Simon in Citrix ShareFile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4f9dd-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f9dd-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4f9dd-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f9dd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4f9dd-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo da Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="4f9dd-148">**tooconfigure AD do Azure-logon único com o Citrix ShareFile, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4f9dd-148">**tooconfigure Azure AD single sign-on with Citrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f9dd-149">Em Olá portal do Azure, Olá **Citrix ShareFile** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-149">In hello Azure portal, on hello **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="4f9dd-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="4f9dd-153">Em Olá **Citrix ShareFile domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9dd-153">On hello **Citrix ShareFile Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="4f9dd-155">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="4f9dd-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4f9dd-156">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-156">This value is not real.</span></span> <span data-ttu-id="4f9dd-157">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4f9dd-158">Entre em contato com [equipe de suporte do cliente do Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) tooget this value.</span></span> 

4. <span data-ttu-id="4f9dd-159">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="4f9dd-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4f9dd-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4f9dd-163">Em Olá **configuração da Citrix ShareFile** seção, clique em **configurar Citrix ShareFile** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-163">On hello **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4f9dd-164">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="4f9dd-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="4f9dd-166">Em outra janela do navegador da Web, faça logon em seu site de empresa do **Citrix ShareFile** como administrador.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="4f9dd-167">Na barra de ferramentas de saudação na parte superior do hello, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-167">In hello toolbar on hello top, click **Admin**.</span></span>

9. <span data-ttu-id="4f9dd-168">No painel de navegação esquerdo hello, selecione **configurar logon único**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-168">In hello left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="4f9dd-169">![Administração de Conta](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Administração de Conta")</span><span class="sxs-lookup"><span data-stu-id="4f9dd-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="4f9dd-170">Em Olá **Single Sign-On / configuração do SAML 2.0** página de diálogo em **configurações básicas**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9dd-170">On hello **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform hello following steps:</span></span>
   
    <span data-ttu-id="4f9dd-171">![Logon Único](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="4f9dd-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="4f9dd-172">a.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-172">a.</span></span> <span data-ttu-id="4f9dd-173">Clique em **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="4f9dd-174">b.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-174">b.</span></span> <span data-ttu-id="4f9dd-175">Em **emissor IDP / ID da entidade** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-175">In **Your IDP Issuer/ Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4f9dd-176">c.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-176">c.</span></span> <span data-ttu-id="4f9dd-177">Clique em **alteração** toohello próximo **certificado x. 509** campo e, em seguida, upload do certificado Olá baixado do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-177">Click **Change** next toohello **X.509 Certificate** field and then upload hello certificate you downloaded from hello Azure portal.</span></span>
    
    <span data-ttu-id="4f9dd-178">d.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-178">d.</span></span> <span data-ttu-id="4f9dd-179">Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-179">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="4f9dd-180">e.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-180">e.</span></span> <span data-ttu-id="4f9dd-181">Em **URL de Logout** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-181">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="4f9dd-182">Clique em **salvar** em Olá portal de gerenciamento do Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-182">Click **Save** on hello Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="4f9dd-183">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="4f9dd-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4f9dd-184">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4f9dd-185">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4f9dd-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4f9dd-186">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f9dd-186">Create an Azure AD test user</span></span>

<span data-ttu-id="4f9dd-187">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="4f9dd-189">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4f9dd-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f9dd-190">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-190">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4f9dd-192">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-192">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4f9dd-194">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-194">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4f9dd-196">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9dd-196">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4f9dd-198">a.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-198">a.</span></span> <span data-ttu-id="4f9dd-199">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-199">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f9dd-200">b.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-200">b.</span></span> <span data-ttu-id="4f9dd-201">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-201">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4f9dd-202">c.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-202">c.</span></span> <span data-ttu-id="4f9dd-203">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-203">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4f9dd-204">d.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-204">d.</span></span> <span data-ttu-id="4f9dd-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="4f9dd-206">Criar um usuário de teste do Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="4f9dd-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="4f9dd-207">Em ordem tooenable AD do Azure usuários toolog no Citrix ShareFile, eles devem ser provisionados no Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-207">In order tooenable Azure AD users toolog into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="4f9dd-208">No caso de saudação do Citrix ShareFile, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-208">In hello case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="4f9dd-209">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4f9dd-209">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f9dd-210">Faça logon no tooyour **Citrix ShareFile** locatário.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-210">Log in tooyour **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="4f9dd-211">Clique em **Gerenciar Usuários \> Gerenciar Página Inicial dos Usuários \> + Criar Funcionário**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="4f9dd-212">![Criar Funcionário](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Criar Funcionário")</span><span class="sxs-lookup"><span data-stu-id="4f9dd-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="4f9dd-213">Em Olá **informações básicas** , execute etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9dd-213">On hello **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="4f9dd-214">![Informações Básicas](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Informações Básicas")</span><span class="sxs-lookup"><span data-stu-id="4f9dd-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="4f9dd-215">a.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-215">a.</span></span> <span data-ttu-id="4f9dd-216">Em Olá **endereço de Email** caixa de texto, endereço de email de saudação do tipo do Britta Simon como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="4f9dd-216">In hello **Email Address** textbox, type hello email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="4f9dd-217">b.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-217">b.</span></span> <span data-ttu-id="4f9dd-218">Em Olá **nome** caixa de texto, tipo **nome** do usuário como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-218">In hello **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="4f9dd-219">c.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-219">c.</span></span> <span data-ttu-id="4f9dd-220">Em Olá **Sobrenome** caixa de texto, tipo **Sobrenome** do usuário como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-220">In hello **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="4f9dd-221">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="4f9dd-222">proprietário de conta do AD do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa. Você pode usar qualquer ferramenta de criação outros Citrix ShareFile usuário conta ou APIs fornecidas pelo Citrix ShareFile tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-222">hello Azure AD account holder will receive an email and follow a link tooconfirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4f9dd-223">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4f9dd-223">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4f9dd-224">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix ShareFile.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="4f9dd-226">**tooassign tooCitrix Britta Simon ShareFile, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4f9dd-226">**tooassign Britta Simon tooCitrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f9dd-227">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4f9dd-229">Na lista de aplicativos hello, selecione **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-229">In hello applications list, select **Citrix ShareFile**.</span></span>

    ![Olá Citrix ShareFile link na lista de aplicativos Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="4f9dd-231">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="4f9dd-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-233">Click **Add** button.</span></span> <span data-ttu-id="4f9dd-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="4f9dd-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4f9dd-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f9dd-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4f9dd-239">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="4f9dd-239">Test single sign-on</span></span>

<span data-ttu-id="4f9dd-240">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4f9dd-241">Quando você clica em Olá Citrix ShareFile bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo da Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="4f9dd-241">When you click hello Citrix ShareFile tile in hello Access Panel, you should get automatically signed-on tooyour Citrix ShareFile application.</span></span>
<span data-ttu-id="4f9dd-242">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4f9dd-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4f9dd-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4f9dd-243">Additional resources</span></span>

* [<span data-ttu-id="4f9dd-244">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4f9dd-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f9dd-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4f9dd-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

