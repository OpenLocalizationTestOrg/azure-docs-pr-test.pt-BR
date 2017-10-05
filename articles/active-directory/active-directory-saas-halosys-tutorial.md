---
title: "Tutorial: integração do Azure Active Directory com o Halosys | Microsoft Docs"
description: "Saiba como usar o Halosys com o Azure Active Directory para habilitar logon único, provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18c5cd8eb4ca211f8ae2b8dd994c0e8c48625a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="75038-103">Tutorial: integração do Azure Active Directory com o Halosys</span><span class="sxs-lookup"><span data-stu-id="75038-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="75038-104">Neste tutorial, você aprenderá a integrar o Halosys ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="75038-104">In this tutorial, you learn how to integrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75038-105">Integrar o Halosys ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="75038-105">Integrating Halosys with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="75038-106">Você pode controlar no Azure AD quem tem acesso ao Halosys</span><span class="sxs-lookup"><span data-stu-id="75038-106">You can control in Azure AD who has access to Halosys</span></span>
- <span data-ttu-id="75038-107">Você pode permitir que seus usuários façam logon automaticamente no Halosys (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="75038-107">You can enable your users to automatically get signed-on to Halosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="75038-108">Gerenciar suas contas em um único local: o Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="75038-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="75038-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="75038-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75038-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="75038-110">Prerequisites</span></span>

<span data-ttu-id="75038-111">Para configurar a integração do Azure AD ao Halosys, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="75038-111">To configure Azure AD integration with Halosys, you need the following items:</span></span>

- <span data-ttu-id="75038-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="75038-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75038-113">Uma assinatura do Halosys habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="75038-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="75038-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="75038-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="75038-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="75038-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75038-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="75038-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="75038-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75038-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="75038-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="75038-118">Scenario description</span></span>
<span data-ttu-id="75038-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="75038-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="75038-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="75038-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75038-121">Como adicionar o Halosys da galeria</span><span class="sxs-lookup"><span data-stu-id="75038-121">Adding Halosys from the gallery</span></span>
2. <span data-ttu-id="75038-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="75038-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-the-gallery"></a><span data-ttu-id="75038-123">Como adicionar o Halosys da galeria</span><span class="sxs-lookup"><span data-stu-id="75038-123">Adding Halosys from the gallery</span></span>
<span data-ttu-id="75038-124">Para configurar a integração do Halosys ao Azure AD, você precisará adicionar o Halosys da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="75038-124">To configure the integration of Halosys into Azure AD, you need to add Halosys from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="75038-125">**Para adicionar o Halosys da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="75038-125">**To add Halosys from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="75038-126">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="75038-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="75038-128">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="75038-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="75038-129">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="75038-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Aplicativos][2]

4. <span data-ttu-id="75038-131">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="75038-131">Click **Add** at the bottom of the page.</span></span>

    ![Aplicativos][3]

5. <span data-ttu-id="75038-133">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="75038-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Aplicativos][4]

6. <span data-ttu-id="75038-135">Na caixa de pesquisa, digite **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="75038-135">In the search box, type **Halosys**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="75038-137">No painel de resultados, selecione **Halosys** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="75038-137">In the results pane, select **Halosys**, and then click **Complete** to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="75038-139">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="75038-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="75038-140">Nesta seção, você configurará e testará o logon único do Azure AD com o Halosys, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="75038-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="75038-141">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Halosys é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75038-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Halosys is to a user in Azure AD.</span></span> <span data-ttu-id="75038-142">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Halosys.</span><span class="sxs-lookup"><span data-stu-id="75038-142">In other words, a link relationship between an Azure AD user and the related user in Halosys needs to be established.</span></span>

<span data-ttu-id="75038-143">Essa relação de vinculação é estabelecida por meio da atribuição do valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Halosys.</span><span class="sxs-lookup"><span data-stu-id="75038-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Halosys.</span></span>

<span data-ttu-id="75038-144">Para configurar e testar o logon único do Azure AD com o Halosys, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="75038-144">To configure and test Azure AD single sign-on with Halosys, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="75038-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="75038-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="75038-146">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar logon único do Azure AD com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="75038-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75038-147">**[Criando um usuário de teste do Halosys](#creating-a-halosys-test-user)**: para ter um equivalente de Brenda Fernandes no Halosys que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75038-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - to have a counterpart of Britta Simon in Halosys that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="75038-148">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="75038-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75038-149">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="75038-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="75038-150">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="75038-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="75038-151">Nesta seção, você habilitará o logon único do Azure AD no portal clássico e configurará o logon único no aplicativo do Halosys.</span><span class="sxs-lookup"><span data-stu-id="75038-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="75038-152">**Para configurar o logon único do Azure AD com o Halosys, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="75038-152">**To configure Azure AD single sign-on with Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="75038-153">No portal clássico, na página de integração de aplicativos do **Halosys**, clique em **Configurar logon único** para abrir a caixa de diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="75038-153">In the classic portal, on the **Halosys** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurar Logon Único][6] 

2. <span data-ttu-id="75038-155">Na página **Como você deseja que os usuários entrem no Halosys**, selecione **Logon Único do Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="75038-155">On the **How would you like users to sign on to Halosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="75038-157">Na página de diálogo **Definir Configurações de Aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="75038-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="75038-159">a.</span><span class="sxs-lookup"><span data-stu-id="75038-159">a.</span></span> <span data-ttu-id="75038-160">Na caixa de texto **URL de entrada**, digite a URL usada pelos usuários para fazer logon no seu aplicativo Halosys usando o seguinte padrão: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="75038-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Halosys application using the following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="75038-161">b.Na caixa de texto **URL de Identificador**, digite a URL no seguinte padrão: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="75038-161">b.In the **Identifier URL** textbox, type the URL in the following pattern: `https://<company-name>.Halosys.com`.</span></span>   
         
4. <span data-ttu-id="75038-162">Na página **Configurar logon único no Halosys**, clique em **Baixar metadados** e salve o arquivo de metadados no computador:</span><span class="sxs-lookup"><span data-stu-id="75038-162">On the **Configure single sign-on at Halosys** page, click **Download metadata**, and then save the file on your computer:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="75038-164">Para que o SSO seja configurado para seu aplicativo, entre em contato com a equipe de suporte do Halosys e forneça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="75038-164">To get SSO configured for your application, contact Halosys support team and provide them with the following:</span></span>

    <span data-ttu-id="75038-165">• O **arquivo de metadados** baixado</span><span class="sxs-lookup"><span data-stu-id="75038-165">• The downloaded **metadata file**</span></span>
    
    <span data-ttu-id="75038-166">• A **URL de SSO do SAML**</span><span class="sxs-lookup"><span data-stu-id="75038-166">• The **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="75038-167">No portal clássico, selecione a confirmação da configuração de logon único e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="75038-167">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Logon Único do AD do Azure][10]

7. <span data-ttu-id="75038-169">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="75038-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Logon Único do AD do Azure][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="75038-171">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="75038-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="75038-172">Nesta seção, você criará uma usuária de teste no portal clássico chamada Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="75038-172">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Criar um usuário do AD do Azure][20]

