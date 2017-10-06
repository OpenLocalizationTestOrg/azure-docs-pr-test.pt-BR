---
title: "Tutorial: Integração do Azure Active Directory ao PolicyStat | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="46cb0-103">Tutorial: Integração do Azure Active Directory ao PolicyStat</span><span class="sxs-lookup"><span data-stu-id="46cb0-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="46cb0-104">Neste tutorial, você aprenderá como toointegrate PolicyStat com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="46cb0-104">In this tutorial, you learn how toointegrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46cb0-105">Integrando PolicyStat com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="46cb0-105">Integrating PolicyStat with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="46cb0-106">Você pode controlar no AD do Azure que tenha acesso tooPolicyStat</span><span class="sxs-lookup"><span data-stu-id="46cb0-106">You can control in Azure AD who has access tooPolicyStat</span></span>
- <span data-ttu-id="46cb0-107">Você pode habilitar seu usuários tooautomatically get conectado tooPolicyStat (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="46cb0-107">You can enable your users tooautomatically get signed-on tooPolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="46cb0-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="46cb0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="46cb0-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="46cb0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46cb0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="46cb0-110">Prerequisites</span></span>

<span data-ttu-id="46cb0-111">tooconfigure integração do AD do Azure com PolicyStat, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="46cb0-111">tooconfigure Azure AD integration with PolicyStat, you need hello following items:</span></span>

- <span data-ttu-id="46cb0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="46cb0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46cb0-113">Uma assinatura habilitada para logon único do PolicyStat</span><span class="sxs-lookup"><span data-stu-id="46cb0-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="46cb0-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="46cb0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="46cb0-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="46cb0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="46cb0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="46cb0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="46cb0-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46cb0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46cb0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="46cb0-118">Scenario description</span></span>
<span data-ttu-id="46cb0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="46cb0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="46cb0-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="46cb0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46cb0-121">Adicionando PolicyStat da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="46cb0-121">Adding PolicyStat from hello gallery</span></span>
2. <span data-ttu-id="46cb0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="46cb0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-hello-gallery"></a><span data-ttu-id="46cb0-123">Adicionando PolicyStat da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="46cb0-123">Adding PolicyStat from hello gallery</span></span>
<span data-ttu-id="46cb0-124">integração de saudação tooconfigure de PolicyStat no AD do Azure, você precisa tooadd PolicyStat da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="46cb0-124">tooconfigure hello integration of PolicyStat into Azure AD, you need tooadd PolicyStat from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="46cb0-125">**tooadd PolicyStat da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="46cb0-125">**tooadd PolicyStat from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="46cb0-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="46cb0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="46cb0-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="46cb0-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="46cb0-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46cb0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="46cb0-133">Na caixa de pesquisa hello, digite **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-133">In hello search box, type **PolicyStat**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="46cb0-135">No painel de resultados de saudação, selecione **PolicyStat**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="46cb0-135">In hello results panel, select **PolicyStat**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="46cb0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="46cb0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="46cb0-138">Nesta seção, você configura e testa o logon único do Azure AD com o PolicyStat, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="46cb0-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="46cb0-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em PolicyStat é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="46cb0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PolicyStat is tooa user in Azure AD.</span></span> <span data-ttu-id="46cb0-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em PolicyStat precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="46cb0-140">In other words, a link relationship between an Azure AD user and hello related user in PolicyStat needs toobe established.</span></span>

<span data-ttu-id="46cb0-141">PolicyStat, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="46cb0-141">In PolicyStat, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="46cb0-142">tooconfigure e teste de logon único do AD do Azure com PolicyStat, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="46cb0-142">tooconfigure and test Azure AD single sign-on with PolicyStat, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="46cb0-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="46cb0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="46cb0-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46cb0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="46cb0-145">**[Criar um usuário de teste PolicyStat](#creating-a-policystat-test-user)**  -toohave um equivalente do Britta Simon em PolicyStat é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="46cb0-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - toohave a counterpart of Britta Simon in PolicyStat that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="46cb0-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="46cb0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="46cb0-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="46cb0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="46cb0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46cb0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="46cb0-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="46cb0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="46cb0-150">**tooconfigure AD do Azure-logon único com PolicyStat, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="46cb0-150">**tooconfigure Azure AD single sign-on with PolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="46cb0-151">Em Olá portal do Azure, Olá **PolicyStat** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-151">In hello Azure portal, on hello **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="46cb0-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="46cb0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="46cb0-155">Em Olá **PolicyStat domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="46cb0-155">On hello **PolicyStat Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="46cb0-157">a.</span><span class="sxs-lookup"><span data-stu-id="46cb0-157">a.</span></span> <span data-ttu-id="46cb0-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="46cb0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="46cb0-159">b.</span><span class="sxs-lookup"><span data-stu-id="46cb0-159">b.</span></span> <span data-ttu-id="46cb0-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="46cb0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="46cb0-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="46cb0-161">These values are not real.</span></span> <span data-ttu-id="46cb0-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="46cb0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="46cb0-163">Entre em contato com [equipe de suporte do cliente PolicyStat](http://www.policystat.com/support/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="46cb0-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="46cb0-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="46cb0-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="46cb0-166">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooPolicyStat com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="46cb0-166">hello objective of this section is toooutline how tooenable users tooauthenticate tooPolicyStat with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="46cb0-167">Olá PolicyStat aplicativo espera asserções SAML de saudação em um formato específico, o que exige que você tooyour de mapeamentos de atributo personalizado tooadd **atributos de tokens SAML** configuração.</span><span class="sxs-lookup"><span data-stu-id="46cb0-167">hello PolicyStat application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="46cb0-168">Olá captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="46cb0-168">hello following screenshot shows an example of this.</span></span>

     <span data-ttu-id="46cb0-169">![Atributos](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="46cb0-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="46cb0-170">mapeamentos de atributo do tooadd Olá necessária, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="46cb0-170">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="46cb0-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="46cb0-171">Attribute Name</span></span>    |   <span data-ttu-id="46cb0-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="46cb0-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="46cb0-173">uid</span><span class="sxs-lookup"><span data-stu-id="46cb0-173">uid</span></span> | <span data-ttu-id="46cb0-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="46cb0-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="46cb0-175">a.</span><span class="sxs-lookup"><span data-stu-id="46cb0-175">a.</span></span> <span data-ttu-id="46cb0-176">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46cb0-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="46cb0-179">b.</span><span class="sxs-lookup"><span data-stu-id="46cb0-179">b.</span></span> <span data-ttu-id="46cb0-180">Em Olá **nome do atributo** caixa de texto, tipo **uid**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-180">In hello **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="46cb0-181">c.</span><span class="sxs-lookup"><span data-stu-id="46cb0-181">c.</span></span> <span data-ttu-id="46cb0-182">Em Olá **o valor do atributo** caixa de texto, selecione **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-182">In hello **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="46cb0-183">d.</span><span class="sxs-lookup"><span data-stu-id="46cb0-183">d.</span></span> <span data-ttu-id="46cb0-184">De saudação **Mail** lista, selecione **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-184">From hello **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="46cb0-185">e.</span><span class="sxs-lookup"><span data-stu-id="46cb0-185">e.</span></span> <span data-ttu-id="46cb0-186">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="46cb0-186">Click **Ok**</span></span>

7. <span data-ttu-id="46cb0-187">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="46cb0-187">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="46cb0-189">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do PolicyStat como administrador.</span><span class="sxs-lookup"><span data-stu-id="46cb0-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="46cb0-190">Clique em Olá **Admin** guia e, em seguida, clique em **configuração de logon único** no painel de navegação esquerdo.</span><span class="sxs-lookup"><span data-stu-id="46cb0-190">Click hello **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="46cb0-191">![Menu Administrador](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu Administrador")</span><span class="sxs-lookup"><span data-stu-id="46cb0-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="46cb0-192">Em Olá **instalação** seção, selecione **integração de logon único habilitar**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-192">In hello **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="46cb0-193">![Configuração de Logon Único](./media/active-directory-saas-policystat-tutorial/ic808634.png "Configuração de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="46cb0-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="46cb0-194">Clique em **configurar atributos**e em seguida, no hello **configurar atributos** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="46cb0-194">Click **Configure Attributes**, and then, in hello **Configure Attributes** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="46cb0-195">![Configuração de Logon Único](./media/active-directory-saas-policystat-tutorial/ic808635.png "Configuração de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="46cb0-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="46cb0-196">a.</span><span class="sxs-lookup"><span data-stu-id="46cb0-196">a.</span></span> <span data-ttu-id="46cb0-197">Em Olá **atributo Username** caixa de texto, tipo **uid**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-197">In hello **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="46cb0-198">b.</span><span class="sxs-lookup"><span data-stu-id="46cb0-198">b.</span></span> <span data-ttu-id="46cb0-199">Em Olá **atributo de nome** caixa de texto, tipo **firstname** do usuário **Britta**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-199">In hello **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="46cb0-200">c.</span><span class="sxs-lookup"><span data-stu-id="46cb0-200">c.</span></span> <span data-ttu-id="46cb0-201">Em Olá **último nome de atributo** caixa de texto, tipo **lastname** do usuário **Simon**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-201">In hello **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="46cb0-202">d.</span><span class="sxs-lookup"><span data-stu-id="46cb0-202">d.</span></span> <span data-ttu-id="46cb0-203">Em Olá **Email atributo** caixa de texto, tipo **emailaddress** do usuário  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="46cb0-203">In hello **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="46cb0-204">e.</span><span class="sxs-lookup"><span data-stu-id="46cb0-204">e.</span></span> <span data-ttu-id="46cb0-205">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="46cb0-206">Clique em **seus metadados de IDP**e em seguida, no hello **seus metadados de IDP** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="46cb0-206">Click **Your IDP Metadata**, and then, in hello **Your IDP Metadata** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="46cb0-207">![Configuração de Logon Único](./media/active-directory-saas-policystat-tutorial/ic808636.png "Configuração de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="46cb0-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="46cb0-208">a.</span><span class="sxs-lookup"><span data-stu-id="46cb0-208">a.</span></span> <span data-ttu-id="46cb0-209">Abra o arquivo de metadados baixado, a saudação de copiar conteúda e, em seguida, cole-Olá **o metadados do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="46cb0-209">Open your downloaded metadata file, copy hello content, and  then paste it into hello **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="46cb0-210">b.</span><span class="sxs-lookup"><span data-stu-id="46cb0-210">b.</span></span> <span data-ttu-id="46cb0-211">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="46cb0-212">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="46cb0-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="46cb0-213">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="46cb0-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="46cb0-214">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="46cb0-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="46cb0-215">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="46cb0-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="46cb0-216">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="46cb0-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="46cb0-218">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="46cb0-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="46cb0-219">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="46cb0-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="46cb0-221">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="46cb0-223">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="46cb0-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="46cb0-225">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="46cb0-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="46cb0-227">a.</span><span class="sxs-lookup"><span data-stu-id="46cb0-227">a.</span></span> <span data-ttu-id="46cb0-228">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="46cb0-229">b.</span><span class="sxs-lookup"><span data-stu-id="46cb0-229">b.</span></span> <span data-ttu-id="46cb0-230">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="46cb0-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="46cb0-231">c.</span><span class="sxs-lookup"><span data-stu-id="46cb0-231">c.</span></span> <span data-ttu-id="46cb0-232">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="46cb0-233">d.</span><span class="sxs-lookup"><span data-stu-id="46cb0-233">d.</span></span> <span data-ttu-id="46cb0-234">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="46cb0-235">Criando um usuário de teste do PolicyStat</span><span class="sxs-lookup"><span data-stu-id="46cb0-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="46cb0-236">Em ordem tooenable AD do Azure usuários toolog em PolicyStat, eles devem ser provisionados no PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="46cb0-236">In order tooenable Azure AD users toolog into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="46cb0-237">O PolicyStat dá suporte ao provisionamento de usuário just in time.</span><span class="sxs-lookup"><span data-stu-id="46cb0-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="46cb0-238">Isso significa que, você não precisa usuários de saudação tooadd manualmente tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="46cb0-238">This means, you do not need tooadd hello users manually tooPolicyStat.</span></span> <span data-ttu-id="46cb0-239">os usuários de saudação serão serão adicionados automaticamente no seu primeiro logon por meio do SSO.</span><span class="sxs-lookup"><span data-stu-id="46cb0-239">hello users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="46cb0-240">Você pode usar qualquer ferramenta de criação outros PolicyStat usuário conta ou APIs fornecidas pelo PolicyStat tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="46cb0-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="46cb0-241">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="46cb0-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="46cb0-242">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="46cb0-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPolicyStat.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="46cb0-244">**tooassign Britta Simon tooPolicyStat, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="46cb0-244">**tooassign Britta Simon tooPolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="46cb0-245">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="46cb0-247">Na lista de aplicativos hello, selecione **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-247">In hello applications list, select **PolicyStat**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="46cb0-249">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="46cb0-251">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="46cb0-251">Click **Add** button.</span></span> <span data-ttu-id="46cb0-252">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46cb0-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="46cb0-254">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="46cb0-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="46cb0-255">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46cb0-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="46cb0-256">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46cb0-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="46cb0-257">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="46cb0-257">Testing single sign-on</span></span>

<span data-ttu-id="46cb0-258">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="46cb0-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="46cb0-259">Quando você clica em bloco PolicyStat Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour PolicyStat aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46cb0-259">When you click hello PolicyStat tile in hello Access Panel, you should get automatically signed-on tooyour PolicyStat application.</span></span>
<span data-ttu-id="46cb0-260">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="46cb0-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="46cb0-261">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="46cb0-261">Additional resources</span></span>

* [<span data-ttu-id="46cb0-262">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="46cb0-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="46cb0-263">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="46cb0-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

