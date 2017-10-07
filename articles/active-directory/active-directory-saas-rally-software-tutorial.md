---
title: "Tutorial: Integração do Azure Active Directory com o Rally Software | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Software Rally."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="52ea9-103">Tutorial: Integração do Azure Active Directory com o Rally Software</span><span class="sxs-lookup"><span data-stu-id="52ea9-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="52ea9-104">Neste tutorial, você aprenderá como toointegrate Software Rally com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="52ea9-104">In this tutorial, you learn how toointegrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52ea9-105">Integração do Software Rally com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="52ea9-105">Integrating Rally Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="52ea9-106">Você pode controlar no AD do Azure que tenha acesso tooRally Software.</span><span class="sxs-lookup"><span data-stu-id="52ea9-106">You can control in Azure AD who has access tooRally Software.</span></span>
- <span data-ttu-id="52ea9-107">Você pode habilitar seu usuários tooautomatically get conectado tooRally Software (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ea9-107">You can enable your users tooautomatically get signed-on tooRally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="52ea9-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ea9-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="52ea9-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52ea9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52ea9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="52ea9-110">Prerequisites</span></span>

<span data-ttu-id="52ea9-111">tooconfigure integração do AD do Azure com o Software Rally, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="52ea9-111">tooconfigure Azure AD integration with Rally Software, you need hello following items:</span></span>

- <span data-ttu-id="52ea9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52ea9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52ea9-113">Uma assinatura do Rally Software habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="52ea9-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52ea9-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="52ea9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52ea9-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="52ea9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52ea9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="52ea9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52ea9-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52ea9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52ea9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="52ea9-118">Scenario description</span></span>
<span data-ttu-id="52ea9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="52ea9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52ea9-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="52ea9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52ea9-121">Adicionar Software Rally da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="52ea9-121">Adding Rally Software from hello gallery</span></span>
2. <span data-ttu-id="52ea9-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52ea9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-hello-gallery"></a><span data-ttu-id="52ea9-123">Adicionar Software Rally da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="52ea9-123">Adding Rally Software from hello gallery</span></span>
<span data-ttu-id="52ea9-124">integração de saudação tooconfigure do Software Rally no AD do Azure, você precisa tooadd Rally Software na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="52ea9-124">tooconfigure hello integration of Rally Software into Azure AD, you need tooadd Rally Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="52ea9-125">**tooadd Software Rally da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52ea9-125">**tooadd Rally Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="52ea9-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="52ea9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="52ea9-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="52ea9-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="52ea9-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52ea9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="52ea9-133">Na caixa de pesquisa hello, digite **Software Rally**, selecione **Software Rally** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="52ea9-133">In hello search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Rally Software na lista de resultados de saudação](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="52ea9-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="52ea9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="52ea9-136">Nesta seção, você configura e testa o logon único do Azure AD com o Rally Software com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="52ea9-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="52ea9-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Rally Software é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ea9-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rally Software is tooa user in Azure AD.</span></span> <span data-ttu-id="52ea9-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Rally Software precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="52ea9-138">In other words, a link relationship between an Azure AD user and hello related user in Rally Software needs toobe established.</span></span>

<span data-ttu-id="52ea9-139">No Software Rally, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="52ea9-139">In Rally Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="52ea9-140">tooconfigure e teste de logon único do AD do Azure com o Rally Software, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="52ea9-140">tooconfigure and test Azure AD single sign-on with Rally Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="52ea9-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="52ea9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="52ea9-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52ea9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52ea9-143">**[Criar um usuário de teste do Software Rally](#create-a-rally-software-test-user)**  -toohave um equivalente do Britta Simon no Rally Software que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="52ea9-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - toohave a counterpart of Britta Simon in Rally Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="52ea9-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="52ea9-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52ea9-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="52ea9-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="52ea9-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="52ea9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="52ea9-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de Software Rally.</span><span class="sxs-lookup"><span data-stu-id="52ea9-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="52ea9-148">**tooconfigure AD do Azure-logon único com o Software Rally, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52ea9-148">**tooconfigure Azure AD single sign-on with Rally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="52ea9-149">Em Olá portal do Azure, Olá **Software Rally** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-149">In hello Azure portal, on hello **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="52ea9-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="52ea9-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="52ea9-153">Em Olá **Rally Software domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="52ea9-153">On hello **Rally Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="52ea9-155">a.</span><span class="sxs-lookup"><span data-stu-id="52ea9-155">a.</span></span> <span data-ttu-id="52ea9-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="52ea9-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="52ea9-157">b.</span><span class="sxs-lookup"><span data-stu-id="52ea9-157">b.</span></span> <span data-ttu-id="52ea9-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="52ea9-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="52ea9-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="52ea9-159">These values are not real.</span></span> <span data-ttu-id="52ea9-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="52ea9-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="52ea9-161">Entre em contato com [equipe de suporte do Rally Software cliente](https://help.rallydev.com/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="52ea9-161">Contact [Rally Software Client support team](https://help.rallydev.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="52ea9-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="52ea9-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="52ea9-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="52ea9-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52ea9-166">Em Olá **configuração do Software Rally** seção, clique em **configurar Software Rally** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="52ea9-166">On hello **Rally Software Configuration** section, click **Configure Rally Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="52ea9-167">Saudação de cópia **URL de logout e a ID da entidade SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="52ea9-167">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuração do Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="52ea9-169">Faça logon no tooyour **Software Rally** locatário.</span><span class="sxs-lookup"><span data-stu-id="52ea9-169">Log in tooyour **Rally Software** tenant.</span></span>

8. <span data-ttu-id="52ea9-170">Na barra de ferramentas de saudação na parte superior do hello, clique em **instalação**e, em seguida, selecione **assinatura**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-170">In hello toolbar on hello top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="52ea9-171">![Assinatura](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Assinatura")</span><span class="sxs-lookup"><span data-stu-id="52ea9-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="52ea9-172">Clique em Olá **ação** botão.</span><span class="sxs-lookup"><span data-stu-id="52ea9-172">Click hello **Action** button.</span></span> <span data-ttu-id="52ea9-173">Selecione **Editar assinatura** Olá superior direita da barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="52ea9-173">Select **Edit Subscription** at hello top right side of hello toolbar.</span></span>

10. <span data-ttu-id="52ea9-174">Em Olá **assinatura** página de diálogo Executar Olá etapas a seguir e, em seguida, clique em **Salvar & Fechar**:</span><span class="sxs-lookup"><span data-stu-id="52ea9-174">On hello **Subscription** dialog page, perform hello following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="52ea9-175">![Autenticação](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Autenticação")</span><span class="sxs-lookup"><span data-stu-id="52ea9-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="52ea9-176">a.</span><span class="sxs-lookup"><span data-stu-id="52ea9-176">a.</span></span> <span data-ttu-id="52ea9-177">Selecione **Autenticação do Rally ou SSO** na lista suspensa Autenticação.</span><span class="sxs-lookup"><span data-stu-id="52ea9-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="52ea9-178">b.</span><span class="sxs-lookup"><span data-stu-id="52ea9-178">b.</span></span> <span data-ttu-id="52ea9-179">Em hello **URL do provedor de identidade** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ea9-179">In hello **Identity provider URL** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="52ea9-180">c.</span><span class="sxs-lookup"><span data-stu-id="52ea9-180">c.</span></span> <span data-ttu-id="52ea9-181">Em Olá **logoff SSO** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ea9-181">In hello **SSO Logout** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="52ea9-182">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="52ea9-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="52ea9-183">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="52ea9-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="52ea9-184">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52ea9-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="52ea9-185">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="52ea9-185">Create an Azure AD test user</span></span>

<span data-ttu-id="52ea9-186">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ea9-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="52ea9-188">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52ea9-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="52ea9-189">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="52ea9-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="52ea9-191">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="52ea9-193">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52ea9-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="52ea9-195">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="52ea9-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="52ea9-197">a.</span><span class="sxs-lookup"><span data-stu-id="52ea9-197">a.</span></span> <span data-ttu-id="52ea9-198">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52ea9-199">b.</span><span class="sxs-lookup"><span data-stu-id="52ea9-199">b.</span></span> <span data-ttu-id="52ea9-200">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52ea9-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="52ea9-201">c.</span><span class="sxs-lookup"><span data-stu-id="52ea9-201">c.</span></span> <span data-ttu-id="52ea9-202">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="52ea9-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="52ea9-203">d.</span><span class="sxs-lookup"><span data-stu-id="52ea9-203">d.</span></span> <span data-ttu-id="52ea9-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="52ea9-205">Criar um usuário de teste do Rally Software</span><span class="sxs-lookup"><span data-stu-id="52ea9-205">Create a Rally Software test user</span></span>

<span data-ttu-id="52ea9-206">Para o AD do Azure usuários toobe capaz de toosign no, eles devem ser provisionado toohello aplicativo de Software Rally usando seus nomes de usuário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ea9-206">For Azure AD users toobe able toosign in, they must be provisioned toohello Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="52ea9-207">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52ea9-207">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="52ea9-208">Faça logon no tooyour locatário do Software Rally.</span><span class="sxs-lookup"><span data-stu-id="52ea9-208">Log in tooyour Rally Software tenant.</span></span>

2. <span data-ttu-id="52ea9-209">Vá muito**instalação \> usuários**e, em seguida, clique em **+ adicionar novo**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-209">Go too**Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="52ea9-210">![Usuários](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="52ea9-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="52ea9-211">Digite o nome de saudação na caixa de texto Olá novo usuário e, em seguida, clique em **adicionar detalhes**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-211">Type hello name in hello New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="52ea9-212">Em Olá **Create User** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="52ea9-212">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="52ea9-213">![Criar usuário](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="52ea9-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="52ea9-214">a.</span><span class="sxs-lookup"><span data-stu-id="52ea9-214">a.</span></span> <span data-ttu-id="52ea9-215">Em Olá **nome de usuário** caixa de texto Nome do tipo saudação do usuário como **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-215">In hello **User Name** textbox, type hello name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="52ea9-216">b.</span><span class="sxs-lookup"><span data-stu-id="52ea9-216">b.</span></span> <span data-ttu-id="52ea9-217">Em **endereço de email** caixa de texto, insira o email de saudação do usuário como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="52ea9-217">In **E-mail Address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="52ea9-218">c.</span><span class="sxs-lookup"><span data-stu-id="52ea9-218">c.</span></span> <span data-ttu-id="52ea9-219">Em **nome** texto, digite o nome saudação do usuário como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-219">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="52ea9-220">d.</span><span class="sxs-lookup"><span data-stu-id="52ea9-220">d.</span></span> <span data-ttu-id="52ea9-221">Em **Sobrenome** texto, digite o sobrenome de saudação do usuário como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-221">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="52ea9-222">e.</span><span class="sxs-lookup"><span data-stu-id="52ea9-222">e.</span></span> <span data-ttu-id="52ea9-223">Clique em **Salvar e Fechar**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="52ea9-224">Você pode usar qualquer ferramenta de criação outros Software Rally usuário conta ou APIs fornecidas pelo Software Rally tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ea9-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="52ea9-225">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52ea9-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="52ea9-226">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooRally Software.</span><span class="sxs-lookup"><span data-stu-id="52ea9-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRally Software.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="52ea9-228">**tooassign Britta Simon tooRally Software, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52ea9-228">**tooassign Britta Simon tooRally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="52ea9-229">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="52ea9-231">Na lista de aplicativos hello, selecione **Software Rally**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-231">In hello applications list, select **Rally Software**.</span></span>

    ![link do Software Rally Olá na lista de aplicativos Olá](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="52ea9-233">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="52ea9-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="52ea9-235">Click **Add** button.</span></span> <span data-ttu-id="52ea9-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52ea9-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="52ea9-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="52ea9-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="52ea9-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52ea9-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52ea9-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52ea9-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="52ea9-241">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="52ea9-241">Test single sign-on</span></span>

<span data-ttu-id="52ea9-242">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="52ea9-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="52ea9-243">Quando você clica em um bloco de Software Rally Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Software Rally.</span><span class="sxs-lookup"><span data-stu-id="52ea9-243">When you click hello Rally Software tile in hello Access Panel, you should get automatically signed-on tooyour Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="52ea9-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="52ea9-244">Additional resources</span></span>

* [<span data-ttu-id="52ea9-245">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="52ea9-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52ea9-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52ea9-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

