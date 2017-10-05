---
title: "Tutorial: integração do Azure Active Directory com o People | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o People."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: caa287a2ed8774965ef722685e4e950336e5e0ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="95e56-103">Tutorial: Integração do Azure Active Directory ao People</span><span class="sxs-lookup"><span data-stu-id="95e56-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="95e56-104">Neste tutorial, você aprenderá a integrar o People ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="95e56-104">In this tutorial, you learn how to integrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95e56-105">A integração do People ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="95e56-105">Integrating People with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="95e56-106">Você pode controlar no Azure AD quem tem acesso ao People</span><span class="sxs-lookup"><span data-stu-id="95e56-106">You can control in Azure AD who has access to People</span></span>
- <span data-ttu-id="95e56-107">Você pode habilitar os usuários a entrar automaticamente no People (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="95e56-107">You can enable your users to automatically get signed-on to People (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="95e56-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="95e56-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="95e56-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="95e56-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95e56-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="95e56-110">Prerequisites</span></span>

<span data-ttu-id="95e56-111">Para configurar a integração do Azure AD ao People, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="95e56-111">To configure Azure AD integration with People, you need the following items:</span></span>

- <span data-ttu-id="95e56-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95e56-112">An Azure AD subscription</span></span>
- <span data-ttu-id="95e56-113">Uma assinatura habilitada para logon único do People</span><span class="sxs-lookup"><span data-stu-id="95e56-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="95e56-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="95e56-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="95e56-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="95e56-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="95e56-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="95e56-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="95e56-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95e56-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95e56-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="95e56-118">Scenario description</span></span>
<span data-ttu-id="95e56-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="95e56-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95e56-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="95e56-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95e56-121">Adição do People a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="95e56-121">Adding People from the gallery</span></span>
2. <span data-ttu-id="95e56-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95e56-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-the-gallery"></a><span data-ttu-id="95e56-123">Adição do People a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="95e56-123">Adding People from the gallery</span></span>
<span data-ttu-id="95e56-124">Para configurar a integração do People ao Azure AD, você precisará adicionar o People à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="95e56-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="95e56-125">**Para adicionar o People por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="95e56-125">**To add People from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="95e56-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95e56-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="95e56-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="95e56-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="95e56-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="95e56-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="95e56-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95e56-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="95e56-133">Na caixa de pesquisa, digite **People**.</span><span class="sxs-lookup"><span data-stu-id="95e56-133">In the search box, type **People**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="95e56-135">No painel de resultados, selecione **People** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95e56-135">In the results panel, select **People**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="95e56-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95e56-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="95e56-138">Nesta seção, você configurará e testará o logon único do Azure AD com o People, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="95e56-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="95e56-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do People é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95e56-139">For single sign-on to work, Azure AD needs to know what the counterpart user in People is to a user in Azure AD.</span></span> <span data-ttu-id="95e56-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do People.</span><span class="sxs-lookup"><span data-stu-id="95e56-140">In other words, a link relationship between an Azure AD user and the related user in People needs to be established.</span></span>

<span data-ttu-id="95e56-141">No People, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="95e56-141">In People, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="95e56-142">Para configurar e testar o logon único do Azure AD com o People, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="95e56-142">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="95e56-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="95e56-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="95e56-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="95e56-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="95e56-145">**[Criação de um usuário de teste do People](#creating-a-people-test-user)** – para ter um equivalente de Brenda Fernandes em People, que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95e56-145">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="95e56-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="95e56-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="95e56-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="95e56-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="95e56-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="95e56-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="95e56-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo People.</span><span class="sxs-lookup"><span data-stu-id="95e56-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="95e56-150">**Para configurar o logon único do Azure AD com o People, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="95e56-150">**To configure Azure AD single sign-on with People, perform the following steps:**</span></span>

1. <span data-ttu-id="95e56-151">No Portal do Azure, na página de integração de aplicativos do **People**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="95e56-151">In the Azure portal, on the **People** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="95e56-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="95e56-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="95e56-155">Na seção **URLs e Domínio do People**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="95e56-155">On the **People Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="95e56-157">a.</span><span class="sxs-lookup"><span data-stu-id="95e56-157">a.</span></span> <span data-ttu-id="95e56-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="95e56-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="95e56-159">b.</span><span class="sxs-lookup"><span data-stu-id="95e56-159">b.</span></span> <span data-ttu-id="95e56-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="95e56-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="95e56-161">c.</span><span class="sxs-lookup"><span data-stu-id="95e56-161">c.</span></span> <span data-ttu-id="95e56-162">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="95e56-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="95e56-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="95e56-163">These values are not real.</span></span> <span data-ttu-id="95e56-164">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="95e56-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="95e56-165">Entre em contato com a [equipe de suporte ao cliente do People](mailto:customerservices@peoplehr.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="95e56-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) to get these values.</span></span>

5. <span data-ttu-id="95e56-166">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="95e56-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="95e56-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="95e56-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="95e56-170">Para configurar o SSO para o aplicativo, você precisa entrar no locatário People como administrador.</span><span class="sxs-lookup"><span data-stu-id="95e56-170">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="95e56-171">No menu à esquerda, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="95e56-171">In the menu on the left side, click **Settings**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="95e56-173">Clique em **Empresa**.</span><span class="sxs-lookup"><span data-stu-id="95e56-173">Click **Company**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="95e56-175">Em **Carregar arquivo de metadados SAML de ‘Logon Único’**, clique em **Procurar** para carregar o arquivo de metadados baixado.</span><span class="sxs-lookup"><span data-stu-id="95e56-175">On the **Upload 'Single Sign On' SAML meta-data file**, click **Browse** to upload the downloaded metadata file.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="95e56-177">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="95e56-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="95e56-178">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="95e56-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="95e56-179">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="95e56-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="95e56-180">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95e56-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="95e56-181">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="95e56-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="95e56-183">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="95e56-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="95e56-184">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95e56-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="95e56-186">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="95e56-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="95e56-188">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95e56-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="95e56-190">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="95e56-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="95e56-192">a.</span><span class="sxs-lookup"><span data-stu-id="95e56-192">a.</span></span> <span data-ttu-id="95e56-193">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="95e56-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="95e56-194">b.</span><span class="sxs-lookup"><span data-stu-id="95e56-194">b.</span></span> <span data-ttu-id="95e56-195">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="95e56-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="95e56-196">c.</span><span class="sxs-lookup"><span data-stu-id="95e56-196">c.</span></span> <span data-ttu-id="95e56-197">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="95e56-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="95e56-198">d.</span><span class="sxs-lookup"><span data-stu-id="95e56-198">d.</span></span> <span data-ttu-id="95e56-199">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="95e56-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="95e56-200">Criação de um usuário de teste do People</span><span class="sxs-lookup"><span data-stu-id="95e56-200">Creating a People test user</span></span>

<span data-ttu-id="95e56-201">Nesta seção, você criará um usuário chamado Brenda Fernandes no People.</span><span class="sxs-lookup"><span data-stu-id="95e56-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="95e56-202">Trabalhe com a [equipe de suporte ao cliente do People](mailto:customerservices@peoplehr.com) para adicionar os usuários na plataforma do People.</span><span class="sxs-lookup"><span data-stu-id="95e56-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add the users in the People platform.</span></span> <span data-ttu-id="95e56-203">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="95e56-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="95e56-204">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95e56-204">Assigning the Azure AD test user</span></span>

<span data-ttu-id="95e56-205">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao People.</span><span class="sxs-lookup"><span data-stu-id="95e56-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to People.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="95e56-207">**Para atribuir Brenda Fernandes ao People, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="95e56-207">**To assign Britta Simon to People, perform the following steps:**</span></span>

1. <span data-ttu-id="95e56-208">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="95e56-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="95e56-210">Na lista de aplicativos, selecione **People**.</span><span class="sxs-lookup"><span data-stu-id="95e56-210">In the applications list, select **People**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="95e56-212">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="95e56-212">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="95e56-214">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="95e56-214">Click **Add** button.</span></span> <span data-ttu-id="95e56-215">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95e56-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="95e56-217">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="95e56-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="95e56-218">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95e56-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="95e56-219">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95e56-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="95e56-220">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="95e56-220">Testing single sign-on</span></span>

<span data-ttu-id="95e56-221">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="95e56-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="95e56-222">Ao clicar no bloco People no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo People.</span><span class="sxs-lookup"><span data-stu-id="95e56-222">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="95e56-223">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="95e56-223">Additional resources</span></span>

* [<span data-ttu-id="95e56-224">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="95e56-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95e56-225">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="95e56-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