<span data-ttu-id="75038-174">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="75038-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="75038-175">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="75038-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="75038-177">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="75038-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="75038-178">Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="75038-178">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="75038-180">Para abrir a caixa de diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="75038-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="75038-182">Sobre o **Conte-nos sobre este usuário** caixa de diálogo página, execute as seguintes etapas: ![criando um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="75038-182">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="75038-183">a.</span><span class="sxs-lookup"><span data-stu-id="75038-183">a.</span></span> <span data-ttu-id="75038-184">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="75038-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="75038-185">b.</span><span class="sxs-lookup"><span data-stu-id="75038-185">b.</span></span> <span data-ttu-id="75038-186">Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="75038-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="75038-187">c.</span><span class="sxs-lookup"><span data-stu-id="75038-187">c.</span></span> <span data-ttu-id="75038-188">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="75038-188">Click **Next**.</span></span>

6.  <span data-ttu-id="75038-189">Na caixa de diálogo **perfil de usuário**, realize as etapas a seguir: ![criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="75038-189">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="75038-190">a.</span><span class="sxs-lookup"><span data-stu-id="75038-190">a.</span></span> <span data-ttu-id="75038-191">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="75038-191">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="75038-192">b.</span><span class="sxs-lookup"><span data-stu-id="75038-192">b.</span></span> <span data-ttu-id="75038-193">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="75038-193">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="75038-194">c.</span><span class="sxs-lookup"><span data-stu-id="75038-194">c.</span></span> <span data-ttu-id="75038-195">Na caixa de texto **Nome de Exibição**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="75038-195">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="75038-196">d.</span><span class="sxs-lookup"><span data-stu-id="75038-196">d.</span></span> <span data-ttu-id="75038-197">Na lista **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="75038-197">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="75038-198">e.</span><span class="sxs-lookup"><span data-stu-id="75038-198">e.</span></span> <span data-ttu-id="75038-199">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="75038-199">Click **Next**.</span></span>

7. <span data-ttu-id="75038-200">Na página de diálogo **Obter senha temporária**, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="75038-200">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="75038-202">Na página de caixa de diálogo **Obter senha temporária** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="75038-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="75038-204">a.</span><span class="sxs-lookup"><span data-stu-id="75038-204">a.</span></span> <span data-ttu-id="75038-205">Anote o valor da **Nova Senha**.</span><span class="sxs-lookup"><span data-stu-id="75038-205">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="75038-206">b.</span><span class="sxs-lookup"><span data-stu-id="75038-206">b.</span></span> <span data-ttu-id="75038-207">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="75038-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="75038-208">Criando um usuário de teste do Halosys</span><span class="sxs-lookup"><span data-stu-id="75038-208">Creating a Halosys test user</span></span>

<span data-ttu-id="75038-209">Nesta seção, você criará um usuário chamado Brenda Fernandes no Halosys.</span><span class="sxs-lookup"><span data-stu-id="75038-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="75038-210">Trabalhe com a equipe de suporte para adicionar usuários à plataforma Halosys.</span><span class="sxs-lookup"><span data-stu-id="75038-210">Please work with Halosys support team to add the users in the Halosys platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="75038-211">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="75038-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="75038-212">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Halosys.</span><span class="sxs-lookup"><span data-stu-id="75038-212">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Halosys.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="75038-214">**Para atribuir Brenda Fernandes ao Halosys, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="75038-214">**To assign Britta Simon to Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="75038-215">No portal clássico, para abrir o modo de exibição de aplicativos, no modo de exibição de diretório, clique em **Aplicativos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="75038-215">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="75038-217">Na lista de aplicativos, selecione **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="75038-217">In the applications list, select **Halosys**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="75038-219">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="75038-219">In the menu on the top, click **Users**.</span></span>

    ![Atribuir usuário][203]

4. <span data-ttu-id="75038-221">Na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="75038-221">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="75038-222">Na barra de ferramentas na parte inferior, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="75038-222">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Atribuir usuário][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="75038-224">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="75038-224">Testing single sign-on</span></span>

<span data-ttu-id="75038-225">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="75038-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="75038-226">Quando você clicar no bloco Halosys no Painel de Acesso, deverá fazer logon automaticamente no seu aplicativo Halosys.</span><span class="sxs-lookup"><span data-stu-id="75038-226">When you click the Halosys tile in the Access Panel, you should get automatically signed-on to your Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="75038-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="75038-227">Additional resources</span></span>

* [<span data-ttu-id="75038-228">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="75038-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75038-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="75038-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
