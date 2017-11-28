---
title: "Tutorial: integração do Azure Active Directory com o Wizergos Productivity Software | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Software de produtividade de Wizergos."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="27b81-103">Tutorial: Integração do Azure Active Directory com o Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="27b81-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="27b81-104">Olá objetivo deste tutorial é tooshow você como toointegrate Wizergos Software de produtividade com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="27b81-104">hello objective of this tutorial is tooshow you how toointegrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27b81-105">Integração de Software de produtividade de Wizergos com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="27b81-105">Integrating Wizergos Productivity Software with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="27b81-106">Você pode controlar no AD do Azure que tenha acesso tooWizergos Software de produtividade</span><span class="sxs-lookup"><span data-stu-id="27b81-106">You can control in Azure AD who has access tooWizergos Productivity Software</span></span>
* <span data-ttu-id="27b81-107">Você pode habilitar seus usuários tooautomatically get conectado tooWizergos Software de produtividade-logon único (SSO) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27b81-107">You can enable your users tooautomatically get signed-on tooWizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="27b81-108">Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="27b81-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="27b81-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="27b81-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27b81-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="27b81-110">Prerequisites</span></span>
<span data-ttu-id="27b81-111">tooconfigure integração do AD do Azure com o Software de produtividade de Wizergos, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="27b81-111">tooconfigure Azure AD integration with Wizergos Productivity Software, you need hello following items:</span></span>

