---
title: "Tutorial: Integração do Azure Active Directory com o SciQuest Spend Director | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SciQuest diretor de gastos."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="83f86-103">Tutorial: Integração do Active Directory do Azure com o SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="83f86-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="83f86-104">Olá objetivo deste tutorial é tooshow você como toointegrate SciQuest diretor de gastos no Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="83f86-104">hello objective of this tutorial is tooshow you how toointegrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="83f86-105">Integrando SciQuest diretor de gastos do Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="83f86-105">Integrating SciQuest Spend Director with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="83f86-106">Você pode controlar no AD do Azure que tenha acesso tooSciQuest diretor de gastos</span><span class="sxs-lookup"><span data-stu-id="83f86-106">You can control in Azure AD who has access tooSciQuest Spend Director</span></span> 
* <span data-ttu-id="83f86-107">Você pode habilitar seu usuários tooautomatically get conectado tooSciQuest diretor de gastos (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83f86-107">You can enable your users tooautomatically get signed-on tooSciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="83f86-108">Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="83f86-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="83f86-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83f86-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83f86-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="83f86-110">Prerequisites</span></span>
<span data-ttu-id="83f86-111">tooconfigure integração do AD do Azure com o Diretor de gastar SciQuest, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="83f86-111">tooconfigure Azure AD integration with SciQuest Spend Director, you need hello following items:</span></span>

* <span data-ttu-id="83f86-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83f86-112">An Azure AD subscription</span></span>
* <span data-ttu-id="83f86-113">Uma assinatura do SciQuest Spend Director com o logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="83f86-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83f86-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="83f86-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="83f86-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="83f86-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="83f86-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="83f86-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="83f86-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83f86-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="83f86-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="83f86-118">Scenario Description</span></span>
<span data-ttu-id="83f86-119">Olá objetivo deste tutorial é tooenable tootest logon único do AD do Azure em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="83f86-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="83f86-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="83f86-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83f86-121">Adicionando SciQuest gastar Diretor da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="83f86-121">Adding SciQuest Spend Director from hello gallery</span></span> 
2. <span data-ttu-id="83f86-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83f86-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a><span data-ttu-id="83f86-123">Adicionando SciQuest gastar Diretor da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="83f86-123">Adding SciQuest Spend Director from hello gallery</span></span>
<span data-ttu-id="83f86-124">integração de saudação tooconfigure do SciQuest diretor de gastos no AD do Azure, você precisa tooadd SciQuest diretor de gastar na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="83f86-124">tooconfigure hello integration of SciQuest Spend Director into Azure AD, you need tooadd SciQuest Spend Director from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="83f86-125">**tooadd SciQuest diretor de gastos da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="83f86-125">**tooadd SciQuest Spend Director from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="83f86-126">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83f86-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="83f86-128">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="83f86-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="83f86-129">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="83f86-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicativos][2]

4. <span data-ttu-id="83f86-131">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="83f86-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicativos][3]

5. <span data-ttu-id="83f86-133">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="83f86-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicativos][4]

6. <span data-ttu-id="83f86-135">Na caixa de pesquisa hello, digite **sciQuest gastar director**.</span><span class="sxs-lookup"><span data-stu-id="83f86-135">In hello search box, type **sciQuest spend director**.</span></span>
   
    ![Aplicativos][5]

7. <span data-ttu-id="83f86-137">No painel de resultados de saudação, selecione **SciQuest gastar Director**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="83f86-137">In hello results pane, select **SciQuest Spend Director**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Aplicativos][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83f86-139">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83f86-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83f86-140">Olá o objetivo desta seção é tooshow como tooconfigure e teste de logon único do AD do Azure com o Diretor de gastar SciQuest com base em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="83f86-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="83f86-141">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá diretor de gastar SciQuest tooan usuário no AD do Azure é.</span><span class="sxs-lookup"><span data-stu-id="83f86-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SciQuest Spend Director tooan user in Azure AD is.</span></span> <span data-ttu-id="83f86-142">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no SciQuest gastar Director precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="83f86-142">In other words, a link relationship between an Azure AD user and hello related user in SciQuest Spend Director needs toobe established.</span></span>  
<span data-ttu-id="83f86-143">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em SciQuest diretor de gastos.</span><span class="sxs-lookup"><span data-stu-id="83f86-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="83f86-144">tooconfigure e teste de logon único do AD do Azure com o Diretor de gastar SciQuest, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="83f86-144">tooconfigure and test Azure AD single sign-on with SciQuest Spend Director, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="83f86-145">**[Configurando o Azure AD único Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="83f86-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="83f86-146">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83f86-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83f86-147">**[Criando um usuário de teste de diretor de gastar SciQuest](#creating-a-halogen-software-test-user)**  -toohave um equivalente do Britta Simon no Director gastar SciQuest que é a representação toohello vinculado do Azure AD de seus.</span><span class="sxs-lookup"><span data-stu-id="83f86-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in SciQuest Spend Director that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="83f86-148">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="83f86-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83f86-149">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="83f86-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="83f86-150">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="83f86-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="83f86-151">objetivo Olá desta seção é tooenable AD do Azure-logon único no hello portal clássico do Azure e tooconfigure logon único no aplicativo SciQuest diretor de gastos.</span><span class="sxs-lookup"><span data-stu-id="83f86-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="83f86-152">**tooconfigure logon único do AD do Azure com o Diretor de gastar SciQuest, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="83f86-152">**tooconfigure Azure AD single sign-on with SciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="83f86-153">Em Olá portal clássico do Azure, em Olá **SciQuest gastar Director** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="83f86-153">In hello Azure classic portal, on hello **SciQuest Spend Director** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar Logon Único][8]

2. <span data-ttu-id="83f86-155">Em Olá **como você gostaria usuários toosign em tooSciQuest diretor de gastos** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="83f86-155">On hello **How would you like users toosign on tooSciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][9]

