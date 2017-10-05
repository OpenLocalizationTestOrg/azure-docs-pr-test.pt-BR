---
title: "Tutorial: Integração do Azure Active Directory com o Reward Gateway | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Reward Gateway."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34336386-998a-4d47-ab55-721d97708e5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: b1a468caa22159ad603dbec1ef530e7e0e24f96d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-reward-gateway"></a><span data-ttu-id="aa4a9-103">Tutorial: Integração do Azure Active Directory com o Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="aa4a9-103">Tutorial: Azure Active Directory integration with Reward Gateway</span></span>

<span data-ttu-id="aa4a9-104">Neste tutorial, você aprenderá a integrar o Reward Gateway com o Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="aa4a9-104">In this tutorial, you learn how to integrate Reward Gateway with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa4a9-105">A integração do Reward Gateway com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-105">Integrating Reward Gateway with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="aa4a9-106">Você pode controlar no Azure AD quem tem acesso ao Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="aa4a9-106">You can control in Azure AD who has access to Reward Gateway</span></span>
- <span data-ttu-id="aa4a9-107">Você pode habilitar seus usuários a fazer logon automaticamente no Reward Gateway (Logon Único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa4a9-107">You can enable your users to automatically get signed-on to Reward Gateway (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa4a9-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="aa4a9-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa4a9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa4a9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aa4a9-110">Prerequisites</span></span>

<span data-ttu-id="aa4a9-111">Para configurar a integração do Azure AD ao Reward Gateway, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-111">To configure Azure AD integration with Reward Gateway, you need the following items:</span></span>

- <span data-ttu-id="aa4a9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa4a9-113">Uma assinatura habilitada para logon único do Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="aa4a9-113">A Reward Gateway single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa4a9-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa4a9-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa4a9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa4a9-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa4a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa4a9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="aa4a9-118">Scenario description</span></span>
<span data-ttu-id="aa4a9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa4a9-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa4a9-121">Adicionar o Gateway de Recompensa da Galeria</span><span class="sxs-lookup"><span data-stu-id="aa4a9-121">Adding Reward Gateway from the gallery</span></span>
2. <span data-ttu-id="aa4a9-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-reward-gateway-from-the-gallery"></a><span data-ttu-id="aa4a9-123">Adicionar o Gateway de Recompensa da Galeria</span><span class="sxs-lookup"><span data-stu-id="aa4a9-123">Adding Reward Gateway from the gallery</span></span>
<span data-ttu-id="aa4a9-124">Para configurar a integração do Reward Gateway ao Azure AD, você precisa adicionar o Reward Gateway da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-124">To configure the integration of Reward Gateway into Azure AD, you need to add Reward Gateway from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aa4a9-125">**Para adicionar o Reward Gateway da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="aa4a9-125">**To add Reward Gateway from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aa4a9-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa4a9-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="aa4a9-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="aa4a9-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="aa4a9-133">Na caixa de pesquisa, digite **Reward Gateway**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-133">In the search box, type **Reward Gateway**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_search.png)

5. <span data-ttu-id="aa4a9-135">No painel de resultados, selecione **Reward Gateway** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-135">In the results panel, select **Reward Gateway**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aa4a9-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aa4a9-138">Nesta seção, você configura e testa o logon único do Azure AD com o Reward Gateway com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-138">In this section, you configure and test Azure AD single sign-on with Reward Gateway based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aa4a9-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Reward Gateway é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Reward Gateway is to a user in Azure AD.</span></span> <span data-ttu-id="aa4a9-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-140">In other words, a link relationship between an Azure AD user and the related user in Reward Gateway needs to be established.</span></span>

<span data-ttu-id="aa4a9-141">No Reward Gateway, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-141">In Reward Gateway, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="aa4a9-142">Para configurar e testar o logon único do Azure AD com o Reward Gateway, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-142">To configure and test Azure AD single sign-on with Reward Gateway, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aa4a9-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aa4a9-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa4a9-145">**[Criação de um usuário de teste do Reward Gateway](#creating-a-reward-gateway-test-user)** – para ter um equivalente de Brenda Fernandes no Reward Gateway que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-145">**[Creating a Reward Gateway test user](#creating-a-reward-gateway-test-user)** - to have a counterpart of Britta Simon in Reward Gateway that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa4a9-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa4a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aa4a9-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa4a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aa4a9-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Reward Gateway application.</span></span>

<span data-ttu-id="aa4a9-150">**Para configurar o logon único do Azure AD com o Reward Gateway, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="aa4a9-150">**To configure Azure AD single sign-on with Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="aa4a9-151">No Portal do Azure, na página de integração de aplicativos do **Reward Gateway**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-151">In the Azure portal, on the **Reward Gateway** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="aa4a9-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_samlbase.png)

3. <span data-ttu-id="aa4a9-155">Na seção **URLs e Domínio do Reward Gateway**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-155">On the **Reward Gateway Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_url.png)

    <span data-ttu-id="aa4a9-157">a.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-157">a.</span></span> <span data-ttu-id="aa4a9-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.rewardgateway.com` |
    | `https://<companyname>.rewardgateway.co.uk/` |
    | `https://<companyname>.rewardgateway.co.nz/` |
    | `https://<companyname>.rewardgateway.com.au/` |

    <span data-ttu-id="aa4a9-159">b.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-159">b.</span></span> <span data-ttu-id="aa4a9-160">Na caixa de texto **URL de resposta** , digite uma URL no seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    |  `https://<companyname>.rewardgateway.com/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.uk/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.nz/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.com.au/Authentication/EndLogin?idp=<Unique Id>` |

    > [!NOTE] 
    > <span data-ttu-id="aa4a9-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-161">These values are not real.</span></span> <span data-ttu-id="aa4a9-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="aa4a9-163">Entre em contato com a [equipe de suporte do Reward Gateway](mailto:clientsupport@rewardgateway.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-163">Contact [Reward Gateway support team](mailto:clientsupport@rewardgateway.com) to get these values.</span></span>
 
4. <span data-ttu-id="aa4a9-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_certificate.png) 

5. <span data-ttu-id="aa4a9-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="aa4a9-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aa4a9-168">Para configurar o logon único no lado do **Reward Gateway**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Reward Gateway](mailto:clientsupport@rewardgateway.com).</span><span class="sxs-lookup"><span data-stu-id="aa4a9-168">To configure single sign-on on **Reward Gateway** side, you need to send the downloaded **Metadata XML** to [Reward Gateway support team](mailto:clientsupport@rewardgateway.com).</span></span> <span data-ttu-id="aa4a9-169">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="aa4a9-170">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="aa4a9-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="aa4a9-171">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="aa4a9-172">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aa4a9-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aa4a9-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="aa4a9-174">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="aa4a9-176">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="aa4a9-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aa4a9-177">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa4a9-179">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa4a9-181">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa4a9-183">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa4a9-185">a.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-185">a.</span></span> <span data-ttu-id="aa4a9-186">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa4a9-187">b.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-187">b.</span></span> <span data-ttu-id="aa4a9-188">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa4a9-189">c.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-189">c.</span></span> <span data-ttu-id="aa4a9-190">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="aa4a9-191">d.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-191">d.</span></span> <span data-ttu-id="aa4a9-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-192">Click **Create**.</span></span>
 
### <a name="creating-a-reward-gateway-test-user"></a><span data-ttu-id="aa4a9-193">Criação de um usuário de teste do Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="aa4a9-193">Creating a Reward Gateway test user</span></span>

<span data-ttu-id="aa4a9-194">Nesta seção, você criará um usuário chamado Brenda Fernandes no Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-194">In this section, you create a user called Britta Simon in Reward Gateway.</span></span> <span data-ttu-id="aa4a9-195">Trabalhe com a [equipe de suporte do Reward Gateway](mailto:clientsupport@rewardgateway.com) para adicionar os usuários a plataforma do Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-195">Work with Reward Gateway [support team](mailto:clientsupport@rewardgateway.com) to add the users in the Reward Gateway platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="aa4a9-196">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="aa4a9-197">Nesta seção, você habilitará Brenda Fernandes a usar logon único do Azure concedendo acesso ao Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Reward Gateway.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="aa4a9-199">**Para atribuir Brenda Fernandes ao Reward Gateway, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="aa4a9-199">**To assign Britta Simon to Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="aa4a9-200">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="aa4a9-202">Na lista de aplicativos, selecione **Reward Gateway**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-202">In the applications list, select **Reward Gateway**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_app.png) 

3. <span data-ttu-id="aa4a9-204">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="aa4a9-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-206">Click **Add** button.</span></span> <span data-ttu-id="aa4a9-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="aa4a9-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="aa4a9-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa4a9-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aa4a9-212">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="aa4a9-212">Testing single sign-on</span></span>

<span data-ttu-id="aa4a9-213">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="aa4a9-214">Ao clicar no bloco Reward Gateway no Painel de Acesso, você deve entrar automaticamente em seu aplicativo Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-214">When you click the Reward Gateway tile in the Access Panel, you should get automatically signed-on to your Reward Gateway application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa4a9-215">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="aa4a9-215">Additional resources</span></span>

* [<span data-ttu-id="aa4a9-216">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa4a9-217">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aa4a9-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_203.png