* <span data-ttu-id="27b81-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27b81-112">An Azure AD subscription</span></span>
* <span data-ttu-id="27b81-113">Uma assinatura do Wizergos Productivity Software habilitada para SSO</span><span class="sxs-lookup"><span data-stu-id="27b81-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="27b81-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="27b81-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="27b81-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="27b81-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="27b81-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="27b81-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="27b81-117">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27b81-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27b81-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="27b81-118">Scenario description</span></span>
<span data-ttu-id="27b81-119">Olá objetivo deste tutorial é tooenable você tootest SSO do AD do Azure em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="27b81-119">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="27b81-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="27b81-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27b81-121">Adicionar Software de produtividade de Wizergos da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="27b81-121">Adding Wizergos Productivity Software from hello gallery</span></span>
2. <span data-ttu-id="27b81-122">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b81-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a><span data-ttu-id="27b81-123">Adicionar Software de produtividade de Wizergos da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="27b81-123">Adding Wizergos Productivity Software from hello gallery</span></span>
<span data-ttu-id="27b81-124">integração de saudação tooconfigure Wizergos de softwares de produtividade no AD do Azure, você precisa tooadd Wizergos Software de produtividade da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="27b81-124">tooconfigure hello integration of Wizergos Productivity Software into Azure AD, you need tooadd Wizergos Productivity Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27b81-125">**tooadd Wizergos Software de produtividade da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27b81-125">**tooadd Wizergos Productivity Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27b81-126">Em Olá **Portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="27b81-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="27b81-128">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="27b81-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="27b81-129">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="27b81-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicativos][2]
4. <span data-ttu-id="27b81-131">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="27b81-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicativos][3]
5. <span data-ttu-id="27b81-133">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="27b81-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicativos][4]
6. <span data-ttu-id="27b81-135">Na caixa de pesquisa hello, digite **Software de produtividade Wizergos**.</span><span class="sxs-lookup"><span data-stu-id="27b81-135">In hello search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="27b81-137">No painel de resultados de saudação, selecione **Software de produtividade Wizergos**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="27b81-137">In hello results panel, select **Wizergos Productivity Software**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Selecionar aplicativo hello na Galeria de saudação](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="27b81-139">Configurar e testar SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b81-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="27b81-140">Olá o objetivo desta seção é tooshow como tooconfigure e teste do Azure AD SSO com Software de produtividade Wizergos com base em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="27b81-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27b81-141">Para SSO toowork, o AD do Azure precisa tooknow é qual usuário de contraparte saudação do usuário do Software de produtividade Wizergos tooan no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="27b81-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Wizergos Productivity Software tooan user in Azure AD is.</span></span> <span data-ttu-id="27b81-142">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Software de produtividade Wizergos precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="27b81-142">In other words, a link relationship between an Azure AD user and hello related user in Wizergos Productivity Software needs toobe established.</span></span>

<span data-ttu-id="27b81-143">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Wizergos Software de produtividade.</span><span class="sxs-lookup"><span data-stu-id="27b81-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="27b81-144">tooconfigure e teste de logon único do AD do Azure com BynWizergos Softwareder de produtividade, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="27b81-144">tooconfigure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27b81-145">**[Configurar o logon único do AD do Azure](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="27b81-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27b81-146">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27b81-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27b81-147">**[Criar um usuário de teste de Software de produtividade Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave um equivalente do Britta Simon em Software de produtividade de Wizergos é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="27b81-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - toohave a counterpart of Britta Simon in Wizergos Productivity Software that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="27b81-148">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="27b81-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27b81-149">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="27b81-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="27b81-150">Configurar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b81-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="27b81-151">Nesta seção, habilitar o AD do Azure-logon único no portal clássico do hello e configurar o logon único no aplicativo Wizergos produtividade.</span><span class="sxs-lookup"><span data-stu-id="27b81-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="27b81-152">**tooconfigure logon único do AD do Azure com o Software de produtividade Wizergos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27b81-152">**tooconfigure Azure AD single sign-on with Wizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="27b81-153">No portal clássico hello, em Olá **Software de produtividade Wizergos** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27b81-153">In hello classic portal, on hello **Wizergos Productivity Software** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar Logon Único][6] 
2. <span data-ttu-id="27b81-155">Em Olá **como você gostaria usuários toosign no Software de produtividade de tooWizergos** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**:</span><span class="sxs-lookup"><span data-stu-id="27b81-155">On hello **How would you like users toosign on tooWizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="27b81-157">Em Olá **definir configurações de aplicativo** página da caixa de diálogo, clique em **próximo**:</span><span class="sxs-lookup"><span data-stu-id="27b81-157">On hello **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="27b81-159">Em Olá **configurar logon único no Software de produtividade Wizergos** , clique em **Download certificado**e, em seguida, salve o arquivo de saudação em seu computador:</span><span class="sxs-lookup"><span data-stu-id="27b81-159">On hello **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save hello file on your computer:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="27b81-161">Em uma janela de navegador web diferente, locatário do Software de produtividade Wizergos tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="27b81-161">In a different web browser window, sign-on tooyour Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="27b81-162">No menu de hambúrguer hello, selecione **Admin**.</span><span class="sxs-lookup"><span data-stu-id="27b81-162">From hello hamburger menu, select **Admin**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="27b81-164">Na página de administração no menu à esquerda, selecione **AUTENTICAÇÃO** e clique em **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="27b81-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="27b81-166">Executar Olá seguindo as etapas na **autenticação** seção.</span><span class="sxs-lookup"><span data-stu-id="27b81-166">Perform hello following steps on **AUTHENTICATION** section.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="27b81-168">Clique em **carregar** saudação do botão tooupload baixado o certificado do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="27b81-168">Click **UPLOAD** button tooupload hello downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="27b81-169">Em Olá **URL do emissor** caixa de texto colocar o valor de saudação de **URL do emissor** do Assistente de configuração de aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="27b81-169">In hello **Issuer URL** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="27b81-170">Em Olá **URL de logon único** caixa de texto colocar o valor de saudação de **o URL de serviço de logon único** do Assistente de configuração de aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="27b81-170">In hello **Single Sign-On URL** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="27b81-171">Em Olá **URL de logout único** caixa de texto colocar o valor de saudação de **URL do serviço de logon único** do Assistente de configuração de aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="27b81-171">In hello **Single Sign-Out URL** textbox put hello value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="27b81-172">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="27b81-172">Click **Save** button.</span></span>
9. <span data-ttu-id="27b81-173">No portal clássico do hello, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="27b81-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][10]
10. <span data-ttu-id="27b81-175">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="27b81-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Logon Único do AD do Azure][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="27b81-177">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b81-177">Create an Azure AD test user</span></span>
<span data-ttu-id="27b81-178">Olá objetivo desta seção é toocreate um usuário de teste no portal clássico do hello chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27b81-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="27b81-180">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27b81-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27b81-181">Em Olá **Portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="27b81-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="27b81-183">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="27b81-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="27b81-184">lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="27b81-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="27b81-186">Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="27b81-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="27b81-188">Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27b81-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="27b81-190">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="27b81-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="27b81-191">Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27b81-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="27b81-192">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="27b81-192">Click **Next**.</span></span>
6. <span data-ttu-id="27b81-193">Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27b81-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="27b81-195">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="27b81-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="27b81-196">Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="27b81-196">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="27b81-197">Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="27b81-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="27b81-198">Em Olá **função** lista, selecione **usuário**.</span><span class="sxs-lookup"><span data-stu-id="27b81-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="27b81-199">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="27b81-199">Click **Next**.</span></span>
7. <span data-ttu-id="27b81-200">Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="27b81-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="27b81-202">Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27b81-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="27b81-204">Anote o valor Olá Olá **nova senha**.</span><span class="sxs-lookup"><span data-stu-id="27b81-204">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="27b81-205">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="27b81-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="27b81-206">Criar um usuário de teste do Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="27b81-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="27b81-207">Nesta seção, você deve criar um usuário chamado Brenda Fernandes no Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="27b81-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="27b81-208">Trabalhe com a equipe de suporte de Software de produtividade Wizergos via [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd usuários de saudação na plataforma de Software de produtividade Wizergos hello.</span><span class="sxs-lookup"><span data-stu-id="27b81-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) tooadd hello users in hello Wizergos Productivity Software platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="27b81-209">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27b81-209">Assign hello Azure AD test user</span></span>
<span data-ttu-id="27b81-210">Olá objetivo desta seção é tooenabling Britta Simon toouse Azure SSO concedendo seu Software de produtividade de tooWizergos de acesso.</span><span class="sxs-lookup"><span data-stu-id="27b81-210">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooWizergos Productivity Software.</span></span>

  ![Atribuir usuário][200]

<span data-ttu-id="27b81-212">**tooassign Britta Simon tooWizergos Software de produtividade, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27b81-212">**tooassign Britta Simon tooWizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="27b81-213">No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="27b81-213">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Atribuir usuário][201]
2. <span data-ttu-id="27b81-215">Na lista de aplicativos hello, selecione **Software de produtividade Wizergos**.</span><span class="sxs-lookup"><span data-stu-id="27b81-215">In hello applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="27b81-217">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="27b81-217">In hello menu on hello top, click **Users**.</span></span>
   
    ![Atribuir usuário][203]
4. <span data-ttu-id="27b81-219">Na lista de usuários hello, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="27b81-219">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="27b81-220">Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="27b81-220">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="27b81-222">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="27b81-222">Test single sign-on</span></span>
<span data-ttu-id="27b81-223">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="27b81-223">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="27b81-224">Quando você clica em um bloco de Software de produtividade Wizergos Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Software de produtividade de Wizergos.</span><span class="sxs-lookup"><span data-stu-id="27b81-224">When you click hello Wizergos Productivity Software tile in hello Access Panel, you should get automatically signed-on tooyour Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="27b81-225">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="27b81-225">Additional resources</span></span>
* [<span data-ttu-id="27b81-226">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="27b81-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27b81-227">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="27b81-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