3. <span data-ttu-id="83f86-157">Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="83f86-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Definir configurações de aplicativo][10]
   
     <span data-ttu-id="83f86-159">a.</span><span class="sxs-lookup"><span data-stu-id="83f86-159">a.</span></span> <span data-ttu-id="83f86-160">Em Olá **URL de logon** caixa de texto, digite a URL usada pelos seu toosign usuários no aplicativo de diretor de gastar SciQuest tooyour usando saudação padrão a seguir: *https://.* SciQuest.com/.**</span><span class="sxs-lookup"><span data-stu-id="83f86-160">In hello **Sign On URL** textbox, type your URL used by your users toosign on tooyour SciQuest Spend Director application using hello following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="83f86-161">b.</span><span class="sxs-lookup"><span data-stu-id="83f86-161">b.</span></span> <span data-ttu-id="83f86-162">Em Olá **URL de resposta** caixa de texto, Olá tipo mesmo valor que você digitou em Olá **URL de logon** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="83f86-162">In hello **Reply URL** textbox, type hello same value you have typed into hello **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="83f86-163">c.</span><span class="sxs-lookup"><span data-stu-id="83f86-163">c.</span></span> <span data-ttu-id="83f86-164">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="83f86-164">Click **Next**.</span></span>

4. <span data-ttu-id="83f86-165">Em Olá **configurar logon único no diretor de gastar SciQuest** , clique em **baixar metadados**e, em seguida, salve o arquivo de metadados de saudação localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="83f86-165">On hello **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
    ![O que é o Azure AD Connect][11]

5. <span data-ttu-id="83f86-167">Entre em contato com SciQuest tooenable de suporte a esse método de autenticação usando metadados de saudação acima baixado.</span><span class="sxs-lookup"><span data-stu-id="83f86-167">Contact SciQuest support tooenable this authentication method using hello above downloaded metadata.</span></span>

6. <span data-ttu-id="83f86-168">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="83f86-168">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span> 
   
    ![O que é o Azure AD Connect][15]

7. <span data-ttu-id="83f86-170">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="83f86-170">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83f86-171">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83f86-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="83f86-172">Olá objetivo desta seção é toocreate um usuário de teste no hello portal clássico do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83f86-172">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="83f86-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="83f86-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="83f86-174">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83f86-174">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![O que é o Azure AD Connect][100] 

2. <span data-ttu-id="83f86-176">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="83f86-176">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="83f86-177">lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="83f86-177">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![O que é o Azure AD Connect][101] 

4. <span data-ttu-id="83f86-179">Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="83f86-179">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![O que é o Azure AD Connect][102] 

5. <span data-ttu-id="83f86-181">Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="83f86-181">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![O que é o Azure AD Connect][103] 
   
    <span data-ttu-id="83f86-183">a.</span><span class="sxs-lookup"><span data-stu-id="83f86-183">a.</span></span> <span data-ttu-id="83f86-184">Em **Tipo de Usuário**, selecione **Novo usuário na organização**.</span><span class="sxs-lookup"><span data-stu-id="83f86-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="83f86-185">b.</span><span class="sxs-lookup"><span data-stu-id="83f86-185">b.</span></span> <span data-ttu-id="83f86-186">Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83f86-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="83f86-187">c.</span><span class="sxs-lookup"><span data-stu-id="83f86-187">c.</span></span> <span data-ttu-id="83f86-188">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="83f86-188">Click **Next**.</span></span>

6. <span data-ttu-id="83f86-189">Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="83f86-189">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![O que é o Azure AD Connect][104] 
   
    <span data-ttu-id="83f86-191">a.</span><span class="sxs-lookup"><span data-stu-id="83f86-191">a.</span></span> <span data-ttu-id="83f86-192">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="83f86-192">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="83f86-193">b.</span><span class="sxs-lookup"><span data-stu-id="83f86-193">b.</span></span> <span data-ttu-id="83f86-194">Em Olá **Sobrenome** txtbox, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="83f86-194">In hello **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="83f86-195">c.</span><span class="sxs-lookup"><span data-stu-id="83f86-195">c.</span></span> <span data-ttu-id="83f86-196">Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="83f86-196">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="83f86-197">d.</span><span class="sxs-lookup"><span data-stu-id="83f86-197">d.</span></span> <span data-ttu-id="83f86-198">Em Olá **função** lista, selecione **usuário**.</span><span class="sxs-lookup"><span data-stu-id="83f86-198">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="83f86-199">e.</span><span class="sxs-lookup"><span data-stu-id="83f86-199">e.</span></span> <span data-ttu-id="83f86-200">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="83f86-200">Click **Next**.</span></span>

