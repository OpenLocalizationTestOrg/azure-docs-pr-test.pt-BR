---
title: "Tutorial: Integração do Azure Active Directory com o Zoom | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Zoom."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 623a1f428ad1f0aa2c8205b79d61720cad5fc6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="08b2f-103">Tutorial: Integração do Active Directory do Azure com o Zoom</span><span class="sxs-lookup"><span data-stu-id="08b2f-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="08b2f-104">Neste tutorial, você aprenderá como toointegrate Zoom com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="08b2f-104">In this tutorial, you learn how toointegrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08b2f-105">Integrando o Zoom com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="08b2f-105">Integrating Zoom with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="08b2f-106">Você pode controlar no AD do Azure que tenha acesso tooZoom.</span><span class="sxs-lookup"><span data-stu-id="08b2f-106">You can control in Azure AD who has access tooZoom.</span></span>
- <span data-ttu-id="08b2f-107">Você pode habilitar seu usuários tooautomatically get conectado tooZoom (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="08b2f-107">You can enable your users tooautomatically get signed-on tooZoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="08b2f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08b2f-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="08b2f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="08b2f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08b2f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="08b2f-110">Prerequisites</span></span>

<span data-ttu-id="08b2f-111">integração de tooconfigure AD do Azure com Zoom, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="08b2f-111">tooconfigure Azure AD integration with Zoom, you need hello following items:</span></span>

- <span data-ttu-id="08b2f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08b2f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="08b2f-113">Uma assinatura do Zoom habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="08b2f-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="08b2f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="08b2f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="08b2f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="08b2f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="08b2f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="08b2f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="08b2f-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08b2f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08b2f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="08b2f-118">Scenario description</span></span>
<span data-ttu-id="08b2f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="08b2f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08b2f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="08b2f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08b2f-121">A adição de Zoom da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="08b2f-121">Adding Zoom from hello gallery</span></span>
2. <span data-ttu-id="08b2f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08b2f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-hello-gallery"></a><span data-ttu-id="08b2f-123">A adição de Zoom da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="08b2f-123">Adding Zoom from hello gallery</span></span>
<span data-ttu-id="08b2f-124">integração de saudação tooconfigure de Zoom no AD do Azure, você precisa tooadd Zoom na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="08b2f-124">tooconfigure hello integration of Zoom into Azure AD, you need tooadd Zoom from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="08b2f-125">**tooadd Zoom da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08b2f-125">**tooadd Zoom from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="08b2f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="08b2f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="08b2f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="08b2f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="08b2f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08b2f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="08b2f-133">Na caixa de pesquisa hello, digite **Zoom**, selecione **Zoom** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="08b2f-133">In hello search box, type **Zoom**, select **Zoom** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Aplicar zoom na lista de resultados de saudação](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="08b2f-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08b2f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="08b2f-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Zoom, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="08b2f-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="08b2f-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Zoom é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="08b2f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoom is tooa user in Azure AD.</span></span> <span data-ttu-id="08b2f-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e hello relacionados ao usuário no Zoom necessidades toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="08b2f-138">In other words, a link relationship between an Azure AD user and hello related user in Zoom needs toobe established.</span></span>

<span data-ttu-id="08b2f-139">Zoom, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="08b2f-139">In Zoom, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="08b2f-140">tooconfigure e teste de logon único do AD do Azure com Zoom, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="08b2f-140">tooconfigure and test Azure AD single sign-on with Zoom, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="08b2f-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="08b2f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="08b2f-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="08b2f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08b2f-143">**[Criar um usuário de teste de Zoom](#create-a-zoom-test-user)**  -toohave um equivalente do Britta Simon de Zoom que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="08b2f-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - toohave a counterpart of Britta Simon in Zoom that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="08b2f-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="08b2f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08b2f-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="08b2f-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="08b2f-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08b2f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="08b2f-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de Zoom.</span><span class="sxs-lookup"><span data-stu-id="08b2f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="08b2f-148">**tooconfigure logon único do AD do Azure com Zoom, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08b2f-148">**tooconfigure Azure AD single sign-on with Zoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="08b2f-149">Em Olá portal do Azure, Olá **Zoom** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-149">In hello Azure portal, on hello **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="08b2f-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="08b2f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="08b2f-153">Em Olá **domínio Zoom e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="08b2f-153">On hello **Zoom Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="08b2f-155">a.</span><span class="sxs-lookup"><span data-stu-id="08b2f-155">a.</span></span> <span data-ttu-id="08b2f-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="08b2f-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="08b2f-157">b.</span><span class="sxs-lookup"><span data-stu-id="08b2f-157">b.</span></span> <span data-ttu-id="08b2f-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="08b2f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="08b2f-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="08b2f-159">These values are not real.</span></span> <span data-ttu-id="08b2f-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="08b2f-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="08b2f-161">Entre em contato com [equipe de suporte de cliente Zoom](https://support.zoom.us/hc) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="08b2f-161">Contact [Zoom Client support team](https://support.zoom.us/hc) tooget these values.</span></span> 
 
4. <span data-ttu-id="08b2f-162">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="08b2f-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="08b2f-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="08b2f-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="08b2f-166">Em Olá **configuração Zoom** seção, clique em **configurar Zoom** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="08b2f-166">On hello **Zoom Configuration** section, click **Configure Zoom** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="08b2f-167">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="08b2f-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="08b2f-169">Em uma janela de navegador web diferente, faça logon no site da empresa Zoom tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="08b2f-169">In a different web browser window, log in tooyour Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="08b2f-170">Clique em Olá **Single Sign-On** guia.</span><span class="sxs-lookup"><span data-stu-id="08b2f-170">Click hello **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="08b2f-171">![Guia Logon único](./media/active-directory-saas-zoom-tutorial/IC784700.png "Logon único")</span><span class="sxs-lookup"><span data-stu-id="08b2f-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="08b2f-172">Clique em Olá **controle de segurança** guia e, em seguida, acesse toohello **Single Sign-On** configurações.</span><span class="sxs-lookup"><span data-stu-id="08b2f-172">Click hello **Security Control** tab, and then go toohello **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="08b2f-173">Olá seção de logon único, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="08b2f-173">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="08b2f-174">![Seção Logon único](./media/active-directory-saas-zoom-tutorial/IC784701.png "Logon único")</span><span class="sxs-lookup"><span data-stu-id="08b2f-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="08b2f-175">a.</span><span class="sxs-lookup"><span data-stu-id="08b2f-175">a.</span></span> <span data-ttu-id="08b2f-176">Em Olá **URL da página de entrada** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08b2f-176">In hello **Sign-in page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="08b2f-177">b.</span><span class="sxs-lookup"><span data-stu-id="08b2f-177">b.</span></span> <span data-ttu-id="08b2f-178">Em Olá **URL da página de logout** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08b2f-178">In hello **Sign-out page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="08b2f-179">c.</span><span class="sxs-lookup"><span data-stu-id="08b2f-179">c.</span></span> <span data-ttu-id="08b2f-180">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="08b2f-180">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="08b2f-181">d.</span><span class="sxs-lookup"><span data-stu-id="08b2f-181">d.</span></span> <span data-ttu-id="08b2f-182">Em hello **emissor** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08b2f-182">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="08b2f-183">e.</span><span class="sxs-lookup"><span data-stu-id="08b2f-183">e.</span></span> <span data-ttu-id="08b2f-184">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="08b2f-185">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="08b2f-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="08b2f-186">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="08b2f-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="08b2f-187">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="08b2f-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="08b2f-188">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08b2f-188">Create an Azure AD test user</span></span>

<span data-ttu-id="08b2f-189">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08b2f-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="08b2f-191">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08b2f-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="08b2f-192">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="08b2f-192">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="08b2f-194">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-194">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="08b2f-196">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08b2f-196">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="08b2f-198">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="08b2f-198">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="08b2f-200">a.</span><span class="sxs-lookup"><span data-stu-id="08b2f-200">a.</span></span> <span data-ttu-id="08b2f-201">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-201">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08b2f-202">b.</span><span class="sxs-lookup"><span data-stu-id="08b2f-202">b.</span></span> <span data-ttu-id="08b2f-203">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="08b2f-203">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="08b2f-204">c.</span><span class="sxs-lookup"><span data-stu-id="08b2f-204">c.</span></span> <span data-ttu-id="08b2f-205">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="08b2f-205">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="08b2f-206">d.</span><span class="sxs-lookup"><span data-stu-id="08b2f-206">d.</span></span> <span data-ttu-id="08b2f-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="08b2f-208">Criar um usuário de teste do Zoom</span><span class="sxs-lookup"><span data-stu-id="08b2f-208">Create a Zoom test user</span></span>

<span data-ttu-id="08b2f-209">Em ordem tooenable AD do Azure usuários toolog em tooZoom, eles devem ser provisionados no Zoom.</span><span class="sxs-lookup"><span data-stu-id="08b2f-209">In order tooenable Azure AD users toolog in tooZoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="08b2f-210">No caso de saudação de Zoom, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="08b2f-210">In hello case of Zoom, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="08b2f-211">tooprovision uma conta de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="08b2f-211">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="08b2f-212">Faça logon no tooyour **Zoom** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="08b2f-212">Log in tooyour **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="08b2f-213">Clique em Olá **gerenciamento de conta** guia e, em seguida, clique em **gerenciamento de usuário**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-213">Click hello **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="08b2f-214">No hello seção Gerenciamento de usuário, clique em **adicionar usuários**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-214">In hello User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="08b2f-215">![Gerenciamento de usuário](./media/active-directory-saas-zoom-tutorial/IC784703.png "Gerenciamento de usuário")</span><span class="sxs-lookup"><span data-stu-id="08b2f-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="08b2f-216">Em Olá **adicionar usuários** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="08b2f-216">On hello **Add users** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="08b2f-217">![Adicionar Usuários](./media/active-directory-saas-zoom-tutorial/IC784704.png "Adicionar Usuários")</span><span class="sxs-lookup"><span data-stu-id="08b2f-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="08b2f-218">a.</span><span class="sxs-lookup"><span data-stu-id="08b2f-218">a.</span></span> <span data-ttu-id="08b2f-219">Para **Tipo de Usuário**, selecione **Básico**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="08b2f-220">b.</span><span class="sxs-lookup"><span data-stu-id="08b2f-220">b.</span></span> <span data-ttu-id="08b2f-221">Em Olá **Emails** caixa de texto, endereço de email de saudação do tipo de um válida do Azure você deseja tooprovision de conta do AD.</span><span class="sxs-lookup"><span data-stu-id="08b2f-221">In hello **Emails** textbox, type hello email address of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="08b2f-222">c.</span><span class="sxs-lookup"><span data-stu-id="08b2f-222">c.</span></span> <span data-ttu-id="08b2f-223">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="08b2f-224">Você pode usar qualquer ferramenta de criação outros Zoom usuário conta ou APIs fornecidas pelo Zoom tooprovision Azure Active Directory as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="08b2f-224">You can use any other Zoom user account creation tools or APIs provided by Zoom tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="08b2f-225">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08b2f-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="08b2f-226">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooZoom.</span><span class="sxs-lookup"><span data-stu-id="08b2f-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoom.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="08b2f-228">**tooassign Britta Simon tooZoom, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08b2f-228">**tooassign Britta Simon tooZoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="08b2f-229">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="08b2f-231">Na lista de aplicativos hello, selecione **Zoom**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-231">In hello applications list, select **Zoom**.</span></span>

    ![link de Zoom de saudação na lista de aplicativos de saudação](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="08b2f-233">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="08b2f-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="08b2f-235">Click **Add** button.</span></span> <span data-ttu-id="08b2f-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08b2f-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="08b2f-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="08b2f-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="08b2f-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08b2f-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="08b2f-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08b2f-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="08b2f-241">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="08b2f-241">Test single sign-on</span></span>

<span data-ttu-id="08b2f-242">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="08b2f-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="08b2f-243">Quando você clica em um bloco de Zoom Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Zoom.</span><span class="sxs-lookup"><span data-stu-id="08b2f-243">When you click hello Zoom tile in hello Access Panel, you should get automatically signed-on tooyour Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="08b2f-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="08b2f-244">Additional resources</span></span>

* [<span data-ttu-id="08b2f-245">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="08b2f-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08b2f-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="08b2f-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

