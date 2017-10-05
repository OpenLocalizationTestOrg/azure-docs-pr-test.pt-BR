---
title: "Tutorial: integração do Azure Active Directory ao Projectplace | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Projectplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: bb9dd10c887cb0e42e544066d9b0dcfa554e10ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="2a380-103">Tutorial: Integração do Active Directory do Azure ao Projectplace</span><span class="sxs-lookup"><span data-stu-id="2a380-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="2a380-104">Neste tutorial, você aprenderá a integrar o Projectplace ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2a380-104">In this tutorial, you learn how to integrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2a380-105">A integração do Projectplace ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="2a380-105">Integrating Projectplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2a380-106">Você pode controlar no Azure AD quem tem acesso ao Projectplace</span><span class="sxs-lookup"><span data-stu-id="2a380-106">You can control in Azure AD who has access to Projectplace</span></span>
- <span data-ttu-id="2a380-107">Você pode permitir que os usuários façam logon automaticamente no Projectplace (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a380-107">You can enable your users to automatically get signed-on to Projectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2a380-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2a380-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2a380-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2a380-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a380-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2a380-110">Prerequisites</span></span>

<span data-ttu-id="2a380-111">Para configurar a integração do Azure AD ao Projectplace, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2a380-111">To configure Azure AD integration with Projectplace, you need the following items:</span></span>

- <span data-ttu-id="2a380-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2a380-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2a380-113">Uma assinatura do Projectplace com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="2a380-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2a380-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2a380-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2a380-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2a380-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2a380-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2a380-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2a380-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a380-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2a380-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2a380-118">Scenario description</span></span>
<span data-ttu-id="2a380-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2a380-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2a380-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="2a380-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2a380-121">Adicionar o Projectplace da galeria</span><span class="sxs-lookup"><span data-stu-id="2a380-121">Adding Projectplace from the gallery</span></span>
2. <span data-ttu-id="2a380-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2a380-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-the-gallery"></a><span data-ttu-id="2a380-123">Adicionar o Projectplace da galeria</span><span class="sxs-lookup"><span data-stu-id="2a380-123">Adding Projectplace from the gallery</span></span>
<span data-ttu-id="2a380-124">Para configurar a integração do Projectplace ao Azure AD, você precisa adicionar o Projectplace à sua lista de aplicativos SaaS gerenciados na galeria.</span><span class="sxs-lookup"><span data-stu-id="2a380-124">To configure the integration of Projectplace into Azure AD, you need to add Projectplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2a380-125">**Para adicionar o Projectplace na galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2a380-125">**To add Projectplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2a380-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2a380-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2a380-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2a380-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2a380-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2a380-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="2a380-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2a380-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="2a380-133">Na caixa de pesquisa, digite **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="2a380-133">In the search box, type **Projectplace**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="2a380-135">No painel de resultados, selecione **Projectplace** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2a380-135">In the results panel, select **Projectplace**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2a380-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2a380-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2a380-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Projectplace, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="2a380-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2a380-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Projectplace é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a380-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Projectplace is to a user in Azure AD.</span></span> <span data-ttu-id="2a380-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Projectplace.</span><span class="sxs-lookup"><span data-stu-id="2a380-140">In other words, a link relationship between an Azure AD user and the related user in Projectplace needs to be established.</span></span>

<span data-ttu-id="2a380-141">No Projectplace, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="2a380-141">In Projectplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2a380-142">Para configurar e testar o logon único do Azure AD com o Projectplace, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="2a380-142">To configure and test Azure AD single sign-on with Projectplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2a380-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2a380-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2a380-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2a380-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2a380-145">**[Criação de um usuário de teste do Projectplace](#creating-a-projectplace-test-user)** – para ter um equivalente de Brenda Fernandes no Projectplace que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a380-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - to have a counterpart of Britta Simon in Projectplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2a380-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a380-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2a380-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="2a380-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2a380-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a380-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2a380-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Projectplace.</span><span class="sxs-lookup"><span data-stu-id="2a380-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="2a380-150">**Para configurar o logon único do Azure AD com o Projectplace, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2a380-150">**To configure Azure AD single sign-on with Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="2a380-151">No Portal do Azure, na página de integração de aplicativos do **Projectplace**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="2a380-151">In the Azure portal, on the **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2a380-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="2a380-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="2a380-155">Na seção **URLs e Domínio do Projectplace**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2a380-155">On the **Projectplace Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="2a380-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="2a380-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2a380-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="2a380-158">This value is not real.</span></span> <span data-ttu-id="2a380-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="2a380-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="2a380-160">Entre em contato com a [equipe de suporte ao cliente do Projectplace](https://success.planview.com/Projectplace/Support) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="2a380-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) to get this value.</span></span> 
 
4. <span data-ttu-id="2a380-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2a380-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="2a380-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2a380-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="2a380-165">Para configurar o logon único no lado do **Projectplace**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="2a380-165">To configure single sign-on on **Projectplace** side, you need to send the downloaded **Metadata XML** to [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="2a380-166">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="2a380-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="2a380-167">A configuração de logon único deve ser executada pela [equipe de suporte do Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="2a380-167">The single sign-on configuration has to be performed by the [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="2a380-168">Assim que a configuração for concluída, você receberá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="2a380-168">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="2a380-169">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="2a380-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2a380-170">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2a380-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2a380-171">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2a380-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2a380-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2a380-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="2a380-173">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2a380-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="2a380-175">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2a380-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2a380-176">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2a380-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2a380-178">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2a380-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2a380-180">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a380-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2a380-182">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2a380-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2a380-184">a.</span><span class="sxs-lookup"><span data-stu-id="2a380-184">a.</span></span> <span data-ttu-id="2a380-185">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="2a380-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2a380-186">b.</span><span class="sxs-lookup"><span data-stu-id="2a380-186">b.</span></span> <span data-ttu-id="2a380-187">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2a380-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2a380-188">c.</span><span class="sxs-lookup"><span data-stu-id="2a380-188">c.</span></span> <span data-ttu-id="2a380-189">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="2a380-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2a380-190">d.</span><span class="sxs-lookup"><span data-stu-id="2a380-190">d.</span></span> <span data-ttu-id="2a380-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2a380-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="2a380-192">Criação de um usuário de teste do Projectplace</span><span class="sxs-lookup"><span data-stu-id="2a380-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="2a380-193">Para permitir que os usuários do AD do Azure façam logon no Projectplace, eles devem ser provisionados no Projectplace.</span><span class="sxs-lookup"><span data-stu-id="2a380-193">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="2a380-194">No caso do Projectplace, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="2a380-194">In the case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="2a380-195">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2a380-195">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2a380-196">Faça logon em seu site de empresa do **Projectplace** como administrador.</span><span class="sxs-lookup"><span data-stu-id="2a380-196">Log in to your **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="2a380-197">Vá para **Pessoas** e clique em **Membros**.</span><span class="sxs-lookup"><span data-stu-id="2a380-197">Go to **People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="2a380-198">![Pessoas](./media/active-directory-saas-projectplace-tutorial/ic790228.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="2a380-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="2a380-199">Clique em **Adicionar Membro**.</span><span class="sxs-lookup"><span data-stu-id="2a380-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="2a380-200">![Adicionar Membros](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Adicionar membros")</span><span class="sxs-lookup"><span data-stu-id="2a380-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="2a380-201">Na seção **Adicionar Membro** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2a380-201">In the **Add Member** section, perform the following steps:</span></span>
   
    <span data-ttu-id="2a380-202">![Novos Membros](./media/active-directory-saas-projectplace-tutorial/ic790233.png "Novos Membros")</span><span class="sxs-lookup"><span data-stu-id="2a380-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="2a380-203">a.</span><span class="sxs-lookup"><span data-stu-id="2a380-203">a.</span></span> <span data-ttu-id="2a380-204">Na caixa de texto **Novos Membros** , digite o endereço de email de uma conta válida do AAD que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="2a380-204">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="2a380-205">b.</span><span class="sxs-lookup"><span data-stu-id="2a380-205">b.</span></span> <span data-ttu-id="2a380-206">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="2a380-206">Click **Send**.</span></span>

   <span data-ttu-id="2a380-207">Um email incluindo um link para confirmar a conta antes que ela se torne ativa é enviado ao titular da conta do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a380-207">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="2a380-208">É possível usar qualquer outra ferramenta de criação da conta de usuário do Projectplace ou APIs fornecidas pelo Projectplace para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="2a380-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2a380-209">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2a380-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2a380-210">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Projectplace.</span><span class="sxs-lookup"><span data-stu-id="2a380-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Projectplace.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="2a380-212">**Para atribuir Brenda Fernandes ao Projectplace, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2a380-212">**To assign Britta Simon to Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="2a380-213">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2a380-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2a380-215">Na lista de aplicativos, selecione **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="2a380-215">In the applications list, select **Projectplace**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="2a380-217">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2a380-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="2a380-219">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2a380-219">Click **Add** button.</span></span> <span data-ttu-id="2a380-220">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a380-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="2a380-222">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2a380-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2a380-223">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a380-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2a380-224">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a380-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2a380-225">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="2a380-225">Testing single sign-on</span></span>

<span data-ttu-id="2a380-226">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="2a380-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2a380-227">Ao clicar no bloco do Projectplace no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Projectplace.</span><span class="sxs-lookup"><span data-stu-id="2a380-227">When you click the Projectplace tile in the Access Panel, you should get automatically signed-on to your Projectplace application.</span></span>
<span data-ttu-id="2a380-228">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2a380-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2a380-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2a380-229">Additional resources</span></span>

* [<span data-ttu-id="2a380-230">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2a380-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2a380-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2a380-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

