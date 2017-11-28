---
title: "Tutorial: Integração do Azure Active Directory ao Inkling | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Inkling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 544101f1972ec16222406b761d2b6f4987458df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="1640e-103">Tutorial: Integração do Azure Active Directory ao Inkling</span><span class="sxs-lookup"><span data-stu-id="1640e-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="1640e-104">Neste tutorial, você aprenderá como toointegrate Inkling com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="1640e-104">In this tutorial, you learn how toointegrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1640e-105">Integrando Inkling com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="1640e-105">Integrating Inkling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1640e-106">Você pode controlar no AD do Azure que tenha acesso tooInkling</span><span class="sxs-lookup"><span data-stu-id="1640e-106">You can control in Azure AD who has access tooInkling</span></span>
- <span data-ttu-id="1640e-107">Você pode habilitar seu usuários tooautomatically get conectado tooInkling (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1640e-107">You can enable your users tooautomatically get signed-on tooInkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1640e-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="1640e-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="1640e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1640e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1640e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1640e-110">Prerequisites</span></span>

<span data-ttu-id="1640e-111">tooconfigure integração do AD do Azure com Inkling, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1640e-111">tooconfigure Azure AD integration with Inkling, you need hello following items:</span></span>

- <span data-ttu-id="1640e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1640e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1640e-113">Uma assinatura habilitada para logon único no Inkling</span><span class="sxs-lookup"><span data-stu-id="1640e-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="1640e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1640e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="1640e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1640e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1640e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1640e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1640e-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1640e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="1640e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1640e-118">Scenario description</span></span>
<span data-ttu-id="1640e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1640e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1640e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="1640e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1640e-121">Adicionando Inkling da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1640e-121">Adding Inkling from hello gallery</span></span>
2. <span data-ttu-id="1640e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1640e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-hello-gallery"></a><span data-ttu-id="1640e-123">Adicionando Inkling da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1640e-123">Adding Inkling from hello gallery</span></span>
<span data-ttu-id="1640e-124">integração de saudação tooconfigure de Inkling no AD do Azure, você precisa tooadd Inkling da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1640e-124">tooconfigure hello integration of Inkling into Azure AD, you need tooadd Inkling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1640e-125">**tooadd Inkling da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1640e-125">**tooadd Inkling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1640e-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1640e-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1640e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1640e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1640e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1640e-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1640e-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1640e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1640e-133">Na caixa de pesquisa hello, digite **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="1640e-133">In hello search box, type **Inkling**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="1640e-135">No painel de resultados de saudação, selecione **Inkling**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1640e-135">In hello results panel, select **Inkling**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1640e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1640e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1640e-138">Nesta seção, você configura e testa o logon único do Azure AD com o Inkling, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="1640e-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1640e-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Inkling é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1640e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Inkling is tooa user in Azure AD.</span></span> <span data-ttu-id="1640e-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Inkling precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1640e-140">In other words, a link relationship between an Azure AD user and hello related user in Inkling needs toobe established.</span></span>

<span data-ttu-id="1640e-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Inkling.</span><span class="sxs-lookup"><span data-stu-id="1640e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Inkling.</span></span>

<span data-ttu-id="1640e-142">teste logon único do AD do Azure com Inkling e tooconfigure, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="1640e-142">tooconfigure and test Azure AD single sign-on with Inkling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1640e-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1640e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1640e-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1640e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1640e-145">**[Criar um usuário de teste Inkling](#creating-an-inkling-test-user)**  -toohave um equivalente do Britta Simon em Inkling é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="1640e-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - toohave a counterpart of Britta Simon in Inkling that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="1640e-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="1640e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1640e-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="1640e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1640e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1640e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1640e-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Inkling.</span><span class="sxs-lookup"><span data-stu-id="1640e-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="1640e-150">**tooconfigure AD do Azure-logon único com Inkling, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1640e-150">**tooconfigure Azure AD single sign-on with Inkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="1640e-151">No portal de gerenciamento do Azure do hello, no hello **Inkling** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="1640e-151">In hello Azure Management portal, on hello **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1640e-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="1640e-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="1640e-155">Em Olá **Inkling domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1640e-155">On hello **Inkling Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="1640e-157">a.</span><span class="sxs-lookup"><span data-stu-id="1640e-157">a.</span></span> <span data-ttu-id="1640e-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="1640e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="1640e-159">b.</span><span class="sxs-lookup"><span data-stu-id="1640e-159">b.</span></span> <span data-ttu-id="1640e-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="1640e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1640e-161">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="1640e-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="1640e-162">Você tem tooupdate esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="1640e-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="1640e-163">Entre em contato com [a equipe de suporte Inkling](mailto:press@inkling.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="1640e-163">Contact [Inkling support team](mailto:press@inkling.com) tooget these values.</span></span>

4. <span data-ttu-id="1640e-164">Em Olá **o certificado de autenticação SAML** seção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="1640e-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="1640e-166">Em Olá **criar um novo certificado** caixa de diálogo, clique o ícone de calendário hello e selecione um **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="1640e-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="1640e-167">Em seguida, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1640e-167">Then click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="1640e-169">Em Olá **o certificado de autenticação SAML** seção, selecione **ativar o novo certificado** e clique em **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="1640e-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="1640e-171">Na janela pop-up de saudação **certificado de substituição** janela, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="1640e-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="1640e-173">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1640e-173">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="1640e-175">tooget SSO configurado para o seu aplicativo, entre em contato com [a equipe de suporte Inkling](mailto:press@inkling.com) e fornecê-los com baixado **metadados**.</span><span class="sxs-lookup"><span data-stu-id="1640e-175">tooget SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1640e-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1640e-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="1640e-177">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1640e-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1640e-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1640e-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1640e-180">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1640e-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1640e-182">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="1640e-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1640e-184">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1640e-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1640e-186">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1640e-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1640e-188">a.</span><span class="sxs-lookup"><span data-stu-id="1640e-188">a.</span></span> <span data-ttu-id="1640e-189">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1640e-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1640e-190">b.</span><span class="sxs-lookup"><span data-stu-id="1640e-190">b.</span></span> <span data-ttu-id="1640e-191">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1640e-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1640e-192">c.</span><span class="sxs-lookup"><span data-stu-id="1640e-192">c.</span></span> <span data-ttu-id="1640e-193">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="1640e-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1640e-194">d.</span><span class="sxs-lookup"><span data-stu-id="1640e-194">d.</span></span> <span data-ttu-id="1640e-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1640e-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="1640e-196">Criando um usuário de teste do Inkling</span><span class="sxs-lookup"><span data-stu-id="1640e-196">Creating an Inkling test user</span></span>

<span data-ttu-id="1640e-197">Nesta seção, você cria um usuário chamado Brenda Fernandes no Inkling.</span><span class="sxs-lookup"><span data-stu-id="1640e-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="1640e-198">Trabalhe com [a equipe de suporte Inkling](mailto:press@inkling.com) tooadd usuários de saudação na plataforma de Inkling hello.</span><span class="sxs-lookup"><span data-stu-id="1640e-198">Please work with [Inkling support team](mailto:press@inkling.com) tooadd hello users in hello Inkling platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1640e-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1640e-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1640e-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooInkling seu acesso.</span><span class="sxs-lookup"><span data-stu-id="1640e-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooInkling.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1640e-202">**tooassign Britta Simon tooInkling, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1640e-202">**tooassign Britta Simon tooInkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="1640e-203">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1640e-203">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1640e-205">Na lista de aplicativos hello, selecione **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="1640e-205">In hello applications list, select **Inkling**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="1640e-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1640e-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1640e-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1640e-209">Click **Add** button.</span></span> <span data-ttu-id="1640e-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1640e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1640e-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="1640e-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1640e-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1640e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1640e-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1640e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="1640e-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1640e-215">Testing single sign-on</span></span>

<span data-ttu-id="1640e-216">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="1640e-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1640e-217">Quando você clica em bloco Inkling Olá Olá painel de acesso, você deve obter o aplicativo de Inkling tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="1640e-217">When you click hello Inkling tile in hello Access Panel, you should get automatically signed-on tooyour Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1640e-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1640e-218">Additional resources</span></span>

* [<span data-ttu-id="1640e-219">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1640e-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1640e-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1640e-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png