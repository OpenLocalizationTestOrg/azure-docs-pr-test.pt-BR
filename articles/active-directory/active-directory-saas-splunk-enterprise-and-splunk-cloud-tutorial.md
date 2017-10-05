---
title: "Tutorial: Integração do Azure Active Directory com o Splunk Enterprise e o Splunk Cloud | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Splunk Enterprise e o Splunk Cloud."
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
ms.openlocfilehash: b78e9b7161207a74880e912241d5e965b353d1c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="f293e-103">Tutorial: Integração do Azure Active Directory com o Splunk Enterprise e o Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="f293e-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="f293e-104">Neste tutorial, você aprenderá como integrar o Splunk Enterprise e o Splunk Cloud ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f293e-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f293e-105">A integração do Splunk Enterprise e do Splunk Cloud ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="f293e-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f293e-106">Você pode controlar no Azure AD quem tem acesso ao Splunk Enterprise e ao Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="f293e-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="f293e-107">Você pode permitir que seus usuários façam logon automaticamente no Splunk Enterprise e no Splunk Cloud usando SSO (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f293e-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="f293e-108">Gerenciar suas contas em um único local: o Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="f293e-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="f293e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f293e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f293e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f293e-110">Prerequisites</span></span>

<span data-ttu-id="f293e-111">Para configurar a integração do Azure AD com o Splunk Enterprise e o Splunk Cloud, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f293e-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="f293e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f293e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f293e-113">Uma assinatura do Splunk Enterprise ou do Splunk Cloud habilitada para SSO</span><span class="sxs-lookup"><span data-stu-id="f293e-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="f293e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f293e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="f293e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f293e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f293e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f293e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f293e-117">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f293e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f293e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f293e-118">Scenario description</span></span>
<span data-ttu-id="f293e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f293e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="f293e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="f293e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f293e-121">Adicionar o Splunk Enterprise e o Splunk Cloud da galeria</span><span class="sxs-lookup"><span data-stu-id="f293e-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="f293e-122">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f293e-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="f293e-123">Adicionar o Splunk Enterprise e o Splunk Cloud da galeria</span><span class="sxs-lookup"><span data-stu-id="f293e-123">Add Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="f293e-124">Para configurar a integração do Splunk Enterprise e do Splunk Cloud com o Azure AD, você precisará adicionar o Splunk Enterprise e o Splunk Cloud à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="f293e-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f293e-125">**Para adicionar o Splunk Enterprise e o Splunk Cloud por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f293e-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f293e-126">No **Portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f293e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="f293e-128">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="f293e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f293e-129">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="f293e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Aplicativos][2]

4. <span data-ttu-id="f293e-131">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="f293e-131">Click **Add** at the bottom of the page.</span></span>

    ![Aplicativos][3]

5. <span data-ttu-id="f293e-133">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="f293e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Aplicativos][4]

