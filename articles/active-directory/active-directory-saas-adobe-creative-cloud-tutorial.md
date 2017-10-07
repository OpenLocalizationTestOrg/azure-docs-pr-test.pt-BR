---
title: "Tutorial: integração do Azure Active Directory com a Adobe Creative Cloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Adobe criativos da nuvem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="abb20-103">Tutorial: integração do Azure Active Directory com a Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="abb20-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="abb20-104">Neste tutorial, você aprenderá como toointegrate Adobe Creative nuvem com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="abb20-104">In this tutorial, you learn how toointegrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="abb20-105">Integração do Adobe criativos da nuvem com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="abb20-105">Integrating Adobe Creative Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="abb20-106">Você pode controlar no AD do Azure que tenha acesso tooAdobe criativos da nuvem</span><span class="sxs-lookup"><span data-stu-id="abb20-106">You can control in Azure AD who has access tooAdobe Creative Cloud</span></span>
- <span data-ttu-id="abb20-107">Você pode habilitar seu usuários tooautomatically get conectado tooAdobe criativos da nuvem (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="abb20-107">You can enable your users tooautomatically get signed-on tooAdobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="abb20-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="abb20-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="abb20-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="abb20-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abb20-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="abb20-110">Prerequisites</span></span>

<span data-ttu-id="abb20-111">tooconfigure integração do AD do Azure com Adobe criativos da nuvem, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="abb20-111">tooconfigure Azure AD integration with Adobe Creative Cloud, you need hello following items:</span></span>

- <span data-ttu-id="abb20-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="abb20-112">An Azure AD subscription</span></span>
- <span data-ttu-id="abb20-113">Uma assinatura da Creative Cloud habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="abb20-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="abb20-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="abb20-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="abb20-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="abb20-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="abb20-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="abb20-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="abb20-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="abb20-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="abb20-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="abb20-118">Scenario description</span></span>
<span data-ttu-id="abb20-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="abb20-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="abb20-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="abb20-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="abb20-121">Adicionando Adobe criativos da nuvem da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="abb20-121">Adding Adobe Creative Cloud from hello gallery</span></span>
2. <span data-ttu-id="abb20-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="abb20-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a><span data-ttu-id="abb20-123">Adicionando Adobe criativos da nuvem da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="abb20-123">Adding Adobe Creative Cloud from hello gallery</span></span>
<span data-ttu-id="abb20-124">integração de saudação tooconfigure do Adobe criativos da nuvem no Azure AD, é necessário tooadd Adobe criativos da nuvem na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="abb20-124">tooconfigure hello integration of Adobe Creative Cloud into Azure AD, you need tooadd Adobe Creative Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="abb20-125">**tooadd Adobe criativos da nuvem da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="abb20-125">**tooadd Adobe Creative Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="abb20-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="abb20-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="abb20-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="abb20-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="abb20-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="abb20-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="abb20-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="abb20-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="abb20-133">Na caixa de pesquisa hello, digite **Adobe criativos da nuvem**.</span><span class="sxs-lookup"><span data-stu-id="abb20-133">In hello search box, type **Adobe Creative Cloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="abb20-135">No painel de resultados de saudação, selecione **Adobe criativos da nuvem**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="abb20-135">In hello results panel, select **Adobe Creative Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="abb20-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="abb20-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="abb20-138">Nesta seção, você configurará e testará o logon único do Azure AD com a Adobe Creative Cloud, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="abb20-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="abb20-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Adobe criativos da nuvem é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="abb20-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Creative Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="abb20-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Adobe criativos da nuvem precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="abb20-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Creative Cloud needs toobe established.</span></span>

<span data-ttu-id="abb20-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Adobe criativos da nuvem.</span><span class="sxs-lookup"><span data-stu-id="abb20-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="abb20-142">tooconfigure e teste de logon único do AD do Azure com Adobe criativos da nuvem, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="abb20-142">tooconfigure and test Azure AD single sign-on with Adobe Creative Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="abb20-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="abb20-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="abb20-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="abb20-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="abb20-145">**[Criar um usuário de teste do Adobe criativos da nuvem](#creating-an-adobe-creative-cloud-test-user)**  -toohave um equivalente do Britta Simon no Adobe criativos da nuvem que é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="abb20-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - toohave a counterpart of Britta Simon in Adobe Creative Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="abb20-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="abb20-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="abb20-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="abb20-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="abb20-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="abb20-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="abb20-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Adobe criativos da nuvem.</span><span class="sxs-lookup"><span data-stu-id="abb20-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="abb20-150">**tooconfigure logon único do AD do Azure com Adobe criativos da nuvem, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="abb20-150">**tooconfigure Azure AD single sign-on with Adobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="abb20-151">No portal de gerenciamento do Azure do hello, no hello **Adobe criativos da nuvem** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="abb20-151">In hello Azure Management portal, on hello **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="abb20-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="abb20-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="abb20-155">Em Olá **Adobe Creative nuvem domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="abb20-155">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="abb20-157">a.</span><span class="sxs-lookup"><span data-stu-id="abb20-157">a.</span></span> <span data-ttu-id="abb20-158">Em Olá **identificador** texto, o valor do tipo hello como:`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="abb20-158">In hello **Identifier** textbox, type hello value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="abb20-159">b.</span><span class="sxs-lookup"><span data-stu-id="abb20-159">b.</span></span> <span data-ttu-id="abb20-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="abb20-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="abb20-161">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="abb20-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="abb20-162">Você tem tooupdate esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="abb20-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="abb20-163">Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação.</span><span class="sxs-lookup"><span data-stu-id="abb20-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="abb20-164">Se você precisar toocreate um usuário manualmente, é necessário a equipe de suporte do toocontact Olá Adobe criativos da nuvem.</span><span class="sxs-lookup"><span data-stu-id="abb20-164">If you need toocreate an user manually, you need toocontact hello Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="abb20-165">Em Olá **Adobe Creative nuvem domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="abb20-165">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="abb20-167">a.</span><span class="sxs-lookup"><span data-stu-id="abb20-167">a.</span></span> <span data-ttu-id="abb20-168">Clique em Olá **Mostrar configurações de URL avançadas** opção</span><span class="sxs-lookup"><span data-stu-id="abb20-168">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="abb20-169">b.</span><span class="sxs-lookup"><span data-stu-id="abb20-169">b.</span></span> <span data-ttu-id="abb20-170">Em Olá **URL de logon** texto, o valor do tipo hello como:`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="abb20-170">In hello **Sign-on URL** textbox, type hello value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="abb20-171">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="abb20-171">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="abb20-173">Em Olá **Adobe Creative configuração de nuvem** seção, clique em **configurar Adobe criativos da nuvem** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="abb20-173">On hello **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="abb20-174">Copie Olá **Id da entidade SAML** e **URL do serviço SSO do SAML** da seção de referência rápida.</span><span class="sxs-lookup"><span data-stu-id="abb20-174">Please copy hello **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="abb20-176">Em uma janela de navegador web diferente, locatário de nuvem Creative Adobe tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="abb20-176">In a different web browser window, sign-on tooyour Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="abb20-177">Vá muito**identidade** Olá painel de navegação esquerdo e clique em seu domínio.</span><span class="sxs-lookup"><span data-stu-id="abb20-177">Go too**Identity** on hello left navigation pane and click your domain.</span></span> <span data-ttu-id="abb20-178">Em seguida, executar Olá seguindo as etapas na **logon único na configuração necessária** seção.</span><span class="sxs-lookup"><span data-stu-id="abb20-178">Then perform hello following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="abb20-179">![Configurações](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="abb20-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="abb20-180">Clique em **procurar** Olá tooupload baixado certificado do AD do Azure muito**certificado IDP**.</span><span class="sxs-lookup"><span data-stu-id="abb20-180">Click **Browse** tooupload hello downloaded certificate from Azure AD too**IDP Certificate**.</span></span>

10. <span data-ttu-id="abb20-181">Em Olá **emissor IDP** caixa de texto, coloque o valor de saudação do **Id da entidade SAML** que você copiou de **configurar o logon** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="abb20-181">In hello **IDP issuer** textbox, put hello value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="abb20-182">Em Olá **URL de logon IDP** caixa de texto, coloque o valor de saudação do **URL do serviço SSO do SAML** que você copiou de **configurar o logon** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="abb20-182">In hello **IDP Login URL** textbox, put hello value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="abb20-183">Selecione **Redirecionamento HTTP** como **Associação IdP**.</span><span class="sxs-lookup"><span data-stu-id="abb20-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="abb20-184">Selecione **Endereço de email** como **Configuração de logon do usuário**.</span><span class="sxs-lookup"><span data-stu-id="abb20-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="abb20-185">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="abb20-185">Click **Save** button.</span></span>

15. <span data-ttu-id="abb20-186">painel Olá agora apresentará Olá XML **"Baixar metadados"** arquivo.</span><span class="sxs-lookup"><span data-stu-id="abb20-186">hello dashboard will now present hello XML **"Download Metadata"** file.</span></span> <span data-ttu-id="abb20-187">Ele contém a URL EntityDescriptor e a URL AssertionConsumerService da Adobe.</span><span class="sxs-lookup"><span data-stu-id="abb20-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="abb20-188">Abra arquivo hello e configurá-las no hello aplicativo AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="abb20-188">Please open hello file and configure them in hello Azure AD application.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="abb20-191">a.</span><span class="sxs-lookup"><span data-stu-id="abb20-191">a.</span></span> <span data-ttu-id="abb20-192">Olá Use EntityDescriptor valor Adobe fornecida por **identificador** em Olá **definir configurações de aplicativo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="abb20-192">Use hello EntityDescriptor value Adobe provided you for **Identifier** on hello **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="abb20-193">b.</span><span class="sxs-lookup"><span data-stu-id="abb20-193">b.</span></span> <span data-ttu-id="abb20-194">Olá Use AssertionConsumerService valor Adobe fornecida por **URL de resposta** em Olá **definir configurações de aplicativo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="abb20-194">Use hello AssertionConsumerService value Adobe provided you for **Reply URL** on hello **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="abb20-195">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="abb20-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="abb20-196">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="abb20-196">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="abb20-198">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="abb20-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="abb20-199">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="abb20-199">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="abb20-201">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="abb20-201">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="abb20-203">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="abb20-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="abb20-205">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="abb20-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="abb20-207">a.</span><span class="sxs-lookup"><span data-stu-id="abb20-207">a.</span></span> <span data-ttu-id="abb20-208">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="abb20-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="abb20-209">b.</span><span class="sxs-lookup"><span data-stu-id="abb20-209">b.</span></span> <span data-ttu-id="abb20-210">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="abb20-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="abb20-211">c.</span><span class="sxs-lookup"><span data-stu-id="abb20-211">c.</span></span> <span data-ttu-id="abb20-212">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="abb20-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="abb20-213">d.</span><span class="sxs-lookup"><span data-stu-id="abb20-213">d.</span></span> <span data-ttu-id="abb20-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="abb20-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="abb20-215">Criando um usuário de teste da Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="abb20-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="abb20-216">Em ordem tooenable AD do Azure usuários toolog em Adobe criativos da nuvem, eles devem ser provisionados no Adobe criativos da nuvem.</span><span class="sxs-lookup"><span data-stu-id="abb20-216">In order tooenable Azure AD users toolog into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="abb20-217">No caso de saudação do Adobe criativos da nuvem, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="abb20-217">In hello case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="abb20-218">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="abb20-218">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="abb20-219">Faça logon tooyour site de empresa do Adobe criativos da nuvem como um administrador.</span><span class="sxs-lookup"><span data-stu-id="abb20-219">Log in tooyour Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="abb20-220">Clique em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="abb20-220">Click **People**.</span></span>

    <span data-ttu-id="abb20-221">![Pessoas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="abb20-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="abb20-222">Clique em **Convidar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="abb20-222">Click **Invite User**.</span></span>

    <span data-ttu-id="abb20-223">![Convidar Usuários](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Convidar Usuários")</span><span class="sxs-lookup"><span data-stu-id="abb20-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="abb20-224">Em Olá **convidar pessoas** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="abb20-224">On hello **Invite People** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="abb20-225">![Convidar Pessoas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="abb20-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="abb20-226">a.</span><span class="sxs-lookup"><span data-stu-id="abb20-226">a.</span></span> <span data-ttu-id="abb20-227">Em Olá **Email** caixa de texto, tipo hello endereço de email da conta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="abb20-227">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="abb20-228">b.</span><span class="sxs-lookup"><span data-stu-id="abb20-228">b.</span></span> <span data-ttu-id="abb20-229">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="abb20-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="abb20-230">proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="abb20-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="abb20-231">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="abb20-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="abb20-232">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooAdobe seu acesso criativos da nuvem.</span><span class="sxs-lookup"><span data-stu-id="abb20-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAdobe Creative Cloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="abb20-234">**tooassign Britta Simon tooAdobe criativos da nuvem, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="abb20-234">**tooassign Britta Simon tooAdobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="abb20-235">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="abb20-235">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="abb20-237">Na lista de aplicativos hello, selecione **Adobe criativos da nuvem**.</span><span class="sxs-lookup"><span data-stu-id="abb20-237">In hello applications list, select **Adobe Creative Cloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="abb20-239">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="abb20-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="abb20-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="abb20-241">Click **Add** button.</span></span> <span data-ttu-id="abb20-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="abb20-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="abb20-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="abb20-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="abb20-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="abb20-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="abb20-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="abb20-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="abb20-247">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="abb20-247">Testing single sign-on</span></span>

<span data-ttu-id="abb20-248">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="abb20-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="abb20-249">Quando você clica em bloco Adobe criativos da nuvem Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Adobe criativos da nuvem.</span><span class="sxs-lookup"><span data-stu-id="abb20-249">When you click hello Adobe Creative Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="abb20-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="abb20-250">Additional resources</span></span>

* [<span data-ttu-id="abb20-251">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="abb20-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="abb20-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="abb20-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png