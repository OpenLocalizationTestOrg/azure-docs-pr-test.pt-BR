---
title: "Tutorial: Integração do Azure Active Directory com o SciQuest Spend Director | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o SciQuest Spend Director."
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
ms.openlocfilehash: 84b707668dc45e92e6151f422f1c919f638533b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="ff050-103">Tutorial: Integração do Active Directory do Azure com o SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="ff050-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="ff050-104">O objetivo desse tutorial é mostrar como integrar o SciQuest Spend Director ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ff050-104">The objective of this tutorial is to show you how to integrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="ff050-105">A integração do SciQuest Spend Director ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="ff050-105">Integrating SciQuest Spend Director with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="ff050-106">Você pode controlar, no Azure AD, quem tem acesso ao SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="ff050-106">You can control in Azure AD who has access to SciQuest Spend Director</span></span> 
* <span data-ttu-id="ff050-107">Você pode habilitar seus usuários a fazerem logon automaticamente no SciQuest Spend Director (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff050-107">You can enable your users to automatically get signed-on to SciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="ff050-108">Gerenciar suas contas em um único local: o Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="ff050-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="ff050-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff050-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff050-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ff050-110">Prerequisites</span></span>
<span data-ttu-id="ff050-111">Para configurar a integração do Azure AD com o SciQuest Spend Director, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ff050-111">To configure Azure AD integration with SciQuest Spend Director, you need the following items:</span></span>

* <span data-ttu-id="ff050-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ff050-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ff050-113">Uma assinatura do SciQuest Spend Director com o logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="ff050-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff050-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ff050-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="ff050-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ff050-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ff050-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ff050-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ff050-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff050-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="ff050-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ff050-118">Scenario Description</span></span>
<span data-ttu-id="ff050-119">O objetivo deste tutorial é permitir que você teste o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ff050-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="ff050-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="ff050-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff050-121">Adição do SciQuest Spend Director por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="ff050-121">Adding SciQuest Spend Director from the gallery</span></span> 
2. <span data-ttu-id="ff050-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ff050-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-the-gallery"></a><span data-ttu-id="ff050-123">Adição do SciQuest Spend Director por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="ff050-123">Adding SciQuest Spend Director from the gallery</span></span>
<span data-ttu-id="ff050-124">Para configurar a integração do SciQuest Spend Director com o Azure AD, você precisa adicionar o SciQuest Spend Director, por meio da galeria, à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ff050-124">To configure the integration of SciQuest Spend Director into Azure AD, you need to add SciQuest Spend Director from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff050-125">**Para adicionar o SciQuest Spend Director por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ff050-125">**To add SciQuest Spend Director from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff050-126">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff050-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="ff050-128">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="ff050-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="ff050-129">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="ff050-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplicativos][2]

4. <span data-ttu-id="ff050-131">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="ff050-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicativos][3]

5. <span data-ttu-id="ff050-133">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="ff050-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicativos][4]

6. <span data-ttu-id="ff050-135">Na caixa de pesquisa, digite **sciQuest spend director**.</span><span class="sxs-lookup"><span data-stu-id="ff050-135">In the search box, type **sciQuest spend director**.</span></span>
   
    ![Aplicativos][5]

