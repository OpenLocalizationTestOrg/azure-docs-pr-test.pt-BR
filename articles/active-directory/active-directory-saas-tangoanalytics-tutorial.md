---
title: "Tutorial: Integração do Azure Active Directory ao Tango Analytics | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Tango Analytics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2f7555d3-e9ba-40b2-9b3a-2f0ab38a4c08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 46f6facc3c86630a9252340b2e89634368c0263d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tango-analytics"></a><span data-ttu-id="e2d1e-103">Tutorial: Integração do Azure Active Directory ao Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="e2d1e-103">Tutorial: Azure Active Directory integration with Tango Analytics</span></span>

<span data-ttu-id="e2d1e-104">Neste tutorial, você aprenderá a integrar o Tango Analytics ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e2d1e-104">In this tutorial, you learn how to integrate Tango Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e2d1e-105">A integração do Tango Analytics ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e2d1e-105">Integrating Tango Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e2d1e-106">Você pode controlar no Azure AD quem tem acesso ao Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="e2d1e-106">You can control in Azure AD who has access to Tango Analytics</span></span>
- <span data-ttu-id="e2d1e-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Tango Analytics (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2d1e-107">You can enable your users to automatically get signed-on to Tango Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e2d1e-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e2d1e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e2d1e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e2d1e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2d1e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e2d1e-110">Prerequisites</span></span>

<span data-ttu-id="e2d1e-111">Para configurar a integração do Azure AD ao Tango Analytics, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e2d1e-111">To configure Azure AD integration with Tango Analytics, you need the following items:</span></span>

- <span data-ttu-id="e2d1e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e2d1e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e2d1e-113">Uma assinatura habilitada para logon único do Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="e2d1e-113">A Tango Analytics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e2d1e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e2d1e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e2d1e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e2d1e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e2d1e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e2d1e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e2d1e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e2d1e-118">Scenario description</span></span>
<span data-ttu-id="e2d1e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e2d1e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e2d1e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e2d1e-121">Adicionar o Tango análise da galeria</span><span class="sxs-lookup"><span data-stu-id="e2d1e-121">Adding Tango Analytics from the gallery</span></span>
2. <span data-ttu-id="e2d1e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e2d1e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tango-analytics-from-the-gallery"></a><span data-ttu-id="e2d1e-123">Adicionar o Tango análise da galeria</span><span class="sxs-lookup"><span data-stu-id="e2d1e-123">Adding Tango Analytics from the gallery</span></span>
<span data-ttu-id="e2d1e-124">Para configurar a integração do Tango Analytics ao Azure AD, você precisará adicionar o Tango Analytics da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-124">To configure the integration of Tango Analytics into Azure AD, you need to add Tango Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e2d1e-125">**Para adicionar o Tango Analytics da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e2d1e-125">**To add Tango Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e2d1e-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e2d1e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e2d1e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e2d1e-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e2d1e-133">Na caixa de pesquisa, digite **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-133">In the search box, type **Tango Analytics**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_search.png)

5. <span data-ttu-id="e2d1e-135">No painel de resultados, selecione **Tango Analytics** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-135">In the results panel, select **Tango Analytics**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e2d1e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e2d1e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e2d1e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Tango Analytics, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-138">In this section, you configure and test Azure AD single sign-on with Tango Analytics based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e2d1e-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Tango Analytics é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tango Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="e2d1e-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-140">In other words, a link relationship between an Azure AD user and the related user in Tango Analytics needs to be established.</span></span>

<span data-ttu-id="e2d1e-141">No Tango Analytics, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-141">In Tango Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e2d1e-142">Para configurar e testar o logon único do Azure AD com o Tango Analytics, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e2d1e-142">To configure and test Azure AD single sign-on with Tango Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e2d1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e2d1e-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e2d1e-145">**[Criação um usuário de teste do Tango Analytics](#creating-a-tango-analytics-test-user)** – para ter um equivalente de Brenda Fernandes no Tango Analytics que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-145">**[Creating a Tango Analytics test user](#creating-a-tango-analytics-test-user)** - to have a counterpart of Britta Simon in Tango Analytics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e2d1e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e2d1e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e2d1e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2d1e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e2d1e-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tango Analytics application.</span></span>

<span data-ttu-id="e2d1e-150">**Para configurar o logon único do Azure AD com o Tango Analytics, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e2d1e-150">**To configure Azure AD single sign-on with Tango Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="e2d1e-151">No portal do Azure, na página de integração de aplicativos do **Tango Analytics**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-151">In the Azure portal, on the **Tango Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e2d1e-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_samlbase.png)

