---
title: "Tutorial: Integração do Azure Active Directory com o Soonr Workplace | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Soonr Workplace."
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
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="c4eca-103">Tutorial: Integração do Active Directory do Azure com o Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="c4eca-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="c4eca-104">O objetivo desse tutorial é mostrar como integrar o Soonr Workplace ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c4eca-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="c4eca-105">A integração do Soonr Workplace ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c4eca-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c4eca-106">No AD do Azure, você pode controlar quem tem acesso ao Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="c4eca-106">You can control in Azure AD who has access to Soonr Workplace</span></span>
- <span data-ttu-id="c4eca-107">Você pode habilitar o logon automático de seus usuários no Soonr Workplace (Logon único) com as contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4eca-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4eca-108">Gerenciar suas contas em um único local: o Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="c4eca-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="c4eca-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4eca-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4eca-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c4eca-110">Prerequisites</span></span>

<span data-ttu-id="c4eca-111">Para configurar a integração do AD do Azure ao Soonr Workplace, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c4eca-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span></span>

- <span data-ttu-id="c4eca-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4eca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4eca-113">Uma assinatura do Soonr Workplace com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="c4eca-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="c4eca-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c4eca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="c4eca-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c4eca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4eca-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c4eca-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c4eca-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4eca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="c4eca-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c4eca-118">Scenario description</span></span>
<span data-ttu-id="c4eca-119">O objetivo deste tutorial é permitir que você teste o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c4eca-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="c4eca-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c4eca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4eca-121">Como adicionar o Soonr Workplace a partir da Galeria</span><span class="sxs-lookup"><span data-stu-id="c4eca-121">Adding Soonr Workplace from the gallery</span></span>
2. <span data-ttu-id="c4eca-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4eca-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-the-gallery"></a><span data-ttu-id="c4eca-123">Como adicionar o Soonr Workplace a partir da Galeria</span><span class="sxs-lookup"><span data-stu-id="c4eca-123">Adding Soonr Workplace from the gallery</span></span>
<span data-ttu-id="c4eca-124">Para configurar a integração do Soonr Workplace ao AD do Azure, você precisa adicionar o Soonr Workplace da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c4eca-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c4eca-125">**Para adicionar o Soonr Workplace da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c4eca-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c4eca-126">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4eca-128">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="c4eca-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="c4eca-129">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="c4eca-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Aplicativos][2]

4. <span data-ttu-id="c4eca-131">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="c4eca-131">Click **Add** at the bottom of the page.</span></span>

    ![Aplicativos][3]

5. <span data-ttu-id="c4eca-133">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
 
    ![Aplicativos][4]

6. <span data-ttu-id="c4eca-135">Na caixa de pesquisa, digite **Soonr Workplace**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-135">In the search box, type **Soonr Workplace**.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="c4eca-137">No painel de resultados, selecione **Soonr Workplace** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c4eca-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4eca-139">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4eca-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4eca-140">O objetivo desta seção é mostrar como configurar e testar logon único do AD do Azure com o Soonr Workplace, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="c4eca-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c4eca-141">Para que o logon único funcione, o AD do Azure precisa saber qual usuário do Soonr Workplace é equivalente a um usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4eca-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span></span> <span data-ttu-id="c4eca-142">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado do Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c4eca-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span></span>  

<span data-ttu-id="c4eca-143">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como sendo o valor de **Nome de usuário** no Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c4eca-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="c4eca-144">Para configurar e testar o logon único do AD do Azure com o Soonr Workplace, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c4eca-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c4eca-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c4eca-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c4eca-146">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c4eca-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4eca-147">**[Criar um usuário de teste do Soonr Workplace](#creating-a-soonr-workplace-test-user)** : para ter um equivalente de Brenda Fernandes no Soonr Workplace que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4eca-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c4eca-148">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4eca-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4eca-149">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c4eca-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4eca-150">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4eca-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4eca-151">Nesta seção, você habilitará o logon único do Azure AD no portal clássico e configurará o logon único no aplicativo do Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c4eca-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="c4eca-152">**Para configurar o logon único do AD do Azure com o Soonr Workplace, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c4eca-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="c4eca-153">No portal clássico do Azure, na página de integração de aplicativos do **Soonr Workplace**, clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![Configurar Logon Único][6] 

2. <span data-ttu-id="c4eca-155">Na página **Como você deseja que os usuários façam logon no Soonr Workplace**, selecione **Logon Único do Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="c4eca-157">Na página do diálogo **Definir Configurações do Aplicativo** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c4eca-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="c4eca-159">a.</span><span class="sxs-lookup"><span data-stu-id="c4eca-159">a.</span></span> <span data-ttu-id="c4eca-160">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="c4eca-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="c4eca-161">b.</span><span class="sxs-lookup"><span data-stu-id="c4eca-161">b.</span></span> <span data-ttu-id="c4eca-162">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4eca-163">Observe que esse não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="c4eca-163">Please note that this is not the real value.</span></span> <span data-ttu-id="c4eca-164">Você precisa atualizar esse valor com a URL de Entrada real.</span><span class="sxs-lookup"><span data-stu-id="c4eca-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="c4eca-165">Entre em contato com a equipe de suporte do Soonr Workplace para obter este valor.</span><span class="sxs-lookup"><span data-stu-id="c4eca-165">Contact Soonr Workplace support team to get this value.</span></span>

4. <span data-ttu-id="c4eca-166">Na página **Configurar o logon único no Soonr Workplace**, clique em **Baixar metadados** e salve o arquivo no seu computador:</span><span class="sxs-lookup"><span data-stu-id="c4eca-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="c4eca-168">Para que o SSO seja configurado para seu aplicativo, entre em contato com a equipe de suporte do Soonr Workplace e forneça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c4eca-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span></span> 

    <span data-ttu-id="c4eca-169">• O arquivo de **Metadados** baixado</span><span class="sxs-lookup"><span data-stu-id="c4eca-169">•  The downloaded **Metadata** file</span></span>

    <span data-ttu-id="c4eca-170">• A **URL do Emissor**</span><span class="sxs-lookup"><span data-stu-id="c4eca-170">•  The **Issuer URL**</span></span>

    <span data-ttu-id="c4eca-171">• A **URL de SSO do SAML**</span><span class="sxs-lookup"><span data-stu-id="c4eca-171">•  The **SAML SSO URL**</span></span>

    <span data-ttu-id="c4eca-172">• A **URL do Serviço de Logoff Único**</span><span class="sxs-lookup"><span data-stu-id="c4eca-172">•  The **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="c4eca-173">Este aplicativo é substituído pelo <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> e você pode consultar <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">este</a> tutorial para configurar o aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4eca-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span></span>
   
6. <span data-ttu-id="c4eca-174">No portal clássico do Azure, selecione a confirmação da configuração de logon único e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Logon Único do AD do Azure][10]

