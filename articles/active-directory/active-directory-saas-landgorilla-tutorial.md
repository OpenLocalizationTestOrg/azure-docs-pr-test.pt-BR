---
title: "Tutorial: integração do Azure Active Directory com o Land Gorilla Client | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Land Gorilla."
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
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: 744c420aa0298c59c44e645b95a716ad876752de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="36a8e-103">Tutorial: integração do Azure Active Directory com o Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="36a8e-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="36a8e-104">Neste tutorial, você aprenderá a integrar o Land Gorilla Client ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="36a8e-104">In this tutorial, you learn how to integrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36a8e-105">A integração do Land Gorilla Client ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="36a8e-105">Integrating Land Gorilla Client with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="36a8e-106">É possível controlar, no Azure AD, quem tem acesso ao Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="36a8e-106">You can control in Azure AD who has access to Land Gorilla Client</span></span>
- <span data-ttu-id="36a8e-107">É possível permitir que seus usuários façam logon automaticamente no Land Gorilla Client (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="36a8e-107">You can enable your users to automatically get signed-on to Land Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36a8e-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="36a8e-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="36a8e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="36a8e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="36a8e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="36a8e-110">Prerequisites</span></span>

<span data-ttu-id="36a8e-111">Para configurar a integração do Azure AD com o Land Gorilla Client, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="36a8e-111">To configure Azure AD integration with Land Gorilla Client, you need the following items:</span></span>

- <span data-ttu-id="36a8e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="36a8e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36a8e-113">Uma assinatura do Land Gorilla Client habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="36a8e-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="36a8e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="36a8e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="36a8e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="36a8e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36a8e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="36a8e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="36a8e-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36a8e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="36a8e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="36a8e-118">Scenario description</span></span>
<span data-ttu-id="36a8e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="36a8e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36a8e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="36a8e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36a8e-121">Adicionando Land Gorilla Client da galeria</span><span class="sxs-lookup"><span data-stu-id="36a8e-121">Adding Land Gorilla Client from the gallery</span></span>
2. <span data-ttu-id="36a8e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="36a8e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-the-gallery"></a><span data-ttu-id="36a8e-123">Adicionando Land Gorilla Client da galeria</span><span class="sxs-lookup"><span data-stu-id="36a8e-123">Adding Land Gorilla Client from the gallery</span></span>
<span data-ttu-id="36a8e-124">Para configurar a integração do Land Gorilla Client com o Azure AD, é necessário adicionar o Land Gorilla Client da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="36a8e-124">To configure the integration of Land Gorilla Client into Azure AD, you need to add Land Gorilla Client from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="36a8e-125">**Para adicionar o Land Gorilla Client da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="36a8e-125">**To add Land Gorilla Client from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="36a8e-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="36a8e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="36a8e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="36a8e-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36a8e-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="36a8e-133">Na caixa de pesquisa, digite **Land Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-133">In the search box, type **Land Gorilla Client**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="36a8e-135">No painel de resultados, selecione **Land Gorilla Client** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36a8e-135">In the results panel, select **Land Gorilla Client**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="36a8e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="36a8e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="36a8e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Land Gorilla Client, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="36a8e-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="36a8e-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Land Gorilla Client é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36a8e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Land Gorilla Client is to a user in Azure AD.</span></span> <span data-ttu-id="36a8e-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="36a8e-140">In other words, a link relationship between an Azure AD user and the related user in Land Gorilla Client needs to be established.</span></span>

<span data-ttu-id="36a8e-141">Essa relação de vínculo é estabelecida por meio da atribuição do valor do **nome de usuário** no Azure AD como o valor de **Nome de Usuário** no Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="36a8e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="36a8e-142">Para configurar e testar o logon único do Azure AD com o Land Gorilla Client, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="36a8e-142">To configure and test Azure AD single sign-on with Land Gorilla Client, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="36a8e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="36a8e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="36a8e-144">**[Criando um usuário de teste do Azure AD](#creating-an-azure-ad-test-user)** – para testar o logon único do Azure AD com o grupo limitado.</span><span class="sxs-lookup"><span data-stu-id="36a8e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="36a8e-145">**[Criando um usuário de teste do Land Gorilla](#creating-a-land-gorilla-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="36a8e-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="36a8e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="36a8e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36a8e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="36a8e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="36a8e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="36a8e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="36a8e-149">Nesta seção, você habilitará o logon único do Azure AD no Portal de Gerenciamento do Azure e configurará o logon único em seu aplicativo Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="36a8e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="36a8e-150">**Para configurar o logon único do Azure AD com o Land Gorilla Client, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="36a8e-150">**To configure Azure AD single sign-on with Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="36a8e-151">No Portal de Gerenciamento do Azure, na página de integração de aplicativos do **Land Gorilla Client**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-151">In the Azure Management portal, on the **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o logon único][4]

2. <span data-ttu-id="36a8e-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="36a8e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar o logon único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="36a8e-155">Na seção **URLs e Domínio do Land Gorilla Client**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="36a8e-155">On the **Land Gorilla Client Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="36a8e-157">a.</span><span class="sxs-lookup"><span data-stu-id="36a8e-157">a.</span></span> <span data-ttu-id="36a8e-158">Na caixa de texto **Identificador**, digite um valor usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="36a8e-158">In the **Identifier** textbox, type the value using one of the following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="36a8e-159">b.</span><span class="sxs-lookup"><span data-stu-id="36a8e-159">b.</span></span> <span data-ttu-id="36a8e-160">Na caixa de texto **URL de Resposta**, digite uma URL usando um dos seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="36a8e-160">In the **Reply URL** textbox, type a URL using one of the following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="36a8e-161">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="36a8e-161">Please note that these are not the real values.</span></span> <span data-ttu-id="36a8e-162">Você precisa atualizar esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="36a8e-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="36a8e-163">Aqui, sugerimos que você use o valor exclusivo de cadeia de caracteres no Identificador.</span><span class="sxs-lookup"><span data-stu-id="36a8e-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="36a8e-164">Contate a [equipe Land Gorilla Client](https://www.landgorilla.com/support/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="36a8e-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="36a8e-165">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="36a8e-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="36a8e-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="36a8e-167">Click **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="36a8e-169">Para concluir a configuração de SSO para seu aplicativo na extremidade do Land Gorilla, contate a [equipe de suporte Land Gorilla Client](https://www.landgorilla.com/support/) e forneça-as com o arquivo **XML de metadados** baixado.</span><span class="sxs-lookup"><span data-stu-id="36a8e-169">To get SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with the downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="36a8e-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="36a8e-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="36a8e-171">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36a8e-171">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="36a8e-173">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="36a8e-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="36a8e-174">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-174">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="36a8e-176">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="36a8e-176">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="36a8e-178">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36a8e-178">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="36a8e-180">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="36a8e-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36a8e-182">a.</span><span class="sxs-lookup"><span data-stu-id="36a8e-182">a.</span></span> <span data-ttu-id="36a8e-183">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36a8e-184">b.</span><span class="sxs-lookup"><span data-stu-id="36a8e-184">b.</span></span> <span data-ttu-id="36a8e-185">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="36a8e-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36a8e-186">c.</span><span class="sxs-lookup"><span data-stu-id="36a8e-186">c.</span></span> <span data-ttu-id="36a8e-187">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="36a8e-188">d.</span><span class="sxs-lookup"><span data-stu-id="36a8e-188">d.</span></span> <span data-ttu-id="36a8e-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="36a8e-190">Criar um usuário de teste do Land Gorilla</span><span class="sxs-lookup"><span data-stu-id="36a8e-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="36a8e-191">Trabalhe com a [equipe de suporte Land Gorilla](https://www.landgorilla.com/support/) para adicionar os usuários na plataforma do Land Gorilla.</span><span class="sxs-lookup"><span data-stu-id="36a8e-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) to add the users in the Land Gorilla platform.</span></span>
    
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="36a8e-192">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="36a8e-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="36a8e-193">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo-lhe acesso ao Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="36a8e-193">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Land Gorilla Client.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="36a8e-195">**Para atribuir Brenda Fernandes ao Land Gorilla Client, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="36a8e-195">**To assign Britta Simon to Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="36a8e-196">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-196">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="36a8e-198">Na lista de aplicativos, selecione **Land Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-198">In the applications list, select **Land Gorilla Client**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="36a8e-200">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="36a8e-202">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="36a8e-202">Click **Add** button.</span></span> <span data-ttu-id="36a8e-203">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36a8e-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="36a8e-205">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="36a8e-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="36a8e-206">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36a8e-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36a8e-207">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36a8e-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="36a8e-208">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="36a8e-208">Testing single sign-on</span></span>

<span data-ttu-id="36a8e-209">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="36a8e-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="36a8e-210">Ao clicar no bloco Land Gorilla Client no Painel de Acesso, seu logon deverá ser feito automaticamente no aplicativo Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="36a8e-210">When you click the Land Gorilla Client tile in the Access Panel, you should get automatically signed-on to your Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="36a8e-211">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="36a8e-211">Additional resources</span></span>

* [<span data-ttu-id="36a8e-212">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="36a8e-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36a8e-213">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="36a8e-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
