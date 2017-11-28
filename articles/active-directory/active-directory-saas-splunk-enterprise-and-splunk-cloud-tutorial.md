---
title: "Tutorial: Integração do Azure Active Directory com o Splunk Enterprise e o Splunk Cloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Splunk Enterprise e Splunk nuvem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="e5b9d-103">Tutorial: Integração do Azure Active Directory com o Splunk Enterprise e o Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="e5b9d-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="e5b9d-104">Neste tutorial, você aprenderá como toointegrate Splunk Enterprise e Splunk nuvem com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="e5b9d-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e5b9d-105">Integração Splunk Enterprise e Splunk nuvem com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5b9d-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e5b9d-106">Você pode controlar no AD do Azure que tenha acesso tooSplunk Enterprise e nuvem Splunk</span><span class="sxs-lookup"><span data-stu-id="e5b9d-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="e5b9d-107">Você pode habilitar seu usuários tooautomatically get conectado tooSplunk Enterprise e nuvem Splunk-logon único (SSO) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5b9d-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="e5b9d-108">Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="e5b9d-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="e5b9d-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e5b9d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5b9d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e5b9d-110">Prerequisites</span></span>

<span data-ttu-id="e5b9d-111">tooconfigure integração do AD do Azure com Splunk Enterprise e Splunk nuvem, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5b9d-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="e5b9d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5b9d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e5b9d-113">Uma assinatura do Splunk Enterprise ou do Splunk Cloud habilitada para SSO</span><span class="sxs-lookup"><span data-stu-id="e5b9d-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="e5b9d-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="e5b9d-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e5b9d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e5b9d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e5b9d-117">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5b9d-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="e5b9d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e5b9d-118">Scenario description</span></span>
<span data-ttu-id="e5b9d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="e5b9d-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="e5b9d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e5b9d-121">Adicionando Splunk Enterprise e nuvem Splunk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e5b9d-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="e5b9d-122">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5b9d-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="e5b9d-123">Adicionar Splunk Enterprise e nuvem Splunk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e5b9d-123">Add Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="e5b9d-124">integração de saudação tooconfigure do Splunk Enterprise e Splunk nuvem no Azure AD, você precisa tooadd Splunk Enterprise e gerenciado de nuvem Splunk de lista de tooyour Olá Galeria de aplicativos SaaS.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e5b9d-125">**tooadd Splunk Enterprise e nuvem Splunk da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e5b9d-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5b9d-126">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="e5b9d-128">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="e5b9d-129">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Aplicativos][2]

4. <span data-ttu-id="e5b9d-131">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Aplicativos][3]

5. <span data-ttu-id="e5b9d-133">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Aplicativos][4]