3. <span data-ttu-id="e2d1e-155">Na seção **URLs e Domínio do Tango Analytics**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e2d1e-155">On the **Tango Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_url.png)

    <span data-ttu-id="e2d1e-157">a.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-157">a.</span></span> <span data-ttu-id="e2d1e-158">Na caixa de texto **Identificador**, digite o valor `TACORE_SSO`</span><span class="sxs-lookup"><span data-stu-id="e2d1e-158">In the **Identifier** textbox, type the value `TACORE_SSO`</span></span>

    <span data-ttu-id="e2d1e-159">b.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-159">b.</span></span> <span data-ttu-id="e2d1e-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span><span class="sxs-lookup"><span data-stu-id="e2d1e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e2d1e-161">O valor de URL de Resposta não é real.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-161">The Reply URL value is not real.</span></span> <span data-ttu-id="e2d1e-162">Atualize-o com a URL de Resposta real.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-162">Update this with the actual Reply URL.</span></span> <span data-ttu-id="e2d1e-163">Entre em contato com a [equipe de suporte do Tango Analytics](mailto:support@tangoanalytics.com) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-163">Contact [Tango Analytics support team](mailto:support@tangoanalytics.com) to get this value.</span></span>

4. <span data-ttu-id="e2d1e-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_certificate.png) 

5. <span data-ttu-id="e2d1e-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e2d1e-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e2d1e-168">Para configurar o logon único no lado do **Tango Analytics**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Tango Analytics](mailto:support@tangoanalytics.com).</span><span class="sxs-lookup"><span data-stu-id="e2d1e-168">To configure single sign-on on **Tango Analytics** side, you need to send the downloaded **Metadata XML** to [Tango Analytics support team](mailto:support@tangoanalytics.com).</span></span> <span data-ttu-id="e2d1e-169">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e2d1e-170">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="e2d1e-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e2d1e-171">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e2d1e-172">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e2d1e-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e2d1e-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e2d1e-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="e2d1e-174">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e2d1e-176">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e2d1e-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e2d1e-177">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e2d1e-179">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e2d1e-181">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e2d1e-183">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e2d1e-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e2d1e-185">a.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-185">a.</span></span> <span data-ttu-id="e2d1e-186">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e2d1e-187">b.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-187">b.</span></span> <span data-ttu-id="e2d1e-188">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e2d1e-189">c.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-189">c.</span></span> <span data-ttu-id="e2d1e-190">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e2d1e-191">d.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-191">d.</span></span> <span data-ttu-id="e2d1e-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-192">Click **Create**.</span></span>
 
### <a name="creating-a-tango-analytics-test-user"></a><span data-ttu-id="e2d1e-193">Criação um usuário de teste do Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="e2d1e-193">Creating a Tango Analytics test user</span></span>

<span data-ttu-id="e2d1e-194">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-194">In this section, you create a user called Britta Simon in Tango Analytics.</span></span> <span data-ttu-id="e2d1e-195">Trabalhe com a [equipe de suporte do Tango Analytics](mailto:support@tangoanalytics.com) para adicionar os usuários na plataforma Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-195">Work with [Tango Analytics support team](mailto:support@tangoanalytics.com) to add the users in the Tango Analytics platform.</span></span> <span data-ttu-id="e2d1e-196">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e2d1e-197">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e2d1e-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e2d1e-198">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tango Analytics.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e2d1e-200">**Para atribuir Brenda Fernandes ao Tango Analytics, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e2d1e-200">**To assign Britta Simon to Tango Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="e2d1e-201">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e2d1e-203">Na lista de aplicativos, selecione **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-203">In the applications list, select **Tango Analytics**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_app.png) 

3. <span data-ttu-id="e2d1e-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e2d1e-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-207">Click **Add** button.</span></span> <span data-ttu-id="e2d1e-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e2d1e-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e2d1e-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e2d1e-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e2d1e-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e2d1e-213">Testing single sign-on</span></span>

<span data-ttu-id="e2d1e-214">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e2d1e-215">Ao clicar no bloco Tango Analytics no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="e2d1e-215">When you click the Tango Analytics tile in the Access Panel, you should get automatically signed-on to your Tango Analytics application.</span></span>
<span data-ttu-id="e2d1e-216">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e2d1e-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e2d1e-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e2d1e-217">Additional resources</span></span>

* [<span data-ttu-id="e2d1e-218">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e2d1e-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2d1e-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e2d1e-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_203.png

