---
title: "Tutorial: Integração do Azure Active Directory com o Image Relay | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e retransmissão de imagem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="10874-103">Tutorial: Integração do Azure Active Directory com o Image Relay</span><span class="sxs-lookup"><span data-stu-id="10874-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="10874-104">Neste tutorial, você aprenderá como toointegrate retransmissão de imagem com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="10874-104">In this tutorial, you learn how toointegrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="10874-105">Integração de retransmissão de imagem com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="10874-105">Integrating Image Relay with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="10874-106">Você pode controlar no AD do Azure que tenha acesso tooImage retransmissão</span><span class="sxs-lookup"><span data-stu-id="10874-106">You can control in Azure AD who has access tooImage Relay</span></span>
- <span data-ttu-id="10874-107">Você pode habilitar seu usuários tooautomatically get conectado tooImage retransmissão (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10874-107">You can enable your users tooautomatically get signed-on tooImage Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="10874-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="10874-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="10874-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="10874-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10874-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="10874-110">Prerequisites</span></span>

<span data-ttu-id="10874-111">tooconfigure integração do AD do Azure com retransmissão de imagem, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="10874-111">tooconfigure Azure AD integration with Image Relay, you need hello following items:</span></span>

- <span data-ttu-id="10874-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10874-112">An Azure AD subscription</span></span>
- <span data-ttu-id="10874-113">Uma assinatura habilitada para logon único do Image Relay</span><span class="sxs-lookup"><span data-stu-id="10874-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="10874-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="10874-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="10874-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="10874-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="10874-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="10874-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="10874-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="10874-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="10874-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="10874-118">Scenario description</span></span>
<span data-ttu-id="10874-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="10874-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="10874-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="10874-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="10874-121">Adicionando a retransmissão de imagem da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="10874-121">Adding Image Relay from hello gallery</span></span>
2. <span data-ttu-id="10874-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10874-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-hello-gallery"></a><span data-ttu-id="10874-123">Adicionando a retransmissão de imagem da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="10874-123">Adding Image Relay from hello gallery</span></span>
<span data-ttu-id="10874-124">integração de saudação tooconfigure de retransmissão de imagem no AD do Azure, você precisa tooadd retransmissão de imagem na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="10874-124">tooconfigure hello integration of Image Relay into Azure AD, you need tooadd Image Relay from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="10874-125">**tooadd retransmissão de imagem da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10874-125">**tooadd Image Relay from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="10874-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="10874-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="10874-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="10874-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="10874-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="10874-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="10874-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10874-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="10874-133">Na caixa de pesquisa hello, digite **imagem retransmissão**.</span><span class="sxs-lookup"><span data-stu-id="10874-133">In hello search box, type **Image Relay**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="10874-135">No painel de resultados de saudação, selecione **imagem retransmissão**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="10874-135">In hello results panel, select **Image Relay**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="10874-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10874-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="10874-138">Nesta seção, você configura e testa o logon único do Azure AD com o Image Relay com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="10874-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="10874-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na imagem de retransmissão é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="10874-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Image Relay is tooa user in Azure AD.</span></span> <span data-ttu-id="10874-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na imagem de retransmissão precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="10874-140">In other words, a link relationship between an Azure AD user and hello related user in Image Relay needs toobe established.</span></span>

<span data-ttu-id="10874-141">Na imagem de retransmissão, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="10874-141">In Image Relay, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="10874-142">tooconfigure e teste de logon único do AD do Azure com a imagem de retransmissão, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="10874-142">tooconfigure and test Azure AD single sign-on with Image Relay, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="10874-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="10874-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="10874-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="10874-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="10874-145">**[Criar um usuário de teste de retransmissão de imagem](#creating-an-image-relay-test-user)**  -toohave um equivalente do Britta Simon na retransmissão de imagem que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="10874-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - toohave a counterpart of Britta Simon in Image Relay that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="10874-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="10874-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="10874-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="10874-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="10874-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="10874-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="10874-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de retransmissão de imagem.</span><span class="sxs-lookup"><span data-stu-id="10874-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="10874-150">**tooconfigure AD do Azure-logon único com retransmissão de imagem, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10874-150">**tooconfigure Azure AD single sign-on with Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="10874-151">Em Olá portal do Azure, Olá **imagem retransmissão** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="10874-151">In hello Azure portal, on hello **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="10874-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="10874-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="10874-155">Em Olá **domínio de retransmissão de imagem e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="10874-155">On hello **Image Relay Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="10874-157">a.</span><span class="sxs-lookup"><span data-stu-id="10874-157">a.</span></span> <span data-ttu-id="10874-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="10874-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="10874-159">b.</span><span class="sxs-lookup"><span data-stu-id="10874-159">b.</span></span> <span data-ttu-id="10874-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="10874-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="10874-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="10874-161">These values are not real.</span></span> <span data-ttu-id="10874-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="10874-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="10874-163">Entre em contato com [equipe de suporte do cliente de retransmissão de imagem](http://support.imagerelay.com/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="10874-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="10874-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="10874-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="10874-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="10874-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="10874-168">Em Olá **configuração de imagem de retransmissão** seção, clique em **configurar imagem retransmissão** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="10874-168">On hello **Image Relay Configuration** section, click **Configure Image Relay** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="10874-169">Saudação de cópia **URL do serviço de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="10874-169">Copy hello **Sign-Out Service URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="10874-171">Em outra janela do navegador, entre no site da empresa tooyour retransmissão de imagem como um administrador.</span><span class="sxs-lookup"><span data-stu-id="10874-171">In another browser window, sign in tooyour Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="10874-172">Na barra de ferramentas de saudação na parte superior do hello, clique em Olá **usuários e permissões** carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="10874-172">In hello toolbar on hello top, click hello **Users & Permissions** workload.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="10874-174">Clique em **Criar Nova Permissão**.</span><span class="sxs-lookup"><span data-stu-id="10874-174">Click **Create New Permission**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="10874-176">Em Olá **logon único** carga de trabalho, selecione Olá **este grupo pode apenas entrar por meio de logon único** caixa de seleção e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="10874-176">In hello **Single Sign On Settings** workload, select hello **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="10874-178">Vá muito**configurações de conta**.</span><span class="sxs-lookup"><span data-stu-id="10874-178">Go too**Account Settings**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="10874-180">Vá toohello **logon único** carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="10874-180">Go toohello **Single Sign On Settings** workload.</span></span>
    
     ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="10874-182">Em Olá **configurações SAML** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="10874-182">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="10874-184">a.</span><span class="sxs-lookup"><span data-stu-id="10874-184">a.</span></span> <span data-ttu-id="10874-185">Em **URL de logon** caixa de texto valor Olá colar **o URL de serviço de logon único** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="10874-185">In **Login URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="10874-186">b.</span><span class="sxs-lookup"><span data-stu-id="10874-186">b.</span></span> <span data-ttu-id="10874-187">Em **URL de Logout** caixa de texto valor Olá colar **URL do serviço de logon único** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="10874-187">In **Logout URL**  textbox, paste hello value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="10874-188">c.</span><span class="sxs-lookup"><span data-stu-id="10874-188">c.</span></span> <span data-ttu-id="10874-189">Em **Formato da Id de Nome**, selecione **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="10874-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="10874-190">d.</span><span class="sxs-lookup"><span data-stu-id="10874-190">d.</span></span> <span data-ttu-id="10874-191">Como **opções de associação para solicitações de saudação (imagem de retransmissão) do provedor de serviços**, selecione **POST associação**.</span><span class="sxs-lookup"><span data-stu-id="10874-191">As **Binding Options for Requests from hello Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="10874-192">e.</span><span class="sxs-lookup"><span data-stu-id="10874-192">e.</span></span> <span data-ttu-id="10874-193">Em **Certificado x.509**, clique em **Atualizar Certificado**.</span><span class="sxs-lookup"><span data-stu-id="10874-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="10874-195">f.</span><span class="sxs-lookup"><span data-stu-id="10874-195">f.</span></span> <span data-ttu-id="10874-196">Abra o certificado de saudação baixado no bloco de notas, copie o conteúdo de hello e cole-o na caixa de texto de certificado de x. 509 hello.</span><span class="sxs-lookup"><span data-stu-id="10874-196">Open hello downloaded certificate in notepad, copy hello content, and then paste it into hello x.509 Certificate textbox.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="10874-198">g.</span><span class="sxs-lookup"><span data-stu-id="10874-198">g.</span></span> <span data-ttu-id="10874-199">Em **just-in-provisionamento de usuário** seção, selecione Olá **habilitar provisionamento de usuário just-in-**.</span><span class="sxs-lookup"><span data-stu-id="10874-199">In **Just-In-Time User Provisioning** section, select hello **Enable Just-In-Time User Provisioning**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="10874-201">h.</span><span class="sxs-lookup"><span data-stu-id="10874-201">h.</span></span> <span data-ttu-id="10874-202">Grupo de permissão de Select hello (por exemplo, **SSO básico**) que é permitido toosign em apenas por meio de logon único.</span><span class="sxs-lookup"><span data-stu-id="10874-202">Select hello permission group (for example, **SSO Basic**) which is allowed toosign in only through single sign-on.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="10874-204">i.</span><span class="sxs-lookup"><span data-stu-id="10874-204">i.</span></span> <span data-ttu-id="10874-205">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="10874-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="10874-206">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="10874-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="10874-207">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="10874-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="10874-208">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="10874-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="10874-209">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10874-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="10874-210">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="10874-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="10874-212">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10874-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="10874-213">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="10874-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="10874-215">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="10874-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="10874-217">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="10874-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="10874-219">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="10874-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="10874-221">a.</span><span class="sxs-lookup"><span data-stu-id="10874-221">a.</span></span> <span data-ttu-id="10874-222">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="10874-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="10874-223">b.</span><span class="sxs-lookup"><span data-stu-id="10874-223">b.</span></span> <span data-ttu-id="10874-224">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="10874-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="10874-225">c.</span><span class="sxs-lookup"><span data-stu-id="10874-225">c.</span></span> <span data-ttu-id="10874-226">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="10874-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="10874-227">d.</span><span class="sxs-lookup"><span data-stu-id="10874-227">d.</span></span> <span data-ttu-id="10874-228">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="10874-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="10874-229">Criar um usuário de teste do Image Relay</span><span class="sxs-lookup"><span data-stu-id="10874-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="10874-230">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon na imagem de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="10874-230">hello objective of this section is toocreate a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="10874-231">**toocreate um usuário chamado Britta Simon na imagem de retransmissão, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10874-231">**toocreate a user called Britta Simon in Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="10874-232">Site de empresa de retransmissão de imagem tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="10874-232">Sign-on tooyour Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="10874-233">Vá muito**usuários e permissões** e selecione **criar usuário de SSO**.</span><span class="sxs-lookup"><span data-stu-id="10874-233">Go too**Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="10874-235">Digite hello **Email**, **nome**, **Sobrenome**, e **empresa** de usuário Olá deseja tooprovision e grupo de permissão de select Olá (por exemplo, SSO básica) que é o grupo de saudação que possa entrar apenas por meio de logon único.</span><span class="sxs-lookup"><span data-stu-id="10874-235">Enter hello **Email**, **First Name**, **Last Name**, and **Company** of hello user you want tooprovision and select hello permission group (for example, SSO Basic) which is hello group that can sign in only through single sign-on.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="10874-237">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="10874-237">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="10874-238">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10874-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="10874-239">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooImage retransmissão.</span><span class="sxs-lookup"><span data-stu-id="10874-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooImage Relay.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="10874-241">**tooassign Britta Simon tooImage retransmissão, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10874-241">**tooassign Britta Simon tooImage Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="10874-242">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="10874-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="10874-244">Na lista de aplicativos hello, selecione **imagem retransmissão**.</span><span class="sxs-lookup"><span data-stu-id="10874-244">In hello applications list, select **Image Relay**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="10874-246">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="10874-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="10874-248">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="10874-248">Click **Add** button.</span></span> <span data-ttu-id="10874-249">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10874-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="10874-251">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="10874-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="10874-252">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10874-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="10874-253">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10874-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="10874-254">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="10874-254">Testing single sign-on</span></span>

<span data-ttu-id="10874-255">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="10874-255">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>    

<span data-ttu-id="10874-256">Quando você clica em um bloco de imagem retransmissão Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de retransmissão de imagem.</span><span class="sxs-lookup"><span data-stu-id="10874-256">When you click hello Image Relay tile in hello Access Panel, you should get automatically signed-on tooyour Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="10874-257">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="10874-257">Additional resources</span></span>

* [<span data-ttu-id="10874-258">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="10874-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="10874-259">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="10874-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

