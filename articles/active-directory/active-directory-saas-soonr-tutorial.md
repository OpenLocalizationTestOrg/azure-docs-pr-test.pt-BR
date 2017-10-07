---
title: "Tutorial: Integração do Azure Active Directory com o Soonr Workplace | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Soonr no local de trabalho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="74440-103">Tutorial: Integração do Active Directory do Azure com o Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="74440-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="74440-104">Olá objetivo deste tutorial é tooshow você como toointegrate Soonr no local de trabalho com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="74440-104">hello objective of this tutorial is tooshow you how toointegrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="74440-105">Integrando Soonr no local de trabalho com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="74440-105">Integrating Soonr Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="74440-106">Você pode controlar no AD do Azure que tenha acesso tooSoonr no local de trabalho</span><span class="sxs-lookup"><span data-stu-id="74440-106">You can control in Azure AD who has access tooSoonr Workplace</span></span>
- <span data-ttu-id="74440-107">Você pode habilitar seu usuários tooautomatically get conectado tooSoonr no local de trabalho (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74440-107">You can enable your users tooautomatically get signed-on tooSoonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="74440-108">Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="74440-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="74440-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="74440-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74440-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="74440-110">Prerequisites</span></span>

<span data-ttu-id="74440-111">tooconfigure integração do AD do Azure com Soonr no local de trabalho, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="74440-111">tooconfigure Azure AD integration with Soonr Workplace, you need hello following items:</span></span>

- <span data-ttu-id="74440-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74440-112">An Azure AD subscription</span></span>
- <span data-ttu-id="74440-113">Uma assinatura do Soonr Workplace com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="74440-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="74440-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="74440-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="74440-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="74440-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="74440-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="74440-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="74440-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="74440-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="74440-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="74440-118">Scenario description</span></span>
<span data-ttu-id="74440-119">Olá objetivo deste tutorial é tooenable tootest logon único do AD do Azure em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="74440-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="74440-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="74440-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="74440-121">Adicionando Soonr no local de trabalho na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="74440-121">Adding Soonr Workplace from hello gallery</span></span>
2. <span data-ttu-id="74440-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74440-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-hello-gallery"></a><span data-ttu-id="74440-123">Adicionando Soonr no local de trabalho na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="74440-123">Adding Soonr Workplace from hello gallery</span></span>
<span data-ttu-id="74440-124">integração de saudação tooconfigure do local de trabalho Soonr no AD do Azure, você precisa tooadd Soonr no local de trabalho da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="74440-124">tooconfigure hello integration of Soonr Workplace into Azure AD, you need tooadd Soonr Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="74440-125">**tooadd Soonr no local de trabalho na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="74440-125">**tooadd Soonr Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="74440-126">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74440-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="74440-128">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="74440-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="74440-129">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="74440-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Aplicativos][2]

4. <span data-ttu-id="74440-131">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="74440-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Aplicativos][3]

5. <span data-ttu-id="74440-133">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="74440-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
 
    ![Aplicativos][4]

6. <span data-ttu-id="74440-135">Na caixa de pesquisa hello, digite **Soonr trabalho**.</span><span class="sxs-lookup"><span data-stu-id="74440-135">In hello search box, type **Soonr Workplace**.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="74440-137">No painel de resultados de saudação, selecione **Soonr trabalho**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="74440-137">In hello results pane, select **Soonr Workplace**, and then click **Complete** tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="74440-139">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74440-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="74440-140">Olá o objetivo desta seção é tooshow como tooconfigure e teste de logon único do AD do Azure com Soonr de espaço de trabalho com base em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="74440-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="74440-141">Para toowork de logon único, o AD do Azure precisa tooknow é que usuário de contraparte Olá no usuário do local de trabalho Soonr tooan no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="74440-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Soonr Workplace tooan user in Azure AD is.</span></span> <span data-ttu-id="74440-142">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na área de trabalho Soonr precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="74440-142">In other words, a link relationship between an Azure AD user and hello related user in Soonr Workplace needs toobe established.</span></span>  

