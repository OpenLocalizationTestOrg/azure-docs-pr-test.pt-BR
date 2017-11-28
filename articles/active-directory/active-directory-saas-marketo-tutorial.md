---
title: "Tutorial: Integração do Azure Active Directory ao Marketo | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="7160d-103">Tutorial: Integração do Azure Active Directory com o Marketo</span><span class="sxs-lookup"><span data-stu-id="7160d-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="7160d-104">Neste tutorial, você aprenderá como toointegrate Marketo com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7160d-104">In this tutorial, you learn how toointegrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7160d-105">Integração do Marketo com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="7160d-105">Integrating Marketo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7160d-106">Você pode controlar no AD do Azure que tenha acesso tooMarketo</span><span class="sxs-lookup"><span data-stu-id="7160d-106">You can control in Azure AD who has access tooMarketo</span></span>
- <span data-ttu-id="7160d-107">Você pode habilitar seu usuários tooautomatically get conectado tooMarketo (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7160d-107">You can enable your users tooautomatically get signed-on tooMarketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7160d-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7160d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7160d-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7160d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7160d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7160d-110">Prerequisites</span></span>

<span data-ttu-id="7160d-111">tooconfigure integração do AD do Azure com Marketo, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7160d-111">tooconfigure Azure AD integration with Marketo, you need hello following items:</span></span>

- <span data-ttu-id="7160d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7160d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7160d-113">Uma assinatura habilitada para logon único do Marketo</span><span class="sxs-lookup"><span data-stu-id="7160d-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7160d-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7160d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7160d-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7160d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7160d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7160d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7160d-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7160d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7160d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7160d-118">Scenario description</span></span>
<span data-ttu-id="7160d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7160d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7160d-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="7160d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7160d-121">Adicionando Marketo da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7160d-121">Adding Marketo from hello gallery</span></span>
2. <span data-ttu-id="7160d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7160d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-hello-gallery"></a><span data-ttu-id="7160d-123">Adicionando Marketo da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7160d-123">Adding Marketo from hello gallery</span></span>
<span data-ttu-id="7160d-124">integração de saudação tooconfigure do Marketo para o AD do Azure, você precisa tooadd Marketo da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7160d-124">tooconfigure hello integration of Marketo into Azure AD, you need tooadd Marketo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7160d-125">**tooadd Marketo da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7160d-125">**tooadd Marketo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7160d-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7160d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7160d-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7160d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7160d-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7160d-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7160d-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7160d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7160d-133">Na caixa de pesquisa hello, digite **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="7160d-133">In hello search box, type **Marketo**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="7160d-135">No painel de resultados de saudação, selecione **Marketo**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7160d-135">In hello results panel, select **Marketo**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7160d-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7160d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7160d-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Marketo, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7160d-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7160d-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Marketo é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7160d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Marketo is tooa user in Azure AD.</span></span> <span data-ttu-id="7160d-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Marketo precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7160d-140">In other words, a link relationship between an Azure AD user and hello related user in Marketo needs toobe established.</span></span>

<span data-ttu-id="7160d-141">No Marketo, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="7160d-141">In Marketo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7160d-142">tooconfigure e teste de logon único do AD do Azure com Marketo, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="7160d-142">tooconfigure and test Azure AD single sign-on with Marketo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7160d-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7160d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7160d-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7160d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7160d-145">**[Criar um usuário de teste do Marketo](#creating-a-marketo-test-user)**  -toohave um equivalente do Britta Simon no Marketo é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7160d-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - toohave a counterpart of Britta Simon in Marketo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7160d-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="7160d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7160d-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7160d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7160d-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7160d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7160d-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Marketo.</span><span class="sxs-lookup"><span data-stu-id="7160d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="7160d-150">**tooconfigure AD do Azure-logon único com Marketo, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7160d-150">**tooconfigure Azure AD single sign-on with Marketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="7160d-151">Em Olá portal do Azure, Olá **Marketo** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="7160d-151">In hello Azure portal, on hello **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7160d-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="7160d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="7160d-155">Em Olá **Marketo domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7160d-155">On hello **Marketo Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="7160d-157">a.</span><span class="sxs-lookup"><span data-stu-id="7160d-157">a.</span></span> <span data-ttu-id="7160d-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="7160d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="7160d-159">b.</span><span class="sxs-lookup"><span data-stu-id="7160d-159">b.</span></span> <span data-ttu-id="7160d-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="7160d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7160d-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="7160d-161">These values are not real.</span></span> <span data-ttu-id="7160d-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="7160d-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="7160d-163">Entre em contato com [equipe de suporte do Marketo](http://investors.marketo.com/contactus.cfm) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="7160d-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) tooget these values.</span></span>
 
4. <span data-ttu-id="7160d-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7160d-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="7160d-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7160d-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7160d-168">Em Olá **Marketo configuração** seção, clique em **configurar Marketo** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="7160d-168">On hello **Marketo Configuration** section, click **Configure Marketo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7160d-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="7160d-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="7160d-171">tooget Munchkin Id do aplicativo, faça logon em tooMarketo usando credenciais de administrador e executar as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="7160d-171">tooget Munchkin Id of your application, log in tooMarketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="7160d-172">a.</span><span class="sxs-lookup"><span data-stu-id="7160d-172">a.</span></span> <span data-ttu-id="7160d-173">Faça logon no aplicativo tooMarketo usando credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="7160d-173">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="7160d-174">b.</span><span class="sxs-lookup"><span data-stu-id="7160d-174">b.</span></span> <span data-ttu-id="7160d-175">Clique em Olá **Admin** botão no painel de navegação superior hello.</span><span class="sxs-lookup"><span data-stu-id="7160d-175">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="7160d-177">c.</span><span class="sxs-lookup"><span data-stu-id="7160d-177">c.</span></span> <span data-ttu-id="7160d-178">Menu de integração toohello navegar e clique em Olá **link Munchkin**.</span><span class="sxs-lookup"><span data-stu-id="7160d-178">Navigate toohello Integration menu and click hello **Munchkin link**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="7160d-180">d.</span><span class="sxs-lookup"><span data-stu-id="7160d-180">d.</span></span> <span data-ttu-id="7160d-181">Copie Olá Id Munchkin mostrada na tela hello e concluir sua URL de resposta no Assistente de configuração de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7160d-181">Copy hello Munchkin Id shown on hello screen and complete your Reply URL in hello Azure AD configuration wizard.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="7160d-183">Olá tooconfigure SSO no aplicativo hello, siga Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7160d-183">tooconfigure hello SSO in hello application, follow hello below steps:</span></span>
   
    <span data-ttu-id="7160d-184">a.</span><span class="sxs-lookup"><span data-stu-id="7160d-184">a.</span></span> <span data-ttu-id="7160d-185">Faça logon no aplicativo tooMarketo usando credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="7160d-185">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="7160d-186">b.</span><span class="sxs-lookup"><span data-stu-id="7160d-186">b.</span></span> <span data-ttu-id="7160d-187">Clique em Olá **Admin** botão no painel de navegação superior hello.</span><span class="sxs-lookup"><span data-stu-id="7160d-187">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="7160d-189">c.</span><span class="sxs-lookup"><span data-stu-id="7160d-189">c.</span></span> <span data-ttu-id="7160d-190">Menu de integração toohello navegar e clique em **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="7160d-190">Navigate toohello Integration menu and click **Single Sign On**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="7160d-192">d.</span><span class="sxs-lookup"><span data-stu-id="7160d-192">d.</span></span> <span data-ttu-id="7160d-193">Olá tooenable configurações do SAML, clique em **editar** botão.</span><span class="sxs-lookup"><span data-stu-id="7160d-193">tooenable hello SAML Settings, click **Edit** button.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="7160d-195">e.</span><span class="sxs-lookup"><span data-stu-id="7160d-195">e.</span></span> <span data-ttu-id="7160d-196">Configurações de logon único **habilitadas**.</span><span class="sxs-lookup"><span data-stu-id="7160d-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="7160d-197">f.</span><span class="sxs-lookup"><span data-stu-id="7160d-197">f.</span></span> <span data-ttu-id="7160d-198">Saudação de colar **ID da entidade SAML**, em Olá **ID do emissor** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="7160d-198">Paste hello **SAML Entity ID**, in hello **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="7160d-199">g.</span><span class="sxs-lookup"><span data-stu-id="7160d-199">g.</span></span> <span data-ttu-id="7160d-200">Em Olá **ID da entidade** caixa de texto, digite a URL hello como `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="7160d-200">In hello **Entity ID** textbox, enter hello URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="7160d-201">h.</span><span class="sxs-lookup"><span data-stu-id="7160d-201">h.</span></span> <span data-ttu-id="7160d-202">Selecione Olá local de ID de usuário como **elemento identificador de nome**.</span><span class="sxs-lookup"><span data-stu-id="7160d-202">Select hello User ID Location as **Name Identifier element**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="7160d-204">Se o identificador de usuário não é valor UPN e alterar o valor de saudação no guia de atributo hello.</span><span class="sxs-lookup"><span data-stu-id="7160d-204">If your User Identifier is not UPN value then change hello value in hello Attribute tab.</span></span>
   
    <span data-ttu-id="7160d-205">i.</span><span class="sxs-lookup"><span data-stu-id="7160d-205">i.</span></span> <span data-ttu-id="7160d-206">Carregar certificado de saudação, que você baixou do Assistente de configuração do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7160d-206">Upload hello certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="7160d-207">**Salvar** Olá configurações.</span><span class="sxs-lookup"><span data-stu-id="7160d-207">**Save** hello settings.</span></span>
   
    <span data-ttu-id="7160d-208">j.</span><span class="sxs-lookup"><span data-stu-id="7160d-208">j.</span></span> <span data-ttu-id="7160d-209">Edite configurações de redirecionamento páginas hello.</span><span class="sxs-lookup"><span data-stu-id="7160d-209">Edit hello Redirect Pages settings.</span></span>
   
    <span data-ttu-id="7160d-210">k.</span><span class="sxs-lookup"><span data-stu-id="7160d-210">k.</span></span> <span data-ttu-id="7160d-211">Saudação de colar **Single Sign-On URL do serviço SAML** em Olá **URL de logon** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="7160d-211">Paste hello **SAML Single Sign-On Service URL** in hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="7160d-212">l.</span><span class="sxs-lookup"><span data-stu-id="7160d-212">l.</span></span> <span data-ttu-id="7160d-213">Saudação de colar **URL de logout** em Olá **URL de Logout** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="7160d-213">Paste hello **Sign-Out URL** in hello **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="7160d-214">m.</span><span class="sxs-lookup"><span data-stu-id="7160d-214">m.</span></span> <span data-ttu-id="7160d-215">Em Olá **URL de erro**, cópia seu **Marketo instância URL** e clique em **salvar** toosave configurações de botão.</span><span class="sxs-lookup"><span data-stu-id="7160d-215">In hello **Error URL**, copy your **Marketo instance URL** and click **Save** button toosave settings.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="7160d-217">tooenable Olá SSO para usuários, Olá concluir ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="7160d-217">tooenable hello SSO for users, complete hello following actions:</span></span>
   
    <span data-ttu-id="7160d-218">a.</span><span class="sxs-lookup"><span data-stu-id="7160d-218">a.</span></span> <span data-ttu-id="7160d-219">Faça logon no aplicativo tooMarketo usando credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="7160d-219">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="7160d-220">b.</span><span class="sxs-lookup"><span data-stu-id="7160d-220">b.</span></span> <span data-ttu-id="7160d-221">Clique em Olá **Admin** botão no painel de navegação superior hello.</span><span class="sxs-lookup"><span data-stu-id="7160d-221">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="7160d-223">c.</span><span class="sxs-lookup"><span data-stu-id="7160d-223">c.</span></span> <span data-ttu-id="7160d-224">Navegue toohello **segurança** menu e clique em **configurações de logon**.</span><span class="sxs-lookup"><span data-stu-id="7160d-224">Navigate toohello **Security** menu and click **Login Settings**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="7160d-226">d.</span><span class="sxs-lookup"><span data-stu-id="7160d-226">d.</span></span> <span data-ttu-id="7160d-227">Verificar Olá **exigem SSO** opção e **salvar** Olá configurações.</span><span class="sxs-lookup"><span data-stu-id="7160d-227">Check hello **Require SSO** option and **Save** hello settings.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="7160d-229">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="7160d-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7160d-230">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="7160d-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7160d-231">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7160d-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7160d-232">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7160d-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="7160d-233">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7160d-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7160d-235">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7160d-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7160d-236">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7160d-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7160d-238">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7160d-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7160d-240">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7160d-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7160d-242">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7160d-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7160d-244">a.</span><span class="sxs-lookup"><span data-stu-id="7160d-244">a.</span></span> <span data-ttu-id="7160d-245">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7160d-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7160d-246">b.</span><span class="sxs-lookup"><span data-stu-id="7160d-246">b.</span></span> <span data-ttu-id="7160d-247">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7160d-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7160d-248">c.</span><span class="sxs-lookup"><span data-stu-id="7160d-248">c.</span></span> <span data-ttu-id="7160d-249">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="7160d-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7160d-250">d.</span><span class="sxs-lookup"><span data-stu-id="7160d-250">d.</span></span> <span data-ttu-id="7160d-251">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7160d-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="7160d-252">Criar um usuário de teste do Marketo</span><span class="sxs-lookup"><span data-stu-id="7160d-252">Creating a Marketo test user</span></span>

<span data-ttu-id="7160d-253">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Marketo.</span><span class="sxs-lookup"><span data-stu-id="7160d-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="7160d-254">Siga essas etapas toocreate um usuário na plataforma do Marketo.</span><span class="sxs-lookup"><span data-stu-id="7160d-254">follow these steps toocreate a user in Marketo platform.</span></span>

1. <span data-ttu-id="7160d-255">Faça logon no aplicativo tooMarketo usando credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="7160d-255">Log in tooMarketo app using admin credentials.</span></span>

2. <span data-ttu-id="7160d-256">Clique em Olá **Admin** botão no painel de navegação superior hello.</span><span class="sxs-lookup"><span data-stu-id="7160d-256">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="7160d-258">Navegue toohello **segurança** menu e clique em **usuários e funções**</span><span class="sxs-lookup"><span data-stu-id="7160d-258">Navigate toohello **Security** menu and click **Users & Roles**</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="7160d-260">Clique em Olá **convidar novo usuário** link na guia de usuários Olá</span><span class="sxs-lookup"><span data-stu-id="7160d-260">Click hello **Invite New User** link on hello Users tab</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="7160d-262">Em Olá convidar novo usuário assistente preenchimento Olá informações a seguir</span><span class="sxs-lookup"><span data-stu-id="7160d-262">In hello Invite New User wizard fill hello following information</span></span>
   
    <span data-ttu-id="7160d-263">a.</span><span class="sxs-lookup"><span data-stu-id="7160d-263">a.</span></span> <span data-ttu-id="7160d-264">Insira o usuário Olá **Email** endereço na caixa de texto de saudação</span><span class="sxs-lookup"><span data-stu-id="7160d-264">Enter hello user **Email** address in hello textbox</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="7160d-266">b.</span><span class="sxs-lookup"><span data-stu-id="7160d-266">b.</span></span> <span data-ttu-id="7160d-267">Digite hello **nome** na caixa de texto de saudação</span><span class="sxs-lookup"><span data-stu-id="7160d-267">Enter hello **First Name** in hello textbox</span></span>
   
    <span data-ttu-id="7160d-268">c.</span><span class="sxs-lookup"><span data-stu-id="7160d-268">c.</span></span> <span data-ttu-id="7160d-269">Digite hello **Sobrenome** na caixa de texto de saudação</span><span class="sxs-lookup"><span data-stu-id="7160d-269">Enter hello **Last Name**  in hello textbox</span></span>
   
    <span data-ttu-id="7160d-270">d.</span><span class="sxs-lookup"><span data-stu-id="7160d-270">d.</span></span> <span data-ttu-id="7160d-271">Clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="7160d-271">Click **Next**</span></span>

6. <span data-ttu-id="7160d-272">Em Olá **permissões** guia, selecione Olá **userRoles** e clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="7160d-272">In hello **Permissions** tab, select hello **userRoles** and click **Next**</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="7160d-274">Clique em Olá **enviar** botão convite de usuário Olá toosend</span><span class="sxs-lookup"><span data-stu-id="7160d-274">Click hello **Send** button toosend hello user invitation</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="7160d-276">Usuário recebe a notificação por email hello e tem tooclick Olá vincular e altere a conta Olá Olá senha tooactivate.</span><span class="sxs-lookup"><span data-stu-id="7160d-276">User receives hello email notification and has tooclick hello link and change hello password tooactivate hello account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7160d-277">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7160d-277">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7160d-278">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMarketo.</span><span class="sxs-lookup"><span data-stu-id="7160d-278">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMarketo.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7160d-280">**tooassign Britta Simon tooMarketo, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7160d-280">**tooassign Britta Simon tooMarketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="7160d-281">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7160d-281">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7160d-283">Na lista de aplicativos hello, selecione **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="7160d-283">In hello applications list, select **Marketo**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="7160d-285">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7160d-285">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7160d-287">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7160d-287">Click **Add** button.</span></span> <span data-ttu-id="7160d-288">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7160d-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7160d-290">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="7160d-290">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7160d-291">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7160d-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7160d-292">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7160d-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7160d-293">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7160d-293">Testing single sign-on</span></span>

<span data-ttu-id="7160d-294">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7160d-294">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7160d-295">Quando você clica em bloco Marketo Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Marketo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7160d-295">When you click hello Marketo tile in hello Access Panel, you should get automatically signed-on tooyour Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7160d-296">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7160d-296">Additional resources</span></span>

* [<span data-ttu-id="7160d-297">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7160d-297">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7160d-298">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7160d-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

