---
title: "Tutorial: Integração do Azure Active Directory ao ASC Contracts | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ASC Contracts."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 87ea3cc55f9683e7d5b9912a87d675575cea0347
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="f1471-103">Tutorial: Integração do Azure Active Directory ao ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="f1471-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="f1471-104">Neste tutorial, você aprenderá a integrar o ASC Contracts ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f1471-104">In this tutorial, you learn how to integrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1471-105">A integração do ASC Contracts ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="f1471-105">Integrating ASC Contracts with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f1471-106">No Azure AD, você pode controlar quem tem acesso ao ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="f1471-106">You can control in Azure AD who has access to ASC Contracts</span></span>
- <span data-ttu-id="f1471-107">Você pode permitir que seus usuários façam logon automaticamente no ASC Contracts (Logon Único) com as próprias contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1471-107">You can enable your users to automatically get signed-on to ASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1471-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f1471-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f1471-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1471-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1471-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f1471-110">Prerequisites</span></span>

<span data-ttu-id="f1471-111">Para configurar a integração do Azure AD ao ASC Contracts, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f1471-111">To configure Azure AD integration with ASC Contracts, you need the following items:</span></span>

- <span data-ttu-id="f1471-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1471-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1471-113">Um logon único do ASC Contracts na assinatura habilitada</span><span class="sxs-lookup"><span data-stu-id="f1471-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1471-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f1471-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1471-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f1471-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1471-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f1471-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1471-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1471-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1471-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f1471-118">Scenario description</span></span>
<span data-ttu-id="f1471-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f1471-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1471-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="f1471-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1471-121">Adicionar contratos ASC da galeria</span><span class="sxs-lookup"><span data-stu-id="f1471-121">Adding ASC Contracts from the gallery</span></span>
2. <span data-ttu-id="f1471-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1471-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-the-gallery"></a><span data-ttu-id="f1471-123">Adicionar contratos ASC da galeria</span><span class="sxs-lookup"><span data-stu-id="f1471-123">Adding ASC Contracts from the gallery</span></span>
<span data-ttu-id="f1471-124">Para configurar a integração do ASC Contracts ao Azure AD, você precisará adicionar o ASC Contracts da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f1471-124">To configure the integration of ASC Contracts into Azure AD, you need to add ASC Contracts from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f1471-125">**Para adicionar o ASC Contracts da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f1471-125">**To add ASC Contracts from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f1471-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1471-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1471-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f1471-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f1471-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f1471-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f1471-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1471-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f1471-133">Na caixa de pesquisa, digite **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="f1471-133">In the search box, type **ASC Contracts**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="f1471-135">No painel de resultados, selecione **ASC Contracts** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1471-135">In the results panel, select **ASC Contracts**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1471-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1471-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1471-138">Nesta seção, você configurará e testará o logon único do Azure AD com o ASC Contracts com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f1471-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f1471-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ASC Contracts é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1471-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ASC Contracts is to a user in Azure AD.</span></span> <span data-ttu-id="f1471-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="f1471-140">In other words, a link relationship between an Azure AD user and the related user in ASC Contracts needs to be established.</span></span>

<span data-ttu-id="f1471-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como sendo o valor de **Nome de usuário** no ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="f1471-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ASC Contracts.</span></span>

