---
title: "Tutorial: integração do Azure Active Directory com o Halosys | Microsoft Docs"
description: "Saiba como toouse Halosys com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="25827-103">Tutorial: integração do Azure Active Directory com o Halosys</span><span class="sxs-lookup"><span data-stu-id="25827-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="25827-104">Neste tutorial, você aprenderá como toointegrate Halosys com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="25827-104">In this tutorial, you learn how toointegrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25827-105">Integrando Halosys com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="25827-105">Integrating Halosys with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="25827-106">Você pode controlar no AD do Azure que tenha acesso tooHalosys</span><span class="sxs-lookup"><span data-stu-id="25827-106">You can control in Azure AD who has access tooHalosys</span></span>
- <span data-ttu-id="25827-107">Você pode habilitar seus usuários tooautomatically get conectado tooHalosys (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="25827-107">You can enable your users tooautomatically get signed-on tooHalosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="25827-108">Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="25827-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="25827-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="25827-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25827-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="25827-110">Prerequisites</span></span>

<span data-ttu-id="25827-111">tooconfigure integração do AD do Azure com Halosys, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="25827-111">tooconfigure Azure AD integration with Halosys, you need hello following items:</span></span>

- <span data-ttu-id="25827-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="25827-112">An Azure AD subscription</span></span>
- <span data-ttu-id="25827-113">Uma assinatura do Halosys habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="25827-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="25827-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="25827-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="25827-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="25827-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="25827-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="25827-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="25827-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25827-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="25827-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="25827-118">Scenario description</span></span>
<span data-ttu-id="25827-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="25827-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="25827-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="25827-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25827-121">Adicionando Halosys da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="25827-121">Adding Halosys from hello gallery</span></span>
2. <span data-ttu-id="25827-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="25827-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-hello-gallery"></a><span data-ttu-id="25827-123">Adicionando Halosys da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="25827-123">Adding Halosys from hello gallery</span></span>
<span data-ttu-id="25827-124">integração de saudação tooconfigure de Halosys no AD do Azure, você precisa tooadd Halosys da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="25827-124">tooconfigure hello integration of Halosys into Azure AD, you need tooadd Halosys from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="25827-125">**tooadd Halosys da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="25827-125">**tooadd Halosys from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="25827-126">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="25827-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="25827-128">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="25827-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="25827-129">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="25827-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Aplicativos][2]

4. <span data-ttu-id="25827-131">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="25827-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Aplicativos][3]

5. <span data-ttu-id="25827-133">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="25827-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Aplicativos][4]

6. <span data-ttu-id="25827-135">Na caixa de pesquisa hello, digite **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="25827-135">In hello search box, type **Halosys**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="25827-137">No painel de resultados de saudação, selecione **Halosys**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="25827-137">In hello results pane, select **Halosys**, and then click **Complete** tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="25827-139">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="25827-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="25827-140">Nesta seção, você configurará e testará o logon único do Azure AD com o Halosys, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="25827-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="25827-141">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Halosys é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="25827-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halosys is tooa user in Azure AD.</span></span> <span data-ttu-id="25827-142">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Halosys precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="25827-142">In other words, a link relationship between an Azure AD user and hello related user in Halosys needs toobe established.</span></span>

<span data-ttu-id="25827-143">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Halosys.</span><span class="sxs-lookup"><span data-stu-id="25827-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Halosys.</span></span>

<span data-ttu-id="25827-144">tooconfigure e teste de logon único do AD do Azure com Halosys, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="25827-144">tooconfigure and test Azure AD single sign-on with Halosys, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="25827-145">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="25827-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="25827-146">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25827-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="25827-147">**[Criar um usuário de teste Halosys](#creating-a-halosys-test-user)**  -toohave um equivalente do Britta Simon em Halosys é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="25827-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - toohave a counterpart of Britta Simon in Halosys that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="25827-148">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="25827-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="25827-149">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="25827-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="25827-150">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="25827-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="25827-151">Nesta seção, habilitar o AD do Azure-logon único no portal clássico do hello e configurar o logon único no aplicativo Halosys.</span><span class="sxs-lookup"><span data-stu-id="25827-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="25827-152">**tooconfigure AD do Azure-logon único com Halosys, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="25827-152">**tooconfigure Azure AD single sign-on with Halosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="25827-153">No portal clássico hello, em Olá **Halosys** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="25827-153">In hello classic portal, on hello **Halosys** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurar Logon Único][6] 

2. <span data-ttu-id="25827-155">Em Olá **como você gostaria usuários toosign em tooHalosys** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25827-155">On hello **How would you like users toosign on tooHalosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="25827-157">Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="25827-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="25827-159">a.</span><span class="sxs-lookup"><span data-stu-id="25827-159">a.</span></span> <span data-ttu-id="25827-160">Em Olá **URL de logon** caixa de texto, digite a URL do hello usada pelo seu aplicativo de Halosys tooyour toosign em usuários usando o saudação padrão a seguir: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="25827-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Halosys application using hello following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="25827-161">Olá b.In **URL de identificador** caixa de texto, digite a URL de saudação em saudação padrão a seguir: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="25827-161">b.In hello **Identifier URL** textbox, type hello URL in hello following pattern: `https://<company-name>.Halosys.com`.</span></span> 
         