<span data-ttu-id="74440-143">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na área de trabalho Soonr.</span><span class="sxs-lookup"><span data-stu-id="74440-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="74440-144">tooconfigure e teste de logon único do AD do Azure com Soonr de espaço de trabalho, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="74440-144">tooconfigure and test Azure AD single sign-on with Soonr Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="74440-145">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="74440-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="74440-146">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74440-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="74440-147">**[Criar um usuário de teste do local de trabalho Soonr](#creating-a-soonr-workplace-test-user)**  -toohave um equivalente do Britta Simon na área de trabalho Soonr que é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="74440-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - toohave a counterpart of Britta Simon in Soonr Workplace that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="74440-148">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="74440-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="74440-149">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="74440-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="74440-150">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="74440-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="74440-151">Nesta seção, você habilitar o AD do Azure-logon único no portal clássico do hello e configurar o logon único em seu aplicativo de área de trabalho Soonr.</span><span class="sxs-lookup"><span data-stu-id="74440-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="74440-152">**tooconfigure AD do Azure-logon único com o local de trabalho Soonr execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="74440-152">**tooconfigure Azure AD single sign-on with Soonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="74440-153">Em Olá portal clássico do Azure, em hello **Soonr trabalho** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**  caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="74440-153">In hello Azure classic portal, on hello **Soonr Workplace** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>

    ![Configurar Logon Único][6] 

2. <span data-ttu-id="74440-155">Em Olá **como você gostaria toosign usuários no local de trabalho do tooSoonr** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="74440-155">On hello **How would you like users toosign on tooSoonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="74440-157">Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:.</span><span class="sxs-lookup"><span data-stu-id="74440-157">On hello **Configure App Settings** dialog page, perform hello following steps:.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="74440-159">a.</span><span class="sxs-lookup"><span data-stu-id="74440-159">a.</span></span> <span data-ttu-id="74440-160">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="74440-160">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="74440-161">b.</span><span class="sxs-lookup"><span data-stu-id="74440-161">b.</span></span> <span data-ttu-id="74440-162">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="74440-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="74440-163">Observe que isso não é um valor real hello.</span><span class="sxs-lookup"><span data-stu-id="74440-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="74440-164">Você tem tooupdate esse valor com hello real URL de logon.</span><span class="sxs-lookup"><span data-stu-id="74440-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="74440-165">Entre em contato com tooget de equipe de suporte local de trabalho Soonr esse valor.</span><span class="sxs-lookup"><span data-stu-id="74440-165">Contact Soonr Workplace support team tooget this value.</span></span>

4. <span data-ttu-id="74440-166">Em Olá **configurar logon único no local de trabalho Soonr** , clique em **baixar metadados** e, em seguida, salve o arquivo de saudação em seu computador:</span><span class="sxs-lookup"><span data-stu-id="74440-166">On hello **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save hello file on your computer:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="74440-168">tooget SSO configurado para o seu aplicativo, entre em contato com sua equipe de suporte local de trabalho Soonr e fornecê-los com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="74440-168">tooget SSO configured for your application, contact your Soonr Workplace support team and provide them with hello following:</span></span> 

    <span data-ttu-id="74440-169">• Olá baixado **metadados** arquivo</span><span class="sxs-lookup"><span data-stu-id="74440-169">•  hello downloaded **Metadata** file</span></span>

    <span data-ttu-id="74440-170">• Olá **URL do emissor**</span><span class="sxs-lookup"><span data-stu-id="74440-170">•  hello **Issuer URL**</span></span>

    <span data-ttu-id="74440-171">• Olá **URL SSO SAML**</span><span class="sxs-lookup"><span data-stu-id="74440-171">•  hello **SAML SSO URL**</span></span>

    <span data-ttu-id="74440-172">• Olá **URL do serviço de logon único**</span><span class="sxs-lookup"><span data-stu-id="74440-172">•  hello **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="74440-173">Este aplicativo é substituído por <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask trabalho</a> e você pode consultar <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">isso</a> tutorial para configurar o aplicativo hello com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74440-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring hello application with Azure AD.</span></span>
   
6. <span data-ttu-id="74440-174">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="74440-174">In hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Logon Único do AD do Azure][10]

