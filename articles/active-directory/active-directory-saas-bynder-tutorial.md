---
title: "Tutorial: Integração do Azure Active Directory ao Bynder | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="fa778-103">Tutorial: Integração do Azure Active Directory ao Bynder</span><span class="sxs-lookup"><span data-stu-id="fa778-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="fa778-104">Olá objetivo deste tutorial é tooshow você como toointegrate Bynder com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="fa778-104">hello objective of this tutorial is tooshow you how toointegrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fa778-105">Integrando Bynder com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa778-105">Integrating Bynder with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="fa778-106">Você pode controlar no AD do Azure que tenha acesso tooBynder</span><span class="sxs-lookup"><span data-stu-id="fa778-106">You can control in Azure AD who has access tooBynder</span></span>
* <span data-ttu-id="fa778-107">Você pode habilitar seu usuários tooautomatically get conectado tooBynder-logon único (SSO) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fa778-107">You can enable your users tooautomatically get signed-on tooBynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="fa778-108">Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="fa778-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="fa778-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fa778-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa778-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fa778-110">Prerequisites</span></span>
<span data-ttu-id="fa778-111">tooconfigure integração do AD do Azure com Bynder, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa778-111">tooconfigure Azure AD integration with Bynder, you need hello following items:</span></span>

* <span data-ttu-id="fa778-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fa778-112">An Azure AD subscription</span></span>
* <span data-ttu-id="fa778-113">Uma assinatura habilitada para SSO (logon único) do Bynder</span><span class="sxs-lookup"><span data-stu-id="fa778-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="fa778-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="fa778-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="fa778-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="fa778-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="fa778-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="fa778-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="fa778-117">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fa778-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fa778-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="fa778-118">Scenario description</span></span>
<span data-ttu-id="fa778-119">Olá objetivo deste tutorial é tooenable você tootest SSO do Microsoft Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="fa778-119">hello objective of this tutorial is tooenable you tootest Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="fa778-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="fa778-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fa778-121">Adicionando Bynder da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="fa778-121">Adding Bynder from hello gallery</span></span>
2. <span data-ttu-id="fa778-122">Configuração e testes do SSO do Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa778-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-hello-gallery"></a><span data-ttu-id="fa778-123">Adicionar Bynder da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="fa778-123">Add Bynder from hello gallery</span></span>
<span data-ttu-id="fa778-124">integração de saudação tooconfigure de Bynder no AD do Azure, você precisa tooadd Bynder da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="fa778-124">tooconfigure hello integration of Bynder into Azure AD, you need tooadd Bynder from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fa778-125">**tooadd Bynder da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fa778-125">**tooadd Bynder from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa778-126">Em Olá **Portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fa778-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="fa778-128">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="fa778-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="fa778-129">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="fa778-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicativos][2]
4. <span data-ttu-id="fa778-131">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="fa778-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicativos][3]
5. <span data-ttu-id="fa778-133">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="fa778-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicativos][4]
6. <span data-ttu-id="fa778-135">Na caixa de pesquisa hello, digite **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="fa778-135">In hello search box, type **Bynder**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="fa778-137">No painel de resultados de saudação, selecione **Bynder**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fa778-137">In hello results panel, select **Bynder**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Selecionar aplicativo hello na Galeria de saudação](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="fa778-139">Configurar e testar o SSO do Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa778-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="fa778-140">Olá o objetivo desta seção é tooshow como tooconfigure e Microsoft Azure AD SSO com Bynder de teste com base em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fa778-140">hello objective of this section is tooshow you how tooconfigure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fa778-141">Para SSO toowork, o AD do Azure precisa tooknow que usuário de contraparte Olá Bynder tooan usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa778-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Bynder tooan user in Azure AD is.</span></span> <span data-ttu-id="fa778-142">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Bynder precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="fa778-142">In other words, a link relationship between an Azure AD user and hello related user in Bynder needs toobe established.</span></span>

<span data-ttu-id="fa778-143">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Bynder.</span><span class="sxs-lookup"><span data-stu-id="fa778-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bynder.</span></span>

