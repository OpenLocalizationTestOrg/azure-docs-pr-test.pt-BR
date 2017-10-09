---
title: "Tutorial: integração do Azure Active Directory com o Peoplecart | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Peoplecart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c83b5d9d-2638-4689-b9f0-f56a9159e7a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 481c7246a63f669ab39cb4ec652cebf40ba35f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-peoplecart"></a><span data-ttu-id="52f58-103">Tutorial: integração do Azure Active Directory ao Peoplecart</span><span class="sxs-lookup"><span data-stu-id="52f58-103">Tutorial: Azure Active Directory integration with Peoplecart</span></span>

<span data-ttu-id="52f58-104">Neste tutorial, você aprenderá como toointegrate Peoplecart com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="52f58-104">In this tutorial, you learn how toointegrate Peoplecart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52f58-105">Integrando Peoplecart com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="52f58-105">Integrating Peoplecart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="52f58-106">Você pode controlar no AD do Azure que tenha acesso tooPeoplecart</span><span class="sxs-lookup"><span data-stu-id="52f58-106">You can control in Azure AD who has access tooPeoplecart</span></span>
- <span data-ttu-id="52f58-107">Você pode habilitar seu usuários tooautomatically get conectado tooPeoplecart (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52f58-107">You can enable your users tooautomatically get signed-on tooPeoplecart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52f58-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="52f58-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="52f58-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52f58-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52f58-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="52f58-110">Prerequisites</span></span>

<span data-ttu-id="52f58-111">tooconfigure integração do AD do Azure com Peoplecart, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="52f58-111">tooconfigure Azure AD integration with Peoplecart, you need hello following items:</span></span>

- <span data-ttu-id="52f58-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52f58-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52f58-113">Uma assinatura do Peoplecart habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="52f58-113">A Peoplecart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52f58-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="52f58-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52f58-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="52f58-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52f58-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="52f58-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52f58-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52f58-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52f58-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="52f58-118">Scenario description</span></span>
<span data-ttu-id="52f58-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="52f58-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52f58-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="52f58-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52f58-121">Adicionando Peoplecart da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="52f58-121">Adding Peoplecart from hello gallery</span></span>
2. <span data-ttu-id="52f58-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52f58-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-peoplecart-from-hello-gallery"></a><span data-ttu-id="52f58-123">Adicionando Peoplecart da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="52f58-123">Adding Peoplecart from hello gallery</span></span>
<span data-ttu-id="52f58-124">integração de saudação tooconfigure de Peoplecart no AD do Azure, você precisa tooadd Peoplecart da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="52f58-124">tooconfigure hello integration of Peoplecart into Azure AD, you need tooadd Peoplecart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="52f58-125">**tooadd Peoplecart da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52f58-125">**tooadd Peoplecart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="52f58-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="52f58-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="52f58-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="52f58-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="52f58-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="52f58-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="52f58-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52f58-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="52f58-133">Na caixa de pesquisa hello, digite **Peoplecart**, selecione **Peoplecart** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="52f58-133">In hello search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Peoplecart na lista de resultados de saudação](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="52f58-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="52f58-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="52f58-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Peoplecart, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="52f58-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="52f58-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Peoplecart é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="52f58-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Peoplecart is tooa user in Azure AD.</span></span> <span data-ttu-id="52f58-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Peoplecart precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="52f58-138">In other words, a link relationship between an Azure AD user and hello related user in Peoplecart needs toobe established.</span></span>

<span data-ttu-id="52f58-139">Peoplecart, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="52f58-139">In Peoplecart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="52f58-140">tooconfigure e teste de logon único do AD do Azure com Peoplecart, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="52f58-140">tooconfigure and test Azure AD single sign-on with Peoplecart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="52f58-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="52f58-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="52f58-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52f58-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52f58-143">**[Criar um usuário de teste Peoplecart](#create-a-peoplecart-test-user)**  -toohave um equivalente do Britta Simon em Peoplecart é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="52f58-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - toohave a counterpart of Britta Simon in Peoplecart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="52f58-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="52f58-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52f58-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="52f58-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="52f58-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="52f58-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="52f58-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="52f58-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Peoplecart application.</span></span>

<span data-ttu-id="52f58-148">**tooconfigure AD do Azure-logon único com Peoplecart, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52f58-148">**tooconfigure Azure AD single sign-on with Peoplecart, perform hello following steps:**</span></span>

1. <span data-ttu-id="52f58-149">Em Olá portal do Azure, Olá **Peoplecart** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="52f58-149">In hello Azure portal, on hello **Peoplecart** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="52f58-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="52f58-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_samlbase.png)

3. <span data-ttu-id="52f58-153">Em Olá **Peoplecart domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="52f58-153">On hello **Peoplecart Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_url.png)

    <span data-ttu-id="52f58-155">a.</span><span class="sxs-lookup"><span data-stu-id="52f58-155">a.</span></span> <span data-ttu-id="52f58-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.peoplecart.com/SignIn.aspx`</span><span class="sxs-lookup"><span data-stu-id="52f58-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span></span>

    <span data-ttu-id="52f58-157">b.</span><span class="sxs-lookup"><span data-stu-id="52f58-157">b.</span></span> <span data-ttu-id="52f58-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.peoplecart.com`</span><span class="sxs-lookup"><span data-stu-id="52f58-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.peoplecart.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="52f58-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="52f58-159">These values are not real.</span></span> <span data-ttu-id="52f58-160">Atualizar esses valores com hello URL de logon real e o identificador.</span><span class="sxs-lookup"><span data-stu-id="52f58-160">Update these values with hello actual Sign-On URL, and Identifier.</span></span> <span data-ttu-id="52f58-161">Entre em contato com [equipe de suporte do cliente Peoplecart](https://peoplecart.com/ContactUs.aspx) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="52f58-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) tooget these values.</span></span> 
 
