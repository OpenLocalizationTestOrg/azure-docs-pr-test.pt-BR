---
title: "Tutorial: Integração do Azure Active Directory ao Gerenciador de Senhas Protetor e Cofre Digital | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Gerenciador de senhas guardião & Digital cofre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 01e59004e6bdccfca08094f9da6f82270d5028d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="4fa81-103">Tutorial: integração do Azure Active Directory ao Gerenciador de Senhas Protetor e Cofre Digital</span><span class="sxs-lookup"><span data-stu-id="4fa81-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="4fa81-104">Neste tutorial, você aprenderá como toointegrate Gerenciador de senhas guardião & cofre Digital com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4fa81-104">In this tutorial, you learn how toointegrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fa81-105">Integração do Gerenciador de senhas guardião & cofre Digital com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa81-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4fa81-106">Você pode controlar no AD do Azure que tenha acesso tooKeeper Gerenciador de senhas & Digital cofre</span><span class="sxs-lookup"><span data-stu-id="4fa81-106">You can control in Azure AD who has access tooKeeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="4fa81-107">Você pode habilitar seus usuários tooautomatically get conectado tooKeeper Gerenciador de senhas e cofre Digital (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa81-107">You can enable your users tooautomatically get signed-on tooKeeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4fa81-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa81-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4fa81-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4fa81-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fa81-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4fa81-110">Prerequisites</span></span>

<span data-ttu-id="4fa81-111">tooconfigure integração do AD do Azure com o Gerenciador de senhas guardião & Digital cofre, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa81-111">tooconfigure Azure AD integration with Keeper Password Manager & Digital Vault, you need hello following items:</span></span>

- <span data-ttu-id="4fa81-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa81-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4fa81-113">Uma assinatura habilitada para logon único do Gerenciador de Senhas Protetor e Cofre Digital</span><span class="sxs-lookup"><span data-stu-id="4fa81-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fa81-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4fa81-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4fa81-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4fa81-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4fa81-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4fa81-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4fa81-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fa81-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fa81-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4fa81-118">Scenario description</span></span>
<span data-ttu-id="4fa81-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4fa81-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4fa81-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="4fa81-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fa81-121">Adicionando o Gerenciador de senhas guardião & Digital cofre da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4fa81-121">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
2. <span data-ttu-id="4fa81-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa81-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-hello-gallery"></a><span data-ttu-id="4fa81-123">Adicionando o Gerenciador de senhas guardião & Digital cofre da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4fa81-123">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
<span data-ttu-id="4fa81-124">integração de saudação tooconfigure do Gerenciador de senhas guardião & cofre Digital no AD do Azure, você precisa tooadd Gerenciador de senhas guardião & cofre Digital na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4fa81-124">tooconfigure hello integration of Keeper Password Manager & Digital Vault into Azure AD, you need tooadd Keeper Password Manager & Digital Vault from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4fa81-125">**tooadd Gerenciador de senhas guardião & Digital cofre da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4fa81-125">**tooadd Keeper Password Manager & Digital Vault from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fa81-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4fa81-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4fa81-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4fa81-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4fa81-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4fa81-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4fa81-133">Na caixa de pesquisa hello, digite **Gerenciador de senhas guardião & cofre Digital**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-133">In hello search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="4fa81-135">No painel de resultados de saudação, selecione **Gerenciador de senhas guardião & cofre Digital**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4fa81-135">In hello results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4fa81-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa81-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4fa81-138">Nesta seção, você pode configurar e testar o logon único do Azure AD com o Gerenciador de Senhas Protetor e Cofre Digital com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="4fa81-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4fa81-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Gerenciador de senhas guardião & cofre Digital é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa81-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Keeper Password Manager & Digital Vault is tooa user in Azure AD.</span></span> <span data-ttu-id="4fa81-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Gerenciador de senhas guardião & cofre Digital precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4fa81-140">In other words, a link relationship between an Azure AD user and hello related user in Keeper Password Manager & Digital Vault needs toobe established.</span></span>

