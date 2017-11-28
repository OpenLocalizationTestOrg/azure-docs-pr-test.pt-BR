---
title: "Tutorial: Integração do Azure Active Directory com o Envoy | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Envoy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="1f97c-103">Tutorial: integração do Active Directory do Azure ao Envoy</span><span class="sxs-lookup"><span data-stu-id="1f97c-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="1f97c-104">Neste tutorial, você aprenderá como toointegrate Envoy com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="1f97c-104">In this tutorial, you learn how toointegrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f97c-105">Integrando o Envoy com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f97c-105">Integrating Envoy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1f97c-106">Você pode controlar no AD do Azure que tenha acesso tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="1f97c-106">You can control in Azure AD who has access tooEnvoy.</span></span>
- <span data-ttu-id="1f97c-107">Você pode habilitar seu usuários tooautomatically get conectado tooEnvoy (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f97c-107">You can enable your users tooautomatically get signed-on tooEnvoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1f97c-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f97c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="1f97c-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f97c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f97c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1f97c-110">Prerequisites</span></span>

<span data-ttu-id="1f97c-111">tooconfigure integração do AD do Azure com o Envoy, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f97c-111">tooconfigure Azure AD integration with Envoy, you need hello following items:</span></span>

- <span data-ttu-id="1f97c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f97c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f97c-113">Uma assinatura do Envoy habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="1f97c-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f97c-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1f97c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f97c-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1f97c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f97c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1f97c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f97c-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f97c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f97c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1f97c-118">Scenario description</span></span>
<span data-ttu-id="1f97c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1f97c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f97c-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="1f97c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f97c-121">Adicionando Envoy da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1f97c-121">Adding Envoy from hello gallery</span></span>
2. <span data-ttu-id="1f97c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f97c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-hello-gallery"></a><span data-ttu-id="1f97c-123">Adicionando Envoy da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1f97c-123">Adding Envoy from hello gallery</span></span>
<span data-ttu-id="1f97c-124">integração de saudação tooconfigure do Envoy no AD do Azure, você precisa tooadd Envoy da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1f97c-124">tooconfigure hello integration of Envoy into Azure AD, you need tooadd Envoy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1f97c-125">**tooadd Envoy da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1f97c-125">**tooadd Envoy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f97c-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1f97c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="1f97c-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1f97c-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="1f97c-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f97c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="1f97c-133">Na caixa de pesquisa hello, digite **Envoy**, selecione **Envoy** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1f97c-133">In hello search box, type **Envoy**, select **Envoy** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Envoy na lista de resultados de saudação](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1f97c-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f97c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1f97c-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Envoy, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1f97c-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1f97c-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Envoy é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f97c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Envoy is tooa user in Azure AD.</span></span> <span data-ttu-id="1f97c-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Envoy precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1f97c-138">In other words, a link relationship between an Azure AD user and hello related user in Envoy needs toobe established.</span></span>

<span data-ttu-id="1f97c-139">No Envoy, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f97c-139">In Envoy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1f97c-140">tooconfigure e teste de logon único do AD do Azure com o Envoy, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f97c-140">tooconfigure and test Azure AD single sign-on with Envoy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1f97c-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1f97c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1f97c-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f97c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f97c-143">**[Criar um usuário de teste Envoy](#create-an-envoy-test-user)**  -toohave um equivalente do Britta Simon no Envoy é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="1f97c-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - toohave a counterpart of Britta Simon in Envoy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f97c-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="1f97c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f97c-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="1f97c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1f97c-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f97c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1f97c-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Envoy.</span><span class="sxs-lookup"><span data-stu-id="1f97c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="1f97c-148">**tooconfigure AD do Azure-logon único com o Envoy, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1f97c-148">**tooconfigure Azure AD single sign-on with Envoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f97c-149">Em Olá portal do Azure, Olá **Envoy** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-149">In hello Azure portal, on hello **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="1f97c-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="1f97c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="1f97c-153">Em Olá **Envoy domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f97c-153">On hello **Envoy Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="1f97c-155">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="1f97c-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="1f97c-156">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="1f97c-156">This value is not real.</span></span> <span data-ttu-id="1f97c-157">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="1f97c-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1f97c-158">Entre em contato com [equipe de suporte do cliente Envoy](https://envoy.com/contact/) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="1f97c-158">Contact [Envoy Client support team](https://envoy.com/contact/) tooget this value.</span></span>

4. <span data-ttu-id="1f97c-159">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="1f97c-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate..</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="1f97c-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1f97c-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1f97c-163">Em Olá **Envoy configuração** seção, clique em **configurar Envoy** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="1f97c-163">On hello **Envoy Configuration** section, click **Configure Envoy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1f97c-164">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="1f97c-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="1f97c-166">Em outra janela do navegador da Web, faça logon em seu site de empresa do Envoy como administrador.</span><span class="sxs-lookup"><span data-stu-id="1f97c-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="1f97c-167">Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-167">In hello toolbar on hello top, click **Settings**.</span></span>

    <span data-ttu-id="1f97c-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="1f97c-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="1f97c-169">Clique em **Empresa**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-169">Click **Company**.</span></span>

    <span data-ttu-id="1f97c-170">![Empresa](./media/active-directory-saas-envoy-tutorial/ic776783.png "Empresa")</span><span class="sxs-lookup"><span data-stu-id="1f97c-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="1f97c-171">Clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-171">Click **SAML**.</span></span>

    <span data-ttu-id="1f97c-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="1f97c-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="1f97c-173">Em Olá **autenticação SAML** configuração, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f97c-173">In hello **SAML Authentication** configuration section, perform hello following steps:</span></span>

    <span data-ttu-id="1f97c-174">![Autenticação SAML](./media/active-directory-saas-envoy-tutorial/ic776785.png "Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="1f97c-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="1f97c-175">valor Olá Olá ID de local de HQ é automaticamente gerado pelo aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1f97c-175">hello value for hello HQ location ID is auto generated by hello application.</span></span>
    
    <span data-ttu-id="1f97c-176">a.</span><span class="sxs-lookup"><span data-stu-id="1f97c-176">a.</span></span> <span data-ttu-id="1f97c-177">Em **impressão digital** caixa de texto, colar Olá **impressão digital** valor de certificado, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f97c-177">In **Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1f97c-178">b.</span><span class="sxs-lookup"><span data-stu-id="1f97c-178">b.</span></span> <span data-ttu-id="1f97c-179">Colar **Single Sign-On URL do serviço SAML** valor que você copiou formam hello Azure portal em Olá **URL HTTP de provedor de identidade SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1f97c-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form hello Azure portal into hello **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="1f97c-180">c.</span><span class="sxs-lookup"><span data-stu-id="1f97c-180">c.</span></span> <span data-ttu-id="1f97c-181">Clique em **Salvar alterações**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="1f97c-182">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="1f97c-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1f97c-183">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="1f97c-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1f97c-184">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f97c-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1f97c-185">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f97c-185">Create an Azure AD test user</span></span>

<span data-ttu-id="1f97c-186">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f97c-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="1f97c-188">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1f97c-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f97c-189">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="1f97c-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1f97c-191">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1f97c-193">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f97c-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1f97c-195">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f97c-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1f97c-197">a.</span><span class="sxs-lookup"><span data-stu-id="1f97c-197">a.</span></span> <span data-ttu-id="1f97c-198">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f97c-199">b.</span><span class="sxs-lookup"><span data-stu-id="1f97c-199">b.</span></span> <span data-ttu-id="1f97c-200">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f97c-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="1f97c-201">c.</span><span class="sxs-lookup"><span data-stu-id="1f97c-201">c.</span></span> <span data-ttu-id="1f97c-202">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="1f97c-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="1f97c-203">d.</span><span class="sxs-lookup"><span data-stu-id="1f97c-203">d.</span></span> <span data-ttu-id="1f97c-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="1f97c-205">Criar um usuário de teste do Envoy</span><span class="sxs-lookup"><span data-stu-id="1f97c-205">Create an Envoy test user</span></span>

<span data-ttu-id="1f97c-206">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="1f97c-206">There is no action item for you tooconfigure user provisioning tooEnvoy.</span></span> <span data-ttu-id="1f97c-207">Quando um usuário atribuído tenta toolog no Envoy usando o painel de acesso hello, o Envoy verifica se o usuário Olá existe.</span><span class="sxs-lookup"><span data-stu-id="1f97c-207">When an assigned user tries toolog into Envoy using hello access panel, Envoy checks whether hello user exists.</span></span> <span data-ttu-id="1f97c-208">Se ainda não houver uma conta de usuário, ela será criada automaticamente pelo Envoy.</span><span class="sxs-lookup"><span data-stu-id="1f97c-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1f97c-209">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f97c-209">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1f97c-210">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="1f97c-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEnvoy.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="1f97c-212">**tooassign Britta Simon tooEnvoy, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1f97c-212">**tooassign Britta Simon tooEnvoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f97c-213">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1f97c-215">Na lista de aplicativos hello, selecione **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-215">In hello applications list, select **Envoy**.</span></span>

    ![link de Envoy Olá na lista de aplicativos Olá](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="1f97c-217">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="1f97c-219">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1f97c-219">Click **Add** button.</span></span> <span data-ttu-id="1f97c-220">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f97c-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="1f97c-222">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f97c-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1f97c-223">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f97c-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f97c-224">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f97c-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1f97c-225">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="1f97c-225">Test single sign-on</span></span>

<span data-ttu-id="1f97c-226">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f97c-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1f97c-227">Quando você clica em bloco Envoy Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Envoy.</span><span class="sxs-lookup"><span data-stu-id="1f97c-227">When you click hello Envoy tile in hello Access Panel, you should get automatically signed-on tooyour Envoy application.</span></span>
<span data-ttu-id="1f97c-228">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f97c-228">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1f97c-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1f97c-229">Additional resources</span></span>

* [<span data-ttu-id="1f97c-230">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1f97c-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f97c-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f97c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

