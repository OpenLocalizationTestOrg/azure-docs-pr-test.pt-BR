---
title: "Tutorial: integração do Azure Active Directory com o Zscaler Beta | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Zscaler Beta."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1471c2b51ca5684a11acd40f4e450521605bb786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a><span data-ttu-id="35daa-103">Tutorial: integração do Azure Active Directory com o Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="35daa-103">Tutorial: Azure Active Directory integration with Zscaler Beta</span></span>

<span data-ttu-id="35daa-104">Neste tutorial, você aprenderá como toointegrate Zscaler Beta com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="35daa-104">In this tutorial, you learn how toointegrate Zscaler Beta with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35daa-105">Integrando o Zscaler Beta com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="35daa-105">Integrating Zscaler Beta with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="35daa-106">Você pode controlar no AD do Azure que tenha acesso tooZscaler Beta</span><span class="sxs-lookup"><span data-stu-id="35daa-106">You can control in Azure AD who has access tooZscaler Beta</span></span>
- <span data-ttu-id="35daa-107">Você pode habilitar seu usuários tooautomatically get conectado tooZscaler Beta (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35daa-107">You can enable your users tooautomatically get signed-on tooZscaler Beta (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="35daa-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="35daa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="35daa-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35daa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35daa-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="35daa-110">Prerequisites</span></span>

<span data-ttu-id="35daa-111">tooconfigure integração do AD do Azure com o Zscaler Beta, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="35daa-111">tooconfigure Azure AD integration with Zscaler Beta, you need hello following items:</span></span>

- <span data-ttu-id="35daa-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35daa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35daa-113">Uma assinatura do Zscaler Beta habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="35daa-113">A Zscaler Beta single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35daa-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="35daa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35daa-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="35daa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35daa-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="35daa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35daa-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35daa-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35daa-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="35daa-118">Scenario description</span></span>
<span data-ttu-id="35daa-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="35daa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35daa-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="35daa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35daa-121">Adicionando Zscaler Beta da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="35daa-121">Adding Zscaler Beta from hello gallery</span></span>
2. <span data-ttu-id="35daa-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35daa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-beta-from-hello-gallery"></a><span data-ttu-id="35daa-123">Adicionando Zscaler Beta da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="35daa-123">Adding Zscaler Beta from hello gallery</span></span>
<span data-ttu-id="35daa-124">integração de saudação tooconfigure do Zscaler Beta no AD do Azure, você precisa tooadd Zscaler Beta da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="35daa-124">tooconfigure hello integration of Zscaler Beta into Azure AD, you need tooadd Zscaler Beta from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="35daa-125">**tooadd Zscaler Beta da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="35daa-125">**tooadd Zscaler Beta from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="35daa-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="35daa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="35daa-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="35daa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="35daa-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="35daa-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="35daa-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35daa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="35daa-133">Na caixa de pesquisa hello, digite **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="35daa-133">In hello search box, type **Zscaler Beta**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

5. <span data-ttu-id="35daa-135">No painel de resultados de saudação, selecione **Zscaler Beta**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="35daa-135">In hello results panel, select **Zscaler Beta**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="35daa-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35daa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="35daa-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Zscaler Beta com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="35daa-138">In this section, you configure and test Azure AD single sign-on with Zscaler Beta based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35daa-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Zscaler Beta é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="35daa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Beta is tooa user in Azure AD.</span></span> <span data-ttu-id="35daa-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Zscaler Beta precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="35daa-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Beta needs toobe established.</span></span>

<span data-ttu-id="35daa-141">No Zscaler Beta, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="35daa-141">In Zscaler Beta, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="35daa-142">tooconfigure e teste de logon único do AD do Azure com o Zscaler Beta, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="35daa-142">tooconfigure and test Azure AD single sign-on with Zscaler Beta, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="35daa-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="35daa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="35daa-144">**[Definir configurações de proxy](#configuring-proxy-settings)**  -configurações de proxy de saudação tooconfigure no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="35daa-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="35daa-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35daa-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="35daa-146">**[Criar um usuário de teste do Zscaler Beta](#creating-a-zscaler-beta-test-user)**  -toohave um equivalente do Britta Simon no Zscaler Beta é a representação toohello vinculado AD do Azure do usuário.</span><span class="sxs-lookup"><span data-stu-id="35daa-146">**[Creating a Zscaler Beta test user](#creating-a-zscaler-beta-test-user)** - toohave a counterpart of Britta Simon in Zscaler Beta that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="35daa-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="35daa-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="35daa-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="35daa-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="35daa-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="35daa-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="35daa-150">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="35daa-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler Beta application.</span></span>

<span data-ttu-id="35daa-151">**tooconfigure AD do Azure-logon único com o Zscaler Beta, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="35daa-151">**tooconfigure Azure AD single sign-on with Zscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="35daa-152">Em Olá portal do Azure, Olá **Zscaler Beta** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="35daa-152">In hello Azure portal, on hello **Zscaler Beta** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="35daa-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="35daa-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

3. <span data-ttu-id="35daa-156">Em Olá **Zscaler Beta domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35daa-156">On hello **Zscaler Beta Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    <span data-ttu-id="35daa-158">Na caixa de texto de URL Olá logon, digite o URL de Olá usada pelos seu usuários em toosign tooyour aplicativo Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="35daa-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour Zscaler Beta application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35daa-159">Você tem tooupdate esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="35daa-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="35daa-160">Entre em contato com [equipe de suporte do Zscaler Beta cliente](https://www.zscaler.com/company/contact) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="35daa-160">Contact [Zscaler Beta Client support team](https://www.zscaler.com/company/contact) tooget this value.</span></span> 

4. <span data-ttu-id="35daa-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="35daa-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

5. <span data-ttu-id="35daa-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="35daa-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="35daa-165">Em Olá **Zscaler Beta configuração** seção, clique em **configurar Zscaler Beta** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="35daa-165">On hello **Zscaler Beta Configuration** section, click **Configure Zscaler Beta** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="35daa-166">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="35daa-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

7. <span data-ttu-id="35daa-168">Em uma janela do navegador web diferente, faça logon no tooyour site da empresa Zscaler Beta como um administrador.</span><span class="sxs-lookup"><span data-stu-id="35daa-168">In a different web browser window, log in tooyour Zscaler Beta company site as an administrator.</span></span>

8. <span data-ttu-id="35daa-169">No menu de saudação na parte superior de saudação, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="35daa-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="35daa-170">![Administração](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="35daa-170">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="35daa-171">Em **Gerenciar Administradores e Funções**, clique em **Gerenciar Usuários e Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="35daa-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="35daa-172">![Gerenciar usuários e autenticação](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Gerenciar usuários e autenticação")</span><span class="sxs-lookup"><span data-stu-id="35daa-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="35daa-173">Em Olá **escolher opções de autenticação para sua organização** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35daa-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="35daa-174">![Autenticação](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Autenticação")</span><span class="sxs-lookup"><span data-stu-id="35daa-174">![Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="35daa-175">a.</span><span class="sxs-lookup"><span data-stu-id="35daa-175">a.</span></span> <span data-ttu-id="35daa-176">Selecione **Autenticar usando o Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="35daa-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="35daa-177">b.</span><span class="sxs-lookup"><span data-stu-id="35daa-177">b.</span></span> <span data-ttu-id="35daa-178">Clique em **Configurar Parâmetros de Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="35daa-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="35daa-179">Em Olá **configurar parâmetros único do SAML logon** página de diálogo Executar Olá etapas a seguir e, em seguida, clique em **feito**</span><span class="sxs-lookup"><span data-stu-id="35daa-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="35daa-180">![Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="35daa-180">![Single Sign-On](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="35daa-181">a.</span><span class="sxs-lookup"><span data-stu-id="35daa-181">a.</span></span> <span data-ttu-id="35daa-182">Saudação de colar **Single Sign-On URL do serviço SAML** valor que você copiou de saudação portal do Azure em hello **URL de usuários de toowhich do Portal SAML Olá são enviados para autenticação** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="35daa-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="35daa-183">b.</span><span class="sxs-lookup"><span data-stu-id="35daa-183">b.</span></span> <span data-ttu-id="35daa-184">Em Olá **atributo que contém o nome de logon** caixa de texto, tipo **NameID**.</span><span class="sxs-lookup"><span data-stu-id="35daa-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="35daa-185">c.</span><span class="sxs-lookup"><span data-stu-id="35daa-185">c.</span></span> <span data-ttu-id="35daa-186">tooupload seu certificado baixado, clique em **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="35daa-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="35daa-187">d.</span><span class="sxs-lookup"><span data-stu-id="35daa-187">d.</span></span> <span data-ttu-id="35daa-188">Selecione **Habilitar Provisionamento Automático do SAML**.</span><span class="sxs-lookup"><span data-stu-id="35daa-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="35daa-189">Em Olá **configurar autenticação de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35daa-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="35daa-190">![Administração](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="35daa-190">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="35daa-191">a.</span><span class="sxs-lookup"><span data-stu-id="35daa-191">a.</span></span> <span data-ttu-id="35daa-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="35daa-192">Click **Save**.</span></span>

    <span data-ttu-id="35daa-193">b.</span><span class="sxs-lookup"><span data-stu-id="35daa-193">b.</span></span> <span data-ttu-id="35daa-194">Clique em **Ativar Agora**.</span><span class="sxs-lookup"><span data-stu-id="35daa-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="35daa-195">Definindo as configurações de proxy</span><span class="sxs-lookup"><span data-stu-id="35daa-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="35daa-196">configurações de proxy de saudação tooconfigure no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="35daa-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="35daa-197">Inicie o **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="35daa-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="35daa-198">Selecione **opções da Internet** de saudação **ferramentas** menu para abrir Olá **opções da Internet** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35daa-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="35daa-199">![Opções da Internet](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Opções da Internet")</span><span class="sxs-lookup"><span data-stu-id="35daa-199">![Internet Options](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="35daa-200">Clique em Olá **conexões** guia.</span><span class="sxs-lookup"><span data-stu-id="35daa-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="35daa-201">![Conexões](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Conexões")</span><span class="sxs-lookup"><span data-stu-id="35daa-201">![Connections](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="35daa-202">Clique em **configurações da LAN** tooopen Olá **configurações da LAN** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35daa-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="35daa-203">Olá seção do servidor Proxy, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35daa-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="35daa-204">![Servidor proxy](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Servidor proxy")</span><span class="sxs-lookup"><span data-stu-id="35daa-204">![Proxy server](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="35daa-205">a.</span><span class="sxs-lookup"><span data-stu-id="35daa-205">a.</span></span> <span data-ttu-id="35daa-206">Selecione **Usar um servidor proxy para LAN**.</span><span class="sxs-lookup"><span data-stu-id="35daa-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="35daa-207">b.</span><span class="sxs-lookup"><span data-stu-id="35daa-207">b.</span></span> <span data-ttu-id="35daa-208">Na caixa de texto de endereço hello, digite **gateway.zscalerbeta.net**.</span><span class="sxs-lookup"><span data-stu-id="35daa-208">In hello Address textbox, type **gateway.zscalerbeta.net**.</span></span>

    <span data-ttu-id="35daa-209">c.</span><span class="sxs-lookup"><span data-stu-id="35daa-209">c.</span></span> <span data-ttu-id="35daa-210">Na caixa de texto de porta hello, digite **80**.</span><span class="sxs-lookup"><span data-stu-id="35daa-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="35daa-211">d.</span><span class="sxs-lookup"><span data-stu-id="35daa-211">d.</span></span> <span data-ttu-id="35daa-212">Selecione **Ignorar servidor proxy para endereços locais**.</span><span class="sxs-lookup"><span data-stu-id="35daa-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="35daa-213">e.</span><span class="sxs-lookup"><span data-stu-id="35daa-213">e.</span></span> <span data-ttu-id="35daa-214">Clique em **Okey** tooclose Olá **configurações de rede Local (LAN)** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35daa-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="35daa-215">Clique em **Okey** tooclose Olá **opções da Internet** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35daa-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="35daa-216">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="35daa-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="35daa-217">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="35daa-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="35daa-218">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="35daa-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="35daa-219">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35daa-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="35daa-220">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="35daa-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="35daa-222">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="35daa-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="35daa-223">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="35daa-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="35daa-225">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="35daa-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="35daa-227">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="35daa-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="35daa-229">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35daa-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="35daa-231">a.</span><span class="sxs-lookup"><span data-stu-id="35daa-231">a.</span></span> <span data-ttu-id="35daa-232">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35daa-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35daa-233">b.</span><span class="sxs-lookup"><span data-stu-id="35daa-233">b.</span></span> <span data-ttu-id="35daa-234">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="35daa-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35daa-235">c.</span><span class="sxs-lookup"><span data-stu-id="35daa-235">c.</span></span> <span data-ttu-id="35daa-236">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="35daa-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="35daa-237">d.</span><span class="sxs-lookup"><span data-stu-id="35daa-237">d.</span></span> <span data-ttu-id="35daa-238">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="35daa-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-beta-test-user"></a><span data-ttu-id="35daa-239">Criação de um usuário de teste do Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="35daa-239">Creating a Zscaler Beta test user</span></span>

<span data-ttu-id="35daa-240">toolog de usuários do AD do Azure de tooenable tooZscaler Beta, elas devem ser provisionado tooZscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="35daa-240">tooenable Azure AD users toolog in tooZscaler Beta, they must be provisioned tooZscaler Beta.</span></span> <span data-ttu-id="35daa-241">No caso de saudação do Zscaler Beta, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="35daa-241">In hello case of Zscaler Beta, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="35daa-242">tooconfigure provisionamento de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35daa-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="35daa-243">Faça logon no tooyour **Zscaler Beta** locatário.</span><span class="sxs-lookup"><span data-stu-id="35daa-243">Log in tooyour **Zscaler Beta** tenant.</span></span>

2. <span data-ttu-id="35daa-244">Clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="35daa-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="35daa-245">![Administração](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="35daa-245">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="35daa-246">Clique em **Gerenciamento de Usuários**.</span><span class="sxs-lookup"><span data-stu-id="35daa-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="35daa-247">![Adicionar](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="35daa-247">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="35daa-248">Em Olá **usuários** , clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="35daa-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="35daa-249">![Adicionar](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="35daa-249">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="35daa-250">Na seção Adicionar usuário do hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35daa-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="35daa-251">![Adicionar Usuário](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="35daa-251">![Add User](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="35daa-252">a.</span><span class="sxs-lookup"><span data-stu-id="35daa-252">a.</span></span> <span data-ttu-id="35daa-253">Saudação de tipo **UserID**, **nome de exibição do usuário**, **senha**, **Confirmar senha**e, em seguida, selecione **grupos**e hello **departamento** de uma válida do Azure você deseja tooprovision de conta do AD.</span><span class="sxs-lookup"><span data-stu-id="35daa-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="35daa-254">b.</span><span class="sxs-lookup"><span data-stu-id="35daa-254">b.</span></span> <span data-ttu-id="35daa-255">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="35daa-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="35daa-256">Você pode usar qualquer ferramenta de criação outros Zscaler Beta usuário conta ou APIs fornecidas pelo Zscaler Beta tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="35daa-256">You can use any other Zscaler Beta user account creation tools or APIs provided by Zscaler Beta tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="35daa-257">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35daa-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="35daa-258">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooZscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="35daa-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler Beta.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="35daa-260">**tooassign Britta Simon tooZscaler Beta, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="35daa-260">**tooassign Britta Simon tooZscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="35daa-261">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="35daa-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="35daa-263">Na lista de aplicativos hello, selecione **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="35daa-263">In hello applications list, select **Zscaler Beta**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

3. <span data-ttu-id="35daa-265">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="35daa-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="35daa-267">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="35daa-267">Click **Add** button.</span></span> <span data-ttu-id="35daa-268">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35daa-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="35daa-270">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="35daa-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="35daa-271">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35daa-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35daa-272">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35daa-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="35daa-273">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="35daa-273">Testing single sign-on</span></span>

<span data-ttu-id="35daa-274">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="35daa-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="35daa-275">Quando você clica em Olá Zscaler Beta bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="35daa-275">When you click hello Zscaler Beta tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Beta application.</span></span>
<span data-ttu-id="35daa-276">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="35daa-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35daa-277">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="35daa-277">Additional resources</span></span>

* [<span data-ttu-id="35daa-278">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="35daa-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35daa-279">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="35daa-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_203.png