<span data-ttu-id="4fa81-141">No Gerenciador de senhas guardião & cofre Digital, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa81-141">In Keeper Password Manager & Digital Vault, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4fa81-142">tooconfigure e teste de logon único do AD do Azure com o Gerenciador de senhas guardião & Digital cofre, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa81-142">tooconfigure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4fa81-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4fa81-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4fa81-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fa81-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4fa81-145">**[Criar um usuário de teste do Gerenciador de senhas guardião & cofre Digital](#creating-a-keeperpasswordmanager-test-user)**  -toohave um equivalente do Britta Simon no Gerenciador de senhas guardião & cofre Digital que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4fa81-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - toohave a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4fa81-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="4fa81-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4fa81-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4fa81-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4fa81-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fa81-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4fa81-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Gerenciador de senhas guardião & Digital cofre.</span><span class="sxs-lookup"><span data-stu-id="4fa81-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="4fa81-150">**tooconfigure logon único do AD do Azure com o Gerenciador de senhas guardião & Digital cofre, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4fa81-150">**tooconfigure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fa81-151">Em Olá portal do Azure, Olá **Gerenciador de senhas guardião & cofre Digital** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-151">In hello Azure portal, on hello **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4fa81-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="4fa81-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="4fa81-155">Em Olá **Gerenciador de senhas guardião & domínio Digital de cofre e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa81-155">On hello **Keeper Password Manager & Digital Vault Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="4fa81-157">a.</span><span class="sxs-lookup"><span data-stu-id="4fa81-157">a.</span></span> <span data-ttu-id="4fa81-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="4fa81-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="4fa81-159">b.</span><span class="sxs-lookup"><span data-stu-id="4fa81-159">b.</span></span> <span data-ttu-id="4fa81-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="4fa81-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="4fa81-161">c.</span><span class="sxs-lookup"><span data-stu-id="4fa81-161">c.</span></span> <span data-ttu-id="4fa81-162">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="4fa81-162">In hello **Identifier** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4fa81-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4fa81-163">These values are not real.</span></span> <span data-ttu-id="4fa81-164">Atualize esses valores com URL de resposta real hello e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="4fa81-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="4fa81-165">Entre em contato com [equipe de suporte do Gerenciador de senhas guardião & cliente de cofre Digital](https://keepersecurity.com/contact.html) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="4fa81-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="4fa81-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4fa81-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="4fa81-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4fa81-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="4fa81-170">Em Olá **Gerenciador de senhas guardião & configuração cofre Digital** seção, clique em **configurar Gerenciador de senha guardião & cofre Digital** tooopen **configurar o logon**janela.</span><span class="sxs-lookup"><span data-stu-id="4fa81-170">On hello **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4fa81-171">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="4fa81-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="4fa81-173">tooconfigure logon único no **Gerenciador de senhas guardião & configuração cofre Digital** lado, seguir as diretrizes de saudação fornecidas no [guardião guia de suporte](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span><span class="sxs-lookup"><span data-stu-id="4fa81-173">tooconfigure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow hello guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="4fa81-174">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="4fa81-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4fa81-175">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa81-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4fa81-176">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4fa81-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4fa81-177">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa81-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="4fa81-178">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa81-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4fa81-180">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4fa81-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fa81-181">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4fa81-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4fa81-183">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4fa81-185">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa81-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4fa81-187">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa81-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4fa81-189">a.</span><span class="sxs-lookup"><span data-stu-id="4fa81-189">a.</span></span> <span data-ttu-id="4fa81-190">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fa81-191">b.</span><span class="sxs-lookup"><span data-stu-id="4fa81-191">b.</span></span> <span data-ttu-id="4fa81-192">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4fa81-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4fa81-193">c.</span><span class="sxs-lookup"><span data-stu-id="4fa81-193">c.</span></span> <span data-ttu-id="4fa81-194">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4fa81-195">d.</span><span class="sxs-lookup"><span data-stu-id="4fa81-195">d.</span></span> <span data-ttu-id="4fa81-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="4fa81-197">Como criar um usuário de teste do Gerenciador de Senhas Protetor Cofre Digital</span><span class="sxs-lookup"><span data-stu-id="4fa81-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="4fa81-198">tooenable AD do Azure usuários toolog em tooKeeper Gerenciador de senhas e cofre Digital, eles devem ser provisionados no Gerenciador de senhas guardião & Digital cofre.</span><span class="sxs-lookup"><span data-stu-id="4fa81-198">tooenable Azure AD users toolog in tooKeeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="4fa81-199">Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação serão criados no aplicativo hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4fa81-199">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="4fa81-200">Você pode contatar [suporte guardião](https://keepersecurity.com/contact.html), se você desejar que usuários toosetup manualmente.</span><span class="sxs-lookup"><span data-stu-id="4fa81-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want toosetup users manually.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4fa81-201">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa81-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4fa81-202">Nesta seção, você deve habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooKeeper Gerenciador de senhas & Digital cofre.</span><span class="sxs-lookup"><span data-stu-id="4fa81-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKeeper Password Manager & Digital Vault.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4fa81-204">**tooassign Britta Simon tooKeeper Gerenciador de senhas & Digital cofre, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4fa81-204">**tooassign Britta Simon tooKeeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fa81-205">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4fa81-207">Na lista de aplicativos hello, selecione **Gerenciador de senhas guardião & cofre Digital**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-207">In hello applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="4fa81-209">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4fa81-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4fa81-211">Click **Add** button.</span></span> <span data-ttu-id="4fa81-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4fa81-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4fa81-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa81-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4fa81-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4fa81-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4fa81-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4fa81-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4fa81-217">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4fa81-217">Testing single sign-on</span></span>

<span data-ttu-id="4fa81-218">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa81-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4fa81-219">Quando você clica em Olá Gerenciador de senhas guardião & Bloco de cofre Digital no painel de acesso de saudação, você deve obter a página de logon do aplicativo Gerenciador de senhas guardião & Digital cofre.</span><span class="sxs-lookup"><span data-stu-id="4fa81-219">When you click hello Keeper Password Manager & Digital Vault tile in hello Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="4fa81-220">Após a autenticação bem-sucedida, você deve obter no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="4fa81-220">Upon successful authentication, you should get into hello application.</span></span> <span data-ttu-id="4fa81-221">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4fa81-221">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4fa81-222">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4fa81-222">Additional resources</span></span>

* [<span data-ttu-id="4fa81-223">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa81-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fa81-224">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4fa81-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