<span data-ttu-id="f1471-142">Para configurar e testar o logon único do Azure AD com o ASC Contracts, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f1471-142">To configure and test Azure AD single sign-on with ASC Contracts, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f1471-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f1471-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f1471-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f1471-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1471-145">**[Criação um usuário de teste do ASC Contracts](#creating-an-asc-contracts-test-user)** – para ter um equivalente de Brenda Fernandes no ASC Contracts que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1471-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - to have a counterpart of Britta Simon in ASC Contracts that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1471-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1471-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1471-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="f1471-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1471-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1471-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1471-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="f1471-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="f1471-150">**Para configurar o logon único do Azure AD com o ASC Contracts, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f1471-150">**To configure Azure AD single sign-on with ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="f1471-151">No portal do Azure, na página de integração de aplicativos do **ASC Contracts**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="f1471-151">In the Azure portal, on the **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f1471-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="f1471-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="f1471-155">Na seção **URLs e Domínio do ASC Contracts**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f1471-155">On the **ASC Contracts Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="f1471-157">a.</span><span class="sxs-lookup"><span data-stu-id="f1471-157">a.</span></span> <span data-ttu-id="f1471-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="f1471-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="f1471-159">b.</span><span class="sxs-lookup"><span data-stu-id="f1471-159">b.</span></span> <span data-ttu-id="f1471-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="f1471-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1471-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="f1471-161">These values are not real.</span></span> <span data-ttu-id="f1471-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="f1471-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="f1471-163">Entre em contato com a equipe ASC Networks Inc. (ASC) **613.599.6178** para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="f1471-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** to get these values.</span></span>

4. <span data-ttu-id="f1471-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f1471-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="f1471-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f1471-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f1471-168">Para configurar o logon único no **ASC Contracts**, contate o suporte de ASC Networks Inc. (ASC) em **613.599.6178** e forneça o **XML de Metadados** baixado.</span><span class="sxs-lookup"><span data-stu-id="f1471-168">To configure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with the downloaded **Metadata XML**.</span></span> <span data-ttu-id="f1471-169">Eles configuram esse aplicativo para que tenham a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="f1471-169">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f1471-170">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="f1471-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f1471-171">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f1471-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f1471-172">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1471-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1471-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1471-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1471-174">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f1471-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f1471-176">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f1471-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f1471-177">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1471-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1471-179">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f1471-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1471-181">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1471-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1471-183">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f1471-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1471-185">a.</span><span class="sxs-lookup"><span data-stu-id="f1471-185">a.</span></span> <span data-ttu-id="f1471-186">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f1471-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1471-187">b.</span><span class="sxs-lookup"><span data-stu-id="f1471-187">b.</span></span> <span data-ttu-id="f1471-188">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f1471-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1471-189">c.</span><span class="sxs-lookup"><span data-stu-id="f1471-189">c.</span></span> <span data-ttu-id="f1471-190">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="f1471-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f1471-191">d.</span><span class="sxs-lookup"><span data-stu-id="f1471-191">d.</span></span> <span data-ttu-id="f1471-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f1471-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="f1471-193">Criação de um usuário de teste do ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="f1471-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="f1471-194">Trabalhe com a equipe de suporte da ASC Networks Inc. (ASC) em **613.599.6178** para obter os usuários adicionados na plataforma ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="f1471-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** to get the users added in the ASC Contracts platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f1471-195">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1471-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f1471-196">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="f1471-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ASC Contracts.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f1471-198">**Para atribuir Brenda Fernandes a ASC Contracts, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f1471-198">**To assign Britta Simon to ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="f1471-199">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f1471-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f1471-201">Na lista de aplicativos, selecione **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="f1471-201">In the applications list, select **ASC Contracts**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="f1471-203">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f1471-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f1471-205">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f1471-205">Click **Add** button.</span></span> <span data-ttu-id="f1471-206">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1471-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f1471-208">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f1471-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f1471-209">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1471-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1471-210">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1471-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1471-211">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f1471-211">Testing single sign-on</span></span>

<span data-ttu-id="f1471-212">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="f1471-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f1471-213">Ao clicar no bloco ASC Contracts no painel de acesso, você deverá entrar automaticamente no aplicativo ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="f1471-213">When you click the ASC Contracts tile in the Access Panel, you should get automatically signed-on to your ASC Contracts application.</span></span> <span data-ttu-id="f1471-214">Para obter mais informações sobre o Painel de Acesso, consulte.</span><span class="sxs-lookup"><span data-stu-id="f1471-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="f1471-215">[Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="f1471-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1471-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f1471-216">Additional resources</span></span>

* [<span data-ttu-id="f1471-217">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f1471-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1471-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1471-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

