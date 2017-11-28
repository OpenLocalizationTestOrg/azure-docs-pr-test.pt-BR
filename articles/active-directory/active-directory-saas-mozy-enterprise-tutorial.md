---
title: "Tutorial: Integração do Azure Active Directory com o Mozy Enterprise | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="1b8d7-103">Tutorial: Integração do Active Directory do Azure com o Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="1b8d7-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="1b8d7-104">Neste tutorial, você aprenderá como toointegrate Mozy Enterprise com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="1b8d7-104">In this tutorial, you learn how toointegrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b8d7-105">Integrando o Mozy Enterprise com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b8d7-105">Integrating Mozy Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1b8d7-106">Você pode controlar no AD do Azure que tenha acesso tooMozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="1b8d7-106">You can control in Azure AD who has access tooMozy Enterprise</span></span>
- <span data-ttu-id="1b8d7-107">Você pode habilitar seu usuários tooautomatically get conectado tooMozy Enterprise (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b8d7-107">You can enable your users tooautomatically get signed-on tooMozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1b8d7-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1b8d7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1b8d7-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1b8d7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b8d7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1b8d7-110">Prerequisites</span></span>

<span data-ttu-id="1b8d7-111">tooconfigure integração do AD do Azure com o Mozy Enterprise, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b8d7-111">tooconfigure Azure AD integration with Mozy Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="1b8d7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b8d7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b8d7-113">Uma assinatura habilitada para logon único do Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="1b8d7-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b8d7-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b8d7-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1b8d7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b8d7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b8d7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b8d7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b8d7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1b8d7-118">Scenario description</span></span>
<span data-ttu-id="1b8d7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b8d7-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="1b8d7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b8d7-121">Adicionando Mozy Enterprise na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1b8d7-121">Adding Mozy Enterprise from hello gallery</span></span>
2. <span data-ttu-id="1b8d7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b8d7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-hello-gallery"></a><span data-ttu-id="1b8d7-123">Adicionando Mozy Enterprise na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1b8d7-123">Adding Mozy Enterprise from hello gallery</span></span>
<span data-ttu-id="1b8d7-124">integração de saudação tooconfigure do Mozy Enterprise no AD do Azure, você precisa tooadd Mozy Enterprise na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-124">tooconfigure hello integration of Mozy Enterprise into Azure AD, you need tooadd Mozy Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1b8d7-125">**tooadd Mozy Enterprise na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1b8d7-125">**tooadd Mozy Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b8d7-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1b8d7-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1b8d7-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1b8d7-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1b8d7-133">Na caixa de pesquisa hello, digite **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-133">In hello search box, type **Mozy Enterprise**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="1b8d7-135">No painel de resultados de saudação, selecione **Mozy Enterprise**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-135">In hello results panel, select **Mozy Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1b8d7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b8d7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1b8d7-138">Nesta seção, você configura e testa o logon único do Azure AD com o Mozy Enterprise, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="1b8d7-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b8d7-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Mozy Enterprise é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mozy Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="1b8d7-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Mozy Enterprise precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-140">In other words, a link relationship between an Azure AD user and hello related user in Mozy Enterprise needs toobe established.</span></span>

<span data-ttu-id="1b8d7-141">No Mozy Enterprise, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-141">In Mozy Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1b8d7-142">tooconfigure e teste de logon único do AD do Azure com o Mozy Enterprise, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b8d7-142">tooconfigure and test Azure AD single sign-on with Mozy Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1b8d7-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1b8d7-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b8d7-145">**[Criar um usuário de teste do Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  -toohave um equivalente do Britta Simon no Mozy Enterprise é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - toohave a counterpart of Britta Simon in Mozy Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1b8d7-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b8d7-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1b8d7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b8d7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1b8d7-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="1b8d7-150">**tooconfigure AD do Azure-logon único com o Mozy Enterprise, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1b8d7-150">**tooconfigure Azure AD single sign-on with Mozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b8d7-151">Em Olá portal do Azure, Olá **Mozy Enterprise** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-151">In hello Azure portal, on hello **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1b8d7-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="1b8d7-155">Em Olá **Mozy Enterprise domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b8d7-155">On hello **Mozy Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="1b8d7-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="1b8d7-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1b8d7-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-158">This value is not real.</span></span> <span data-ttu-id="1b8d7-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1b8d7-160">Entre em contato com [equipe de suporte do Mozy Enterprise Client](http://support.mozy.com/) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) tooget this value.</span></span>

4. <span data-ttu-id="1b8d7-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="1b8d7-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1b8d7-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1b8d7-165">Em Olá **Mozy Enterprise configuração** seção, clique em **configurar Mozy Enterprise** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-165">On hello **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1b8d7-166">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="1b8d7-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="1b8d7-168">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Mozy Enterprise como administrador.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="1b8d7-169">Em Olá **configuração** seção, clique em **política de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-169">In hello **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="1b8d7-170">![Política de autenticação](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Política de autenticação")</span><span class="sxs-lookup"><span data-stu-id="1b8d7-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="1b8d7-171">Em Olá **política de autenticação** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b8d7-171">On hello **Authentication Policy** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="1b8d7-172">![Política de autenticação](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Política de autenticação")</span><span class="sxs-lookup"><span data-stu-id="1b8d7-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="1b8d7-173">a.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-173">a.</span></span> <span data-ttu-id="1b8d7-174">Selecione **Serviço de Diretório** como **Provedor**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="1b8d7-175">b.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-175">b.</span></span> <span data-ttu-id="1b8d7-176">Selecione **Usar Push do LDAP**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="1b8d7-177">c.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-177">c.</span></span> <span data-ttu-id="1b8d7-178">Clique em Olá **autenticação SAML** guia.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-178">Click hello **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="1b8d7-179">d.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-179">d.</span></span> <span data-ttu-id="1b8d7-180">Colar **Single Sign-On URL do serviço SAML**, que você copiou de saudação portal do Azure em hello **URL autenticação** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-180">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="1b8d7-181">e.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-181">e.</span></span> <span data-ttu-id="1b8d7-182">Colar **ID da entidade SAML**, que você copiou de saudação portal do Azure em hello **ponto de extremidade do SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-182">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="1b8d7-183">f.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-183">f.</span></span> <span data-ttu-id="1b8d7-184">Abra seu certificado baixado de codificada de base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e cole Olá certificado inteiro na **certificado SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-184">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="1b8d7-185">g.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-185">g.</span></span> <span data-ttu-id="1b8d7-186">Selecione **habilitar SSO para administradores toolog com suas credenciais de rede**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-186">Select **Enable SSO for Admins toolog in with their network credentials**.</span></span>
   
   <span data-ttu-id="1b8d7-187">h.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-187">h.</span></span> <span data-ttu-id="1b8d7-188">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="1b8d7-189">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="1b8d7-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1b8d7-190">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1b8d7-191">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1b8d7-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1b8d7-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b8d7-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="1b8d7-193">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1b8d7-195">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1b8d7-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b8d7-196">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1b8d7-198">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1b8d7-200">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1b8d7-202">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b8d7-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1b8d7-204">a.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-204">a.</span></span> <span data-ttu-id="1b8d7-205">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b8d7-206">b.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-206">b.</span></span> <span data-ttu-id="1b8d7-207">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1b8d7-208">c.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-208">c.</span></span> <span data-ttu-id="1b8d7-209">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1b8d7-210">d.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-210">d.</span></span> <span data-ttu-id="1b8d7-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="1b8d7-212">Criando um usuário de teste do Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="1b8d7-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="1b8d7-213">Em ordem tooenable AD do Azure usuários toolog no Mozy Enterprise, eles devem ser provisionados no Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-213">In order tooenable Azure AD users toolog into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="1b8d7-214">No caso de saudação do Mozy Enterprise, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-214">In hello case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="1b8d7-215">Você pode usar qualquer ferramenta de criação outros Mozy Enterprise usuário conta ou APIs fornecidas pelo Mozy Enterprise tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise tooprovision AAD user accounts.</span></span>

<span data-ttu-id="1b8d7-216">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1b8d7-216">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b8d7-217">Faça logon no tooyour **Mozy Enterprise** locatário.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-217">Log in tooyour **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="1b8d7-218">Clique em **Usuários** e em **Adicionar Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="1b8d7-219">![Usuários](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="1b8d7-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1b8d7-220">Olá **adicionar novo usuário** opção somente é exibida somente se **Mozy** é selecionado como o provedor de saudação em **política de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-220">hello **Add New User** option is only displayed only if **Mozy** is selected as hello provider under **Authentication policy**.</span></span> <span data-ttu-id="1b8d7-221">Se a autenticação de SAML for configurada, em seguida, Olá usuários são adicionados automaticamente no seu primeiro logon por meio de logon único no.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-221">If SAML Authentication is configured, then hello users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="1b8d7-222">Na caixa de diálogo Olá de novo usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b8d7-222">On hello new user dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="1b8d7-223">![Adicionar Usuários](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Adicionar Usuários")</span><span class="sxs-lookup"><span data-stu-id="1b8d7-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="1b8d7-224">a.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-224">a.</span></span> <span data-ttu-id="1b8d7-225">De saudação **escolha um grupo de** lista, selecione um grupo.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-225">From hello **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="1b8d7-226">b.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-226">b.</span></span> <span data-ttu-id="1b8d7-227">De saudação **que tipo de usuário** lista, selecione um tipo.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-227">From hello **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="1b8d7-228">c.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-228">c.</span></span> <span data-ttu-id="1b8d7-229">Em Olá **Username** caixa de texto Nome do tipo saudação do usuário de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-229">In hello **Username** textbox, type hello name of hello Azure AD user.</span></span>
   
   <span data-ttu-id="1b8d7-230">d.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-230">d.</span></span> <span data-ttu-id="1b8d7-231">Em Olá **Email** caixa de texto, endereço de email do tipo saudação do usuário de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-231">In hello **Email** textbox, type hello email address of hello Azure AD user.</span></span>
   
   <span data-ttu-id="1b8d7-232">e.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-232">e.</span></span> <span data-ttu-id="1b8d7-233">Selecione **Enviar email de instruções ao usuário**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="1b8d7-234">f.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-234">f.</span></span> <span data-ttu-id="1b8d7-235">Clique em **Adicionar Usuário(s)**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="1b8d7-236">Depois de criar usuário Olá, um email será enviado de usuário do AD do Azure toohello que inclui uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-236">After creating hello user, an email will be sent toohello Azure AD user that includes a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1b8d7-237">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1b8d7-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1b8d7-238">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMozy Enterprise.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1b8d7-240">**tooassign Britta Simon tooMozy Enterprise, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1b8d7-240">**tooassign Britta Simon tooMozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b8d7-241">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1b8d7-243">Na lista de aplicativos hello, selecione **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-243">In hello applications list, select **Mozy Enterprise**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="1b8d7-245">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1b8d7-247">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-247">Click **Add** button.</span></span> <span data-ttu-id="1b8d7-248">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1b8d7-250">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1b8d7-251">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b8d7-252">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1b8d7-253">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1b8d7-253">Testing single sign-on</span></span>

<span data-ttu-id="1b8d7-254">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1b8d7-255">Quando você clica em Olá Mozy Enterprise bloco no painel de acesso de saudação, você deve obter a página de logon do aplicativo do Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="1b8d7-255">When you click hello Mozy Enterprise tile in hello Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="1b8d7-256">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1b8d7-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b8d7-257">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1b8d7-257">Additional resources</span></span>

* [<span data-ttu-id="1b8d7-258">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1b8d7-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b8d7-259">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b8d7-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