7. <span data-ttu-id="c4eca-176">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Logon Único do AD do Azure][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4eca-178">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4eca-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4eca-179">O objetivo desta seção é criar um usuário de teste no Portal Clássico do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c4eca-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="c4eca-181">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c4eca-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c4eca-182">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="c4eca-184">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="c4eca-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="c4eca-185">Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4eca-187">Para abrir a caixa de diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="c4eca-189">Na página do diálogo **Conte-nos sobre este usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c4eca-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="c4eca-191">a.</span><span class="sxs-lookup"><span data-stu-id="c4eca-191">a.</span></span> <span data-ttu-id="c4eca-192">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="c4eca-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="c4eca-193">b.</span><span class="sxs-lookup"><span data-stu-id="c4eca-193">b.</span></span> <span data-ttu-id="c4eca-194">Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4eca-195">c.</span><span class="sxs-lookup"><span data-stu-id="c4eca-195">c.</span></span> <span data-ttu-id="c4eca-196">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-196">Click **Next**.</span></span>

6.  <span data-ttu-id="c4eca-197">Na página do diálogo **Perfil do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c4eca-197">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="c4eca-199">a.</span><span class="sxs-lookup"><span data-stu-id="c4eca-199">a.</span></span> <span data-ttu-id="c4eca-200">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-200">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="c4eca-201">b.</span><span class="sxs-lookup"><span data-stu-id="c4eca-201">b.</span></span> <span data-ttu-id="c4eca-202">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-202">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="c4eca-203">c.</span><span class="sxs-lookup"><span data-stu-id="c4eca-203">c.</span></span> <span data-ttu-id="c4eca-204">Na caixa de texto **Nome de Exibição**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="c4eca-205">d.</span><span class="sxs-lookup"><span data-stu-id="c4eca-205">d.</span></span> <span data-ttu-id="c4eca-206">Na lista **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-206">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="c4eca-207">e.</span><span class="sxs-lookup"><span data-stu-id="c4eca-207">e.</span></span> <span data-ttu-id="c4eca-208">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-208">Click **Next**.</span></span>

7. <span data-ttu-id="c4eca-209">Na página de diálogo **Obter senha temporária**, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-209">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="c4eca-211">Na página de caixa de diálogo **Obter senha temporária** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c4eca-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="c4eca-213">a.</span><span class="sxs-lookup"><span data-stu-id="c4eca-213">a.</span></span> <span data-ttu-id="c4eca-214">Anote o valor da **Nova Senha**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-214">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="c4eca-215">b.</span><span class="sxs-lookup"><span data-stu-id="c4eca-215">b.</span></span> <span data-ttu-id="c4eca-216">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="c4eca-217">Criar um usuário de teste do Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="c4eca-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="c4eca-218">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c4eca-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="c4eca-219">Trabalhe com a equipe de suporte do Soonr Workplace para criar um usuário na plataforma.</span><span class="sxs-lookup"><span data-stu-id="c4eca-219">Please work with Soonr Workplace support team to create a user in the platform.</span></span> <span data-ttu-id="c4eca-220">Você pode gerar o tíquete de suporte do Soonr <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">aqui</a>.</span><span class="sxs-lookup"><span data-stu-id="c4eca-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c4eca-221">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4eca-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c4eca-222">O objetivo desta seção é habilitar Brenda Fernandes a usar o logon único do Azure, concedendo a ela acesso ao Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c4eca-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c4eca-224">**Para atribuir Brenda Fernandes ao Soonr Workplace, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c4eca-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="c4eca-225">No portal clássico do Azure, para abrir a exibição de aplicativos, na exibição de diretório, clique em **Aplicativos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="c4eca-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c4eca-227">Na lista de aplicativos, selecione **Soonr Workplace**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-227">In the applications list, select **Soonr Workplace**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="c4eca-229">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-229">In the menu on the top, click **Users**.</span></span>

    ![Atribuir usuário][203] 

1. <span data-ttu-id="c4eca-231">Na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-231">In the Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="c4eca-232">Na barra de ferramentas na parte inferior, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="c4eca-232">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Atribuir usuário][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="c4eca-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c4eca-234">Testing single sign-on</span></span>

<span data-ttu-id="c4eca-235">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c4eca-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="c4eca-236">Quando você clica no bloco Soonr Workplace no Painel de Acesso, você deve ser conectado automaticamente ao seu aplicativo Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="c4eca-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c4eca-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c4eca-237">Additional resources</span></span>

* [<span data-ttu-id="c4eca-238">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c4eca-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4eca-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c4eca-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


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
