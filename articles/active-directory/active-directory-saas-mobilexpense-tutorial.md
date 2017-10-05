---
title: "Tutorial: Integração do Azure Active Directory com o MobileXpense | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o MobileXpense."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e649fc4e-3e15-4948-b977-00bfe9f7db13
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: jeedes
ms.openlocfilehash: 030a1fc9f36d6fcfa607552d85ce232e36eaa64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mobilexpense"></a><span data-ttu-id="589c2-103">Tutorial: integração do Azure Active Directory ao MobileXpense</span><span class="sxs-lookup"><span data-stu-id="589c2-103">Tutorial: Azure Active Directory integration with MobileXpense</span></span>

<span data-ttu-id="589c2-104">Neste tutorial, você aprenderá a integrar o MobileXpense ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="589c2-104">In this tutorial, you learn how to integrate MobileXpense with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="589c2-105">A integração do MobileXpense ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="589c2-105">Integrating MobileXpense with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="589c2-106">No Azure AD, é possível controlar quem tem acesso ao MobileXpense</span><span class="sxs-lookup"><span data-stu-id="589c2-106">You can control in Azure AD who has access to MobileXpense</span></span>
- <span data-ttu-id="589c2-107">Você pode permitir que os usuários façam logon automaticamente no MobileXpense (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="589c2-107">You can enable your users to automatically get signed-on to MobileXpense (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="589c2-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="589c2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="589c2-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="589c2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="589c2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="589c2-110">Prerequisites</span></span>

<span data-ttu-id="589c2-111">Para configurar a integração do Azure AD ao MobileXpense, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="589c2-111">To configure Azure AD integration with MobileXpense, you need the following items:</span></span>

- <span data-ttu-id="589c2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="589c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="589c2-113">Uma assinatura do MobileXpense habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="589c2-113">A MobileXpense single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="589c2-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="589c2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="589c2-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="589c2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="589c2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="589c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="589c2-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="589c2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="589c2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="589c2-118">Scenario description</span></span>
<span data-ttu-id="589c2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="589c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="589c2-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="589c2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="589c2-121">Adicionar o MobileXpense da galeria</span><span class="sxs-lookup"><span data-stu-id="589c2-121">Adding MobileXpense from the gallery</span></span>
2. <span data-ttu-id="589c2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="589c2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobilexpense-from-the-gallery"></a><span data-ttu-id="589c2-123">Adicionar o MobileXpense da galeria</span><span class="sxs-lookup"><span data-stu-id="589c2-123">Adding MobileXpense from the gallery</span></span>
<span data-ttu-id="589c2-124">Para configurar a integração do MobileXpense com o Azure AD, você precisará adicionar o MobileXpense por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="589c2-124">To configure the integration of MobileXpense into Azure AD, you need to add MobileXpense from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="589c2-125">**Para adicionar o MobileXpense por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="589c2-125">**To add MobileXpense from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="589c2-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="589c2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="589c2-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="589c2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="589c2-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="589c2-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="589c2-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="589c2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="589c2-133">Na caixa de pesquisa, digite **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="589c2-133">In the search box, type **MobileXpense**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_search.png)

5. <span data-ttu-id="589c2-135">No painel de resultados, selecione **MobileXpense** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="589c2-135">In the results panel, select **MobileXpense**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="589c2-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="589c2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="589c2-138">Nesta seção, você configurará e testará o logon único do Azure AD com o MobileXpense, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="589c2-138">In this section, you configure and test Azure AD single sign-on with MobileXpense based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="589c2-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do MobileXpense é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="589c2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MobileXpense is to a user in Azure AD.</span></span> <span data-ttu-id="589c2-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="589c2-140">In other words, a link relationship between an Azure AD user and the related user in MobileXpense needs to be established.</span></span>

<span data-ttu-id="589c2-141">No MobileXpense, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="589c2-141">In MobileXpense, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="589c2-142">Para configurar e testar o logon único do Azure AD com o MobileXpense, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="589c2-142">To configure and test Azure AD single sign-on with MobileXpense, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="589c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="589c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="589c2-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="589c2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="589c2-145">**[Criar um usuário de teste do MobileXpense](#creating-a-mobilexpense-test-user)** – para ter um equivalente de Brenda Fernandes no MobileXpense que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="589c2-145">**[Creating a MobileXpense test user](#creating-a-mobilexpense-test-user)** - to have a counterpart of Britta Simon in MobileXpense that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="589c2-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="589c2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="589c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="589c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="589c2-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="589c2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="589c2-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="589c2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MobileXpense application.</span></span>

<span data-ttu-id="589c2-150">**Para configurar o logon único do Azure AD com o MobileXpense, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="589c2-150">**To configure Azure AD single sign-on with MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="589c2-151">No Portal do Azure, na página de integração de aplicativos do **MobileXpense**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="589c2-151">In the Azure portal, on the **MobileXpense** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="589c2-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="589c2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_samlbase.png)

3. <span data-ttu-id="589c2-155">Na seção **Domínio e URLs do MobileXpense**, se você desejar configurar o aplicativo em **Modo iniciado pelo IdP**:</span><span class="sxs-lookup"><span data-stu-id="589c2-155">On the **MobileXpense Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url11.png)

    <span data-ttu-id="589c2-157">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="589c2-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span></span>