4. <span data-ttu-id="52f58-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="52f58-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_certificate.png) 

5. <span data-ttu-id="52f58-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="52f58-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-peoplecart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52f58-166">Em Olá **Peoplecart configuração** seção, clique em **configurar Peoplecart** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="52f58-166">On hello **Peoplecart Configuration** section, click **Configure Peoplecart** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="52f58-167">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="52f58-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_configure.png) 

7. <span data-ttu-id="52f58-169">tooconfigure logon único no **Peoplecart** lado, você precisa toosend Olá baixado **Metadata XML** e **Single Sign-On URL do serviço SAML** muito[ A equipe de suporte Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="52f58-169">tooconfigure single sign-on on **Peoplecart** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span></span> <span data-ttu-id="52f58-170">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="52f58-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="52f58-171">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="52f58-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="52f58-172">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="52f58-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="52f58-173">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52f58-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="52f58-174">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="52f58-174">Create an Azure AD test user</span></span>
<span data-ttu-id="52f58-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="52f58-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="52f58-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52f58-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="52f58-178">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="52f58-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52f58-180">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="52f58-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52f58-182">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="52f58-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52f58-184">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="52f58-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52f58-186">a.</span><span class="sxs-lookup"><span data-stu-id="52f58-186">a.</span></span> <span data-ttu-id="52f58-187">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52f58-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52f58-188">b.</span><span class="sxs-lookup"><span data-stu-id="52f58-188">b.</span></span> <span data-ttu-id="52f58-189">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="52f58-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52f58-190">c.</span><span class="sxs-lookup"><span data-stu-id="52f58-190">c.</span></span> <span data-ttu-id="52f58-191">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="52f58-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="52f58-192">d.</span><span class="sxs-lookup"><span data-stu-id="52f58-192">d.</span></span> <span data-ttu-id="52f58-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="52f58-193">Click **Create**.</span></span>
 
### <a name="create-a-peoplecart-test-user"></a><span data-ttu-id="52f58-194">Criar um usuário de teste do Peoplecart</span><span class="sxs-lookup"><span data-stu-id="52f58-194">Create a Peoplecart test user</span></span>

<span data-ttu-id="52f58-195">Nesta seção, você criará um usuário chamado Brenda Fernandes no Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="52f58-195">In this section, you create a user called Britta Simon in Peoplecart.</span></span> <span data-ttu-id="52f58-196">Trabalhar com [Peoplecart a equipe de suporte](https://peoplecart.com/ContactUs.aspx) tooadd usuários de saudação na plataforma de Peoplecart hello.</span><span class="sxs-lookup"><span data-stu-id="52f58-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) tooadd hello users in hello Peoplecart platform.</span></span> <span data-ttu-id="52f58-197">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="52f58-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="52f58-198">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52f58-198">Assign hello Azure AD test user</span></span>

<span data-ttu-id="52f58-199">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPeoplecart.</span><span class="sxs-lookup"><span data-stu-id="52f58-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeoplecart.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="52f58-201">**tooassign Britta Simon tooPeoplecart, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52f58-201">**tooassign Britta Simon tooPeoplecart, perform hello following steps:**</span></span>

1. <span data-ttu-id="52f58-202">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="52f58-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="52f58-204">Na lista de aplicativos hello, selecione **Peoplecart**.</span><span class="sxs-lookup"><span data-stu-id="52f58-204">In hello applications list, select **Peoplecart**.</span></span>

    ![link de Peoplecart Olá na lista de aplicativos Olá](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_app.png) 

3. <span data-ttu-id="52f58-206">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="52f58-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202] 

4. <span data-ttu-id="52f58-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="52f58-208">Click **Add** button.</span></span> <span data-ttu-id="52f58-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52f58-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="52f58-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="52f58-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="52f58-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52f58-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52f58-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52f58-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="52f58-214">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="52f58-214">Test single sign-on</span></span>

<span data-ttu-id="52f58-215">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="52f58-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="52f58-216">Quando você clica em bloco Peoplecart Olá Olá painel de acesso, você deve obter a página de logon do aplicativo Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="52f58-216">When you click hello Peoplecart tile in hello Access Panel, you should get login page of Peoplecart application.</span></span>
<span data-ttu-id="52f58-217">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="52f58-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="52f58-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="52f58-218">Additional resources</span></span>

* [<span data-ttu-id="52f58-219">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="52f58-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52f58-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52f58-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_203.png

