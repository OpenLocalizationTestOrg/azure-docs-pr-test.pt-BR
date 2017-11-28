---
title: "Tutorial: Integração do Azure Active Directory ao MaxxPoint | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e MaxxPoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 03b13908add8d8c62f1d1480ed2288658fce14d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="95e41-103">Tutorial: Integração do Azure Active Directory ao MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="95e41-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="95e41-104">Neste tutorial, você aprenderá como toointegrate MaxxPoint com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="95e41-104">In this tutorial, you learn how toointegrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95e41-105">Integrando MaxxPoint com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="95e41-105">Integrating MaxxPoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="95e41-106">Você pode controlar no AD do Azure que tenha acesso tooMaxxPoint</span><span class="sxs-lookup"><span data-stu-id="95e41-106">You can control in Azure AD who has access tooMaxxPoint</span></span>
- <span data-ttu-id="95e41-107">Você pode habilitar seu usuários tooautomatically get conectado tooMaxxPoint (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95e41-107">You can enable your users tooautomatically get signed-on tooMaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="95e41-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="95e41-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="95e41-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="95e41-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95e41-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="95e41-110">Prerequisites</span></span>

<span data-ttu-id="95e41-111">tooconfigure integração do AD do Azure com MaxxPoint, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="95e41-111">tooconfigure Azure AD integration with MaxxPoint, you need hello following items:</span></span>

- <span data-ttu-id="95e41-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95e41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="95e41-113">Uma assinatura habilitada para logon único do MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="95e41-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="95e41-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="95e41-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="95e41-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="95e41-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="95e41-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="95e41-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="95e41-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95e41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95e41-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="95e41-118">Scenario description</span></span>
<span data-ttu-id="95e41-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="95e41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95e41-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="95e41-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95e41-121">Adicionando MaxxPoint da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="95e41-121">Adding MaxxPoint from hello gallery</span></span>
2. <span data-ttu-id="95e41-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95e41-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-hello-gallery"></a><span data-ttu-id="95e41-123">Adicionando MaxxPoint da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="95e41-123">Adding MaxxPoint from hello gallery</span></span>
<span data-ttu-id="95e41-124">integração de saudação tooconfigure de MaxxPoint no AD do Azure, você precisa tooadd MaxxPoint da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="95e41-124">tooconfigure hello integration of MaxxPoint into Azure AD, you need tooadd MaxxPoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="95e41-125">**tooadd MaxxPoint da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95e41-125">**tooadd MaxxPoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="95e41-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="95e41-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="95e41-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="95e41-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="95e41-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="95e41-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="95e41-131">Clique em **novo aplicativo** botão na parte superior de saudação do novo aplicativo do diálogo tooadd.</span><span class="sxs-lookup"><span data-stu-id="95e41-131">Click **New application** button on hello top of dialog tooadd new application.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="95e41-133">Na caixa de pesquisa hello, digite **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="95e41-133">In hello search box, type **MaxxPoint**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="95e41-135">No painel de resultados de saudação, selecione **MaxxPoint**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="95e41-135">In hello results panel, select **MaxxPoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="95e41-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95e41-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="95e41-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o MaxxPoint com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="95e41-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="95e41-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em MaxxPoint é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="95e41-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MaxxPoint is tooa user in Azure AD.</span></span> <span data-ttu-id="95e41-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em MaxxPoint precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="95e41-140">In other words, a link relationship between an Azure AD user and hello related user in MaxxPoint needs toobe established.</span></span>

<span data-ttu-id="95e41-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="95e41-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in MaxxPoint.</span></span>

<span data-ttu-id="95e41-142">tooconfigure e teste de logon único do AD do Azure com MaxxPoint, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="95e41-142">tooconfigure and test Azure AD single sign-on with MaxxPoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="95e41-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="95e41-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="95e41-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95e41-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="95e41-145">**[Criar um usuário de teste MaxxPoint](#creating-a-maxxpoint-test-user)**  -toohave um equivalente do Britta Simon em MaxxPoint é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="95e41-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - toohave a counterpart of Britta Simon in MaxxPoint that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="95e41-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="95e41-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="95e41-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="95e41-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="95e41-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="95e41-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="95e41-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="95e41-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="95e41-150">**tooconfigure AD do Azure-logon único com MaxxPoint, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95e41-150">**tooconfigure Azure AD single sign-on with MaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="95e41-151">Em Olá portal do Azure, Olá **MaxxPoint** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="95e41-151">In hello Azure portal, on hello **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="95e41-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="95e41-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="95e41-155">Em Olá **MaxxPoint domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**, não precisa tooperform todas as etapas.</span><span class="sxs-lookup"><span data-stu-id="95e41-155">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, no need tooperform any steps.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="95e41-157">Em Olá **MaxxPoint domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95e41-157">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="95e41-159">a.</span><span class="sxs-lookup"><span data-stu-id="95e41-159">a.</span></span> <span data-ttu-id="95e41-160">Clique na opção **Mostrar configurações avançadas de URL**</span><span class="sxs-lookup"><span data-stu-id="95e41-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="95e41-161">b.</span><span class="sxs-lookup"><span data-stu-id="95e41-161">b.</span></span> <span data-ttu-id="95e41-162">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="95e41-162">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="95e41-163">Observe que isso não é um valor real hello.</span><span class="sxs-lookup"><span data-stu-id="95e41-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="95e41-164">Você tem tooupdate esse valor com hello real URL de logon.</span><span class="sxs-lookup"><span data-stu-id="95e41-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="95e41-165">Chamar team MaxxPoint **888-728-0950** tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="95e41-165">Call MaxxPoint team on **888-728-0950** tooget this value.</span></span>

5. <span data-ttu-id="95e41-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="95e41-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="95e41-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="95e41-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="95e41-170">tooget SSO configurado para o seu aplicativo, chame a equipe de suporte MaxxPoint em **888-728-0950** e vai ajudá-lo ainda mais em como tooprovide-los Olá baixadas **Metadata XML** arquivo.</span><span class="sxs-lookup"><span data-stu-id="95e41-170">tooget SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how tooprovide them hello downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="95e41-171">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="95e41-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="95e41-172">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="95e41-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="95e41-173">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="95e41-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="95e41-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95e41-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="95e41-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="95e41-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="95e41-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95e41-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="95e41-178">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="95e41-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="95e41-180">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="95e41-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="95e41-182">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95e41-182">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="95e41-184">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95e41-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="95e41-186">a.</span><span class="sxs-lookup"><span data-stu-id="95e41-186">a.</span></span> <span data-ttu-id="95e41-187">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="95e41-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="95e41-188">b.</span><span class="sxs-lookup"><span data-stu-id="95e41-188">b.</span></span> <span data-ttu-id="95e41-189">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="95e41-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="95e41-190">c.</span><span class="sxs-lookup"><span data-stu-id="95e41-190">c.</span></span> <span data-ttu-id="95e41-191">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="95e41-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="95e41-192">d.</span><span class="sxs-lookup"><span data-stu-id="95e41-192">d.</span></span> <span data-ttu-id="95e41-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="95e41-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="95e41-194">Criar um usuário de teste do MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="95e41-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="95e41-195">Nesta seção, você criará uma usuária chamada Brenda Fernandes no MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="95e41-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="95e41-196">Entre em contato com a equipe de suporte MaxxPoint em **888-728-0950** tooadd usuários Olá Olá MaxxPoint aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95e41-196">Please call MaxxPoint support team on **888-728-0950** tooadd hello users in hello MaxxPoint application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="95e41-197">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95e41-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="95e41-198">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooMaxxPoint seu acesso.</span><span class="sxs-lookup"><span data-stu-id="95e41-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooMaxxPoint.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="95e41-200">**tooassign Britta Simon tooMaxxPoint, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95e41-200">**tooassign Britta Simon tooMaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="95e41-201">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="95e41-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="95e41-203">Na lista de aplicativos hello, selecione **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="95e41-203">In hello applications list, select **MaxxPoint**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="95e41-205">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="95e41-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="95e41-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="95e41-207">Click **Add** button.</span></span> <span data-ttu-id="95e41-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95e41-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="95e41-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="95e41-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="95e41-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95e41-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="95e41-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95e41-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="95e41-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="95e41-213">Testing single sign-on</span></span>

<span data-ttu-id="95e41-214">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="95e41-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="95e41-215">Quando você clica em bloco MaxxPoint Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour MaxxPoint aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95e41-215">When you click hello MaxxPoint tile in hello Access Panel, you should get automatically signed-on tooyour MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="95e41-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="95e41-216">Additional resources</span></span>

* [<span data-ttu-id="95e41-217">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="95e41-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95e41-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="95e41-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png