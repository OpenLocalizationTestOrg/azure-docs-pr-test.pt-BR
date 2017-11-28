---
title: "Tutorial: Integração do Active Directory do Azure com @Task| Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o @Task."
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
ms.openlocfilehash: ebb19ca6cbaf04106fbce937d95651e709854cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="8db50-103">Tutorial: Integração do Active Directory do Azure com @Task</span><span class="sxs-lookup"><span data-stu-id="8db50-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="8db50-104">O objetivo desse tutorial é mostrar como integrar @Task ao Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="8db50-104">The objective of this tutorial is to show you how to integrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="8db50-105">A integração de @Task ao AD do Azure oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="8db50-105">Integrating @Task with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="8db50-106">No AD do Azure, é possível controlar quem tem acesso a @Task</span><span class="sxs-lookup"><span data-stu-id="8db50-106">You can control in Azure AD who has access to @Task</span></span>
* <span data-ttu-id="8db50-107">Você pode permitir que seus usuários façam logon automaticamente em @Task (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8db50-107">You can enable your users to automatically get signed-on to @Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="8db50-108">Você pode gerenciar suas contas em um único local: o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="8db50-108">You can manage your accounts in one central location - the Azure classic Portal</span></span>

<span data-ttu-id="8db50-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8db50-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8db50-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8db50-110">Prerequisites</span></span>
<span data-ttu-id="8db50-111">Para configurar a integração do AD do Azure com @Task, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8db50-111">To configure Azure AD integration with @Task, you need the following items:</span></span>

* <span data-ttu-id="8db50-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8db50-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8db50-113">Uma assinatura habilitada para logon único @Task</span><span class="sxs-lookup"><span data-stu-id="8db50-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8db50-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8db50-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="8db50-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8db50-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8db50-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8db50-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8db50-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8db50-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="8db50-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8db50-118">Scenario Description</span></span>
<span data-ttu-id="8db50-119">O objetivo deste tutorial é permitir que você teste o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8db50-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="8db50-120">O cenário descrito neste tutorial consiste em três blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="8db50-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="8db50-121">Adicionar @Task da galeria</span><span class="sxs-lookup"><span data-stu-id="8db50-121">Adding @Task from the gallery</span></span> 
2. <span data-ttu-id="8db50-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8db50-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-the-gallery"></a><span data-ttu-id="8db50-123">Adicionar @Task da galeria</span><span class="sxs-lookup"><span data-stu-id="8db50-123">Adding @Task from the gallery</span></span>
<span data-ttu-id="8db50-124">Para configurar a integração de @Task ao AD do Azure, você precisa adicionar @Task por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8db50-124">To configure the integration of @Task into Azure AD, you need to add @Task from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8db50-125">**Para adicionar @Task por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8db50-125">**To add @Task from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8db50-126">No **Portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8db50-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="8db50-128">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="8db50-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8db50-129">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="8db50-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplicativos][2] 
4. <span data-ttu-id="8db50-131">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="8db50-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicativos][3] 
5. <span data-ttu-id="8db50-133">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="8db50-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicativos][4] 
6. <span data-ttu-id="8db50-135">Na caixa de pesquisa, digite **@Task**.</span><span class="sxs-lookup"><span data-stu-id="8db50-135">In the search box, type **@Task**.</span></span>
   
    ![Aplicativos][5] 
7. <span data-ttu-id="8db50-137">No painel de resultados, selecione **@Task** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8db50-137">In the results pane, select **@Task**, and then click **Complete** to add the application.</span></span>
   
    ![Aplicativos][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8db50-139">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8db50-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8db50-140">O objetivo desta seção é mostrar como configurar e testar o logon único do AD do Azure com @Task, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8db50-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8db50-141">Para que o logon único funcione, o AD do Azure precisa saber qual usuário de @Task é equivalente a um usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8db50-141">For single sign-on to work, Azure AD needs to know what the counterpart user in @Task to an user in Azure AD is.</span></span> <span data-ttu-id="8db50-142">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado em @Task.</span><span class="sxs-lookup"><span data-stu-id="8db50-142">In other words, a link relationship between an Azure AD user and the related user in @Task needs to be established.</span></span>   
<span data-ttu-id="8db50-143">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como sendo o valor de **Nome de usuário** no @Task.</span><span class="sxs-lookup"><span data-stu-id="8db50-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in @Task.</span></span>

<span data-ttu-id="8db50-144">Para configurar e testar o AD do Azure-logon único com @Task, você precisa concluir os blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="8db50-144">To configure and test Azure AD single sign-on with @Task, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8db50-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8db50-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8db50-146">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8db50-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8db50-147">**[Criar um @Tasktest usuário](#creating-a-halogen-software-test-user)** - para ter um equivalente de Brenda Fernandes em @Taskthat que esteja vinculado à representação dela no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8db50-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in @Taskthat is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8db50-148">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8db50-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8db50-149">**[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="8db50-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8db50-150">Configuração do logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8db50-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="8db50-151">O objetivo desta seção é habilitar o logon único do AD do Azure no portal clássico do Azure e configurar o logon único em seu aplicativo de @Task.</span><span class="sxs-lookup"><span data-stu-id="8db50-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your @Task application.</span></span>

<span data-ttu-id="8db50-152">**Para configurar o AD do Azure-logon único com @Task, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8db50-152">**To configure Azure AD single sign-on with @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="8db50-153">No portal clássico do Azure, na página de integração de aplicativos **@Task**, clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="8db50-153">In the Azure classic portal, on the **@Task** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar Logon Único][6] 
2. <span data-ttu-id="8db50-155">Na página **Como você deseja que os usuários façam logon em @Task**, selecione **Logon único do AD do Azure** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8db50-155">On the **How would you like users to sign on to @Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][7] 
3. <span data-ttu-id="8db50-157">Na página de diálogo **Definir Configurações de Aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8db50-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Definir Configurações de Aplicativo][8] 
   
     <span data-ttu-id="8db50-159">a.</span><span class="sxs-lookup"><span data-stu-id="8db50-159">a.</span></span> <span data-ttu-id="8db50-160">Na caixa de texto **URL de Resposta**, digite a URL usada pelos usuários para entrar no site @Task (por exemplo: *https://<Tenant name>.attask-ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="8db50-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="8db50-161">b.</span><span class="sxs-lookup"><span data-stu-id="8db50-161">b.</span></span> <span data-ttu-id="8db50-162">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8db50-162">Click **Next**.</span></span>
4. <span data-ttu-id="8db50-163">Na página **Configurar logon único em @Task**, clique em **Baixar metadados** e salve o arquivo de metadados localmente no computador e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8db50-163">On the **Configure single sign-on at @Task** page, click **Download metadata**, save the metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![O que é o Azure AD Connect][9] 
5. <span data-ttu-id="8db50-165">Faça logon no site da empresa @Task como administrador.</span><span class="sxs-lookup"><span data-stu-id="8db50-165">Sign-on to your @Task company site as administrator.</span></span>
6. <span data-ttu-id="8db50-166">Vá para **Configuração de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="8db50-166">Go to **Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="8db50-167">Na caixa de diálogo **Logon Único** , realize as seguintes etapas</span><span class="sxs-lookup"><span data-stu-id="8db50-167">On the **Single Sign-On** dialog, perform the following steps</span></span>
   
    ![Configurar Logon Único][23]
   
    <span data-ttu-id="8db50-169">a.</span><span class="sxs-lookup"><span data-stu-id="8db50-169">a.</span></span> <span data-ttu-id="8db50-170">Como **Tipo**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="8db50-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="8db50-171">b.</span><span class="sxs-lookup"><span data-stu-id="8db50-171">b.</span></span> <span data-ttu-id="8db50-172">Selecione **ID do Provedor de Serviços**.</span><span class="sxs-lookup"><span data-stu-id="8db50-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="8db50-173">c.</span><span class="sxs-lookup"><span data-stu-id="8db50-173">c.</span></span> <span data-ttu-id="8db50-174">No portal clássico do Azure, copie a **URL de Logon Remoto** e cole-a na caixa de texto **URL do Portal de Logon**.</span><span class="sxs-lookup"><span data-stu-id="8db50-174">On the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="8db50-175">d.</span><span class="sxs-lookup"><span data-stu-id="8db50-175">d.</span></span> <span data-ttu-id="8db50-176">No portal clássico do Azure, copie a **URL do Serviço de Logout Único** e cole-a na caixa de texto **URL de Logout**.</span><span class="sxs-lookup"><span data-stu-id="8db50-176">On the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="8db50-177">e.</span><span class="sxs-lookup"><span data-stu-id="8db50-177">e.</span></span> <span data-ttu-id="8db50-178">No portal clássico do Azure, copie a **URL de Alteração de Senha** e cole-a na caixa de texto URL de **Alteração de Senha**.</span><span class="sxs-lookup"><span data-stu-id="8db50-178">On the Azure classic portal, copy the **Change Password URL**, and then paste it into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="8db50-179">f.</span><span class="sxs-lookup"><span data-stu-id="8db50-179">f.</span></span> <span data-ttu-id="8db50-180">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8db50-180">Click **Save**.</span></span>
8. <span data-ttu-id="8db50-181">No portal clássico do Azure, selecione a confirmação de configuração de logon único e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8db50-181">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![O que é o Azure AD Connect][10]
9. <span data-ttu-id="8db50-183">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="8db50-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![O que é o Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8db50-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8db50-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="8db50-186">O objetivo desta seção é criar um usuário de teste no Portal Clássico do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8db50-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="8db50-188">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8db50-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8db50-189">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8db50-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="8db50-191">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="8db50-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8db50-192">Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="8db50-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="8db50-194">Para abrir a caixa de diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="8db50-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="8db50-196">Na página do diálogo **Conte-nos sobre este usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8db50-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="8db50-198">a.</span><span class="sxs-lookup"><span data-stu-id="8db50-198">a.</span></span> <span data-ttu-id="8db50-199">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="8db50-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="8db50-200">b.</span><span class="sxs-lookup"><span data-stu-id="8db50-200">b.</span></span> <span data-ttu-id="8db50-201">Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="8db50-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="8db50-202">c.</span><span class="sxs-lookup"><span data-stu-id="8db50-202">c.</span></span> <span data-ttu-id="8db50-203">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8db50-203">Click **Next**.</span></span>
6. <span data-ttu-id="8db50-204">Na página do diálogo **Perfil do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8db50-204">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="8db50-206">a.</span><span class="sxs-lookup"><span data-stu-id="8db50-206">a.</span></span> <span data-ttu-id="8db50-207">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="8db50-207">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="8db50-208">b.</span><span class="sxs-lookup"><span data-stu-id="8db50-208">b.</span></span> <span data-ttu-id="8db50-209">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="8db50-209">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="8db50-210">c.</span><span class="sxs-lookup"><span data-stu-id="8db50-210">c.</span></span> <span data-ttu-id="8db50-211">Na caixa de texto **Nome de Exibição**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="8db50-211">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="8db50-212">d.</span><span class="sxs-lookup"><span data-stu-id="8db50-212">d.</span></span> <span data-ttu-id="8db50-213">Na lista **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="8db50-213">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="8db50-214">e.</span><span class="sxs-lookup"><span data-stu-id="8db50-214">e.</span></span> <span data-ttu-id="8db50-215">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8db50-215">Click **Next**.</span></span>

7. <span data-ttu-id="8db50-216">Na página de diálogo **Obter senha temporária**, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="8db50-216">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="8db50-218">Na página de caixa de diálogo **Obter senha temporária** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8db50-218">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="8db50-220">a.</span><span class="sxs-lookup"><span data-stu-id="8db50-220">a.</span></span> <span data-ttu-id="8db50-221">Anote o valor da **Nova Senha**.</span><span class="sxs-lookup"><span data-stu-id="8db50-221">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="8db50-222">b.</span><span class="sxs-lookup"><span data-stu-id="8db50-222">b.</span></span> <span data-ttu-id="8db50-223">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="8db50-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="8db50-224">Criando um usuário de teste de @Task</span><span class="sxs-lookup"><span data-stu-id="8db50-224">Creating an @Task test user</span></span>
<span data-ttu-id="8db50-225">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no @Task.</span><span class="sxs-lookup"><span data-stu-id="8db50-225">The objective of this section is to create a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="8db50-226">**Para criar um usuário chamado Britta Simon no @Task, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8db50-226">**To create a user called Britta Simon in @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="8db50-227">Faça logon no site da empresa @Task como administrador.</span><span class="sxs-lookup"><span data-stu-id="8db50-227">Sign on to your @Task company site as administrator.</span></span>
2. <span data-ttu-id="8db50-228">No menu na parte superior, clique em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="8db50-228">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="8db50-229">Clique em **Nova Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="8db50-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="8db50-230">Na caixa de diálogo Nova Pessoa, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8db50-230">On the New Person dialog, perform the following steps:</span></span>
   
    ![Criar um usuário de teste de @Task][21] 
   
    <span data-ttu-id="8db50-232">a.</span><span class="sxs-lookup"><span data-stu-id="8db50-232">a.</span></span> <span data-ttu-id="8db50-233">Na caixa de texto **Nome** , digite “Brenda”.</span><span class="sxs-lookup"><span data-stu-id="8db50-233">In the **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="8db50-234">b.</span><span class="sxs-lookup"><span data-stu-id="8db50-234">b.</span></span> <span data-ttu-id="8db50-235">Na caixa de texto **Sobrenome** , digite “Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8db50-235">In the **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="8db50-236">c.</span><span class="sxs-lookup"><span data-stu-id="8db50-236">c.</span></span> <span data-ttu-id="8db50-237">Na caixa de texto **Endereço de Email** , digite o endereço de email de Brenda Fernandes no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="8db50-237">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="8db50-238">d.</span><span class="sxs-lookup"><span data-stu-id="8db50-238">d.</span></span> <span data-ttu-id="8db50-239">Clique em **Adicionar Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="8db50-239">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8db50-240">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8db50-240">Assigning the Azure AD test user</span></span>
<span data-ttu-id="8db50-241">O objetivo desta seção é habilitar Brenda Fernandes para usar o logon único do Azure, concedendo a ela acesso ao @Task.</span><span class="sxs-lookup"><span data-stu-id="8db50-241">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to @Task.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8db50-243">**Para atribuir Britta Simon para @Task, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8db50-243">**To assign Britta Simon to @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="8db50-244">No portal clássico do Azure, para abrir o modo de exibição de aplicativos, na exibição de diretório, clique em **Aplicativos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="8db50-244">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Atribuir usuário][201] 
2. <span data-ttu-id="8db50-246">Na lista de aplicativos, selecione **@Task**.</span><span class="sxs-lookup"><span data-stu-id="8db50-246">In the applications list, select **@Task**.</span></span>
   
    ![Atribuir usuário][202] 
3. <span data-ttu-id="8db50-248">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="8db50-248">In the menu on the top, click **Users**.</span></span>
   
    ![Atribuir usuário][203] 
4. <span data-ttu-id="8db50-250">Na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="8db50-250">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="8db50-251">Na barra de ferramentas na parte inferior, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="8db50-251">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="8db50-253">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8db50-253">Testing Single Sign-On</span></span>
<span data-ttu-id="8db50-254">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="8db50-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="8db50-255">Ao clicar no bloco de @Task no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo de @Task.</span><span class="sxs-lookup"><span data-stu-id="8db50-255">When you click the @Task tile in the Access Panel, you should get automatically signed-on to your @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8db50-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8db50-256">Additional Resources</span></span>
* [<span data-ttu-id="8db50-257">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8db50-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8db50-258">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8db50-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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






