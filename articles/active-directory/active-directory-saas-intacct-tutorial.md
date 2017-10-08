---
title: "Tutorial: Integração do Azure Active Directory com o Intacct | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="2f148-103">Tutorial: Integração do Active Directory do Azure com o Intacct</span><span class="sxs-lookup"><span data-stu-id="2f148-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="2f148-104">Neste tutorial, você aprenderá como toointegrate Intacct com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="2f148-104">In this tutorial, you learn how toointegrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f148-105">Integrando o Intacct com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f148-105">Integrating Intacct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2f148-106">Você pode controlar no AD do Azure que tenha acesso tooIntacct</span><span class="sxs-lookup"><span data-stu-id="2f148-106">You can control in Azure AD who has access tooIntacct</span></span>
- <span data-ttu-id="2f148-107">Você pode habilitar seu usuários tooautomatically get conectado tooIntacct (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f148-107">You can enable your users tooautomatically get signed-on tooIntacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f148-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2f148-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2f148-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f148-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f148-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2f148-110">Prerequisites</span></span>

<span data-ttu-id="2f148-111">tooconfigure integração do AD do Azure com Intacct, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f148-111">tooconfigure Azure AD integration with Intacct, you need hello following items:</span></span>

- <span data-ttu-id="2f148-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f148-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f148-113">Uma assinatura habilitada para logon único do Intacct</span><span class="sxs-lookup"><span data-stu-id="2f148-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f148-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2f148-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f148-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2f148-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f148-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2f148-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f148-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f148-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f148-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2f148-118">Scenario description</span></span>
<span data-ttu-id="2f148-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2f148-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f148-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="2f148-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f148-121">Adicionando Intacct da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2f148-121">Adding Intacct from hello gallery</span></span>
2. <span data-ttu-id="2f148-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f148-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-hello-gallery"></a><span data-ttu-id="2f148-123">Adicionando Intacct da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2f148-123">Adding Intacct from hello gallery</span></span>
<span data-ttu-id="2f148-124">integração de saudação tooconfigure do Intacct no AD do Azure, você precisa tooadd Intacct da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2f148-124">tooconfigure hello integration of Intacct into Azure AD, you need tooadd Intacct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2f148-125">**tooadd Intacct da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f148-125">**tooadd Intacct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f148-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="2f148-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f148-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2f148-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2f148-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2f148-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="2f148-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f148-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="2f148-133">Na caixa de pesquisa hello, digite **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="2f148-133">In hello search box, type **Intacct**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="2f148-135">No painel de resultados de saudação, selecione **Intacct**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2f148-135">In hello results panel, select **Intacct**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f148-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f148-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f148-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Intacct, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="2f148-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f148-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Intacct é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f148-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intacct is tooa user in Azure AD.</span></span> <span data-ttu-id="2f148-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Intacct precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="2f148-140">In other words, a link relationship between an Azure AD user and hello related user in Intacct needs toobe established.</span></span>

<span data-ttu-id="2f148-141">No Intacct, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f148-141">In Intacct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2f148-142">tooconfigure e teste de logon único do AD do Azure com Intacct, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f148-142">tooconfigure and test Azure AD single sign-on with Intacct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2f148-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2f148-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2f148-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f148-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f148-145">**[Criar um usuário de teste do Intacct](#creating-an-intacct-test-user)**  -toohave um equivalente do Britta Simon no Intacct é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="2f148-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - toohave a counterpart of Britta Simon in Intacct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f148-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="2f148-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f148-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="2f148-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f148-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f148-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f148-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Intacct.</span><span class="sxs-lookup"><span data-stu-id="2f148-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="2f148-150">**tooconfigure AD do Azure-logon único com Intacct, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f148-150">**tooconfigure Azure AD single sign-on with Intacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f148-151">Em Olá portal do Azure, Olá **Intacct** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="2f148-151">In hello Azure portal, on hello **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2f148-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="2f148-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="2f148-155">Em Olá **Intacct domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f148-155">On hello **Intacct Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="2f148-157">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f148-157">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="2f148-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="2f148-158">This value is not real.</span></span> <span data-ttu-id="2f148-159">Atualize esse valor com hello URL de resposta real.</span><span class="sxs-lookup"><span data-stu-id="2f148-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="2f148-160">Entre em contato com [equipe de suporte do Intacct](https://us.intacct.com/support) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="2f148-160">Contact [Intacct support team](https://us.intacct.com/support) tooget this value.</span></span>

4. <span data-ttu-id="2f148-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2f148-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="2f148-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2f148-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2f148-165">Em Olá **Intacct configuração** seção, clique em **configurar Intacct** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="2f148-165">On hello **Intacct Configuration** section, click **Configure Intacct** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2f148-166">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="2f148-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="2f148-168">Em uma janela de navegador web diferente, entre no site da empresa Intacct tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="2f148-168">In a different web browser window, sign in tooyour Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="2f148-169">Clique em Olá **empresa** guia e, em seguida, clique em **informações sobre a empresa**.</span><span class="sxs-lookup"><span data-stu-id="2f148-169">Click hello **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="2f148-170">![Empresa](./media/active-directory-saas-intacct-tutorial/ic790037.png "Empresa")</span><span class="sxs-lookup"><span data-stu-id="2f148-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="2f148-171">Clique em Olá **segurança** guia e, em seguida, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="2f148-171">Click hello **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="2f148-172">![Segurança](./media/active-directory-saas-intacct-tutorial/ic790038.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="2f148-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="2f148-173">Em Olá **(SSO) do logon único** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f148-173">In hello **Single sign on (SSO)** section, perform hello following steps:</span></span>

    <span data-ttu-id="2f148-174">![Logon único](./media/active-directory-saas-intacct-tutorial/ic790039.png "logon único")</span><span class="sxs-lookup"><span data-stu-id="2f148-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="2f148-175">a.</span><span class="sxs-lookup"><span data-stu-id="2f148-175">a.</span></span> <span data-ttu-id="2f148-176">Selecione **Habilitar logon único**.</span><span class="sxs-lookup"><span data-stu-id="2f148-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="2f148-177">b.</span><span class="sxs-lookup"><span data-stu-id="2f148-177">b.</span></span> <span data-ttu-id="2f148-178">Para **Tipo de provedor de identidade**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="2f148-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="2f148-179">c.</span><span class="sxs-lookup"><span data-stu-id="2f148-179">c.</span></span> <span data-ttu-id="2f148-180">Em **URL do emissor** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f148-180">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="2f148-181">d.</span><span class="sxs-lookup"><span data-stu-id="2f148-181">d.</span></span> <span data-ttu-id="2f148-182">Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f148-182">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2f148-183">e.</span><span class="sxs-lookup"><span data-stu-id="2f148-183">e.</span></span> <span data-ttu-id="2f148-184">Abra seu **base 64** codificado certificado no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado** caixa.</span><span class="sxs-lookup"><span data-stu-id="2f148-184">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** box.</span></span>
   
    <span data-ttu-id="2f148-185">f.</span><span class="sxs-lookup"><span data-stu-id="2f148-185">f.</span></span> <span data-ttu-id="2f148-186">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2f148-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2f148-187">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="2f148-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2f148-188">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="2f148-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2f148-189">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f148-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f148-190">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f148-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f148-191">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f148-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="2f148-193">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f148-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f148-194">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="2f148-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f148-196">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2f148-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f148-198">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f148-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f148-200">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f148-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f148-202">a.</span><span class="sxs-lookup"><span data-stu-id="2f148-202">a.</span></span> <span data-ttu-id="2f148-203">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f148-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f148-204">b.</span><span class="sxs-lookup"><span data-stu-id="2f148-204">b.</span></span> <span data-ttu-id="2f148-205">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2f148-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f148-206">c.</span><span class="sxs-lookup"><span data-stu-id="2f148-206">c.</span></span> <span data-ttu-id="2f148-207">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="2f148-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2f148-208">d.</span><span class="sxs-lookup"><span data-stu-id="2f148-208">d.</span></span> <span data-ttu-id="2f148-209">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2f148-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="2f148-210">Criação de um usuário de teste do Intacct</span><span class="sxs-lookup"><span data-stu-id="2f148-210">Creating an Intacct test user</span></span>

<span data-ttu-id="2f148-211">tooset os usuários do AD do Azure para que possam entrar em tooIntacct, eles devem ser provisionados no Intacct.</span><span class="sxs-lookup"><span data-stu-id="2f148-211">tooset up Azure AD users so they can sign in tooIntacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="2f148-212">Para o Intacct, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="2f148-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="2f148-213">**contas de usuário tooprovision, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f148-213">**tooprovision user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f148-214">Entrar tooyour **Intacct** locatário.</span><span class="sxs-lookup"><span data-stu-id="2f148-214">Sign in tooyour **Intacct** tenant.</span></span>

2. <span data-ttu-id="2f148-215">Clique em Olá **empresa** guia e, em seguida, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="2f148-215">Click hello **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="2f148-216">![Usuários](./media/active-directory-saas-intacct-tutorial/ic790041.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="2f148-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="2f148-217">Clique em Olá **adicionar** guia.</span><span class="sxs-lookup"><span data-stu-id="2f148-217">Click hello **Add** tab.</span></span>

    <span data-ttu-id="2f148-218">![Adicionar](./media/active-directory-saas-intacct-tutorial/ic790042.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="2f148-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="2f148-219">Em Olá **informações do usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f148-219">In hello **User Information** section, perform hello following steps:</span></span>

    <span data-ttu-id="2f148-220">![Informações do Usuário](./media/active-directory-saas-intacct-tutorial/ic790043.png "informações do Usuário")</span><span class="sxs-lookup"><span data-stu-id="2f148-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="2f148-221">a.</span><span class="sxs-lookup"><span data-stu-id="2f148-221">a.</span></span> <span data-ttu-id="2f148-222">Digite hello **ID de usuário**, Olá **Sobrenome**, **nome**, Olá **endereço de Email**, Olá **título**, e hello **Phone** de uma conta do AD do Azure que você deseja tooprovision em Olá **informações do usuário** seção.</span><span class="sxs-lookup"><span data-stu-id="2f148-222">Enter hello **User ID**, hello **Last name**, **First name**, hello **Email address**, hello **Title**, and hello **Phone** of an Azure AD account that you want tooprovision into hello **User Information** section.</span></span>

    <span data-ttu-id="2f148-223">b.</span><span class="sxs-lookup"><span data-stu-id="2f148-223">b.</span></span> <span data-ttu-id="2f148-224">Selecione Olá **privilégios de administrador** de uma conta do AD do Azure que você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="2f148-224">Select hello **Admin privileges** of an Azure AD account that you want tooprovision.</span></span>
   
    <span data-ttu-id="2f148-225">c.</span><span class="sxs-lookup"><span data-stu-id="2f148-225">c.</span></span> <span data-ttu-id="2f148-226">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2f148-226">Click **Save**.</span></span> <span data-ttu-id="2f148-227">proprietário de conta do AD do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="2f148-227">hello Azure AD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="2f148-228">contas de usuário do AD do Azure tooprovision, você pode usar outras ferramentas de criação de conta de usuário do Intacct ou APIs fornecidas pela Intacct.</span><span class="sxs-lookup"><span data-stu-id="2f148-228">tooprovision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2f148-229">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f148-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2f148-230">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooIntacct.</span><span class="sxs-lookup"><span data-stu-id="2f148-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntacct.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="2f148-232">**tooassign Britta Simon tooIntacct, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f148-232">**tooassign Britta Simon tooIntacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f148-233">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2f148-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2f148-235">Na lista de aplicativos hello, selecione **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="2f148-235">In hello applications list, select **Intacct**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="2f148-237">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2f148-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="2f148-239">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2f148-239">Click **Add** button.</span></span> <span data-ttu-id="2f148-240">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f148-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="2f148-242">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f148-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2f148-243">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f148-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f148-244">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f148-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f148-245">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="2f148-245">Testing single sign-on</span></span>

<span data-ttu-id="2f148-246">Nesta seção, você pode testar a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f148-246">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="2f148-247">Quando você clica em bloco Intacct Olá Olá painel de acesso, você deve ser conectado automaticamente tooyour Intacct aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2f148-247">When you click hello Intacct tile in hello Access Panel, you should be automatically signed in tooyour Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f148-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2f148-248">Additional resources</span></span>

* [<span data-ttu-id="2f148-249">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2f148-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f148-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f148-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

