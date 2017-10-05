---
title: "Tutorial: integração do Azure Active Directory ao Concur | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 0b44437b3dcf69dae3587529da7d12e7809b9f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="003df-103">Tutorial: integração do Active Directory do Azure ao Concur</span><span class="sxs-lookup"><span data-stu-id="003df-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="003df-104">Neste tutorial, você aprenderá a integrar o Concur ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="003df-104">In this tutorial, you learn how to integrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="003df-105">A integração do Concur com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="003df-105">Integrating Concur with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="003df-106">No Azure AD, você pode controlar quem terá acesso ao Concur</span><span class="sxs-lookup"><span data-stu-id="003df-106">You can control in Azure AD who has access to Concur</span></span>
- <span data-ttu-id="003df-107">É possível permitir que usuários façam logon automaticamente no Concur (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="003df-107">You can enable your users to automatically get signed-on to Concur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="003df-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="003df-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="003df-109">Caso deseje obter mais informações sobre a integração de aplicativos SaaS ao Azure AD, consulte [O que é o acesso de aplicativos e o logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="003df-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="003df-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="003df-110">Prerequisites</span></span>

<span data-ttu-id="003df-111">Para configurar a integração do Azure AD com o Concur, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="003df-111">To configure Azure AD integration with Concur, you need the following items:</span></span>

- <span data-ttu-id="003df-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="003df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="003df-113">Uma assinatura habilitada para logon único do Concur</span><span class="sxs-lookup"><span data-stu-id="003df-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="003df-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="003df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="003df-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="003df-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="003df-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="003df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="003df-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="003df-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="003df-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="003df-118">Scenario description</span></span>
<span data-ttu-id="003df-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="003df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="003df-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="003df-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="003df-121">Como adicionar o Concur por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="003df-121">Adding Concur from the gallery</span></span>
2. <span data-ttu-id="003df-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="003df-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="003df-123">A configuração de sua assinatura do Concur para SSO federado via SAML é uma tarefa separada e você deve entrar com a [equipe de suporte do Cliente Concur](https://www.concur.co.in/contact) para executá-la.</span><span class="sxs-lookup"><span data-stu-id="003df-123">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 

## <a name="adding-concur-from-the-gallery"></a><span data-ttu-id="003df-124">Como adicionar o Concur por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="003df-124">Adding Concur from the gallery</span></span>
<span data-ttu-id="003df-125">Para configurar a integração do Concur ao Azure AD, você precisará adicionar o Concur por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="003df-125">To configure the integration of Concur into Azure AD, you need to add Concur from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="003df-126">**Para adicionar o Concur da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="003df-126">**To add Concur from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="003df-127">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="003df-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="003df-129">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="003df-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="003df-130">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="003df-130">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="003df-132">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="003df-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="003df-134">Na caixa de pesquisa, digite **Concur**.</span><span class="sxs-lookup"><span data-stu-id="003df-134">In the search box, type **Concur**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="003df-136">No painel de resultados, selecione **Concur** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="003df-136">In the results panel, select **Concur**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="003df-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="003df-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="003df-139">Nesta seção, você configurará e testará o logon único do Azure AD com o Concur, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="003df-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="003df-140">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Concur é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="003df-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Concur is to a user in Azure AD.</span></span> <span data-ttu-id="003df-141">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Concur.</span><span class="sxs-lookup"><span data-stu-id="003df-141">In other words, a link relationship between an Azure AD user and the related user in Concur needs to be established.</span></span>

<span data-ttu-id="003df-142">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como sendo o valor de **Nome de usuário** no Concur.</span><span class="sxs-lookup"><span data-stu-id="003df-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Concur.</span></span>

<span data-ttu-id="003df-143">Para configurar e testar o logon único do Azure AD com o Concur, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="003df-143">To configure and test Azure AD single sign-on with Concur, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="003df-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="003df-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="003df-145">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="003df-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="003df-146">**[Criação de um usuário de teste do Concur](#creating-a-concur-test-user)**: para ter um equivalente de Brenda Fernandes no Concur que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="003df-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - to have a counterpart of Britta Simon in Concur that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="003df-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="003df-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="003df-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="003df-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="003df-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="003df-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="003df-150">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Concur.</span><span class="sxs-lookup"><span data-stu-id="003df-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="003df-151">**Para configurar o logon único do Azure AD com o Concur, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="003df-151">**To configure Azure AD single sign-on with Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="003df-152">No Portal do Azure, na página de integração de aplicativos do **Concur**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="003df-152">In the Azure portal, on the **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="003df-154">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="003df-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="003df-156">Na seção **URLs e Domínio do Concur**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="003df-156">On the **Concur Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="003df-158">a.</span><span class="sxs-lookup"><span data-stu-id="003df-158">a.</span></span> <span data-ttu-id="003df-159">Na caixa de texto **URL de Logon**, digite o valor usando o seguinte padrão: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="003df-159">In the **Sign on URL** textbox, type the value using the following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="003df-160">b.</span><span class="sxs-lookup"><span data-stu-id="003df-160">b.</span></span> <span data-ttu-id="003df-161">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="003df-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="003df-162">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="003df-162">These values are not the real.</span></span> <span data-ttu-id="003df-163">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="003df-163">Update these values with the actual Sign on URL and Identifier.</span></span> <span data-ttu-id="003df-164">Contate a [equipe de suporte do Cliente Concur](https://www.concur.co.in/contact) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="003df-164">Contact [Concur Client support team](https://www.concur.co.in/contact) to get these values.</span></span> 

4. <span data-ttu-id="003df-165">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="003df-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="003df-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="003df-167">Click **Save** button.</span></span>

    <span data-ttu-id="003df-168">![Configurar Logon Único](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="003df-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="003df-169">Para configurar o logon único no lado do **Concur**, é necessário enviar o **XML de Metadados** baixado para o suporte do Concur.</span><span class="sxs-lookup"><span data-stu-id="003df-169">To configure single sign-on on **Concur** side, you need to send the downloaded **Metadata XML** to Concur support.</span></span> <span data-ttu-id="003df-170">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="003df-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="003df-171">A configuração de sua assinatura do Concur para SSO federado via SAML é uma tarefa separada e você deve entrar com a [equipe de suporte do Cliente Concur](https://www.concur.co.in/contact) para executá-la.</span><span class="sxs-lookup"><span data-stu-id="003df-171">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="003df-172">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="003df-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="003df-173">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="003df-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="003df-174">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="003df-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="003df-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="003df-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="003df-176">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="003df-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="003df-178">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="003df-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="003df-179">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="003df-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="003df-181">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="003df-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="003df-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="003df-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="003df-185">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="003df-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="003df-187">a.</span><span class="sxs-lookup"><span data-stu-id="003df-187">a.</span></span> <span data-ttu-id="003df-188">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="003df-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="003df-189">b.</span><span class="sxs-lookup"><span data-stu-id="003df-189">b.</span></span> <span data-ttu-id="003df-190">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="003df-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="003df-191">c.</span><span class="sxs-lookup"><span data-stu-id="003df-191">c.</span></span> <span data-ttu-id="003df-192">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="003df-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="003df-193">d.</span><span class="sxs-lookup"><span data-stu-id="003df-193">d.</span></span> <span data-ttu-id="003df-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="003df-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="003df-195">Criação de um usuário de teste do Concur</span><span class="sxs-lookup"><span data-stu-id="003df-195">Creating a Concur test user</span></span>

<span data-ttu-id="003df-196">O aplicativo dá suporte ao provisionamento de usuário Just-In-Time e, após a autenticação, os usuários são criados no aplicativo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="003df-196">Application supports the Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="003df-197">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="003df-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="003df-198">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Concur.</span><span class="sxs-lookup"><span data-stu-id="003df-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Concur.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="003df-200">**Para atribuir Brenda Fernandes ao Concur, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="003df-200">**To assign Britta Simon to Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="003df-201">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="003df-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="003df-203">Na lista de aplicativos, selecione **Concur**.</span><span class="sxs-lookup"><span data-stu-id="003df-203">In the applications list, select **Concur**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="003df-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="003df-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="003df-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="003df-207">Click **Add** button.</span></span> <span data-ttu-id="003df-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="003df-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="003df-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="003df-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="003df-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="003df-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="003df-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="003df-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="003df-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="003df-213">Testing single sign-on</span></span>

<span data-ttu-id="003df-214">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="003df-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="003df-215">Ao clicar no bloco Concur no Painel de Acesso, você deve acessar a página de logon do aplicativo Concur.</span><span class="sxs-lookup"><span data-stu-id="003df-215">When you click the Concur tile in the Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="003df-216">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="003df-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="003df-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="003df-217">Additional resources</span></span>

* [<span data-ttu-id="003df-218">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="003df-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="003df-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="003df-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="003df-220">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="003df-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

