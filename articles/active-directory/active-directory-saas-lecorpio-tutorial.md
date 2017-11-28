---
title: "Tutorial: integração do Azure Active Directory ao Lecorpio | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Lecorpio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 35c94e2d9d8a938971f85ea732a74a7e1655545e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="9cadb-103">Tutorial: integração do Azure Active Directory com o Lecorpio</span><span class="sxs-lookup"><span data-stu-id="9cadb-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="9cadb-104">Neste tutorial, você aprenderá a integrar o Lecorpio ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9cadb-104">In this tutorial, you learn how to integrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cadb-105">A integração do Lecorpio ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="9cadb-105">Integrating Lecorpio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9cadb-106">Você pode controlar no Azure AD quem tem acesso ao Lecorpio</span><span class="sxs-lookup"><span data-stu-id="9cadb-106">You can control in Azure AD who has access to Lecorpio</span></span>
- <span data-ttu-id="9cadb-107">Você pode permitir que seus usuários façam logon automaticamente em Lecorpio (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cadb-107">You can enable your users to automatically get signed-on to Lecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9cadb-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9cadb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9cadb-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9cadb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cadb-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9cadb-110">Prerequisites</span></span>

<span data-ttu-id="9cadb-111">Para configurar a integração do Azure AD ao Lecorpio, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9cadb-111">To configure Azure AD integration with Lecorpio, you need the following items:</span></span>

- <span data-ttu-id="9cadb-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9cadb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9cadb-113">Uma assinatura habilitada para logon único do Lecorpio</span><span class="sxs-lookup"><span data-stu-id="9cadb-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9cadb-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9cadb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9cadb-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9cadb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cadb-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9cadb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9cadb-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cadb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9cadb-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9cadb-118">Scenario description</span></span>
<span data-ttu-id="9cadb-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9cadb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cadb-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="9cadb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cadb-121">Adicionando o Lecorpio da galeria</span><span class="sxs-lookup"><span data-stu-id="9cadb-121">Adding Lecorpio from the gallery</span></span>
2. <span data-ttu-id="9cadb-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9cadb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-the-gallery"></a><span data-ttu-id="9cadb-123">Adicionando o Lecorpio da galeria</span><span class="sxs-lookup"><span data-stu-id="9cadb-123">Adding Lecorpio from the gallery</span></span>
<span data-ttu-id="9cadb-124">Para configurar a integração do Lecorpio ao Azure AD, você precisa adicionar o Lecorpio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9cadb-124">To configure the integration of Lecorpio into Azure AD, you need to add Lecorpio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9cadb-125">**Para adicionar o Lecorpio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9cadb-125">**To add Lecorpio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9cadb-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9cadb-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9cadb-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9cadb-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cadb-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9cadb-133">Na caixa de pesquisa, digite **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-133">In the search box, type **Lecorpio**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="9cadb-135">No painel de resultados, selecione **Lecorpio** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9cadb-135">In the results panel, select **Lecorpio**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9cadb-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9cadb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9cadb-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Lecorpio, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="9cadb-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9cadb-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Lecorpio é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cadb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lecorpio is to a user in Azure AD.</span></span> <span data-ttu-id="9cadb-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="9cadb-140">In other words, a link relationship between an Azure AD user and the related user in Lecorpio needs to be established.</span></span>

<span data-ttu-id="9cadb-141">Essa relação de vinculação é estabelecida por meio da atribuição do valor de **nome de usuário** no Azure AD como o valor de **Nome de Usuário** no Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="9cadb-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lecorpio.</span></span>

<span data-ttu-id="9cadb-142">Para configurar e testar o logon único do Azure AD com o Lecorpio, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="9cadb-142">To configure and test Azure AD single sign-on with Lecorpio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9cadb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9cadb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9cadb-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9cadb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cadb-145">**[Criação de um usuário de teste do Lecorpio](#creating-a-lecorpio-test-user)** – para ter um equivalente de Brenda Fernandes no Lecorpio que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cadb-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - to have a counterpart of Britta Simon in Lecorpio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9cadb-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cadb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cadb-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="9cadb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9cadb-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cadb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9cadb-149">Nesta seção, você vai habilitar o logon único do Azure AD no Portal do Azure e configurar o logon único em seu aplicativo Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="9cadb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="9cadb-150">**Para configurar o logon único do Azure AD com o Lecorpio, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9cadb-150">**To configure Azure AD single sign-on with Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="9cadb-151">No Portal do Azure, na página de integração de aplicativos do **Lecorpio**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-151">In the Azure portal, on the **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9cadb-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="9cadb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="9cadb-155">Na seção **Domínio e URLs do Lecorpio**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9cadb-155">On the **Lecorpio Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="9cadb-157">a.</span><span class="sxs-lookup"><span data-stu-id="9cadb-157">a.</span></span> <span data-ttu-id="9cadb-158">Na caixa de texto **URL de Logon**, digite o valor usando o seguinte padrão: `https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="9cadb-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="9cadb-159">b.</span><span class="sxs-lookup"><span data-stu-id="9cadb-159">b.</span></span> <span data-ttu-id="9cadb-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="9cadb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9cadb-161">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="9cadb-161">These values are not the real.</span></span> <span data-ttu-id="9cadb-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="9cadb-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="9cadb-163">Aqui, sugerimos que você use o valor exclusivo de cadeia de caracteres no Identificador.</span><span class="sxs-lookup"><span data-stu-id="9cadb-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="9cadb-164">Contate a [equipe de suporte do Cliente Lecorpio](mailto:info@lecorpio.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="9cadb-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to get these values.</span></span> 
 
4. <span data-ttu-id="9cadb-165">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9cadb-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="9cadb-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9cadb-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9cadb-169">Para configurar o logon único no lado do **Lecorpio**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="9cadb-169">To configure single sign-on on **Lecorpio** side, you need to send the downloaded **Metadata XML** to [Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="9cadb-170">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="9cadb-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9cadb-171">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9cadb-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9cadb-172">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9cadb-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9cadb-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9cadb-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="9cadb-174">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9cadb-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9cadb-176">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9cadb-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9cadb-177">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9cadb-179">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9cadb-179">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9cadb-181">Na parte superior da caixa de diálogo, clique em **Adicionar** para abrir a caixa de diálogo **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-181">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9cadb-183">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9cadb-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9cadb-185">a.</span><span class="sxs-lookup"><span data-stu-id="9cadb-185">a.</span></span> <span data-ttu-id="9cadb-186">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cadb-187">b.</span><span class="sxs-lookup"><span data-stu-id="9cadb-187">b.</span></span> <span data-ttu-id="9cadb-188">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9cadb-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9cadb-189">c.</span><span class="sxs-lookup"><span data-stu-id="9cadb-189">c.</span></span> <span data-ttu-id="9cadb-190">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9cadb-191">d.</span><span class="sxs-lookup"><span data-stu-id="9cadb-191">d.</span></span> <span data-ttu-id="9cadb-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="9cadb-193">Criando um usuário de teste do Lecorpio</span><span class="sxs-lookup"><span data-stu-id="9cadb-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="9cadb-194">Nesta seção, você criará um usuário chamado Brenda Fernandes no Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="9cadb-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="9cadb-195">É preciso contatar a [equipe de suporte do Cliente Lecorpio](mailto:info@lecorpio.com) para adicionar os usuários no aplicativo Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="9cadb-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to add the users in the Lecorpio application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9cadb-196">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9cadb-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9cadb-197">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="9cadb-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lecorpio.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9cadb-199">**Para atribuir Brenda Fernandes ao Lecorpio, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9cadb-199">**To assign Britta Simon to Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="9cadb-200">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9cadb-202">Na lista de aplicativos, selecione **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-202">In the applications list, select **Lecorpio**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="9cadb-204">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9cadb-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9cadb-206">Click **Add** button.</span></span> <span data-ttu-id="9cadb-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cadb-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9cadb-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9cadb-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9cadb-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cadb-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cadb-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cadb-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9cadb-212">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9cadb-212">Testing single sign-on</span></span>

<span data-ttu-id="9cadb-213">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="9cadb-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9cadb-214">Quando você clicar no bloco Lecorpio no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="9cadb-214">When you click the Lecorpio tile in the Access Panel, you should get automatically signed-on to your Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9cadb-215">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9cadb-215">Additional resources</span></span>

* [<span data-ttu-id="9cadb-216">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9cadb-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cadb-217">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9cadb-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

