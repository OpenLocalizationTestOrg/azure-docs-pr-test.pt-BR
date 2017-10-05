---
title: "Tutorial: integração do Azure Active Directory com o FM:Systems | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o FM:Systems."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3a597d228f6c9234ec2fd2644ec3ac50b98f3b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="c7735-103">Tutorial: Integração do Azure Active Directory com o FM:Systems</span><span class="sxs-lookup"><span data-stu-id="c7735-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="c7735-104">Neste tutorial, você aprenderá a integrar o FM:Systems ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c7735-104">In this tutorial, you learn how to integrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7735-105">A integração do FM:Systems ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c7735-105">Integrating FM:Systems with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c7735-106">No Azure AD, é possível controlar quem tem acesso ao FM:Systems</span><span class="sxs-lookup"><span data-stu-id="c7735-106">You can control in Azure AD who has access to FM:Systems</span></span>
- <span data-ttu-id="c7735-107">Você pode permitir que seus usuários entrem automaticamente no FM:Systems (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7735-107">You can enable your users to automatically get signed-on to FM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7735-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c7735-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c7735-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7735-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7735-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c7735-110">Prerequisites</span></span>

<span data-ttu-id="c7735-111">Para configurar a integração do Azure AD ao FM:Systems, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c7735-111">To configure Azure AD integration with FM:Systems, you need the following items:</span></span>

- <span data-ttu-id="c7735-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7735-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7735-113">Uma assinatura habilitada para logon único do FM:Systems</span><span class="sxs-lookup"><span data-stu-id="c7735-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7735-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c7735-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7735-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c7735-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7735-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c7735-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7735-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7735-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7735-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c7735-118">Scenario description</span></span>
<span data-ttu-id="c7735-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c7735-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7735-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c7735-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7735-121">Adicionando FM:Systems da Galeria</span><span class="sxs-lookup"><span data-stu-id="c7735-121">Adding FM:Systems from the gallery</span></span>
2. <span data-ttu-id="c7735-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7735-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-the-gallery"></a><span data-ttu-id="c7735-123">Adicionando FM:Systems da Galeria</span><span class="sxs-lookup"><span data-stu-id="c7735-123">Adding FM:Systems from the gallery</span></span>
<span data-ttu-id="c7735-124">Para configurar a integração do FM:Systems ao Azure AD, você precisará adicionar o FM:Systems da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c7735-124">To configure the integration of FM:Systems into Azure AD, you need to add FM:Systems from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c7735-125">**Para adicionar o FM:Systems da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c7735-125">**To add FM:Systems from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c7735-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7735-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7735-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c7735-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c7735-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7735-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c7735-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7735-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c7735-133">Na caixa de pesquisa, digite **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="c7735-133">In the search box, type **FM:Systems**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="c7735-135">No painel de resultados, selecione **FM:Systems** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7735-135">In the results panel, select **FM:Systems**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7735-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7735-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7735-138">Nesta seção, você configurará e testará o logon único do Azure AD com o FM:Systems com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c7735-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c7735-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do FM:Systems é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7735-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FM:Systems is to a user in Azure AD.</span></span> <span data-ttu-id="c7735-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="c7735-140">In other words, a link relationship between an Azure AD user and the related user in FM:Systems needs to be established.</span></span>

<span data-ttu-id="c7735-141">No FM:Systems, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="c7735-141">In FM:Systems, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c7735-142">Para configurar e testar o logon único do Azure AD com o FM:Systems, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c7735-142">To configure and test Azure AD single sign-on with FM:Systems, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c7735-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c7735-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c7735-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c7735-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7735-145">**[Como criar um usuário de teste do FM:Systems](#creating-an-fmsystems-test-user)** – para ter um equivalente de Brenda Fernandes no FM:Systems que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7735-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - to have a counterpart of Britta Simon in FM:Systems that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7735-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7735-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7735-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c7735-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7735-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7735-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7735-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="c7735-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="c7735-150">**Para configurar o logon único do Azure AD com o FM:Systems, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c7735-150">**To configure Azure AD single sign-on with FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="c7735-151">No portal do Azure, na página de integração de aplicativos do **FM:Systems**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c7735-151">In the Azure portal, on the **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c7735-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c7735-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="c7735-155">Na seção **URLs e Domínio do FM:Systems**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c7735-155">On the **FM:Systems Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="c7735-157">Na caixa de texto **URL de resposta**, digite a **URL de resposta** do FM:Systems usando o seguinte padrão: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="c7735-157">In the **Reply URL** textbox, type your FM:Systems **Reply URL**, type the URL using the following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7735-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="c7735-158">This value is not real.</span></span> <span data-ttu-id="c7735-159">Atualize esse valor com a URL de Resposta real.</span><span class="sxs-lookup"><span data-stu-id="c7735-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="c7735-160">Entre em contato com [equipe de suporte do FM:Systems](https://fmsystems.com/ask-us/) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="c7735-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) to get this value.</span></span>
 
4. <span data-ttu-id="c7735-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c7735-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="c7735-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c7735-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7735-165">Para configurar o logon único no lado do **FM:Systems**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do FM:Systems](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="c7735-165">To configure single sign-on on **FM:Systems** side, you need to send the downloaded **Metadata XML** to [FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="c7735-166">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="c7735-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="c7735-167">Você receberá uma notificação quando o SSO tiver sido habilitado para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c7735-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="c7735-168">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c7735-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c7735-169">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c7735-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c7735-170">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7735-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7735-171">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7735-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7735-172">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c7735-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c7735-174">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c7735-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c7735-175">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7735-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7735-177">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c7735-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7735-179">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7735-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7735-181">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c7735-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7735-183">a.</span><span class="sxs-lookup"><span data-stu-id="c7735-183">a.</span></span> <span data-ttu-id="c7735-184">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c7735-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7735-185">b.</span><span class="sxs-lookup"><span data-stu-id="c7735-185">b.</span></span> <span data-ttu-id="c7735-186">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c7735-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7735-187">c.</span><span class="sxs-lookup"><span data-stu-id="c7735-187">c.</span></span> <span data-ttu-id="c7735-188">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="c7735-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c7735-189">d.</span><span class="sxs-lookup"><span data-stu-id="c7735-189">d.</span></span> <span data-ttu-id="c7735-190">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c7735-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="c7735-191">Criar um usuário de teste do FM:Systems</span><span class="sxs-lookup"><span data-stu-id="c7735-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="c7735-192">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do FM:Systems como administrador.</span><span class="sxs-lookup"><span data-stu-id="c7735-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="c7735-193">Vá para **Administração do Sistema \> Gerenciar Segurança \> Usuários \> Lista de usuários**.</span><span class="sxs-lookup"><span data-stu-id="c7735-193">Go to **System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="c7735-194">![Administração do Sistema](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Administração do Sistema")</span><span class="sxs-lookup"><span data-stu-id="c7735-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="c7735-195">Clique em **Criar novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="c7735-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="c7735-196">![Criar Novo Usuário](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Criar Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="c7735-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="c7735-197">Na seção **Criar Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c7735-197">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c7735-198">![Criar usuário](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="c7735-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="c7735-199">a.</span><span class="sxs-lookup"><span data-stu-id="c7735-199">a.</span></span> <span data-ttu-id="c7735-200">Digite o **Nome de Usuário**, a **Senha**, **Confirmar Senha**, o **Email** e a **ID do Funcionário** de uma conta válida do Azure Active Directory que você deseje provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="c7735-200">Type the **UserName**, the **Password**, **Confirm Password**, **E-mail** and the **Employee ID** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="c7735-201">b.</span><span class="sxs-lookup"><span data-stu-id="c7735-201">b.</span></span> <span data-ttu-id="c7735-202">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c7735-202">Click **Next**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c7735-203">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7735-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c7735-204">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="c7735-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FM:Systems.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c7735-206">**Para atribuir Brenda Fernandes ao FM:Systems, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c7735-206">**To assign Britta Simon to FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="c7735-207">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7735-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c7735-209">Na lista de aplicativos, selecione **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="c7735-209">In the applications list, select **FM:Systems**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="c7735-211">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7735-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c7735-213">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c7735-213">Click **Add** button.</span></span> <span data-ttu-id="c7735-214">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7735-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c7735-216">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c7735-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c7735-217">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7735-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7735-218">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7735-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7735-219">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c7735-219">Testing single sign-on</span></span>

<span data-ttu-id="c7735-220">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c7735-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c7735-221">Ao clicar no bloco FM:Systems no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="c7735-221">When you click the FM:Systems tile in the Access Panel, you should get automatically signed-on to your FM:Systems application.</span></span>
<span data-ttu-id="c7735-222">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7735-222">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7735-223">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c7735-223">Additional resources</span></span>

* [<span data-ttu-id="c7735-224">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c7735-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7735-225">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7735-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

