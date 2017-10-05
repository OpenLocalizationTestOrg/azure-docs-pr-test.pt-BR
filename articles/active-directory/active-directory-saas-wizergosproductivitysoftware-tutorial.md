---
title: "Tutorial: integração do Azure Active Directory com o Wizergos Productivity Software | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Wizergos Productivity Software."
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
ms.openlocfilehash: 73b3bc05aeb337c12acb7e47c0dbebe6d0196530
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="99b66-103">Tutorial: Integração do Azure Active Directory com o Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="99b66-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="99b66-104">O objetivo desse tutorial é mostrar como integrar o Wizergos Productivity Software ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="99b66-104">The objective of this tutorial is to show you how to integrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99b66-105">A integração do Wizergos Productivity Software ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="99b66-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="99b66-106">No Azure AD, você pode controlar quem tem acesso ao Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="99b66-106">You can control in Azure AD who has access to Wizergos Productivity Software</span></span>
* <span data-ttu-id="99b66-107">Você pode permitir que seus usuários façam logon automaticamente no Wizergos Productivity Software usando SSO (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="99b66-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="99b66-108">Gerenciar suas contas em um único local: o Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="99b66-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="99b66-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99b66-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99b66-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="99b66-110">Prerequisites</span></span>
<span data-ttu-id="99b66-111">Para configurar a integração do Azure AD com o Wizergos Productivity Software, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="99b66-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span></span>

* <span data-ttu-id="99b66-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="99b66-112">An Azure AD subscription</span></span>
* <span data-ttu-id="99b66-113">Uma assinatura do Wizergos Productivity Software habilitada para SSO</span><span class="sxs-lookup"><span data-stu-id="99b66-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="99b66-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="99b66-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="99b66-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="99b66-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="99b66-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="99b66-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="99b66-117">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99b66-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="99b66-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="99b66-118">Scenario description</span></span>
<span data-ttu-id="99b66-119">O objetivo deste tutorial é permitir que você teste o SSO do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="99b66-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="99b66-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="99b66-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99b66-121">Adição do software de produtividade Wizergos da galeria</span><span class="sxs-lookup"><span data-stu-id="99b66-121">Adding Wizergos Productivity Software from the gallery</span></span>
2. <span data-ttu-id="99b66-122">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="99b66-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-the-gallery"></a><span data-ttu-id="99b66-123">Adição do software de produtividade Wizergos da galeria</span><span class="sxs-lookup"><span data-stu-id="99b66-123">Adding Wizergos Productivity Software from the gallery</span></span>
<span data-ttu-id="99b66-124">Para configurar a integração do Wizergos Productivity Software com o Azure AD, você precisa adicionar o Wizergos Productivity Software, por meio da galeria, à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="99b66-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="99b66-125">**Para adicionar o Wizergos Productivity Software da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="99b66-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="99b66-126">No **Portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99b66-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="99b66-128">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="99b66-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="99b66-129">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="99b66-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplicativos][2]
4. <span data-ttu-id="99b66-131">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="99b66-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicativos][3]
5. <span data-ttu-id="99b66-133">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="99b66-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicativos][4]
6. <span data-ttu-id="99b66-135">Na caixa de pesquisa, digite **Wizergos Productivity Software**.</span><span class="sxs-lookup"><span data-stu-id="99b66-135">In the search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="99b66-137">No painel de resultados, selecione **Wizergos Productivity Software** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99b66-137">In the results panel, select **Wizergos Productivity Software**, and then click **Complete** to add the application.</span></span>
   
    ![Seleção do aplicativo na galeria](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="99b66-139">Configurar e testar SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="99b66-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="99b66-140">O objetivo desta seção é mostrar como configurar e testar o SSO do Azure AD com o Wizergos Productivity Software, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="99b66-140">The objective of this section is to show you how to configure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99b66-141">Para que o SSO funcione, o Azure AD precisa saber qual usuário do Wizergos Productivity Software é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99b66-141">For SSO to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software to an user in Azure AD is.</span></span> <span data-ttu-id="99b66-142">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="99b66-142">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span></span>

<span data-ttu-id="99b66-143">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como sendo o valor de **Nome de usuário** no Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="99b66-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="99b66-144">Para configurar e testar o logon único do Azure AD com o BynWizergos Productivity Softwareder, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="99b66-144">To configure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="99b66-145">**[Configurar logon único do Azure AD](#configuring-azure-ad-single-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="99b66-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="99b66-146">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="99b66-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99b66-147">**[Criação de um usuário de teste do Wizergos Productivity Software](#creating-a-wizergos-productivity-software-test-user)** - para ter um equivalente de Brenda Fernandes no Wizergos Productivity Software que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99b66-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="99b66-148">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99b66-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99b66-149">**[Teste do logon único](#testing-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="99b66-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="99b66-150">Configurar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="99b66-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="99b66-151">Nesta seção, você habilitará o logon único do Azure AD no portal clássico e configurará o logon único em seu aplicativo Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="99b66-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="99b66-152">**Para configurar o logon único do Azure AD com o Wizergos Productivity Software, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="99b66-152">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="99b66-153">No portal clássico do Azure, na página de integração de aplicativos do **Wizergos Productivity Software**, clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="99b66-153">In the classic portal, on the **Wizergos Productivity Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar o logon único][6] 
2. <span data-ttu-id="99b66-155">Na página **Como você deseja que os usuários façam logon no Wizergos Productivity Software**, selecione **Logon Único do Azure AD** e clique em **Avançar**:</span><span class="sxs-lookup"><span data-stu-id="99b66-155">On the **How would you like users to sign on to Wizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="99b66-157">Na caixa de diálogo **Definir configurações de aplicativo**, clique em **Avançar**:</span><span class="sxs-lookup"><span data-stu-id="99b66-157">On the **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="99b66-159">Na página **Configurar logon único no Wizergos Productivity Software**, clique em **Baixar certificado** e salve o arquivo no computador:</span><span class="sxs-lookup"><span data-stu-id="99b66-159">On the **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save the file on your computer:</span></span>
   
    ![Configurar o logon único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="99b66-161">Em uma janela diferente do navegador da Web, faça logon em seu locatário do Wizergos Productivity Software como um administrador.</span><span class="sxs-lookup"><span data-stu-id="99b66-161">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="99b66-162">No menu hambúrguer, selecione **Admin**.</span><span class="sxs-lookup"><span data-stu-id="99b66-162">From the hamburger menu, select **Admin**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="99b66-164">Na página de administração no menu à esquerda, selecione **AUTENTICAÇÃO** e clique em **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="99b66-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="99b66-166">Execute as etapas a seguir na seção **AUTENTICAÇÃO** .</span><span class="sxs-lookup"><span data-stu-id="99b66-166">Perform the following steps on **AUTHENTICATION** section.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="99b66-168">Clique no ícone **Carregar** para carregar o certificado baixado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99b66-168">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="99b66-169">Na caixa de texto **URL do Emissor**, coloque o valor de **URL do Emissor** do assistente de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99b66-169">In the **Issuer URL** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="99b66-170">Na caixa de texto **URL de Logon Único**, insira o valor da **URL de serviço de logon único** do assistente de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99b66-170">In the **Single Sign-On URL** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="99b66-171">Na caixa de texto **URL de Logon Único**, insira o valor da **URL de serviço de logoff único** do assistente de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99b66-171">In the **Single Sign-Out URL** textbox put the value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="99b66-172">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="99b66-172">Click **Save** button.</span></span>
9. <span data-ttu-id="99b66-173">No portal clássico, selecione a confirmação da configuração de logon único e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="99b66-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][10]
10. <span data-ttu-id="99b66-175">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="99b66-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Logon Único do AD do Azure][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="99b66-177">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="99b66-177">Create an Azure AD test user</span></span>
<span data-ttu-id="99b66-178">O objetivo desta seção é criar um usuário de teste no Portal Clássico do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="99b66-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="99b66-180">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="99b66-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="99b66-181">No **Portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99b66-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="99b66-183">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="99b66-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="99b66-184">Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="99b66-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="99b66-186">Para abrir a caixa de diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="99b66-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="99b66-188">Na página do diálogo **Conte-nos sobre este usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="99b66-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="99b66-190">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="99b66-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="99b66-191">Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="99b66-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="99b66-192">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="99b66-192">Click **Next**.</span></span>
6. <span data-ttu-id="99b66-193">Na página do diálogo **Perfil do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="99b66-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="99b66-195">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="99b66-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="99b66-196">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="99b66-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="99b66-197">Na caixa de texto **Nome de Exibição**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="99b66-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="99b66-198">Na lista **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="99b66-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="99b66-199">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="99b66-199">Click **Next**.</span></span>
7. <span data-ttu-id="99b66-200">Na página de diálogo **Obter senha temporária**, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="99b66-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="99b66-202">Na página de caixa de diálogo **Obter senha temporária** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="99b66-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="99b66-204">Anote o valor da **Nova Senha**.</span><span class="sxs-lookup"><span data-stu-id="99b66-204">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="99b66-205">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="99b66-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="99b66-206">Criar um usuário de teste do Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="99b66-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="99b66-207">Nesta seção, você deve criar um usuário chamado Brenda Fernandes no Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="99b66-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="99b66-208">Trabalhe com a equipe de suporte do Wizergos Productivity Software via [support@wizergos.com](emailTo:support@wizergos.com) para adicionar os usuários à plataforma do Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="99b66-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="99b66-209">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="99b66-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="99b66-210">O objetivo desta seção é permitir que Brenda Fernandes use o SSO do Azure, concedendo a ela acesso ao Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="99b66-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Wizergos Productivity Software.</span></span>

  ![Atribuir usuário][200]

<span data-ttu-id="99b66-212">**Para atribuir Brenda Fernandes ao Wizergos Productivity Software, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="99b66-212">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="99b66-213">No portal clássico, para abrir o modo de exibição de aplicativos, no modo de exibição de diretório, clique em **Aplicativos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="99b66-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Atribuir usuário][201]
2. <span data-ttu-id="99b66-215">Na lista de aplicativos, selecione **Wizergos Productivity Software**.</span><span class="sxs-lookup"><span data-stu-id="99b66-215">In the applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="99b66-217">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="99b66-217">In the menu on the top, click **Users**.</span></span>
   
    ![Atribuir usuário][203]
4. <span data-ttu-id="99b66-219">Na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="99b66-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="99b66-220">Na barra de ferramentas na parte inferior, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="99b66-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="99b66-222">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="99b66-222">Test single sign-on</span></span>
<span data-ttu-id="99b66-223">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="99b66-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="99b66-224">Quando clica no bloco Wizergos Productivity Software no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="99b66-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="99b66-225">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="99b66-225">Additional resources</span></span>
* [<span data-ttu-id="99b66-226">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="99b66-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99b66-227">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99b66-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
