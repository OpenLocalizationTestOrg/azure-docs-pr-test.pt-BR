---
title: "Tutorial: integração do Azure Active Directory com o Showpad | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Showpad."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2c8c306b4b94c368a93f92123d3abe9fe35167db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="8bb6e-103">Tutorial: Integração do Azure Active Directory com o Showpad</span><span class="sxs-lookup"><span data-stu-id="8bb6e-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="8bb6e-104">Neste tutorial, você aprenderá como toointegrate Showpad com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="8bb6e-104">In this tutorial, you learn how toointegrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8bb6e-105">Integrando Showpad com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="8bb6e-105">Integrating Showpad with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8bb6e-106">Você pode controlar no AD do Azure que tenha acesso tooShowpad</span><span class="sxs-lookup"><span data-stu-id="8bb6e-106">You can control in Azure AD who has access tooShowpad</span></span>
- <span data-ttu-id="8bb6e-107">Você pode habilitar seu usuários tooautomatically get conectado tooShowpad (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8bb6e-107">You can enable your users tooautomatically get signed-on tooShowpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8bb6e-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8bb6e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8bb6e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8bb6e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bb6e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8bb6e-110">Prerequisites</span></span>

<span data-ttu-id="8bb6e-111">tooconfigure integração do AD do Azure com Showpad, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8bb6e-111">tooconfigure Azure AD integration with Showpad, you need hello following items:</span></span>

- <span data-ttu-id="8bb6e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8bb6e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8bb6e-113">Uma assinatura habilitada para logon único do Showpad</span><span class="sxs-lookup"><span data-stu-id="8bb6e-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8bb6e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8bb6e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8bb6e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8bb6e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8bb6e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8bb6e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8bb6e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8bb6e-118">Scenario description</span></span>
<span data-ttu-id="8bb6e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8bb6e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="8bb6e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8bb6e-121">Adicionando Showpad da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8bb6e-121">Adding Showpad from hello gallery</span></span>
2. <span data-ttu-id="8bb6e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8bb6e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-hello-gallery"></a><span data-ttu-id="8bb6e-123">Adicionando Showpad da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8bb6e-123">Adding Showpad from hello gallery</span></span>

<span data-ttu-id="8bb6e-124">integração de saudação tooconfigure de Showpad no AD do Azure, você precisa tooadd Showpad da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-124">tooconfigure hello integration of Showpad into Azure AD, you need tooadd Showpad from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8bb6e-125">**tooadd Showpad da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8bb6e-125">**tooadd Showpad from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bb6e-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8bb6e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8bb6e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8bb6e-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8bb6e-133">Na caixa de pesquisa hello, digite **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-133">In hello search box, type **Showpad**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="8bb6e-135">No painel de resultados de saudação, selecione **Showpad**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-135">In hello results panel, select **Showpad**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8bb6e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8bb6e-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="8bb6e-138">Nesta seção, você configura e testa o logon único do Azure AD com o Showpad, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8bb6e-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Showpad é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Showpad is tooa user in Azure AD.</span></span> <span data-ttu-id="8bb6e-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Showpad precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-140">In other words, a link relationship between an Azure AD user and hello related user in Showpad needs toobe established.</span></span>

<span data-ttu-id="8bb6e-141">Showpad, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-141">In Showpad, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8bb6e-142">tooconfigure e teste de logon único do AD do Azure com Showpad, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="8bb6e-142">tooconfigure and test Azure AD single sign-on with Showpad, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8bb6e-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8bb6e-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8bb6e-145">**[Criar um usuário de teste Showpad](#creating-a-showpad-test-user)**  -toohave um equivalente do Britta Simon em Showpad é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - toohave a counterpart of Britta Simon in Showpad that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8bb6e-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8bb6e-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8bb6e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bb6e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8bb6e-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Showpad.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="8bb6e-150">**tooconfigure AD do Azure-logon único com Showpad, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8bb6e-150">**tooconfigure Azure AD single sign-on with Showpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bb6e-151">Em Olá portal do Azure, Olá **Showpad** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-151">In hello Azure portal, on hello **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8bb6e-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="8bb6e-155">Em Olá **Showpad domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8bb6e-155">On hello **Showpad Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="8bb6e-157">a.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-157">a.</span></span> <span data-ttu-id="8bb6e-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="8bb6e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="8bb6e-159">b.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-159">b.</span></span> <span data-ttu-id="8bb6e-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="8bb6e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8bb6e-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-161">These values are not real.</span></span> <span data-ttu-id="8bb6e-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8bb6e-163">Entre em contato com [Showpad a equipe de suporte](https://help.showpad.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-163">Contact [Showpad support team](https://help.showpad.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="8bb6e-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="8bb6e-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8bb6e-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8bb6e-168">Locatário de Showpad tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-168">Sign-on tooyour Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="8bb6e-169">No menu de saudação na parte superior do hello, clique Olá **configurações**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-169">In hello menu on hello top, click hello **Settings**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="8bb6e-171">Navegue muito"**Single Sign-On**"e clique em"**habilitar**."</span><span class="sxs-lookup"><span data-stu-id="8bb6e-171">Navigate too"**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="8bb6e-173">Em Olá **adicionar um serviço do SAML 2.0** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8bb6e-173">On hello **Add a SAML 2.0 Service** dialog, perform hello following steps:</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="8bb6e-175">a.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-175">a.</span></span> <span data-ttu-id="8bb6e-176">Em Olá **nome** caixa de texto, nome de saudação do tipo do provedor de identificador (por exemplo: o nome da empresa).</span><span class="sxs-lookup"><span data-stu-id="8bb6e-176">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="8bb6e-177">b.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-177">b.</span></span> <span data-ttu-id="8bb6e-178">Como **Fonte de Metadados**, selecione **XML**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="8bb6e-179">c.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-179">c.</span></span> <span data-ttu-id="8bb6e-180">Copiar o conteúdo de saudação do arquivo XML de metadados, que você baixou do hello portal do Azure, e, em seguida, cole-Olá **Metadata XML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-180">Copy hello content of metadata XML file, which you have downloaded from hello Azure portal, and then paste it into hello **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="8bb6e-181">d.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-181">d.</span></span> <span data-ttu-id="8bb6e-182">Selecione **Provisionar automaticamente contas para novos usuários quando eles fizerem logon**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="8bb6e-183">e.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-183">e.</span></span> <span data-ttu-id="8bb6e-184">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="8bb6e-185">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="8bb6e-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8bb6e-186">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8bb6e-187">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8bb6e-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8bb6e-188">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8bb6e-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="8bb6e-189">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8bb6e-191">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8bb6e-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bb6e-192">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8bb6e-194">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8bb6e-196">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8bb6e-198">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8bb6e-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8bb6e-200">a.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-200">a.</span></span> <span data-ttu-id="8bb6e-201">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8bb6e-202">b.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-202">b.</span></span> <span data-ttu-id="8bb6e-203">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8bb6e-204">c.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-204">c.</span></span> <span data-ttu-id="8bb6e-205">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8bb6e-206">d.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-206">d.</span></span> <span data-ttu-id="8bb6e-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="8bb6e-208">Criar um usuário de teste do Showpad</span><span class="sxs-lookup"><span data-stu-id="8bb6e-208">Creating a Showpad test user</span></span>

<span data-ttu-id="8bb6e-209">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Showpad.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-209">hello objective of this section is toocreate a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="8bb6e-210">O Showpad dá suporte ao provisionamento just-in-time.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="8bb6e-211">Você já habilitou o provisionamento em **[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="8bb6e-212">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8bb6e-213">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8bb6e-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8bb6e-214">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooShowpad.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooShowpad.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8bb6e-216">**tooassign Britta Simon tooShowpad, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8bb6e-216">**tooassign Britta Simon tooShowpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bb6e-217">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8bb6e-219">Na lista de aplicativos hello, selecione **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-219">In hello applications list, select **Showpad**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="8bb6e-221">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8bb6e-223">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-223">Click **Add** button.</span></span> <span data-ttu-id="8bb6e-224">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8bb6e-226">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8bb6e-227">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8bb6e-228">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8bb6e-229">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8bb6e-229">Testing single sign-on</span></span>

<span data-ttu-id="8bb6e-230">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8bb6e-231">Quando você clica em bloco Showpad Olá Olá painel de acesso, você deve obter tooShowpad automaticamente conectado no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8bb6e-231">When you click hello Showpad tile in hello Access Panel, you should get automatically signed-on tooShowpad application.</span></span>
<span data-ttu-id="8bb6e-232">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8bb6e-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8bb6e-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8bb6e-233">Additional resources</span></span>

* [<span data-ttu-id="8bb6e-234">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8bb6e-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8bb6e-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8bb6e-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

