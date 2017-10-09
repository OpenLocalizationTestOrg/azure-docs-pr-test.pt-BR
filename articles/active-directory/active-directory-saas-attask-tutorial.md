---
title: "Tutorial: Integração do Active Directory do Azure com @Task| Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="daef7-103">Tutorial: Integração do Active Directory do Azure com @Task</span><span class="sxs-lookup"><span data-stu-id="daef7-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="daef7-104">Olá objetivo deste tutorial é tooshow você como toointegrate @Task com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="daef7-104">hello objective of this tutorial is tooshow you how toointegrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="daef7-105">Integrando @Task com o Azure AD fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="daef7-105">Integrating @Task with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="daef7-106">Você pode controlar no AD do Azure que tenha acessotoo@Task</span><span class="sxs-lookup"><span data-stu-id="daef7-106">You can control in Azure AD who has access too@Task</span></span>
* <span data-ttu-id="daef7-107">Você pode permitir que os usuários tooautomatically obter conectado too@Task (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="daef7-107">You can enable your users tooautomatically get signed-on too@Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="daef7-108">Você pode gerenciar suas contas em um local central - Olá Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="daef7-108">You can manage your accounts in one central location - hello Azure classic Portal</span></span>

<span data-ttu-id="daef7-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="daef7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daef7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="daef7-110">Prerequisites</span></span>
<span data-ttu-id="daef7-111">integração tooconfigure AD do Azure com @Task, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="daef7-111">tooconfigure Azure AD integration with @Task, you need hello following items:</span></span>

* <span data-ttu-id="daef7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="daef7-112">An Azure AD subscription</span></span>
* <span data-ttu-id="daef7-113">Uma assinatura habilitada para logon único @Task</span><span class="sxs-lookup"><span data-stu-id="daef7-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="daef7-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="daef7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="daef7-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="daef7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="daef7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="daef7-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="daef7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="daef7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="daef7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="daef7-118">Scenario Description</span></span>
<span data-ttu-id="daef7-119">Olá objetivo deste tutorial é tooenable tootest logon único do AD do Azure em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="daef7-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="daef7-120">cenário de saudação descrito neste tutorial consiste em três principais blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="daef7-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="daef7-121">Adicionando @Task da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="daef7-121">Adding @Task from hello gallery</span></span> 
2. <span data-ttu-id="daef7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="daef7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-hello-gallery"></a><span data-ttu-id="daef7-123">Adicionando @Task da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="daef7-123">Adding @Task from hello gallery</span></span>
<span data-ttu-id="daef7-124">integração de saudação tooconfigure do @Task no AD do Azure, você precisa tooadd @Task da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="daef7-124">tooconfigure hello integration of @Task into Azure AD, you need tooadd @Task from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="daef7-125">**tooadd @Task da Galeria hello, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="daef7-125">**tooadd @Task from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="daef7-126">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="daef7-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="daef7-128">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="daef7-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="daef7-129">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="daef7-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicativos][2] 
4. <span data-ttu-id="daef7-131">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="daef7-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicativos][3] 
5. <span data-ttu-id="daef7-133">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="daef7-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicativos][4] 
6. <span data-ttu-id="daef7-135">Na caixa de pesquisa hello, digite  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="daef7-135">In hello search box, type **@Task**.</span></span>
   
    ![Aplicativos][5] 
7. <span data-ttu-id="daef7-137">No painel de resultados de saudação, selecione  **@Task** e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="daef7-137">In hello results pane, select **@Task**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Aplicativos][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="daef7-139">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="daef7-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="daef7-140">Olá, o objetivo desta seção é tooshow você como um único teste AD do Azure e tooconfigure logon com @Task com base em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="daef7-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="daef7-141">Para toowork de logon único, AD do Azure precisa tooknow que usuário de contraparte Olá no @Task tooan usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="daef7-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in @Task tooan user in Azure AD is.</span></span> <span data-ttu-id="daef7-142">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em @Task precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="daef7-142">In other words, a link relationship between an Azure AD user and hello related user in @Task needs toobe established.</span></span>   
<span data-ttu-id="daef7-143">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** em @Task.</span><span class="sxs-lookup"><span data-stu-id="daef7-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in @Task.</span></span>

<span data-ttu-id="daef7-144">teste do AD do Azure e tooconfigure o logon único com @Task, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="daef7-144">tooconfigure and test Azure AD single sign-on with @Task, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="daef7-145">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="daef7-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="daef7-146">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="daef7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="daef7-147">**[Criando um @Tasktest usuário](#creating-a-halogen-software-test-user)**  -toohave a contraparte de Britta Simon em @Taskthat é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="daef7-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in @Taskthat is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="daef7-148">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="daef7-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="daef7-149">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="daef7-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="daef7-150">Configuração do logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="daef7-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="daef7-151">Olá objetivo desta seção é tooenable AD do Azure-logon único no hello portal clássico do Azure e tooconfigure logon único no seu @Task aplicativo.</span><span class="sxs-lookup"><span data-stu-id="daef7-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your @Task application.</span></span>

<span data-ttu-id="daef7-152">**tooconfigure logon único do AD do Azure com @Task, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="daef7-152">**tooconfigure Azure AD single sign-on with @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="daef7-153">Em Olá portal clássico do Azure, em Olá  **@Task**  página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**  caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="daef7-153">In hello Azure classic portal, on hello **@Task** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar Logon Único][6] 
2. <span data-ttu-id="daef7-155">Em Olá **como você gostaria que os usuários toosign em too@Task**  página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="daef7-155">On hello **How would you like users toosign on too@Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][7] 
3. <span data-ttu-id="daef7-157">Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="daef7-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Definir configurações de aplicativo][8] 
   
     <span data-ttu-id="daef7-159">a.</span><span class="sxs-lookup"><span data-stu-id="daef7-159">a.</span></span> <span data-ttu-id="daef7-160">Em Olá **URL de logon** caixa de texto, digite a URL Olá usada por seu usuários em toosign tooyour @Task aplicativo (por exemplo:*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="daef7-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="daef7-161">b.</span><span class="sxs-lookup"><span data-stu-id="daef7-161">b.</span></span> <span data-ttu-id="daef7-162">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="daef7-162">Click **Next**.</span></span>
4. <span data-ttu-id="daef7-163">Em Olá **configurar logon único no @Task**  , clique em **baixar metadados**, salvar o arquivo de metadados de saudação localmente no seu computador e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="daef7-163">On hello **Configure single sign-on at @Task** page, click **Download metadata**, save hello metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![O que é o Azure AD Connect][9] 
5. <span data-ttu-id="daef7-165">Logon tooyour @Task site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="daef7-165">Sign-on tooyour @Task company site as administrator.</span></span>
6. <span data-ttu-id="daef7-166">Vá muito**logon único na configuração**.</span><span class="sxs-lookup"><span data-stu-id="daef7-166">Go too**Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="daef7-167">Em Olá **Single Sign-On** caixa de diálogo, executar Olá etapas</span><span class="sxs-lookup"><span data-stu-id="daef7-167">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
   
    ![Configurar Logon Único][23]
   
    <span data-ttu-id="daef7-169">a.</span><span class="sxs-lookup"><span data-stu-id="daef7-169">a.</span></span> <span data-ttu-id="daef7-170">Como **Tipo**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="daef7-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="daef7-171">b.</span><span class="sxs-lookup"><span data-stu-id="daef7-171">b.</span></span> <span data-ttu-id="daef7-172">Selecione **ID do Provedor de Serviços**.</span><span class="sxs-lookup"><span data-stu-id="daef7-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="daef7-173">c.</span><span class="sxs-lookup"><span data-stu-id="daef7-173">c.</span></span> <span data-ttu-id="daef7-174">No hello portal clássico do Azure, copie Olá **URL de logon remoto**e, em seguida, cole-Olá **URL de logon do Portal** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="daef7-174">On hello Azure classic portal, copy hello **Remote Login URL**, and then paste it into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="daef7-175">d.</span><span class="sxs-lookup"><span data-stu-id="daef7-175">d.</span></span> <span data-ttu-id="daef7-176">No hello portal clássico do Azure, copie Olá **URL do serviço de logon único**e, em seguida, cole-Olá **URL de logout** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="daef7-176">On hello Azure classic portal, copy hello **Single Sign-Out Service URL**, and then paste it into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="daef7-177">e.</span><span class="sxs-lookup"><span data-stu-id="daef7-177">e.</span></span> <span data-ttu-id="daef7-178">No hello portal clássico do Azure, copie Olá **alterar a URL da senha**e, em seguida, cole-Olá **alterar a URL da senha** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="daef7-178">On hello Azure classic portal, copy hello **Change Password URL**, and then paste it into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="daef7-179">f.</span><span class="sxs-lookup"><span data-stu-id="daef7-179">f.</span></span> <span data-ttu-id="daef7-180">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="daef7-180">Click **Save**.</span></span>
8. <span data-ttu-id="daef7-181">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="daef7-181">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![O que é o Azure AD Connect][10]
9. <span data-ttu-id="daef7-183">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="daef7-183">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![O que é o Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="daef7-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="daef7-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="daef7-186">Olá objetivo desta seção é toocreate um usuário de teste no hello portal clássico do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="daef7-186">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="daef7-188">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="daef7-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="daef7-189">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="daef7-189">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="daef7-191">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="daef7-191">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="daef7-192">lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="daef7-192">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="daef7-194">Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="daef7-194">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="daef7-196">Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="daef7-196">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="daef7-198">a.</span><span class="sxs-lookup"><span data-stu-id="daef7-198">a.</span></span> <span data-ttu-id="daef7-199">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="daef7-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="daef7-200">b.</span><span class="sxs-lookup"><span data-stu-id="daef7-200">b.</span></span> <span data-ttu-id="daef7-201">Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="daef7-201">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="daef7-202">c.</span><span class="sxs-lookup"><span data-stu-id="daef7-202">c.</span></span> <span data-ttu-id="daef7-203">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="daef7-203">Click **Next**.</span></span>
6. <span data-ttu-id="daef7-204">Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="daef7-204">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="daef7-206">a.</span><span class="sxs-lookup"><span data-stu-id="daef7-206">a.</span></span> <span data-ttu-id="daef7-207">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="daef7-207">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="daef7-208">b.</span><span class="sxs-lookup"><span data-stu-id="daef7-208">b.</span></span> <span data-ttu-id="daef7-209">Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="daef7-209">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="daef7-210">c.</span><span class="sxs-lookup"><span data-stu-id="daef7-210">c.</span></span> <span data-ttu-id="daef7-211">Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="daef7-211">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="daef7-212">d.</span><span class="sxs-lookup"><span data-stu-id="daef7-212">d.</span></span> <span data-ttu-id="daef7-213">Em Olá **função** lista, selecione **usuário**.</span><span class="sxs-lookup"><span data-stu-id="daef7-213">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="daef7-214">e.</span><span class="sxs-lookup"><span data-stu-id="daef7-214">e.</span></span> <span data-ttu-id="daef7-215">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="daef7-215">Click **Next**.</span></span>

7. <span data-ttu-id="daef7-216">Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="daef7-216">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="daef7-218">Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="daef7-218">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="daef7-220">a.</span><span class="sxs-lookup"><span data-stu-id="daef7-220">a.</span></span> <span data-ttu-id="daef7-221">Anote o valor Olá Olá **nova senha**.</span><span class="sxs-lookup"><span data-stu-id="daef7-221">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="daef7-222">b.</span><span class="sxs-lookup"><span data-stu-id="daef7-222">b.</span></span> <span data-ttu-id="daef7-223">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="daef7-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="daef7-224">Criando um usuário de teste de @Task</span><span class="sxs-lookup"><span data-stu-id="daef7-224">Creating an @Task test user</span></span>
<span data-ttu-id="daef7-225">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no @Task.</span><span class="sxs-lookup"><span data-stu-id="daef7-225">hello objective of this section is toocreate a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="daef7-226">**toocreate um usuário chamado Britta Simon no @Task, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="daef7-226">**toocreate a user called Britta Simon in @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="daef7-227">Logon tooyour @Task site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="daef7-227">Sign on tooyour @Task company site as administrator.</span></span>
2. <span data-ttu-id="daef7-228">No menu de saudação na parte superior de saudação, clique em **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="daef7-228">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="daef7-229">Clique em **Nova Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="daef7-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="daef7-230">Na caixa de diálogo de nova pessoa hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="daef7-230">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Criar um usuário de teste de @Task][21] 
   
    <span data-ttu-id="daef7-232">a.</span><span class="sxs-lookup"><span data-stu-id="daef7-232">a.</span></span> <span data-ttu-id="daef7-233">Em Olá **nome** caixa de texto, digite "Britta".</span><span class="sxs-lookup"><span data-stu-id="daef7-233">In hello **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="daef7-234">b.</span><span class="sxs-lookup"><span data-stu-id="daef7-234">b.</span></span> <span data-ttu-id="daef7-235">Em Olá **Sobrenome** caixa de texto, digite "Simon".</span><span class="sxs-lookup"><span data-stu-id="daef7-235">In hello **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="daef7-236">c.</span><span class="sxs-lookup"><span data-stu-id="daef7-236">c.</span></span> <span data-ttu-id="daef7-237">Em Olá **endereço de Email** caixa de texto, digite o endereço de email Britta Simon no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="daef7-237">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="daef7-238">d.</span><span class="sxs-lookup"><span data-stu-id="daef7-238">d.</span></span> <span data-ttu-id="daef7-239">Clique em **Adicionar Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="daef7-239">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="daef7-240">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="daef7-240">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="daef7-241">Olá objetivo desta seção é tooenabling Britta Simon toouse logon único do Azure, concedendo o acesso too@Task.</span><span class="sxs-lookup"><span data-stu-id="daef7-241">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access too@Task.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="daef7-243">**tooassign Britta Simon too@Task, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="daef7-243">**tooassign Britta Simon too@Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="daef7-244">No hello Azure portal clássico, exibição de aplicativos tooopen hello, no modo de exibição de diretório hello, clique em **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="daef7-244">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Atribuir usuário][201] 
2. <span data-ttu-id="daef7-246">Na lista de aplicativos hello, selecione  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="daef7-246">In hello applications list, select **@Task**.</span></span>
   
    ![Atribuir usuário][202] 
3. <span data-ttu-id="daef7-248">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="daef7-248">In hello menu on hello top, click **Users**.</span></span>
   
    ![Atribuir usuário][203] 
4. <span data-ttu-id="daef7-250">Na lista de usuários hello, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="daef7-250">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="daef7-251">Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="daef7-251">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="daef7-253">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="daef7-253">Testing Single Sign-On</span></span>
<span data-ttu-id="daef7-254">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="daef7-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="daef7-255">Quando você clica em Olá @Task Olá de bloco no painel de acesso, você deve obter automaticamente assinado em tooyour @Task aplicativo.</span><span class="sxs-lookup"><span data-stu-id="daef7-255">When you click hello @Task tile in hello Access Panel, you should get automatically signed-on tooyour @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="daef7-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="daef7-256">Additional Resources</span></span>
* [<span data-ttu-id="daef7-257">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="daef7-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="daef7-258">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="daef7-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