7. <span data-ttu-id="83f86-201">Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="83f86-201">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![O que é o Azure AD Connect][105]  

8. <span data-ttu-id="83f86-203">Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="83f86-203">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![O que é o Azure AD Connect][106]   
   
    <span data-ttu-id="83f86-205">a.</span><span class="sxs-lookup"><span data-stu-id="83f86-205">a.</span></span> <span data-ttu-id="83f86-206">Anote o valor Olá Olá **nova senha**.</span><span class="sxs-lookup"><span data-stu-id="83f86-206">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="83f86-207">b.</span><span class="sxs-lookup"><span data-stu-id="83f86-207">b.</span></span> <span data-ttu-id="83f86-208">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="83f86-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="83f86-209">Criação de um usuário de teste do SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="83f86-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="83f86-210">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no SciQuest diretor de gastos.</span><span class="sxs-lookup"><span data-stu-id="83f86-210">hello objective of this section is toocreate a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="83f86-211">Necessário toocontact sua equipe de suporte SciQuest diretor de gastos e fornecer detalhes de saudação sobre seu tooget de conta de teste criado por ele.</span><span class="sxs-lookup"><span data-stu-id="83f86-211">You need toocontact your SciQuest Spend Director support team and provide them with hello details about your test account tooget it created.</span></span>

<span data-ttu-id="83f86-212">Como alternativa, você também pode usar o provisionamento just-in-time, um recurso de logon único com suporte do SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="83f86-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="83f86-213">Se o provisionamento Just-In-Time estiver habilitado, os usuários serão automaticamente criados pelo SciQuest Spend Director durante uma tentativa de logon único, caso não existam.</span><span class="sxs-lookup"><span data-stu-id="83f86-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="83f86-214">Este recurso elimina a necessidade de saudação toomanually criar equivalente de logon único de usuários.</span><span class="sxs-lookup"><span data-stu-id="83f86-214">This feature eliminates hello need toomanually create single sign-on counterpart users.</span></span>

<span data-ttu-id="83f86-215">provisionamento do tooget just-in-time habilitada, é necessário toocontact estiver sua equipe de suporte SciQuest diretor de gastos.</span><span class="sxs-lookup"><span data-stu-id="83f86-215">tooget just-in-time provisioning enabled, you need toocontact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="83f86-216">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83f86-216">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="83f86-217">Olá objetivo desta seção é tooenabling Britta Simon toouse logon único do Azure concedendo tooSciQuest seu acesso diretor de gastos.</span><span class="sxs-lookup"><span data-stu-id="83f86-217">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSciQuest Spend Director.</span></span>

![O que é o Azure AD Connect][200]

<span data-ttu-id="83f86-219">**tooassign Britta Simon tooSciQuest diretor de gastos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="83f86-219">**tooassign Britta Simon tooSciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="83f86-220">No hello Azure portal clássico, exibição de aplicativos tooopen hello, no modo de exibição de diretório hello, clique em **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="83f86-220">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![O que é o Azure AD Connect][201]

2. <span data-ttu-id="83f86-222">Na lista de aplicativos hello, selecione **SciQuest gastar Director**.</span><span class="sxs-lookup"><span data-stu-id="83f86-222">In hello applications list, select **SciQuest Spend Director**.</span></span>
   
    ![O que é o Azure AD Connect][202]

3. <span data-ttu-id="83f86-224">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="83f86-224">In hello menu on hello top, click **Users**.</span></span>
   
    ![O que é o Azure AD Connect][203]

4. <span data-ttu-id="83f86-226">Na lista de usuários hello, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="83f86-226">In hello Users list, select **Britta Simon**.</span></span>
   
    ![O que é o Azure AD Connect][204]

5. <span data-ttu-id="83f86-228">Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="83f86-228">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![O que é o Azure AD Connect][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="83f86-230">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="83f86-230">Testing Single Sign-On</span></span>
<span data-ttu-id="83f86-231">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="83f86-231">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="83f86-232">Quando você clica em bloco SciQuest gastar Director Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour SciQuest gastar Director aplicativo.</span><span class="sxs-lookup"><span data-stu-id="83f86-232">When you click hello SciQuest Spend Director tile in hello Access Panel, you should get automatically signed-on tooyour SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="83f86-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="83f86-233">Additional Resources</span></span>
* [<span data-ttu-id="83f86-234">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="83f86-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83f86-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83f86-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

