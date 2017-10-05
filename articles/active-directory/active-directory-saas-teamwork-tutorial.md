---
title: "Tutorial: Integração do Azure Active Directory com o Teamwork | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Teamwork."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: edd2f9446515531f1147a8abf99295b618b89b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="62ca5-103">Tutorial: Integração do Azure Active Directory ao Teamwork</span><span class="sxs-lookup"><span data-stu-id="62ca5-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="62ca5-104">Neste tutorial, você aprenderá a integrar o Teamwork ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="62ca5-104">In this tutorial, you learn how to integrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62ca5-105">A integração do Teamwork ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="62ca5-105">Integrating Teamwork with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="62ca5-106">No Azure AD, é possível controlar quem tem acesso ao Teamwork</span><span class="sxs-lookup"><span data-stu-id="62ca5-106">You can control in Azure AD who has access to Teamwork</span></span>
- <span data-ttu-id="62ca5-107">Você pode permitir que os usuários façam logon automaticamente no Teamwork (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="62ca5-107">You can enable your users to automatically get signed-on to Teamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62ca5-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="62ca5-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="62ca5-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62ca5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62ca5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="62ca5-110">Prerequisites</span></span>

<span data-ttu-id="62ca5-111">Para configurar a integração do Azure AD ao Teamwork, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="62ca5-111">To configure Azure AD integration with Teamwork, you need the following items:</span></span>

- <span data-ttu-id="62ca5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62ca5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62ca5-113">Uma assinatura do Teamwork habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="62ca5-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="62ca5-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="62ca5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="62ca5-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="62ca5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62ca5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="62ca5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="62ca5-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62ca5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="62ca5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="62ca5-118">Scenario description</span></span>
<span data-ttu-id="62ca5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="62ca5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62ca5-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="62ca5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62ca5-121">Adicionar o Teamwork da galeria</span><span class="sxs-lookup"><span data-stu-id="62ca5-121">Adding Teamwork from the gallery</span></span>
2. <span data-ttu-id="62ca5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62ca5-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-the-gallery"></a><span data-ttu-id="62ca5-123">Adicionar o Teamwork da galeria</span><span class="sxs-lookup"><span data-stu-id="62ca5-123">Adding Teamwork from the gallery</span></span>
<span data-ttu-id="62ca5-124">Para configurar a integração do Teamwork ao Azure AD, é necessário adicionar o Teamwork da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="62ca5-124">To configure the integration of Teamwork into Azure AD, you need to add Teamwork from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="62ca5-125">**Para adicionar o Teamwork da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="62ca5-125">**To add Teamwork from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="62ca5-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62ca5-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="62ca5-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="62ca5-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62ca5-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="62ca5-133">Na caixa de pesquisa, digite **Teamwork**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-133">In the search box, type **Teamwork**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="62ca5-135">No painel de resultados, selecione **Teamwork** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="62ca5-135">In the results panel, select **Teamwork**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62ca5-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62ca5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62ca5-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Teamwork, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="62ca5-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62ca5-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Teamwork é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62ca5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork is to a user in Azure AD.</span></span> <span data-ttu-id="62ca5-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Teamwork.</span><span class="sxs-lookup"><span data-stu-id="62ca5-140">In other words, a link relationship between an Azure AD user and the related user in Teamwork needs to be established.</span></span>

<span data-ttu-id="62ca5-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como sendo o valor do **Nome de usuário** no Teamwork.</span><span class="sxs-lookup"><span data-stu-id="62ca5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamwork.</span></span>

<span data-ttu-id="62ca5-142">Para configurar e testar o logon único do Azure AD com o Teamwork, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="62ca5-142">To configure and test Azure AD single sign-on with Teamwork, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="62ca5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="62ca5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="62ca5-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar logon único do Azure AD com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62ca5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62ca5-145">**[Criar um usuário de teste do Teamwork](#creating-a-teamwork-test-user)** - para ter um equivalente de Brenda Fernandes no Teamwork que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62ca5-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - to have a counterpart of Britta Simon in Teamwork that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="62ca5-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="62ca5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62ca5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="62ca5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62ca5-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="62ca5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62ca5-149">Nesta seção, você habilita o logon único do Azure AD no Portal de Gerenciamento do Azure e configura o logon único em seu aplicativo Teamwork.</span><span class="sxs-lookup"><span data-stu-id="62ca5-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="62ca5-150">**Para configurar o logon único do Azure AD com o Teamwork, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="62ca5-150">**To configure Azure AD single sign-on with Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="62ca5-151">No Portal de Gerenciamento do Azure, na página de integração de aplicativos do **Teamwork**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-151">In the Azure Management portal, on the **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="62ca5-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="62ca5-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="62ca5-155">Na seção **Domínio e URLs do Teamwork**, na caixa de texto **URL de Entrada**, digite uma URL no seguinte padrão: `https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="62ca5-155">On the **Teamwork Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Configurar o logon único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="62ca5-157">Observe que esse não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="62ca5-157">Please note that this is not the real value.</span></span> <span data-ttu-id="62ca5-158">Você precisa atualizar esse valor com a URL de Entrada real.</span><span class="sxs-lookup"><span data-stu-id="62ca5-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="62ca5-159">Para obter esse valor, entre em contato com a [equipe de suporte do Teamwork](mailto:support@teamwork.com).</span><span class="sxs-lookup"><span data-stu-id="62ca5-159">Contact [Teamwork support team](mailto:support@teamwork.com) to get this value.</span></span> 

4. <span data-ttu-id="62ca5-160">Na seção **Certificado de Autenticação SAML**, clique em **Criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="62ca5-162">Na caixa de diálogo **Criar um Novo Certificado**, clique no ícone de calendário e selecione uma **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="62ca5-163">Em seguida, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-163">Then click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="62ca5-165">Na seção **Certificado de Autenticação SAML**, selecione **Ativar o novo certificado** e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="62ca5-167">Na janela pop-up **Certificado de substituição**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="62ca5-169">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="62ca5-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="62ca5-171">Para que o SSO seja configurado para o aplicativo, entre em contato com sua [equipe de suporte do Teamwork](mailto:support@teamwork.com) e forneça os **metadados** baixados.</span><span class="sxs-lookup"><span data-stu-id="62ca5-171">To get SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with the downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62ca5-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62ca5-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="62ca5-173">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62ca5-173">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="62ca5-175">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="62ca5-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="62ca5-176">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-176">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62ca5-178">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="62ca5-178">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62ca5-180">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62ca5-180">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62ca5-182">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="62ca5-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62ca5-184">a.</span><span class="sxs-lookup"><span data-stu-id="62ca5-184">a.</span></span> <span data-ttu-id="62ca5-185">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62ca5-186">b.</span><span class="sxs-lookup"><span data-stu-id="62ca5-186">b.</span></span> <span data-ttu-id="62ca5-187">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="62ca5-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62ca5-188">c.</span><span class="sxs-lookup"><span data-stu-id="62ca5-188">c.</span></span> <span data-ttu-id="62ca5-189">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="62ca5-190">d.</span><span class="sxs-lookup"><span data-stu-id="62ca5-190">d.</span></span> <span data-ttu-id="62ca5-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="62ca5-192">Criar um usuário de teste do Teamwork</span><span class="sxs-lookup"><span data-stu-id="62ca5-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="62ca5-193">Nesta seção, você criará uma usuária chamado Brenda Fernandes no Teamwork.</span><span class="sxs-lookup"><span data-stu-id="62ca5-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="62ca5-194">Trabalhe com a [equipe de suporte do Teamwork](mailto:support@teamwork.com) para adicionar os usuários na plataforma Teamwork.</span><span class="sxs-lookup"><span data-stu-id="62ca5-194">Please work with [Teamwork support team](mailto:support@teamwork.com) to add the users in the Teamwork platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="62ca5-195">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62ca5-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="62ca5-196">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Teamwork.</span><span class="sxs-lookup"><span data-stu-id="62ca5-196">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamwork.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="62ca5-198">**Para atribuir Brenda Fernandes ao Teamwork, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="62ca5-198">**To assign Britta Simon to Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="62ca5-199">No Portal de Gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **Aplicativos empresariais**, depois clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-199">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="62ca5-201">Na lista de aplicativos, selecione **Teamwork**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-201">In the applications list, select **Teamwork**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="62ca5-203">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="62ca5-205">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="62ca5-205">Click **Add** button.</span></span> <span data-ttu-id="62ca5-206">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62ca5-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="62ca5-208">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="62ca5-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="62ca5-209">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62ca5-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62ca5-210">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62ca5-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="62ca5-211">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="62ca5-211">Testing single sign-on</span></span>

<span data-ttu-id="62ca5-212">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="62ca5-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="62ca5-213">Ao clicar no bloco Teamwork no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Teamwork.</span><span class="sxs-lookup"><span data-stu-id="62ca5-213">When you click the Teamwork tile in the Access Panel, you should get automatically signed-on to your Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="62ca5-214">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="62ca5-214">Additional resources</span></span>

* [<span data-ttu-id="62ca5-215">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="62ca5-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62ca5-216">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62ca5-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png