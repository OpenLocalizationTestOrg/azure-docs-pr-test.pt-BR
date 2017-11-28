---
title: "Tutorial: Integração do Azure Active Directory com o Kintone | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Kintone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="b0aca-103">Tutorial: integração do Azure Active Directory com o Kintone</span><span class="sxs-lookup"><span data-stu-id="b0aca-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="b0aca-104">Neste tutorial, você aprenderá como toointegrate Kintone com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="b0aca-104">In this tutorial, you learn how toointegrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0aca-105">Integrando o Kintone com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0aca-105">Integrating Kintone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b0aca-106">Você pode controlar no AD do Azure que tenha acesso tooKintone</span><span class="sxs-lookup"><span data-stu-id="b0aca-106">You can control in Azure AD who has access tooKintone</span></span>
- <span data-ttu-id="b0aca-107">Você pode habilitar seu usuários tooautomatically get conectado tooKintone (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b0aca-107">You can enable your users tooautomatically get signed-on tooKintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0aca-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b0aca-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b0aca-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0aca-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0aca-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b0aca-110">Prerequisites</span></span>

<span data-ttu-id="b0aca-111">tooconfigure integração do AD do Azure com o Kintone, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0aca-111">tooconfigure Azure AD integration with Kintone, you need hello following items:</span></span>

- <span data-ttu-id="b0aca-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b0aca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0aca-113">Uma assinatura do Kintone com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="b0aca-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0aca-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b0aca-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0aca-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b0aca-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0aca-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b0aca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0aca-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0aca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0aca-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b0aca-118">Scenario description</span></span>
<span data-ttu-id="b0aca-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b0aca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0aca-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="b0aca-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0aca-121">Adicionando Kintone da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b0aca-121">Adding Kintone from hello gallery</span></span>
2. <span data-ttu-id="b0aca-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b0aca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-hello-gallery"></a><span data-ttu-id="b0aca-123">Adicionando Kintone da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b0aca-123">Adding Kintone from hello gallery</span></span>
<span data-ttu-id="b0aca-124">integração de saudação tooconfigure do Kintone no AD do Azure, você precisa tooadd Kintone da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b0aca-124">tooconfigure hello integration of Kintone into Azure AD, you need tooadd Kintone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b0aca-125">**tooadd Kintone da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b0aca-125">**tooadd Kintone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0aca-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b0aca-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b0aca-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b0aca-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="b0aca-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b0aca-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="b0aca-133">Na caixa de pesquisa hello, digite **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-133">In hello search box, type **Kintone**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="b0aca-135">No painel de resultados de saudação, selecione **Kintone**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b0aca-135">In hello results panel, select **Kintone**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b0aca-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b0aca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b0aca-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Kintone, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="b0aca-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0aca-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Kintone é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0aca-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kintone is tooa user in Azure AD.</span></span> <span data-ttu-id="b0aca-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Kintone precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b0aca-140">In other words, a link relationship between an Azure AD user and hello related user in Kintone needs toobe established.</span></span>

<span data-ttu-id="b0aca-141">No Kintone, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0aca-141">In Kintone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b0aca-142">tooconfigure e teste de logon único do AD do Azure com o Kintone, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0aca-142">tooconfigure and test Azure AD single sign-on with Kintone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b0aca-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b0aca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b0aca-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0aca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0aca-145">**[Criar um usuário de teste do Kintone](#creating-a-kintone-test-user)**  -toohave um equivalente do Britta Simon no Kintone é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="b0aca-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - toohave a counterpart of Britta Simon in Kintone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0aca-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="b0aca-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0aca-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="b0aca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b0aca-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0aca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b0aca-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Kintone.</span><span class="sxs-lookup"><span data-stu-id="b0aca-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="b0aca-150">**tooconfigure AD do Azure-logon único com o Kintone, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b0aca-150">**tooconfigure Azure AD single sign-on with Kintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0aca-151">Em Olá portal do Azure, Olá **Kintone** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-151">In hello Azure portal, on hello **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="b0aca-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="b0aca-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="b0aca-155">Em Olá **Kintone domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0aca-155">On hello **Kintone Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="b0aca-157">a.</span><span class="sxs-lookup"><span data-stu-id="b0aca-157">a.</span></span> <span data-ttu-id="b0aca-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="b0aca-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="b0aca-159">b.</span><span class="sxs-lookup"><span data-stu-id="b0aca-159">b.</span></span> <span data-ttu-id="b0aca-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0aca-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="b0aca-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="b0aca-161">These values are not real.</span></span> <span data-ttu-id="b0aca-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="b0aca-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b0aca-163">Entre em contato com [equipe de suporte do cliente Kintone](https://www.kintone.com/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="b0aca-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="b0aca-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b0aca-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="b0aca-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b0aca-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0aca-168">Em Olá **Kintone configuração** seção, clique em **configurar Kintone** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="b0aca-168">On hello **Kintone Configuration** section, click **Configure Kintone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b0aca-169">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="b0aca-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="b0aca-171">Em outra janela do navegador da Web, faça logon no site da sua empresa do **Kintone** como administrador.</span><span class="sxs-lookup"><span data-stu-id="b0aca-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="b0aca-172">Clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="b0aca-173">![Configurações](./media/active-directory-saas-kintone-tutorial/ic785879.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="b0aca-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="b0aca-174">Clique em **Usuários e administração do sistema**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="b0aca-175">![Administração do Sistema e de Usuários](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administração do Sistema e de Usuários")</span><span class="sxs-lookup"><span data-stu-id="b0aca-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="b0aca-176">Em **Administração do Sistema \> Segurança**, clique em **Logon**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="b0aca-177">![Logon](./media/active-directory-saas-kintone-tutorial/ic785881.png "Logon")</span><span class="sxs-lookup"><span data-stu-id="b0aca-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="b0aca-178">Selecione **Habilitar a autenticação do SAML**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="b0aca-179">![Autenticação SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="b0aca-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="b0aca-180">Olá seção autenticação SAML, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0aca-180">In hello SAML Authentication section, perform hello following steps:</span></span>
    
    <span data-ttu-id="b0aca-181">![Autenticação SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="b0aca-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="b0aca-182">a.</span><span class="sxs-lookup"><span data-stu-id="b0aca-182">a.</span></span> <span data-ttu-id="b0aca-183">Em Olá **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0aca-183">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="b0aca-184">b.</span><span class="sxs-lookup"><span data-stu-id="b0aca-184">b.</span></span> <span data-ttu-id="b0aca-185">Em Olá **URL de Logout** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0aca-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="b0aca-186">c.</span><span class="sxs-lookup"><span data-stu-id="b0aca-186">c.</span></span> <span data-ttu-id="b0aca-187">Clique em **procurar** tooupload seu certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="b0aca-187">Click **Browse** tooupload your downloaded certificate.</span></span>
    
    <span data-ttu-id="b0aca-188">d.</span><span class="sxs-lookup"><span data-stu-id="b0aca-188">d.</span></span> <span data-ttu-id="b0aca-189">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b0aca-190">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="b0aca-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b0aca-191">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="b0aca-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b0aca-192">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0aca-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b0aca-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b0aca-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="b0aca-194">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0aca-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="b0aca-196">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b0aca-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0aca-197">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b0aca-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0aca-199">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0aca-201">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0aca-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0aca-203">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0aca-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0aca-205">a.</span><span class="sxs-lookup"><span data-stu-id="b0aca-205">a.</span></span> <span data-ttu-id="b0aca-206">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0aca-207">b.</span><span class="sxs-lookup"><span data-stu-id="b0aca-207">b.</span></span> <span data-ttu-id="b0aca-208">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b0aca-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b0aca-209">c.</span><span class="sxs-lookup"><span data-stu-id="b0aca-209">c.</span></span> <span data-ttu-id="b0aca-210">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b0aca-211">d.</span><span class="sxs-lookup"><span data-stu-id="b0aca-211">d.</span></span> <span data-ttu-id="b0aca-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="b0aca-213">Criação de um usuário de teste do Kintone</span><span class="sxs-lookup"><span data-stu-id="b0aca-213">Creating a Kintone test user</span></span>

<span data-ttu-id="b0aca-214">tooenable AD do Azure usuários toolog em tooKintone, eles devem ser provisionados no Kintone.</span><span class="sxs-lookup"><span data-stu-id="b0aca-214">tooenable Azure AD users toolog in tooKintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="b0aca-215">No caso de saudação do Kintone, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="b0aca-215">In hello case of Kintone, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="b0aca-216">tooprovision uma conta de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0aca-216">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="b0aca-217">Faça logon no tooyour **Kintone** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="b0aca-217">Log in tooyour **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="b0aca-218">Clique em **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="b0aca-219">![Configurações](./media/active-directory-saas-kintone-tutorial/ic785879.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="b0aca-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="b0aca-220">Clique em **Usuários e administração do sistema**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="b0aca-221">![Administração do Sistema e de Usuários](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administração do Sistema e de Usuários")</span><span class="sxs-lookup"><span data-stu-id="b0aca-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="b0aca-222">Em **Administração de Usuários**, clique em **Departamentos e Usuários**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="b0aca-223">![Departamento e Usuários](./media/active-directory-saas-kintone-tutorial/ic785888.png "Departamento e Usuários")</span><span class="sxs-lookup"><span data-stu-id="b0aca-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="b0aca-224">Clique em **Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-224">Click **New User**.</span></span>
   
    <span data-ttu-id="b0aca-225">![Novos Usuários](./media/active-directory-saas-kintone-tutorial/ic785889.png "novos Usuários")</span><span class="sxs-lookup"><span data-stu-id="b0aca-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="b0aca-226">Em Olá **novo usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0aca-226">In hello **New User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b0aca-227">![Novos Usuários](./media/active-directory-saas-kintone-tutorial/ic785890.png "novos Usuários")</span><span class="sxs-lookup"><span data-stu-id="b0aca-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="b0aca-228">a.</span><span class="sxs-lookup"><span data-stu-id="b0aca-228">a.</span></span> <span data-ttu-id="b0aca-229">Digite um **exibir nome**, **nome de logon**, **nova senha**, **Confirmar senha**, **endereço de email**, e outros detalhes de uma conta válida do AAD que você deseja tooprovision em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="b0aca-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
 
    <span data-ttu-id="b0aca-230">b.</span><span class="sxs-lookup"><span data-stu-id="b0aca-230">b.</span></span> <span data-ttu-id="b0aca-231">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="b0aca-232">Você pode usar qualquer ferramenta de criação outros Kintone usuário conta ou APIs fornecidas pela Kintone tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="b0aca-232">You can use any other Kintone user account creation tools or APIs provided by Kintone tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b0aca-233">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b0aca-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b0aca-234">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooKintone.</span><span class="sxs-lookup"><span data-stu-id="b0aca-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKintone.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="b0aca-236">**tooassign Britta Simon tooKintone, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b0aca-236">**tooassign Britta Simon tooKintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0aca-237">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b0aca-239">Na lista de aplicativos hello, selecione **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-239">In hello applications list, select **Kintone**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="b0aca-241">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="b0aca-243">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b0aca-243">Click **Add** button.</span></span> <span data-ttu-id="b0aca-244">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b0aca-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="b0aca-246">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0aca-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b0aca-247">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b0aca-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0aca-248">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b0aca-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b0aca-249">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="b0aca-249">Testing single sign-on</span></span>

<span data-ttu-id="b0aca-250">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="b0aca-250">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b0aca-251">Quando você clica em bloco Kintone Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Kintone aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b0aca-251">When you click hello Kintone tile in hello Access Panel, you should get automatically signed-on tooyour Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0aca-252">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b0aca-252">Additional resources</span></span>

* [<span data-ttu-id="b0aca-253">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b0aca-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0aca-254">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b0aca-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