4. <span data-ttu-id="25827-162">Em Olá **configurar logon único no Halosys** , clique em **baixar metadados**e, em seguida, salve o arquivo de saudação em seu computador:</span><span class="sxs-lookup"><span data-stu-id="25827-162">On hello **Configure single sign-on at Halosys** page, click **Download metadata**, and then save hello file on your computer:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="25827-164">tooget SSO configurado para o seu aplicativo, entre em contato com a equipe de suporte Halosys e fornecê-los com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="25827-164">tooget SSO configured for your application, contact Halosys support team and provide them with hello following:</span></span>

    <span data-ttu-id="25827-165">• Olá baixado **arquivo de metadados**</span><span class="sxs-lookup"><span data-stu-id="25827-165">• hello downloaded **metadata file**</span></span>
    
    <span data-ttu-id="25827-166">• Olá **URL SSO SAML**</span><span class="sxs-lookup"><span data-stu-id="25827-166">• hello **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="25827-167">No portal clássico do hello, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="25827-167">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Logon Único do AD do Azure][10]

7. <span data-ttu-id="25827-169">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="25827-169">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Logon Único do AD do Azure][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="25827-171">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="25827-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="25827-172">Nesta seção, você pode criar um usuário de teste no portal clássico do hello chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25827-172">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>


![Criar um usuário do AD do Azure][20]

<span data-ttu-id="25827-174">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="25827-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="25827-175">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="25827-175">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="25827-177">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="25827-177">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="25827-178">lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="25827-178">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="25827-180">Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="25827-180">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="25827-182">Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir: ![criando um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="25827-182">On hello **Tell us about this user** dialog page, perform hello following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="25827-183">a.</span><span class="sxs-lookup"><span data-stu-id="25827-183">a.</span></span> <span data-ttu-id="25827-184">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="25827-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="25827-185">b.</span><span class="sxs-lookup"><span data-stu-id="25827-185">b.</span></span> <span data-ttu-id="25827-186">Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="25827-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="25827-187">c.</span><span class="sxs-lookup"><span data-stu-id="25827-187">c.</span></span> <span data-ttu-id="25827-188">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="25827-188">Click **Next**.</span></span>

6.  <span data-ttu-id="25827-189">Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir: ![criando um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="25827-189">On hello **User Profile** dialog page, perform hello following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="25827-190">a.</span><span class="sxs-lookup"><span data-stu-id="25827-190">a.</span></span> <span data-ttu-id="25827-191">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="25827-191">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="25827-192">b.</span><span class="sxs-lookup"><span data-stu-id="25827-192">b.</span></span> <span data-ttu-id="25827-193">Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="25827-193">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="25827-194">c.</span><span class="sxs-lookup"><span data-stu-id="25827-194">c.</span></span> <span data-ttu-id="25827-195">Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="25827-195">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="25827-196">d.</span><span class="sxs-lookup"><span data-stu-id="25827-196">d.</span></span> <span data-ttu-id="25827-197">Em Olá **função** lista, selecione **usuário**.</span><span class="sxs-lookup"><span data-stu-id="25827-197">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="25827-198">e.</span><span class="sxs-lookup"><span data-stu-id="25827-198">e.</span></span> <span data-ttu-id="25827-199">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="25827-199">Click **Next**.</span></span>

7. <span data-ttu-id="25827-200">Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="25827-200">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="25827-202">Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="25827-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="25827-204">a.</span><span class="sxs-lookup"><span data-stu-id="25827-204">a.</span></span> <span data-ttu-id="25827-205">Anote o valor Olá Olá **nova senha**.</span><span class="sxs-lookup"><span data-stu-id="25827-205">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="25827-206">b.</span><span class="sxs-lookup"><span data-stu-id="25827-206">b.</span></span> <span data-ttu-id="25827-207">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="25827-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="25827-208">Criando um usuário de teste do Halosys</span><span class="sxs-lookup"><span data-stu-id="25827-208">Creating a Halosys test user</span></span>

<span data-ttu-id="25827-209">Nesta seção, você criará um usuário chamado Brenda Fernandes no Halosys.</span><span class="sxs-lookup"><span data-stu-id="25827-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="25827-210">Trabalhe com Halosys suporte team tooadd Olá usuários na plataforma de Halosys hello.</span><span class="sxs-lookup"><span data-stu-id="25827-210">Please work with Halosys support team tooadd hello users in hello Halosys platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="25827-211">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="25827-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="25827-212">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooHalosys seu acesso.</span><span class="sxs-lookup"><span data-stu-id="25827-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHalosys.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="25827-214">**tooassign Britta Simon tooHalosys, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="25827-214">**tooassign Britta Simon tooHalosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="25827-215">No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="25827-215">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="25827-217">Na lista de aplicativos hello, selecione **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="25827-217">In hello applications list, select **Halosys**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="25827-219">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="25827-219">In hello menu on hello top, click **Users**.</span></span>

    ![Atribuir usuário][203]

4. <span data-ttu-id="25827-221">Na lista de usuários hello, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="25827-221">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="25827-222">Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="25827-222">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Atribuir usuário][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="25827-224">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="25827-224">Testing single sign-on</span></span>

<span data-ttu-id="25827-225">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="25827-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="25827-226">Quando você clica em Olá Halosys bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Halosys aplicativo.</span><span class="sxs-lookup"><span data-stu-id="25827-226">When you click hello Halosys tile in hello Access Panel, you should get automatically signed-on tooyour Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="25827-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="25827-227">Additional resources</span></span>

* [<span data-ttu-id="25827-228">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="25827-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25827-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="25827-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
