---
title: "Tutorial: Integração do Azure Active Directory ao Tableau Server | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Tableau Server."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="9f457-103">Tutorial: Integração do Azure Active Directory ao Tableau Server</span><span class="sxs-lookup"><span data-stu-id="9f457-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="9f457-104">Neste tutorial, você aprenderá como toointegrate Tableau Server com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="9f457-104">In this tutorial, you learn how toointegrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f457-105">Integrando Tableau servidor com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f457-105">Integrating Tableau Server with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9f457-106">Você pode controlar no AD do Azure que tenha acesso tooTableau Server</span><span class="sxs-lookup"><span data-stu-id="9f457-106">You can control in Azure AD who has access tooTableau Server</span></span>
- <span data-ttu-id="9f457-107">Você pode habilitar seu usuários tooautomatically get conectado tooTableau servidor (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f457-107">You can enable your users tooautomatically get signed-on tooTableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f457-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9f457-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9f457-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f457-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f457-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9f457-110">Prerequisites</span></span>

<span data-ttu-id="9f457-111">tooconfigure integração do AD do Azure com o servidor Tableau, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f457-111">tooconfigure Azure AD integration with Tableau Server, you need hello following items:</span></span>

- <span data-ttu-id="9f457-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f457-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f457-113">Uma assinatura habilitada para logon único do Tableau Server</span><span class="sxs-lookup"><span data-stu-id="9f457-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f457-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9f457-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f457-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9f457-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f457-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9f457-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f457-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f457-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f457-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9f457-118">Scenario description</span></span>
<span data-ttu-id="9f457-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9f457-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f457-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="9f457-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f457-121">Adicionando Tableau Server da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9f457-121">Adding Tableau Server from hello gallery</span></span>
2. <span data-ttu-id="9f457-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f457-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-hello-gallery"></a><span data-ttu-id="9f457-123">Adicionando Tableau Server da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9f457-123">Adding Tableau Server from hello gallery</span></span>
<span data-ttu-id="9f457-124">integração de saudação tooconfigure do servidor Tableau no AD do Azure, você precisa tooadd Tableau servidor da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9f457-124">tooconfigure hello integration of Tableau Server into Azure AD, you need tooadd Tableau Server from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f457-125">**tooadd Tableau Server da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f457-125">**tooadd Tableau Server from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f457-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9f457-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9f457-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9f457-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9f457-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f457-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9f457-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f457-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9f457-133">Na caixa de pesquisa hello, digite **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="9f457-133">In hello search box, type **Tableau Server**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="9f457-135">No painel de resultados de saudação, selecione **Tableau servidor**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9f457-135">In hello results panel, select **Tableau Server**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f457-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f457-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f457-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Tableau Server, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9f457-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9f457-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no servidor Tableau é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f457-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Server is tooa user in Azure AD.</span></span> <span data-ttu-id="9f457-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no servidor Tableau precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9f457-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Server needs toobe established.</span></span>

<span data-ttu-id="9f457-141">No servidor Tableau, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f457-141">In Tableau Server, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9f457-142">tooconfigure e teste de logon único do AD do Azure com o servidor Tableau, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f457-142">tooconfigure and test Azure AD single sign-on with Tableau Server, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f457-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9f457-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f457-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f457-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f457-145">**[Criar um usuário de teste do servidor Tableau](#creating-a-tableau-server-test-user)**  -toohave um equivalente do Britta Simon no servidor Tableau toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="9f457-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - toohave a counterpart of Britta Simon in Tableau Server that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f457-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="9f457-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f457-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="9f457-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f457-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f457-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f457-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de servidor Tableau.</span><span class="sxs-lookup"><span data-stu-id="9f457-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="9f457-150">**tooconfigure AD do Azure-logon único com o servidor Tableau, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f457-150">**tooconfigure Azure AD single sign-on with Tableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f457-151">Em Olá portal do Azure, Olá **Tableau servidor** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="9f457-151">In hello Azure portal, on hello **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9f457-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="9f457-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="9f457-155">Em Olá **Tableau o domínio do servidor e as URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f457-155">On hello **Tableau Server Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="9f457-157">a.</span><span class="sxs-lookup"><span data-stu-id="9f457-157">a.</span></span> <span data-ttu-id="9f457-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="9f457-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="9f457-159">b.</span><span class="sxs-lookup"><span data-stu-id="9f457-159">b.</span></span> <span data-ttu-id="9f457-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="9f457-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="9f457-161">c.</span><span class="sxs-lookup"><span data-stu-id="9f457-161">c.</span></span> <span data-ttu-id="9f457-162">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="9f457-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9f457-163">Olá anteriores valores não são valores reais.</span><span class="sxs-lookup"><span data-stu-id="9f457-163">hello preceding values are not real values.</span></span> <span data-ttu-id="9f457-164">Posteriormente, você atualiza valores hello com URL real hello e o identificador de página de configuração do servidor de Tableau de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f457-164">Later, you update hello values with hello actual URL and identifier from hello Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="9f457-165">Aplicativo de servidor tableau espera as asserções de SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="9f457-165">Tableau Server application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="9f457-166">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9f457-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="9f457-167">Você pode gerenciar os valores hello desses atributos de saudação **"Atributos do usuário"** seção na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9f457-167">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="9f457-168">Olá, seguinte captura de tela mostra um exemplo de hello mesmo.</span><span class="sxs-lookup"><span data-stu-id="9f457-168">hello following screenshot shows an example for hello same.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="9f457-170">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f457-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="9f457-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="9f457-171">Attribute Name</span></span> | <span data-ttu-id="9f457-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="9f457-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="9f457-173">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="9f457-173">username</span></span> | <span data-ttu-id="9f457-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="9f457-174">*user.displayname*</span></span> |

    <span data-ttu-id="9f457-175">a.</span><span class="sxs-lookup"><span data-stu-id="9f457-175">a.</span></span> <span data-ttu-id="9f457-176">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f457-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="9f457-179">b.</span><span class="sxs-lookup"><span data-stu-id="9f457-179">b.</span></span> <span data-ttu-id="9f457-180">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="9f457-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="9f457-181">c.</span><span class="sxs-lookup"><span data-stu-id="9f457-181">c.</span></span> <span data-ttu-id="9f457-182">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="9f457-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="9f457-183">d.</span><span class="sxs-lookup"><span data-stu-id="9f457-183">d.</span></span> <span data-ttu-id="9f457-184">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="9f457-184">Click **Ok**</span></span>


6. <span data-ttu-id="9f457-185">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9f457-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="9f457-187">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9f457-187">Click **Save** button.</span></span>

    <span data-ttu-id="9f457-188">![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="9f457-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="9f457-189">tooget SSO configurado para o seu aplicativo, você precisa de locatário de servidor Tableau toosign em tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="9f457-189">tooget SSO configured for your application, you need toosign-on tooyour Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="9f457-190">a.</span><span class="sxs-lookup"><span data-stu-id="9f457-190">a.</span></span> <span data-ttu-id="9f457-191">Configuração de servidor Tableau hello, clique em Olá **SAML** guia.</span><span class="sxs-lookup"><span data-stu-id="9f457-191">In hello Tableau Server configuration, click hello **SAML** tab.</span></span>
  
    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="9f457-193">b.</span><span class="sxs-lookup"><span data-stu-id="9f457-193">b.</span></span> <span data-ttu-id="9f457-194">Selecione caixa de seleção de saudação do **SAML de uso para o logon único**.</span><span class="sxs-lookup"><span data-stu-id="9f457-194">Select hello checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="9f457-195">c.</span><span class="sxs-lookup"><span data-stu-id="9f457-195">c.</span></span> <span data-ttu-id="9f457-196">URL de retorno de servidor tableau — Olá URL que os usuários Tableau Server acessará, como http://tableau_server.</span><span class="sxs-lookup"><span data-stu-id="9f457-196">Tableau Server return URL—hello URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="9f457-197">Não é recomendável usar http://localhost.</span><span class="sxs-lookup"><span data-stu-id="9f457-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="9f457-198">O uso de URL com barra à direita (por exemplo, http://tableau_server/) não é aceito.</span><span class="sxs-lookup"><span data-stu-id="9f457-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="9f457-199">Cópia **URL de retorno de servidor Tableau** e cole-o tooAzure AD **URL de logon** textbox em **Tableau o domínio do servidor e as URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="9f457-199">Copy **Tableau Server return URL** and paste it tooAzure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="9f457-200">d.</span><span class="sxs-lookup"><span data-stu-id="9f457-200">d.</span></span> <span data-ttu-id="9f457-201">ID de entidade SAML, ID da entidade Olá identifica exclusivamente a instalação de servidor Tableau toohello IdP.</span><span class="sxs-lookup"><span data-stu-id="9f457-201">SAML entity ID—hello entity ID uniquely identifies your Tableau Server installation toohello IdP.</span></span> <span data-ttu-id="9f457-202">Você pode inserir a URL do servidor Tableau novamente aqui, se desejar, mas ele não tem toobe a URL do servidor Tableau.</span><span class="sxs-lookup"><span data-stu-id="9f457-202">You can enter your Tableau Server URL again here, if you like, but it does not have toobe your Tableau Server URL.</span></span> <span data-ttu-id="9f457-203">Cópia **ID da entidade SAML** e cole-o tooAzure AD **identificador** textbox em **Tableau o domínio do servidor e as URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="9f457-203">Copy **SAML entity ID** and paste it tooAzure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="9f457-204">e.</span><span class="sxs-lookup"><span data-stu-id="9f457-204">e.</span></span> <span data-ttu-id="9f457-205">Clique em Olá **Exportar arquivo de metadados** e abri-lo no aplicativo de editor de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f457-205">Click hello **Export Metadata File** and open it in hello text editor application.</span></span> <span data-ttu-id="9f457-206">Localize o URL do serviço de consumidor de declaração com Http Post e índice 0 e copiar Olá URL.</span><span class="sxs-lookup"><span data-stu-id="9f457-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy hello URL.</span></span> <span data-ttu-id="9f457-207">Agora colar tooAzure AD **URL de resposta** textbox em **Tableau o domínio do servidor e as URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="9f457-207">Now paste it tooAzure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="9f457-208">f.</span><span class="sxs-lookup"><span data-stu-id="9f457-208">f.</span></span> <span data-ttu-id="9f457-209">Localize o arquivo de metadados de federação que baixou do portal do Azure e, em seguida, carregá-lo no hello **arquivo de metadados Idp SAML**.</span><span class="sxs-lookup"><span data-stu-id="9f457-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in hello **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="9f457-210">g.</span><span class="sxs-lookup"><span data-stu-id="9f457-210">g.</span></span> <span data-ttu-id="9f457-211">Clique em Olá **Okey** botão na página de configuração do servidor Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="9f457-211">Click hello **OK** button in hello Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="9f457-212">Cliente tem tooupload nenhum certificado na configuração de SSO do SAML Server Tableau hello e ele será obter ignorado em Olá fluxo SSO.</span><span class="sxs-lookup"><span data-stu-id="9f457-212">Customer have tooupload any certificate in hello Tableau Server SAML SSO configuration and it will get ignored in hello SSO flow.</span></span>
    ><span data-ttu-id="9f457-213">Se você precisar ajudar a configurar o SAML no servidor Tableau, consulte o artigo toothis [configurar SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="9f457-213">If you need help configuring SAML on Tableau Server then please refer toothis article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="9f457-214">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="9f457-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9f457-215">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="9f457-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9f457-216">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f457-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f457-217">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f457-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f457-218">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f457-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9f457-220">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f457-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f457-221">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9f457-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f457-223">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="9f457-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f457-225">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f457-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f457-227">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f457-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f457-229">a.</span><span class="sxs-lookup"><span data-stu-id="9f457-229">a.</span></span> <span data-ttu-id="9f457-230">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9f457-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f457-231">b.</span><span class="sxs-lookup"><span data-stu-id="9f457-231">b.</span></span> <span data-ttu-id="9f457-232">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9f457-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f457-233">c.</span><span class="sxs-lookup"><span data-stu-id="9f457-233">c.</span></span> <span data-ttu-id="9f457-234">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="9f457-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9f457-235">d.</span><span class="sxs-lookup"><span data-stu-id="9f457-235">d.</span></span> <span data-ttu-id="9f457-236">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9f457-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="9f457-237">Criação de um usuário de teste do Tableau Server</span><span class="sxs-lookup"><span data-stu-id="9f457-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="9f457-238">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no servidor Tableau.</span><span class="sxs-lookup"><span data-stu-id="9f457-238">hello objective of this section is toocreate a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="9f457-239">É necessário tooprovision todos os usuários de saudação no servidor de Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="9f457-239">You need tooprovision all hello users in hello Tableau server.</span></span> 

<span data-ttu-id="9f457-240">Esse nome de usuário de saudação deve corresponder o valor de saudação que você configurou no atributo personalizado de saudação do AD do Azure de **nome de usuário**.</span><span class="sxs-lookup"><span data-stu-id="9f457-240">That username of hello user should match hello value which you have configured in hello Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="9f457-241">Com hello correto de mapeamento de integração Olá deve funcionar [Configurando o AD do Azure Single Sign-On](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="9f457-241">With hello correct mapping hello integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="9f457-242">Se você precisar toocreate um usuário manualmente, é necessário ter toocontact Olá Tableau Server administrador em sua organização.</span><span class="sxs-lookup"><span data-stu-id="9f457-242">If you need toocreate a user manually, you need toocontact hello Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9f457-243">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f457-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9f457-244">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTableau Server.</span><span class="sxs-lookup"><span data-stu-id="9f457-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Server.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9f457-246">**tooassign Britta Simon tooTableau Server, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f457-246">**tooassign Britta Simon tooTableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f457-247">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f457-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9f457-249">Na lista de aplicativos hello, selecione **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="9f457-249">In hello applications list, select **Tableau Server**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="9f457-251">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9f457-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9f457-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9f457-253">Click **Add** button.</span></span> <span data-ttu-id="9f457-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f457-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9f457-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f457-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9f457-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f457-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f457-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f457-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f457-259">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9f457-259">Testing single sign-on</span></span>

<span data-ttu-id="9f457-260">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f457-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9f457-261">Quando você clica em bloco Tableau Server Olá Olá painel de acesso, você deve obter um aplicativo de servidor Tableau tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="9f457-261">When you click hello Tableau Server tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Server application.</span></span>
<span data-ttu-id="9f457-262">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9f457-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9f457-263">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9f457-263">Additional resources</span></span>

* [<span data-ttu-id="9f457-264">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9f457-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f457-265">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f457-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

