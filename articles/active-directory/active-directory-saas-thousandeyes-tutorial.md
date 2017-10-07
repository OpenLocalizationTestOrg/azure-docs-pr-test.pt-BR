---
title: "Tutorial: Integração do Azure Active Directory ao ThousandEyes | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ThousandEyes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="a9f84-103">Tutorial: Integração do Active Directory do Azure ao ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="a9f84-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="a9f84-104">Neste tutorial, você aprenderá como toointegrate ThousandEyes com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="a9f84-104">In this tutorial, you learn how toointegrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9f84-105">Integrando ThousandEyes com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9f84-105">Integrating ThousandEyes with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a9f84-106">Você pode controlar no AD do Azure que tenha acesso tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="a9f84-106">You can control in Azure AD who has access tooThousandEyes</span></span>
- <span data-ttu-id="a9f84-107">Você pode habilitar seus usuários tooautomatically get conectado tooThousandEyes (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a9f84-107">You can enable your users tooautomatically get signed-on tooThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a9f84-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a9f84-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a9f84-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a9f84-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9f84-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a9f84-110">Prerequisites</span></span>

<span data-ttu-id="a9f84-111">tooconfigure integração do AD do Azure com ThousandEyes, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9f84-111">tooconfigure Azure AD integration with ThousandEyes, you need hello following items:</span></span>

- <span data-ttu-id="a9f84-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a9f84-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9f84-113">Uma assinatura do ThousandEyes habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="a9f84-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9f84-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a9f84-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9f84-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a9f84-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9f84-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a9f84-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9f84-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9f84-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9f84-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a9f84-118">Scenario description</span></span>
<span data-ttu-id="a9f84-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a9f84-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9f84-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="a9f84-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9f84-121">Adicionando ThousandEyes da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a9f84-121">Adding ThousandEyes from hello gallery</span></span>
2. <span data-ttu-id="a9f84-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a9f84-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-hello-gallery"></a><span data-ttu-id="a9f84-123">Adicionando ThousandEyes da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a9f84-123">Adding ThousandEyes from hello gallery</span></span>
<span data-ttu-id="a9f84-124">integração de saudação tooconfigure do ThousandEyes no AD do Azure, você precisa tooadd ThousandEyes da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a9f84-124">tooconfigure hello integration of ThousandEyes into Azure AD, you need tooadd ThousandEyes from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a9f84-125">**tooadd ThousandEyes da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a9f84-125">**tooadd ThousandEyes from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9f84-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a9f84-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a9f84-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a9f84-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a9f84-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a9f84-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a9f84-133">Na caixa de pesquisa hello, digite **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-133">In hello search box, type **ThousandEyes**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="a9f84-135">No painel de resultados de saudação, selecione **ThousandEyes**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a9f84-135">In hello results panel, select **ThousandEyes**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a9f84-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a9f84-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a9f84-138">Nesta seção, você configurará e testará o logon único do Azure AD com o ThousandEyes, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a9f84-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9f84-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ThousandEyes é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9f84-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThousandEyes is tooa user in Azure AD.</span></span> <span data-ttu-id="a9f84-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no ThousandEyes precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a9f84-140">In other words, a link relationship between an Azure AD user and hello related user in ThousandEyes needs toobe established.</span></span>

<span data-ttu-id="a9f84-141">No ThousandEyes, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9f84-141">In ThousandEyes, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a9f84-142">tooconfigure e teste de logon único do AD do Azure com ThousandEyes, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9f84-142">tooconfigure and test Azure AD single sign-on with ThousandEyes, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a9f84-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a9f84-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a9f84-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9f84-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a9f84-145">**[Criar um usuário de teste ThousandEyes](#creating-a-thousandeyes-test-user)**  -toohave um equivalente do Britta Simon no ThousandEyes é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="a9f84-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - toohave a counterpart of Britta Simon in ThousandEyes that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a9f84-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="a9f84-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a9f84-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="a9f84-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a9f84-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9f84-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a9f84-149">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="a9f84-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="a9f84-150">**tooconfigure AD do Azure-logon único com ThousandEyes, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a9f84-150">**tooconfigure Azure AD single sign-on with ThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9f84-151">Em Olá portal do Azure, Olá **ThousandEyes** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-151">In hello Azure portal, on hello **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a9f84-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="a9f84-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="a9f84-155">Em Olá **ThousandEyes domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9f84-155">On hello **ThousandEyes Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="a9f84-157">Em Olá **URL de logon** caixa de texto, digite um URL como:`https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="a9f84-157">In hello **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="a9f84-158">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a9f84-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="a9f84-160">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a9f84-160">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a9f84-162">Em Olá **ThousandEyes configuração** seção, clique em **configurar ThousandEyes** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="a9f84-162">On hello **ThousandEyes Configuration** section, click **Configure ThousandEyes** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a9f84-163">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="a9f84-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="a9f84-165">Em uma janela de navegador web diferente, logon tooyour **ThousandEyes** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="a9f84-165">In a different web browser window, sign on tooyour **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="a9f84-166">No menu de saudação na parte superior de saudação, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-166">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="a9f84-167">![Configurações](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="a9f84-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="a9f84-168">Clique em **Conta**</span><span class="sxs-lookup"><span data-stu-id="a9f84-168">Click **Account**</span></span>
   
    <span data-ttu-id="a9f84-169">![Conta](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Conta")</span><span class="sxs-lookup"><span data-stu-id="a9f84-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="a9f84-170">Clique em Olá **segurança & autenticação** guia.</span><span class="sxs-lookup"><span data-stu-id="a9f84-170">Click hello **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="a9f84-171">![Segurança e autenticação](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Segurança e autenticação")</span><span class="sxs-lookup"><span data-stu-id="a9f84-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="a9f84-172">Em Olá **instalação Single Sign-On** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9f84-172">In hello **Setup Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a9f84-173">![Configurar o logon único](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Configurar o logon único")</span><span class="sxs-lookup"><span data-stu-id="a9f84-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="a9f84-174">a.</span><span class="sxs-lookup"><span data-stu-id="a9f84-174">a.</span></span> <span data-ttu-id="a9f84-175">Selecione **Habilitar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="a9f84-176">b.</span><span class="sxs-lookup"><span data-stu-id="a9f84-176">b.</span></span> <span data-ttu-id="a9f84-177">Na caixa de texto **URL de Página de Logon**, cole a **URL do Serviço de Logon Único SAML** copiada do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9f84-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="a9f84-178">c.</span><span class="sxs-lookup"><span data-stu-id="a9f84-178">c.</span></span> <span data-ttu-id="a9f84-179">Na caixa de texto **URL de Página de Logoff**, cole a **URL de Saída** copiada do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9f84-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="a9f84-180">d.</span><span class="sxs-lookup"><span data-stu-id="a9f84-180">d.</span></span> <span data-ttu-id="a9f84-181">Na caixa de texto **Emissor do Provedor de Identidade**, cole a **ID de Entidade SAML** copiada do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9f84-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="a9f84-182">e.</span><span class="sxs-lookup"><span data-stu-id="a9f84-182">e.</span></span> <span data-ttu-id="a9f84-183">Em **certificado de verificação**, clique em **Escolher arquivo**e, em seguida, carregue o certificado de saudação que baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9f84-183">In **Verification Certificate**, click **Choose file**, and then upload hello certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="a9f84-184">f.</span><span class="sxs-lookup"><span data-stu-id="a9f84-184">f.</span></span> <span data-ttu-id="a9f84-185">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="a9f84-186">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="a9f84-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a9f84-187">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="a9f84-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a9f84-188">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a9f84-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a9f84-189">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a9f84-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="a9f84-190">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9f84-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a9f84-192">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a9f84-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9f84-193">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a9f84-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a9f84-195">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a9f84-197">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9f84-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a9f84-199">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9f84-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a9f84-201">a.</span><span class="sxs-lookup"><span data-stu-id="a9f84-201">a.</span></span> <span data-ttu-id="a9f84-202">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9f84-203">b.</span><span class="sxs-lookup"><span data-stu-id="a9f84-203">b.</span></span> <span data-ttu-id="a9f84-204">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a9f84-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a9f84-205">c.</span><span class="sxs-lookup"><span data-stu-id="a9f84-205">c.</span></span> <span data-ttu-id="a9f84-206">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a9f84-207">d.</span><span class="sxs-lookup"><span data-stu-id="a9f84-207">d.</span></span> <span data-ttu-id="a9f84-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="a9f84-209">Criação de um usuário de teste do ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="a9f84-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="a9f84-210">Ordem tooenable AD do Azure usuários toolog no ThousandEyes, eles devem ser provisionados no ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="a9f84-210">In order tooenable Azure AD users toolog into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="a9f84-211">No caso de saudação de ThousandEyes, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="a9f84-211">In hello case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="a9f84-212">Você pode usar qualquer ferramenta de criação outros ThousandEyes usuário conta ou APIs fornecidas pelo ThousandEyes tooprovision Azure Active Directory as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="a9f84-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="a9f84-213">**tooprovision um tooThousandEyes de conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a9f84-213">**tooprovision a user account tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9f84-214">Faça logon em seu site de empresa ThousandEyes como um administrador.</span><span class="sxs-lookup"><span data-stu-id="a9f84-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="a9f84-215">Clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="a9f84-216">![Configurações](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="a9f84-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="a9f84-217">Clique em **Conta**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-217">Click **Account**.</span></span>
   
    <span data-ttu-id="a9f84-218">![Conta](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Conta")</span><span class="sxs-lookup"><span data-stu-id="a9f84-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="a9f84-219">Clique em Olá **contas & usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="a9f84-219">Click hello **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="a9f84-220">![Contas e usuários](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Contas e usuários")</span><span class="sxs-lookup"><span data-stu-id="a9f84-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="a9f84-221">Em Olá **adicionar usuários e contas** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9f84-221">In hello **Add Users & Accounts** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a9f84-222">![Adicionar contas de usuário](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Adicionar contas de usuário")</span><span class="sxs-lookup"><span data-stu-id="a9f84-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="a9f84-223">a.</span><span class="sxs-lookup"><span data-stu-id="a9f84-223">a.</span></span> <span data-ttu-id="a9f84-224">Em **nome** caixa de texto Nome do tipo saudação do usuário como **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-224">In **Name** textbox, type hello name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="a9f84-225">b.</span><span class="sxs-lookup"><span data-stu-id="a9f84-225">b.</span></span> <span data-ttu-id="a9f84-226">Em **Email** caixa de texto, como o email de saudação do tipo de usuário  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="a9f84-226">In **Email** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="a9f84-227">b.</span><span class="sxs-lookup"><span data-stu-id="a9f84-227">b.</span></span> <span data-ttu-id="a9f84-228">Clique em **tooAccount adicionar novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-228">Click **Add New User tooAccount**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="a9f84-229">proprietário de conta do Active Directory do Azure Hello serão recebe um email incluindo um link tooconfirm e ativar conta hello.</span><span class="sxs-lookup"><span data-stu-id="a9f84-229">hello Azure Active Directory account holder will get an email including a link tooconfirm and activate hello account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a9f84-230">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a9f84-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a9f84-231">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="a9f84-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThousandEyes.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a9f84-233">**tooassign Britta Simon tooThousandEyes, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a9f84-233">**tooassign Britta Simon tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9f84-234">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a9f84-236">Na lista de aplicativos hello, selecione **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-236">In hello applications list, select **ThousandEyes**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="a9f84-238">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a9f84-240">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a9f84-240">Click **Add** button.</span></span> <span data-ttu-id="a9f84-241">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a9f84-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a9f84-243">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9f84-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a9f84-244">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a9f84-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a9f84-245">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a9f84-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a9f84-246">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a9f84-246">Testing single sign-on</span></span>

<span data-ttu-id="a9f84-247">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9f84-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a9f84-248">Quando você clica em Olá ThousandEyes bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="a9f84-248">When you click hello ThousandEyes tile in hello Access Panel, you should get automatically signed-on tooyour ThousandEyes application.</span></span>

<span data-ttu-id="a9f84-249">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a9f84-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9f84-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a9f84-250">Additional resources</span></span>

* [<span data-ttu-id="a9f84-251">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a9f84-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a9f84-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9f84-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