6. <span data-ttu-id="e5b9d-135">Na caixa de pesquisa hello, digite **Splunk Enterprise ou nuvem Splunk**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-135">In hello search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="e5b9d-137">No painel de resultados de saudação, selecione **Splunk Enterprise e nuvem Splunk**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-137">In hello results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e5b9d-139">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5b9d-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="e5b9d-140">Nesta seção, você configurará e testará o logon único do Azure AD com o Splunk Enterprise e o Splunk Cloud, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="e5b9d-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e5b9d-141">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá Splunk Enterprise e nuvem Splunk é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="e5b9d-142">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Splunk Enterprise e nuvem Splunk precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-142">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="e5b9d-143">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Splunk Enterprise e Splunk nuvem.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="e5b9d-144">tooconfigure e teste de logon único do AD do Azure com Splunk Enterprise e Splunk nuvem, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5b9d-144">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e5b9d-145">**[Configurar o logon único do AD do Azure](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e5b9d-146">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e5b9d-147">**[Criar um usuário de teste Splunk Enterprise e nuvem Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave um equivalente de Britta Simon Splunk empresa e Splunk em nuvem que é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="e5b9d-148">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e5b9d-149">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e5b9d-150">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5b9d-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e5b9d-151">Nesta seção, habilitar o SSO de AD do Azure no portal clássico do hello e configurar SSO em seu aplicativo Splunk Enterprise e Splunk nuvem.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-151">In this section, you enable Azure AD SSO in hello classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="e5b9d-152">**tooconfigure logon único do AD do Azure com Splunk Enterprise e nuvem Splunk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e5b9d-152">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5b9d-153">No portal clássico hello, em Olá **Splunk Enterprise e nuvem Splunk** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-153">In hello classic portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurar Logon Único][6] 

2. <span data-ttu-id="e5b9d-155">Em Olá **como você gostaria que usuários toosign em tooSplunk Enterprise e nuvem Splunk** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-155">On hello **How would you like users toosign on tooSplunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="e5b9d-157">Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5b9d-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="e5b9d-159">Em Olá **URL de logon** caixa de texto, digite a URL Olá usada por seus usuários em toosign tooyour Splunk Enterprise e o aplicativo de nuvem Splunk usando saudação padrão a seguir:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="e5b9d-159">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Splunk Enterprise and Splunk Cloud application using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="e5b9d-160">Em Olá **identificador** caixa de texto, digite a URL de saudação do servidor Splunk.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="e5b9d-161">Em Olá **URL de resposta** caixa de texto, digite a URL de saudação com saudação padrão a seguir:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="e5b9d-161">In hello **Reply URL** textbox, type hello URL with hello following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="e5b9d-162">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="e5b9d-163">Em Olá **configurar logon único no Splunk Enterprise e nuvem Splunk** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5b9d-163">On hello **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="e5b9d-165">Clique em **baixar metadados**e, em seguida, salve o arquivo de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-165">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="e5b9d-166">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-166">Click **Next**.</span></span>

5. <span data-ttu-id="e5b9d-167">tooget SSO configurado para o seu aplicativo, entre em contato com Splunk Enterprise e a equipe de suporte de nuvem Splunk e fornecê-los com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="e5b9d-167">tooget SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with hello following:</span></span>

    * <span data-ttu-id="e5b9d-168">Olá baixado **federaton metadados**</span><span class="sxs-lookup"><span data-stu-id="e5b9d-168">hello downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="e5b9d-169">No portal clássico do hello, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-169">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Logon Único do AD do Azure][10]

7. <span data-ttu-id="e5b9d-171">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-171">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Logon Único do AD do Azure][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e5b9d-173">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5b9d-173">Create an Azure AD test user</span></span>
<span data-ttu-id="e5b9d-174">Nesta seção, você pode criar um usuário de teste no portal clássico do hello chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-174">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="e5b9d-176">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e5b9d-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5b9d-177">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-177">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="e5b9d-179">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-179">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="e5b9d-180">lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-180">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e5b9d-182">Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-182">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="e5b9d-184">Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5b9d-184">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="e5b9d-186">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="e5b9d-187">Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-187">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="e5b9d-188">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-188">Click **Next**.</span></span>

6.  <span data-ttu-id="e5b9d-189">Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5b9d-189">On hello **User Profile** dialog page, perform hello following steps:</span></span>
  
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="e5b9d-191">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-191">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="e5b9d-192">Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-192">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="e5b9d-193">Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-193">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="e5b9d-194">Em Olá **função** lista, selecione **usuário**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-194">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="e5b9d-195">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-195">Click **Next**.</span></span>

7. <span data-ttu-id="e5b9d-196">Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-196">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="e5b9d-198">Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5b9d-198">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="e5b9d-200">Anote o valor Olá Olá **nova senha**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-200">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="e5b9d-201">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="e5b9d-202">Criar um usuário de teste do Splunk Enterprise e do Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="e5b9d-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="e5b9d-203">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Splunk Enterprise e no Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="e5b9d-204">Trabalhe com Splunk Enterprise e nuvem Splunk suporte team tooadd Olá usuários Olá Splunk Enterprise e plataforma de nuvem Splunk.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-204">Please work with Splunk Enterprise and Splunk Cloud support team tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e5b9d-205">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5b9d-205">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e5b9d-206">Nesta seção, você deve habilitar Britta Simon toouse SSOy Azure concedendo o acesso tooSplunk Enterprise e Splunk nuvem.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-206">In this section, you enable Britta Simon toouse Azure SSOy granting her access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e5b9d-208">**tooassign Britta Simon tooSplunk Enterprise e nuvem Splunk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e5b9d-208">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5b9d-209">No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-209">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e5b9d-211">Na lista de aplicativos hello, selecione **Splunk Enterprise e nuvem Splunk**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-211">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="e5b9d-213">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-213">In hello menu on hello top, click **Users**.</span></span>

    ![Atribuir usuário][203]

4. <span data-ttu-id="e5b9d-215">Na lista de usuários hello, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-215">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="e5b9d-216">Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-216">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="e5b9d-218">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="e5b9d-218">Test single sign-on</span></span>

<span data-ttu-id="e5b9d-219">Nesta seção, você deve testar seu SSOonfiguration do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-219">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="e5b9d-220">Quando você clica em hello Splunk Enterprise e o bloco de nuvem Splunk no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Splunk Enterprise e nuvem Splunk o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e5b9d-220">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e5b9d-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e5b9d-221">Additional resources</span></span>

* [<span data-ttu-id="e5b9d-222">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e5b9d-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e5b9d-223">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e5b9d-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