7. <span data-ttu-id="ff050-137">No painel de resultados, selecione **SciQuest Spend Director** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff050-137">In the results pane, select **SciQuest Spend Director**, and then click **Complete** to add the application.</span></span>
   
    ![Aplicativos][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff050-139">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ff050-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff050-140">O objetivo desta seção é mostrar como configurar e testar logon único do Azure AD com o SciQuest Spend Director, com base em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ff050-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff050-141">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SciQuest Spend Director é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff050-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SciQuest Spend Director to an user in Azure AD is.</span></span> <span data-ttu-id="ff050-142">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="ff050-142">In other words, a link relationship between an Azure AD user and the related user in SciQuest Spend Director needs to be established.</span></span>  
<span data-ttu-id="ff050-143">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="ff050-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="ff050-144">Para configurar e testar o logon único do Azure AD com o SciQuest Spend Director, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="ff050-144">To configure and test Azure AD single sign-on with SciQuest Spend Director, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff050-145">**[Configuração do logon único do Azure AD](#configuring-azure-ad-single-single-sign-on)** - para permitir que os usuários usem esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ff050-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ff050-146">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ff050-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff050-147">**[Criação de um usuário de teste do SciQuest Spend Director](#creating-a-halogen-software-test-user)** - para ter um equivalente de Brenda Fernandes no SciQuest Spend Director vinculado à representação dela no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff050-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in SciQuest Spend Director that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ff050-148">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff050-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff050-149">**[Teste do logon único](#testing-single-sign-on)** - para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="ff050-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="ff050-150">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff050-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="ff050-151">O objetivo desta seção é habilitar o logon único do Azure AD no Portal Clássico do Azure e configurar o logon único em seu aplicativo do SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="ff050-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="ff050-152">**Para configurar o logon único do Azure AD com o SciQuest Spend Director, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ff050-152">**To configure Azure AD single sign-on with SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="ff050-153">No portal clássico do Azure, na página de integração do aplicativo **SciQuest Spend Director**, clique em **Configurar logon único** para abrir a caixa de diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="ff050-153">In the Azure classic portal, on the **SciQuest Spend Director** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar Logon Único][8]

2. <span data-ttu-id="ff050-155">Na página **Como você deseja que os usuários façam logon no SciQuest Spend Director**, selecione **Logon Único do Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ff050-155">On the **How would you like users to sign on to SciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][9]

3. <span data-ttu-id="ff050-157">Na página de diálogo **Definir Configurações de Aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ff050-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Definir Configurações de Aplicativo][10]
   
     <span data-ttu-id="ff050-159">a.</span><span class="sxs-lookup"><span data-stu-id="ff050-159">a.</span></span> <span data-ttu-id="ff050-160">Na caixa de texto **URL de Logon**, digite a URL usada pelos usuários para fazer logon no seu aplicativo SciQuest Spend Director usando o seguinte padrão: *https://.*sciquest.com/.**</span><span class="sxs-lookup"><span data-stu-id="ff050-160">In the **Sign On URL** textbox, type your URL used by your users to sign on to your SciQuest Spend Director application using the following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="ff050-161">b.</span><span class="sxs-lookup"><span data-stu-id="ff050-161">b.</span></span> <span data-ttu-id="ff050-162">Na caixa de texto **URL de Resposta**, digite o mesmo valor que você digitou na caixa de texto **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="ff050-162">In the **Reply URL** textbox, type the same value you have typed into the **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="ff050-163">c.</span><span class="sxs-lookup"><span data-stu-id="ff050-163">c.</span></span> <span data-ttu-id="ff050-164">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ff050-164">Click **Next**.</span></span>

4. <span data-ttu-id="ff050-165">Na página **Configurar logon único no SciQuest Spend Director**, clique em **Baixar metadados** e salve o arquivo de metadados localmente em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ff050-165">On the **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![O que é o Azure AD Connect][11]

5. <span data-ttu-id="ff050-167">Entre em contato com o suporte da SciQuest para habilitar esse método de autenticação usando os metadados baixado acima.</span><span class="sxs-lookup"><span data-stu-id="ff050-167">Contact SciQuest support to enable this authentication method using the above downloaded metadata.</span></span>

6. <span data-ttu-id="ff050-168">No portal clássico do Azure, selecione a confirmação da configuração de logon único e clique em **Concluir** para fechar a caixa de diálogo **Configurar logon único**.</span><span class="sxs-lookup"><span data-stu-id="ff050-168">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span> 
   
    ![O que é o Azure AD Connect][15]

7. <span data-ttu-id="ff050-170">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="ff050-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff050-171">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ff050-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff050-172">O objetivo desta seção é criar um usuário de teste no Portal Clássico do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ff050-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="ff050-173">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ff050-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff050-174">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff050-174">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![O que é o Azure AD Connect][100] 

2. <span data-ttu-id="ff050-176">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="ff050-176">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="ff050-177">Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="ff050-177">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![O que é o Azure AD Connect][101] 

4. <span data-ttu-id="ff050-179">Para abrir a caixa de diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="ff050-179">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![O que é o Azure AD Connect][102] 

5. <span data-ttu-id="ff050-181">Na página do diálogo **Conte-nos sobre este usuário** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ff050-181">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![O que é o Azure AD Connect][103] 
   
    <span data-ttu-id="ff050-183">a.</span><span class="sxs-lookup"><span data-stu-id="ff050-183">a.</span></span> <span data-ttu-id="ff050-184">Em **Tipo de Usuário**, selecione **Novo usuário na organização**.</span><span class="sxs-lookup"><span data-stu-id="ff050-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="ff050-185">b.</span><span class="sxs-lookup"><span data-stu-id="ff050-185">b.</span></span> <span data-ttu-id="ff050-186">Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="ff050-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="ff050-187">c.</span><span class="sxs-lookup"><span data-stu-id="ff050-187">c.</span></span> <span data-ttu-id="ff050-188">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ff050-188">Click **Next**.</span></span>

6. <span data-ttu-id="ff050-189">Na página da caixa de diálogo **Perfil do Usuário** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ff050-189">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![O que é o Azure AD Connect][104] 
   
    <span data-ttu-id="ff050-191">a.</span><span class="sxs-lookup"><span data-stu-id="ff050-191">a.</span></span> <span data-ttu-id="ff050-192">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="ff050-192">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="ff050-193">b.</span><span class="sxs-lookup"><span data-stu-id="ff050-193">b.</span></span> <span data-ttu-id="ff050-194">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="ff050-194">In the **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="ff050-195">c.</span><span class="sxs-lookup"><span data-stu-id="ff050-195">c.</span></span> <span data-ttu-id="ff050-196">Na caixa de texto **Nome de Exibição**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="ff050-196">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="ff050-197">d.</span><span class="sxs-lookup"><span data-stu-id="ff050-197">d.</span></span> <span data-ttu-id="ff050-198">Na lista **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="ff050-198">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="ff050-199">e.</span><span class="sxs-lookup"><span data-stu-id="ff050-199">e.</span></span> <span data-ttu-id="ff050-200">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ff050-200">Click **Next**.</span></span>

7. <span data-ttu-id="ff050-201">Na página de diálogo **Obter senha temporária**, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="ff050-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![O que é o Azure AD Connect][105]  

8. <span data-ttu-id="ff050-203">Na página de caixa de diálogo **Obter senha temporária** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ff050-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![O que é o Azure AD Connect][106]   
   
    <span data-ttu-id="ff050-205">a.</span><span class="sxs-lookup"><span data-stu-id="ff050-205">a.</span></span> <span data-ttu-id="ff050-206">Anote o valor da **Nova Senha**.</span><span class="sxs-lookup"><span data-stu-id="ff050-206">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="ff050-207">b.</span><span class="sxs-lookup"><span data-stu-id="ff050-207">b.</span></span> <span data-ttu-id="ff050-208">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="ff050-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="ff050-209">Criação de um usuário de teste do SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="ff050-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="ff050-210">O objetivo desta seção é criar um usuário chamado Britta Simon no SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="ff050-210">The objective of this section is to create a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="ff050-211">Você precisa entrar em contato com a equipe de suporte do SciQuest Spend Director e fornecer a eles os detalhes da sua conta de teste para que ela seja criada.</span><span class="sxs-lookup"><span data-stu-id="ff050-211">You need to contact your SciQuest Spend Director support team and provide them with the details about your test account to get it created.</span></span>

<span data-ttu-id="ff050-212">Como alternativa, você também pode usar o provisionamento just-in-time, um recurso de logon único com suporte do SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="ff050-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="ff050-213">Se o provisionamento Just-In-Time estiver habilitado, os usuários serão automaticamente criados pelo SciQuest Spend Director durante uma tentativa de logon único, caso não existam.</span><span class="sxs-lookup"><span data-stu-id="ff050-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="ff050-214">Este recurso elimina a necessidade de criar manualmente os usuários correspondentes ao logon único.</span><span class="sxs-lookup"><span data-stu-id="ff050-214">This feature eliminates the need to manually create single sign-on counterpart users.</span></span>

<span data-ttu-id="ff050-215">Para habilitar o provisionamento just-in-time, você precisa entrar em contato com a equipe de suporte do SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="ff050-215">To get just-in-time provisioning enabled, you need to contact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ff050-216">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ff050-216">Assigning the Azure AD test user</span></span>
<span data-ttu-id="ff050-217">O objetivo desta seção é permitir que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="ff050-217">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SciQuest Spend Director.</span></span>

![O que é o Azure AD Connect][200]

<span data-ttu-id="ff050-219">**Para atribuir Britta Simon ao SciQuest Spend Director, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ff050-219">**To assign Britta Simon to SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="ff050-220">No portal clássico do Azure, para abrir o modo de exibição de aplicativos, no modo de exibição de diretório, clique em **Aplicativos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="ff050-220">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![O que é o Azure AD Connect][201]

2. <span data-ttu-id="ff050-222">Na lista de aplicativos, selecione **SciQuest Spend Director**.</span><span class="sxs-lookup"><span data-stu-id="ff050-222">In the applications list, select **SciQuest Spend Director**.</span></span>
   
    ![O que é o Azure AD Connect][202]

3. <span data-ttu-id="ff050-224">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="ff050-224">In the menu on the top, click **Users**.</span></span>
   
    ![O que é o Azure AD Connect][203]

4. <span data-ttu-id="ff050-226">Na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="ff050-226">In the Users list, select **Britta Simon**.</span></span>
   
    ![O que é o Azure AD Connect][204]

5. <span data-ttu-id="ff050-228">Na barra de ferramentas na parte inferior, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="ff050-228">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![O que é o Azure AD Connect][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="ff050-230">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ff050-230">Testing Single Sign-On</span></span>
<span data-ttu-id="ff050-231">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="ff050-231">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="ff050-232">Quando clica no bloco SciQuest Spend Director no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="ff050-232">When you click the SciQuest Spend Director tile in the Access Panel, you should get automatically signed-on to your SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff050-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ff050-233">Additional Resources</span></span>
* [<span data-ttu-id="ff050-234">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ff050-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff050-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff050-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

