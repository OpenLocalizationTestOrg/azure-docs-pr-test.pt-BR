---
title: "Tutorial: integração do Azure Active Directory com o Fuze | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Fuze."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: d0ea8c6456824e348301ed8bf1f5e00f4bfa8121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="460ca-103">Tutorial: integração do Azure Active Directory com o Fuze</span><span class="sxs-lookup"><span data-stu-id="460ca-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="460ca-104">Neste tutorial, você aprenderá como toointegrate Fuze com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="460ca-104">In this tutorial, you learn how toointegrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="460ca-105">Integrando Fuze com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="460ca-105">Integrating Fuze with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="460ca-106">Você pode controlar no AD do Azure que tenha acesso tooFuze</span><span class="sxs-lookup"><span data-stu-id="460ca-106">You can control in Azure AD who has access tooFuze</span></span>
- <span data-ttu-id="460ca-107">Você pode habilitar seu usuários tooautomatically get conectado tooFuze (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="460ca-107">You can enable your users tooautomatically get signed-on tooFuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="460ca-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="460ca-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="460ca-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="460ca-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="460ca-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="460ca-110">Prerequisites</span></span>

<span data-ttu-id="460ca-111">tooconfigure integração do AD do Azure com Fuze, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="460ca-111">tooconfigure Azure AD integration with Fuze, you need hello following items:</span></span>

- <span data-ttu-id="460ca-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="460ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="460ca-113">Uma assinatura do Fuze habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="460ca-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="460ca-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="460ca-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="460ca-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="460ca-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="460ca-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="460ca-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="460ca-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="460ca-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="460ca-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="460ca-118">Scenario description</span></span>
<span data-ttu-id="460ca-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="460ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="460ca-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="460ca-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="460ca-121">Adicionando Fuze da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="460ca-121">Adding Fuze from hello gallery</span></span>
2. <span data-ttu-id="460ca-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="460ca-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-hello-gallery"></a><span data-ttu-id="460ca-123">Adicionando Fuze da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="460ca-123">Adding Fuze from hello gallery</span></span>
<span data-ttu-id="460ca-124">integração de saudação tooconfigure de Fuze no AD do Azure, você precisa tooadd Fuze da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="460ca-124">tooconfigure hello integration of Fuze into Azure AD, you need tooadd Fuze from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="460ca-125">**tooadd Fuze da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="460ca-125">**tooadd Fuze from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="460ca-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="460ca-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="460ca-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="460ca-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="460ca-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="460ca-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="460ca-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="460ca-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="460ca-133">Na caixa de pesquisa hello, digite **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="460ca-133">In hello search box, type **Fuze**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="460ca-135">No painel de resultados de saudação, selecione **Fuze**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="460ca-135">In hello results panel, select **Fuze**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="460ca-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="460ca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="460ca-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Fuze, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="460ca-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="460ca-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Fuze é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="460ca-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuze is tooa user in Azure AD.</span></span> <span data-ttu-id="460ca-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Fuze precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="460ca-140">In other words, a link relationship between an Azure AD user and hello related user in Fuze needs toobe established.</span></span>

<span data-ttu-id="460ca-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Fuze.</span><span class="sxs-lookup"><span data-stu-id="460ca-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Fuze.</span></span>

<span data-ttu-id="460ca-142">tooconfigure e teste de logon único do AD do Azure com Fuze, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="460ca-142">tooconfigure and test Azure AD single sign-on with Fuze, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="460ca-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="460ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="460ca-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="460ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="460ca-145">**[Criar um usuário de teste Fuze](#creating-a-fuze-test-user)**  -toohave um equivalente do Britta Simon em Fuze é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="460ca-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - toohave a counterpart of Britta Simon in Fuze that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="460ca-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="460ca-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="460ca-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="460ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="460ca-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="460ca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="460ca-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Fuze.</span><span class="sxs-lookup"><span data-stu-id="460ca-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="460ca-150">**tooconfigure AD do Azure-logon único com Fuze, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="460ca-150">**tooconfigure Azure AD single sign-on with Fuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="460ca-151">No portal de gerenciamento do Azure do hello, no hello **Fuze** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="460ca-151">In hello Azure Management portal, on hello **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="460ca-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="460ca-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="460ca-155">Em Olá **Fuze domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="460ca-155">On hello **Fuze Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="460ca-157">Em Olá **URL de logon** caixa de texto, digite a URL de saudação logon como:`https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="460ca-157">In hello **Sign on URL** textbox, type hello Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="460ca-158">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="460ca-158">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="460ca-160">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de xml de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="460ca-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello xml file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="460ca-162">tooconfigure logon único no **Fuze** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte Fuze](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="460ca-162">tooconfigure single sign-on on **Fuze** side, you need toosend hello downloaded **Metadata XML** too[Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="460ca-163">Eles serão configurados isso no hello toohave de ordem conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="460ca-163">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="460ca-164">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="460ca-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="460ca-165">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="460ca-165">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="460ca-167">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="460ca-167">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="460ca-168">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="460ca-168">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="460ca-170">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="460ca-170">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="460ca-172">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="460ca-172">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="460ca-174">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="460ca-174">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="460ca-176">a.</span><span class="sxs-lookup"><span data-stu-id="460ca-176">a.</span></span> <span data-ttu-id="460ca-177">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="460ca-177">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="460ca-178">b.</span><span class="sxs-lookup"><span data-stu-id="460ca-178">b.</span></span> <span data-ttu-id="460ca-179">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="460ca-179">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="460ca-180">c.</span><span class="sxs-lookup"><span data-stu-id="460ca-180">c.</span></span> <span data-ttu-id="460ca-181">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="460ca-181">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="460ca-182">d.</span><span class="sxs-lookup"><span data-stu-id="460ca-182">d.</span></span> <span data-ttu-id="460ca-183">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="460ca-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="460ca-184">Criando um usuário de teste do Fuze</span><span class="sxs-lookup"><span data-stu-id="460ca-184">Creating a Fuze test user</span></span>

<span data-ttu-id="460ca-185">O aplicativo Fuze dá suporte ao provisionamento de usuário just-in-time completo. Dessa forma, os usuários serão criados automaticamente quando eles conectarem.</span><span class="sxs-lookup"><span data-stu-id="460ca-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="460ca-186">Para outros esclarecimentos, contate o [suporte](https://www.fuze.com/support) Fuze.</span><span class="sxs-lookup"><span data-stu-id="460ca-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="460ca-187">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="460ca-187">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="460ca-188">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooFuze seu acesso.</span><span class="sxs-lookup"><span data-stu-id="460ca-188">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFuze.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="460ca-190">**tooassign Britta Simon tooFuze, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="460ca-190">**tooassign Britta Simon tooFuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="460ca-191">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="460ca-191">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="460ca-193">Na lista de aplicativos hello, selecione **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="460ca-193">In hello applications list, select **Fuze**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="460ca-195">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="460ca-195">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="460ca-197">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="460ca-197">Click **Add** button.</span></span> <span data-ttu-id="460ca-198">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="460ca-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="460ca-200">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="460ca-200">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="460ca-201">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="460ca-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="460ca-202">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="460ca-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="460ca-203">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="460ca-203">Testing single sign-on</span></span>

<span data-ttu-id="460ca-204">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="460ca-204">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="460ca-205">Quando você clica em bloco Fuze Olá Olá painel de acesso, você deve obter o aplicativo de Fuze tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="460ca-205">When you click hello Fuze tile in hello Access Panel, you should get automatically signed-on tooyour Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="460ca-206">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="460ca-206">Additional resources</span></span>

* [<span data-ttu-id="460ca-207">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="460ca-207">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="460ca-208">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="460ca-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png