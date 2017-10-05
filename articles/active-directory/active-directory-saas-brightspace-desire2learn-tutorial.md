---
title: "Tutorial: Integração do Azure Active Directory ao Brightspace by Desire2Learn | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Brightspace by Desire2Learn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7076b476ba71c5d94ae4728e5f6032b0d7e047ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="4dfe9-103">Tutorial: Integração do Active Directory do Azure ao Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="4dfe9-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>

<span data-ttu-id="4dfe9-104">Neste tutorial, você aprende a integrar o Brightspace by Desire2Learn ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4dfe9-104">In this tutorial, you learn how to integrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4dfe9-105">A integração do Brightspace by Desire2Learn ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4dfe9-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4dfe9-106">No Azure AD, é possível controlar quem tem acesso ao Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="4dfe9-106">You can control in Azure AD who has access to Brightspace by Desire2Learn</span></span>
- <span data-ttu-id="4dfe9-107">É possível permitir que os usuários se conectem automaticamente ao Brightspace by Desire2Learn (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4dfe9-107">You can enable your users to automatically get signed-on to Brightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4dfe9-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4dfe9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4dfe9-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4dfe9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4dfe9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4dfe9-110">Prerequisites</span></span>

<span data-ttu-id="4dfe9-111">Para configurar a integração do Azure AD ao Brightspace by Desire2Learn, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4dfe9-111">To configure Azure AD integration with Brightspace by Desire2Learn, you need the following items:</span></span>

- <span data-ttu-id="4dfe9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4dfe9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4dfe9-113">Uma assinatura habilitada para logon único do Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="4dfe9-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4dfe9-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4dfe9-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4dfe9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4dfe9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4dfe9-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4dfe9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4dfe9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4dfe9-118">Scenario description</span></span>
<span data-ttu-id="4dfe9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4dfe9-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4dfe9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4dfe9-121">Adicionando o Brightspace by Desire2Learn por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="4dfe9-121">Adding Brightspace by Desire2Learn from the gallery</span></span>
2. <span data-ttu-id="4dfe9-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4dfe9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-brightspace-by-desire2learn-from-the-gallery"></a><span data-ttu-id="4dfe9-123">Adicionando o Brightspace by Desire2Learn por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="4dfe9-123">Adding Brightspace by Desire2Learn from the gallery</span></span>
<span data-ttu-id="4dfe9-124">Para configurar a integração do Brightspace by Desire2Learn ao Azure AD, você precisa adicionar o Brightspace by Desire2Learn à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-124">To configure the integration of Brightspace by Desire2Learn into Azure AD, you need to add Brightspace by Desire2Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4dfe9-125">**Para adicionar o Brightspace by Desire2Learn por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4dfe9-125">**To add Brightspace by Desire2Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4dfe9-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4dfe9-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4dfe9-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4dfe9-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4dfe9-133">Na caixa de pesquisa, digite **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-133">In the search box, type **Brightspace by Desire2Learn**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_search.png)

5. <span data-ttu-id="4dfe9-135">No painel de resultados, selecione **Brightspace by Desire2Learn** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-135">In the results panel, select **Brightspace by Desire2Learn**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4dfe9-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4dfe9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4dfe9-138">Nesta seção, você configura e testa o logon único do Azure AD com o Brightspace by Desire2Learn, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4dfe9-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Brightspace by Desire2Learn é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Brightspace by Desire2Learn is to a user in Azure AD.</span></span> <span data-ttu-id="4dfe9-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-140">In other words, a link relationship between an Azure AD user and the related user in Brightspace by Desire2Learn needs to be established.</span></span>

<span data-ttu-id="4dfe9-141">No Brightspace by Desire2Learn, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-141">In Brightspace by Desire2Learn, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4dfe9-142">Para configurar e testar o logon único do Azure AD com o Brightspace by Desire2Learn, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4dfe9-142">To configure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4dfe9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4dfe9-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4dfe9-145">**[Criando um usuário de teste do Brightspace by Desire2Learn](#creating-a-brightspace-by-desire2learn-test-user)** – para ter um equivalente de Brenda Fernandes no Brightspace by Desire2Learn que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - to have a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4dfe9-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4dfe9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4dfe9-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4dfe9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4dfe9-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span></span>

<span data-ttu-id="4dfe9-150">**Para configurar o logon único do Azure AD com o Brightspace by Desire2Learn, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4dfe9-150">**To configure Azure AD single sign-on with Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="4dfe9-151">No portal do Azure, na página de integração do aplicativo do **Brightspace by Desire2Learn**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-151">In the Azure portal, on the **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4dfe9-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_samlbase.png)

3. <span data-ttu-id="4dfe9-155">Na seção **Domínio e URLs do Brightspace by Desire2Learn**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4dfe9-155">On the **Brightspace by Desire2Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_url.png)

    <span data-ttu-id="4dfe9-157">a.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-157">a.</span></span> <span data-ttu-id="4dfe9-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="4dfe9-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.tenants.brightspace.com/samlLogin`|
    | `https://<companyname>.desire2learn.com/shibboleth-sp`|

    <span data-ttu-id="4dfe9-159">b.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-159">b.</span></span> <span data-ttu-id="4dfe9-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span><span class="sxs-lookup"><span data-stu-id="4dfe9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4dfe9-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-161">These values are not real.</span></span> <span data-ttu-id="4dfe9-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="4dfe9-163">Contate a [equipe de suporte do Brightspace by Desire2Learn](https://www.d2l.com/contact/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) to get these values.</span></span>
 


4. <span data-ttu-id="4dfe9-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_certificate.png) 

5. <span data-ttu-id="4dfe9-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4dfe9-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4dfe9-168">Para configurar o logon único no lado do **Brightspace by Desire2Learn**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Brightspace by Desire2Learn](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="4dfe9-168">To configure single sign-on on **Brightspace by Desire2Learn** side, you need to send the downloaded **Metadata XML** to [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="4dfe9-169">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4dfe9-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4dfe9-170">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4dfe9-171">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4dfe9-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4dfe9-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4dfe9-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="4dfe9-173">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4dfe9-175">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4dfe9-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4dfe9-176">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4dfe9-178">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4dfe9-180">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4dfe9-182">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4dfe9-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4dfe9-184">a.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-184">a.</span></span> <span data-ttu-id="4dfe9-185">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4dfe9-186">b.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-186">b.</span></span> <span data-ttu-id="4dfe9-187">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4dfe9-188">c.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-188">c.</span></span> <span data-ttu-id="4dfe9-189">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4dfe9-190">d.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-190">d.</span></span> <span data-ttu-id="4dfe9-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-191">Click **Create**.</span></span>
 
### <a name="creating-a-brightspace-by-desire2learn-test-user"></a><span data-ttu-id="4dfe9-192">Criando um usuário de teste do Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="4dfe9-192">Creating a Brightspace by Desire2Learn test user</span></span>

<span data-ttu-id="4dfe9-193">Para permitir que os usuários do AD do Azure façam logon no Brightspace by Desire2Learn, eles devem ser provisionados no Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-193">In order to enable Azure AD users to log into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="4dfe9-194">No caso do Brightspace by Desire2Learn, as contas de usuário precisam ser criadas pela [equipe de suporte do Brightspace by Desire2Learn](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="4dfe9-194">In the case of Brightspace by Desire2Learn, the user accounts need to be created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

>[!NOTE]
><span data-ttu-id="4dfe9-195">Você pode usar qualquer outra ferramenta de criação da conta de usuário do Brightspace by Desire2Learn ou as APIs fornecidas pelo Brightspace by Desire2Learn para provisionar as contas de usuário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4dfe9-196">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4dfe9-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4dfe9-197">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Brightspace by Desire2Learn.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4dfe9-199">**Para atribuir Brenda Fernandes ao Brightspace by Desire2Learn, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4dfe9-199">**To assign Britta Simon to Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="4dfe9-200">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4dfe9-202">Na lista de aplicativos, selecione **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-202">In the applications list, select **Brightspace by Desire2Learn**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_app.png) 

3. <span data-ttu-id="4dfe9-204">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4dfe9-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-206">Click **Add** button.</span></span> <span data-ttu-id="4dfe9-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4dfe9-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4dfe9-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4dfe9-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4dfe9-212">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4dfe9-212">Testing single sign-on</span></span>

<span data-ttu-id="4dfe9-213">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4dfe9-214">Quando você clicar no bloco Brightspace by Desire2Learn no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="4dfe9-214">When you click the Brightspace by Desire2Learn tile in the Access Panel, you should get automatically signed-on to your Brightspace by Desire2Learn application.</span></span>
<span data-ttu-id="4dfe9-215">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4dfe9-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4dfe9-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4dfe9-216">Additional resources</span></span>

* [<span data-ttu-id="4dfe9-217">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4dfe9-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4dfe9-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4dfe9-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_203.png