7. <span data-ttu-id="74440-176">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="74440-176">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Logon Único do AD do Azure][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="74440-178">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74440-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="74440-179">Olá objetivo desta seção é toocreate um usuário de teste no hello portal clássico do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74440-179">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="74440-181">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="74440-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="74440-182">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74440-182">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="74440-184">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="74440-184">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="74440-185">lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="74440-185">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="74440-187">Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="74440-187">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="74440-189">Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="74440-189">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="74440-191">a.</span><span class="sxs-lookup"><span data-stu-id="74440-191">a.</span></span> <span data-ttu-id="74440-192">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="74440-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="74440-193">b.</span><span class="sxs-lookup"><span data-stu-id="74440-193">b.</span></span> <span data-ttu-id="74440-194">Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="74440-194">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="74440-195">c.</span><span class="sxs-lookup"><span data-stu-id="74440-195">c.</span></span> <span data-ttu-id="74440-196">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="74440-196">Click **Next**.</span></span>

6.  <span data-ttu-id="74440-197">Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="74440-197">On hello **User Profile** dialog page, perform hello following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="74440-199">a.</span><span class="sxs-lookup"><span data-stu-id="74440-199">a.</span></span> <span data-ttu-id="74440-200">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="74440-200">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="74440-201">b.</span><span class="sxs-lookup"><span data-stu-id="74440-201">b.</span></span> <span data-ttu-id="74440-202">Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="74440-202">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="74440-203">c.</span><span class="sxs-lookup"><span data-stu-id="74440-203">c.</span></span> <span data-ttu-id="74440-204">Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="74440-204">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="74440-205">d.</span><span class="sxs-lookup"><span data-stu-id="74440-205">d.</span></span> <span data-ttu-id="74440-206">Em Olá **função** lista, selecione **usuário**.</span><span class="sxs-lookup"><span data-stu-id="74440-206">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="74440-207">e.</span><span class="sxs-lookup"><span data-stu-id="74440-207">e.</span></span> <span data-ttu-id="74440-208">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="74440-208">Click **Next**.</span></span>

7. <span data-ttu-id="74440-209">Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="74440-209">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="74440-211">Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="74440-211">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="74440-213">a.</span><span class="sxs-lookup"><span data-stu-id="74440-213">a.</span></span> <span data-ttu-id="74440-214">Anote o valor Olá Olá **nova senha**.</span><span class="sxs-lookup"><span data-stu-id="74440-214">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="74440-215">b.</span><span class="sxs-lookup"><span data-stu-id="74440-215">b.</span></span> <span data-ttu-id="74440-216">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="74440-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="74440-217">Criar um usuário de teste do Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="74440-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="74440-218">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon na área de trabalho Soonr.</span><span class="sxs-lookup"><span data-stu-id="74440-218">hello objective of this section is toocreate a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="74440-219">Trabalhe com toocreate de equipe de suporte local de trabalho Soonr um usuário na plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="74440-219">Please work with Soonr Workplace support team toocreate a user in hello platform.</span></span> <span data-ttu-id="74440-220">Você pode gerar um tíquete de suporte de saudação com Soonr de <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">aqui</a>.</span><span class="sxs-lookup"><span data-stu-id="74440-220">You can raise hello support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="74440-221">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74440-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="74440-222">Olá objetivo desta seção é tooenabling Britta Simon toouse logon único do Azure concedendo tooSoonr seu acesso no local de trabalho.</span><span class="sxs-lookup"><span data-stu-id="74440-222">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSoonr Workplace.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="74440-224">**tooassign Britta Simon tooSoonr no local de trabalho, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="74440-224">**tooassign Britta Simon tooSoonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="74440-225">No hello Azure portal clássico, exibição de aplicativos tooopen hello, no modo de exibição de diretório hello, clique em **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="74440-225">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="74440-227">Na lista de aplicativos hello, selecione **Soonr trabalho**.</span><span class="sxs-lookup"><span data-stu-id="74440-227">In hello applications list, select **Soonr Workplace**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="74440-229">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="74440-229">In hello menu on hello top, click **Users**.</span></span>

    ![Atribuir usuário][203] 

1. <span data-ttu-id="74440-231">Na lista de usuários hello, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="74440-231">In hello Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="74440-232">Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="74440-232">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Atribuir usuário][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="74440-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="74440-234">Testing single sign-on</span></span>

<span data-ttu-id="74440-235">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="74440-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="74440-236">Quando você clica em Olá Soonr no local de trabalho lado a lado no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de área de trabalho Soonr.</span><span class="sxs-lookup"><span data-stu-id="74440-236">When you click hello Soonr Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="74440-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="74440-237">Additional resources</span></span>

* [<span data-ttu-id="74440-238">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="74440-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="74440-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="74440-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