6. <span data-ttu-id="f293e-135">Na caixa de pesquisa, digite **Splunk Enterprise ou Splunk Cloud** .</span><span class="sxs-lookup"><span data-stu-id="f293e-135">In the search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="f293e-137">No painel de resultados, selecione **Splunk Enterprise e Splunk Cloud**  e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f293e-137">In the results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f293e-139">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f293e-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f293e-140">Nesta seção, você configurará e testará o logon único do Azure AD com o Splunk Enterprise e o Splunk Cloud, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="f293e-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f293e-141">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Splunk Enterprise e do Splunk Cloud é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f293e-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="f293e-142">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Splunk Enterprise e do Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f293e-142">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="f293e-143">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD ao valor de **Nome de usuário** no Splunk Enterprise e no Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f293e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="f293e-144">Para configurar e testar o logon único do Azure AD com o Splunk Enterprise e o Splunk Cloud, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f293e-144">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f293e-145">**[Configurar logon único do Azure AD](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f293e-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f293e-146">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f293e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f293e-147">**[Criação de um usuário de teste do Splunk Enterprise e do Splunk Cloud ](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**: para ter um equivalente de Brenda Fernandes no Splunk Enterprise e no Splunk Cloud que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f293e-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f293e-148">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f293e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f293e-149">**[Teste do logon único](#testing-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="f293e-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f293e-150">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f293e-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f293e-151">Nesta seção, você habilitará o SSO do Azure AD no Portal Clássico e configurará o SSO em seu aplicativo Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f293e-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="f293e-152">**Para configurar o logon único do Azure AD com o Splunk Enterprise e o Splunk Cloud, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f293e-152">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="f293e-153">No portal clássico, na página de integração de aplicativos do **Splunk Enterprise e Splunk Cloud** , clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="f293e-153">In the classic portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurar o logon único][6] 

2. <span data-ttu-id="f293e-155">Na página **Como você deseja que os usuários façam logon no Splunk Enterprise e no Splunk Cloud** , selecione **Logon Único do Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f293e-155">On the **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="f293e-157">Na página de diálogo **Definir Configurações de Aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f293e-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="f293e-159">Na caixa de texto **URL de Logon**, digite a URL usada pelos usuários para fazer logon no seu aplicativo Splunk Enterprise e Splunk Cloud usando o seguinte padrão: `https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="f293e-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Splunk Enterprise and Splunk Cloud application using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="f293e-160">Na caixa de texto **Identificador**, digite a URL de seu Servidor Splunk.</span><span class="sxs-lookup"><span data-stu-id="f293e-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="f293e-161">Na caixa de texto **URL de Resposta**, digite a URL no seguinte padrão: `https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="f293e-161">In the **Reply URL** textbox, type the URL with the following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="f293e-162">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f293e-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="f293e-163">Na página **Configurar o logon único no Splunk Enterprise e o Splunk Cloud**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f293e-163">On the **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform the following steps:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="f293e-165">Clique em **Baixar metadados**e salve o arquivo no computador.</span><span class="sxs-lookup"><span data-stu-id="f293e-165">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="f293e-166">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f293e-166">Click **Next**.</span></span>

5. <span data-ttu-id="f293e-167">Para que o SSO seja configurado para seu aplicativo, entre em contato com a equipe de suporte do Splunk Enterprise e do Splunk Cloud e forneça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f293e-167">To get SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with the following:</span></span>

    * <span data-ttu-id="f293e-168">Os **metadados de federação** baixados</span><span class="sxs-lookup"><span data-stu-id="f293e-168">The downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="f293e-169">No portal clássico, selecione a confirmação da configuração de logon único e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f293e-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Logon Único do AD do Azure][10]

7. <span data-ttu-id="f293e-171">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="f293e-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Logon Único do AD do Azure][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f293e-173">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f293e-173">Create an Azure AD test user</span></span>
<span data-ttu-id="f293e-174">Nesta seção, você criará uma usuária de teste no portal clássico chamada Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f293e-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="f293e-176">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f293e-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f293e-177">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f293e-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="f293e-179">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="f293e-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f293e-180">Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="f293e-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f293e-182">Para abrir a caixa de diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="f293e-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="f293e-184">Na página do diálogo **Conte-nos sobre este usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f293e-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="f293e-186">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="f293e-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="f293e-187">Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="f293e-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="f293e-188">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f293e-188">Click **Next**.</span></span>

6.  <span data-ttu-id="f293e-189">Na página do diálogo **Perfil do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f293e-189">On the **User Profile** dialog page, perform the following steps:</span></span>
  
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="f293e-191">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="f293e-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="f293e-192">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f293e-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="f293e-193">Na caixa de texto **Nome de Exibição**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f293e-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="f293e-194">Na lista **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="f293e-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="f293e-195">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f293e-195">Click **Next**.</span></span>

7. <span data-ttu-id="f293e-196">Na página de diálogo **Obter senha temporária**, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="f293e-196">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="f293e-198">Na página de caixa de diálogo **Obter senha temporária** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f293e-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="f293e-200">Anote o valor da **Nova Senha**.</span><span class="sxs-lookup"><span data-stu-id="f293e-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="f293e-201">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="f293e-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="f293e-202">Criar um usuário de teste do Splunk Enterprise e do Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="f293e-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="f293e-203">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Splunk Enterprise e no Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f293e-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="f293e-204">Trabalhe com a equipe de suporte do Splunk Enterprise e do Splunk Cloud para adicionar os usuários à plataforma do Splunk Enterprise e do Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f293e-204">Please work with Splunk Enterprise and Splunk Cloud support team to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f293e-205">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f293e-205">Assign the Azure AD test user</span></span>

<span data-ttu-id="f293e-206">Nesta seção, você habilitará Brenda Fernandes a usar o SSO do Azure concedendo-lhe acesso ao Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f293e-206">In this section, you enable Britta Simon to use Azure SSOy granting her access to Splunk Enterprise and Splunk Cloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f293e-208">**Para adicionar Brenda Fernandes ao Splunk Enterprise e o Splunk Cloud, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f293e-208">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="f293e-209">No portal clássico, para abrir o modo de exibição de aplicativos, no modo de exibição de diretório, clique em **Aplicativos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="f293e-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f293e-211">Na lista de aplicativos, selecione **Splunk Enterprise e Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="f293e-211">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="f293e-213">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="f293e-213">In the menu on the top, click **Users**.</span></span>

    ![Atribuir usuário][203]

4. <span data-ttu-id="f293e-215">Na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f293e-215">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="f293e-216">Na barra de ferramentas na parte inferior, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="f293e-216">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="f293e-218">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="f293e-218">Test single sign-on</span></span>

<span data-ttu-id="f293e-219">Nesta seção, você testará sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="f293e-219">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="f293e-220">Ao clicar no bloco do Splunk Enterprise e do Splunk Cloud no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f293e-220">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f293e-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f293e-221">Additional resources</span></span>

* [<span data-ttu-id="f293e-222">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f293e-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f293e-223">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f293e-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


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