4. <span data-ttu-id="589c2-158">Marque **Mostrar configurações avançadas de URL** se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="589c2-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url22.png)

<span data-ttu-id="589c2-160">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<sub domain>.mobilexpense.com/<customername>`</span><span class="sxs-lookup"><span data-stu-id="589c2-160">In the **Sign-on URL** textbox, type a URL using the following pattern:: `https://<sub domain>.mobilexpense.com/<customername>`</span></span>

> [!NOTE] 
> <span data-ttu-id="589c2-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="589c2-161">These values are not real.</span></span> <span data-ttu-id="589c2-162">Atualize esses valores com a URL de Resposta e a URL de Logon reais.</span><span class="sxs-lookup"><span data-stu-id="589c2-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="589c2-163">Contate a [equipe de suporte do Cliente MobileXpense](http://www.mobilexpense.net/contact) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="589c2-163">Contact [MobileXpense Client support team](http://www.mobilexpense.net/contact) to get these values.</span></span> 

5. <span data-ttu-id="589c2-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="589c2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_certificate.png) 

6. <span data-ttu-id="589c2-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="589c2-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="589c2-168">Para configurar o logon único no lado do **MobileXpense**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do MobileXpense](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="589c2-168">To configure single sign-on on **MobileXpense** side, you need to send the downloaded **Metadata XML** to [MobileXpense support team](http://www.mobilexpense.net/contact).</span></span>

> [!TIP]
> <span data-ttu-id="589c2-169">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="589c2-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="589c2-170">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="589c2-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="589c2-171">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="589c2-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="589c2-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="589c2-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="589c2-173">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="589c2-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="589c2-175">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="589c2-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="589c2-176">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="589c2-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="589c2-178">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="589c2-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="589c2-180">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="589c2-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="589c2-182">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="589c2-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="589c2-184">a.</span><span class="sxs-lookup"><span data-stu-id="589c2-184">a.</span></span> <span data-ttu-id="589c2-185">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="589c2-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="589c2-186">b.</span><span class="sxs-lookup"><span data-stu-id="589c2-186">b.</span></span> <span data-ttu-id="589c2-187">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="589c2-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="589c2-188">c.</span><span class="sxs-lookup"><span data-stu-id="589c2-188">c.</span></span> <span data-ttu-id="589c2-189">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="589c2-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="589c2-190">d.</span><span class="sxs-lookup"><span data-stu-id="589c2-190">d.</span></span> <span data-ttu-id="589c2-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="589c2-191">Click **Create**.</span></span>
 
### <a name="creating-a-mobilexpense-test-user"></a><span data-ttu-id="589c2-192">Criar um usuário de teste do MobileXpense</span><span class="sxs-lookup"><span data-stu-id="589c2-192">Creating a MobileXpense test user</span></span>

<span data-ttu-id="589c2-193">Nesta seção, você criará uma usuária chamada Brenda Fernandes no MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="589c2-193">In this section, you create a user called Britta Simon in MobileXpense.</span></span> <span data-ttu-id="589c2-194">Trabalhe com a [equipe de suporte do MobileXpense](http://www.mobilexpense.net/contact) para adicionar os usuários na plataforma do MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="589c2-194">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add the users in the MobileXpense platform.</span></span> <span data-ttu-id="589c2-195">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="589c2-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="589c2-196">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="589c2-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="589c2-197">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo-lhe acesso ao MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="589c2-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MobileXpense.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="589c2-199">**Para atribuir Brenda Fernandes ao MobileXpense, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="589c2-199">**To assign Britta Simon to MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="589c2-200">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="589c2-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="589c2-202">Na lista de aplicativos, selecione **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="589c2-202">In the applications list, select **MobileXpense**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_app.png) 

3. <span data-ttu-id="589c2-204">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="589c2-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="589c2-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="589c2-206">Click **Add** button.</span></span> <span data-ttu-id="589c2-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="589c2-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="589c2-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="589c2-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="589c2-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="589c2-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="589c2-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="589c2-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="589c2-212">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="589c2-212">Testing single sign-on</span></span>

<span data-ttu-id="589c2-213">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="589c2-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="589c2-214">Ao clicar no bloco do MobileXpense no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="589c2-214">When you click the MobileXpense tile in the Access Panel, you should get automatically signed-on to your MobileXpense application.</span></span>
<span data-ttu-id="589c2-215">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="589c2-215">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="589c2-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="589c2-216">Additional resources</span></span>

* [<span data-ttu-id="589c2-217">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="589c2-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="589c2-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="589c2-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_203.png