<span data-ttu-id="fa778-144">tooconfigure e Microsoft Azure AD SSO com Bynder de teste, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa778-144">tooconfigure and test Microsoft Azure AD SSO with Bynder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fa778-145">**[Configurar o logon único do Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="fa778-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fa778-146">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Microsoft Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fa778-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="fa778-147">**[Criar um usuário de teste Bynder](#creating-a-bynder-test-user)**  -toohave um equivalente do Britta Simon em Bynder é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="fa778-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - toohave a counterpart of Britta Simon in Bynder that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="fa778-148">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable toouse Britta Simon AD do Microsoft Azure Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="fa778-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="fa778-149">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="fa778-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="fa778-150">Configuração do SSO do Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa778-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="fa778-151">Nesta seção, habilitar SSO de AD do Microsoft Azure no portal clássico do hello e configurar o SSO em seu aplicativo Bynder.</span><span class="sxs-lookup"><span data-stu-id="fa778-151">In this section, you enable Microsoft Azure AD SSO in hello classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="fa778-152">**tooconfigure Microsoft Azure AD SSO com Bynder, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fa778-152">**tooconfigure Microsoft Azure AD SSO with Bynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa778-153">No portal clássico hello, em Olá **Bynder** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fa778-153">In hello classic portal, on hello **Bynder** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar Logon Único][6] 
2. <span data-ttu-id="fa778-155">Em Olá **como você gostaria usuários toosign em tooBynder** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fa778-155">On hello **How would you like users toosign on tooBynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="fa778-157">Em Olá **definir configurações de aplicativo** página de diálogo, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**, execute Olá etapas a seguir e clique em **próximo**:</span><span class="sxs-lookup"><span data-stu-id="fa778-157">On hello **Configure App Settings** dialog page, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps and click **Next**:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="fa778-159">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="fa778-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="fa778-160">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="fa778-160">Click **Next**.</span></span>
4. <span data-ttu-id="fa778-161">Se desejar que o aplicativo hello tooconfigure **modo iniciado do SP** em Olá **definir configurações de aplicativo** página de diálogo, em seguida, clique em Olá **"Show advanced configurações (opcional)"**e, em seguida, digite Olá **URL de logon** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fa778-161">If you wish tooconfigure hello application in **SP initiated mode** on hello **Configure App Settings** dialog page, then click on hello **“Show advanced settings (optional)”** and then enter hello **Sign On URL** and click **Next**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="fa778-163">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="fa778-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="fa778-164">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="fa778-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="fa778-165">valor Olá Olá URL de logon neste tutorial é apenas um placeholfer.</span><span class="sxs-lookup"><span data-stu-id="fa778-165">hello value for hello Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="fa778-166">saudação de tooget valor real para o seu ambiente, entre em contato com Bynder.</span><span class="sxs-lookup"><span data-stu-id="fa778-166">tooget hello actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="fa778-167">Em Olá **configurar logon único no Bynder** página, execute Olá etapas a seguir e clique em **próximo**:</span><span class="sxs-lookup"><span data-stu-id="fa778-167">On hello **Configure single sign-on at Bynder** page, perform hello following steps and click **Next**:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="fa778-169">Clique em **baixar metadados**e, em seguida, salve o arquivo de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="fa778-169">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="fa778-170">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="fa778-170">Click **Next**.</span></span>
6. <span data-ttu-id="fa778-171">tooget SSO configurado para o seu aplicativo, entre em contato com sua equipe de suporte de Bynder.</span><span class="sxs-lookup"><span data-stu-id="fa778-171">tooget SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="fa778-172">Anexar o arquivo de metadados baixado hello e compartilhá-lo com tooset de equipe Bynder o logon único em seu lado.</span><span class="sxs-lookup"><span data-stu-id="fa778-172">Attach hello downloaded metadata file and share it with Bynder team tooset up SSO on their side.</span></span>
7. <span data-ttu-id="fa778-173">No portal clássico do hello, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fa778-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][10]
8. <span data-ttu-id="fa778-175">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="fa778-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Logon Único do AD do Azure][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fa778-177">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa778-177">Create an Azure AD test user</span></span>
<span data-ttu-id="fa778-178">Olá objetivo desta seção é toocreate um usuário de teste no portal clássico do hello chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fa778-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="fa778-180">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fa778-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa778-181">Em Olá **Portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fa778-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="fa778-183">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="fa778-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="fa778-184">lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="fa778-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="fa778-186">Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="fa778-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="fa778-188">Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa778-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="fa778-190">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="fa778-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="fa778-191">Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fa778-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="fa778-192">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="fa778-192">Click **Next**.</span></span>
6. <span data-ttu-id="fa778-193">Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa778-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="fa778-195">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fa778-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="fa778-196">Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fa778-196">In hello **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="fa778-197">Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fa778-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="fa778-198">Em Olá **função** lista, selecione **usuário**.</span><span class="sxs-lookup"><span data-stu-id="fa778-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="fa778-199">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="fa778-199">Click **Next**.</span></span>
7. <span data-ttu-id="fa778-200">Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="fa778-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="fa778-202">Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa778-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="fa778-204">Anote o valor Olá Olá **nova senha**.</span><span class="sxs-lookup"><span data-stu-id="fa778-204">Write down hello value of hello **New Password**.</span></span>
   2. <span data-ttu-id="fa778-205">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="fa778-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="fa778-206">Criar um usuário de teste do Bynder</span><span class="sxs-lookup"><span data-stu-id="fa778-206">Create a Bynder test user</span></span>
<span data-ttu-id="fa778-207">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Bynder.</span><span class="sxs-lookup"><span data-stu-id="fa778-207">hello objective of this section is toocreate a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="fa778-208">O Bynder dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="fa778-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="fa778-209">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="fa778-209">There is no action item for you in this section.</span></span> <span data-ttu-id="fa778-210">Será criado um novo usuário durante uma tentativa tooaccess Bynder se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="fa778-210">A new user will be created during an attempt tooaccess Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="fa778-211">Se você precisar toocreate um usuário manualmente, é necessário a equipe de suporte de Bynder toocontact hello.</span><span class="sxs-lookup"><span data-stu-id="fa778-211">If you need toocreate an user manually, you need toocontact hello Bynder support team.</span></span> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fa778-212">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fa778-212">Assign hello Azure AD test user</span></span>
<span data-ttu-id="fa778-213">Olá objetivo desta seção é tooenabling Britta Simon toouse Azure SSO concedendo tooBynder seu acesso.</span><span class="sxs-lookup"><span data-stu-id="fa778-213">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooBynder.</span></span>

   ![Atribuir usuário][200]

<span data-ttu-id="fa778-215">**tooassign Britta Simon tooBynder, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fa778-215">**tooassign Britta Simon tooBynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa778-216">No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="fa778-216">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Atribuir usuário][201]
2. <span data-ttu-id="fa778-218">Na lista de aplicativos hello, selecione **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="fa778-218">In hello applications list, select **Bynder**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="fa778-220">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="fa778-220">In hello menu on hello top, click **Users**.</span></span>
   
    ![Atribuir usuário][203]
4. <span data-ttu-id="fa778-222">Na lista de usuários hello, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fa778-222">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="fa778-223">Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="fa778-223">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="fa778-225">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="fa778-225">Test single sign-on</span></span>
<span data-ttu-id="fa778-226">Olá o objetivo desta seção é tootest sua configuração de SSO do Microsoft Azure AD usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="fa778-226">hello objective of this section is tootest your Microsoft Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="fa778-227">Quando você clica em bloco Bynder Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Bynder aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fa778-227">When you click hello Bynder tile in hello Access Panel, you should get automatically signed-on tooyour Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fa778-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fa778-228">Additional resources</span></span>
* [<span data-ttu-id="fa778-229">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="fa778-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fa778-230">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fa778-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
