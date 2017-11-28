---
title: "Tutorial: integração do Azure Active Directory ao Certify | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Certify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bbb2357d17535de438555a0b1f8256b134c8a40e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="73a08-103">Tutorial: Integração do Active Directory do Azure ao Certify</span><span class="sxs-lookup"><span data-stu-id="73a08-103">Tutorial: Azure Active Directory integration with Certify</span></span>

<span data-ttu-id="73a08-104">Neste tutorial, você aprenderá a integrar o Certify ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="73a08-104">In this tutorial, you learn how to integrate Certify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73a08-105">A integração do Certify ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="73a08-105">Integrating Certify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="73a08-106">No AD do Azure, é possível controlar  quem tem acesso ao Certify</span><span class="sxs-lookup"><span data-stu-id="73a08-106">You can control in Azure AD who has access to Certify</span></span>
- <span data-ttu-id="73a08-107">Você pode permitir que seus usuários façam logon automaticamente no Certify (Logon Único) com as contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73a08-107">You can enable your users to automatically get signed-on to Certify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73a08-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="73a08-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="73a08-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73a08-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73a08-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="73a08-110">Prerequisites</span></span>

<span data-ttu-id="73a08-111">Para configurar a integração do AD do Azure ao Certify, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="73a08-111">To configure Azure AD integration with Certify, you need the following items:</span></span>

- <span data-ttu-id="73a08-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73a08-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73a08-113">Uma assinatura habilitada para logon único do Certify</span><span class="sxs-lookup"><span data-stu-id="73a08-113">A Certify single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73a08-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="73a08-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73a08-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="73a08-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73a08-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="73a08-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73a08-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73a08-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73a08-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="73a08-118">Scenario description</span></span>
<span data-ttu-id="73a08-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="73a08-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73a08-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="73a08-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73a08-121">Adicionando o Certify da galeria</span><span class="sxs-lookup"><span data-stu-id="73a08-121">Adding Certify from the gallery</span></span>
2. <span data-ttu-id="73a08-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73a08-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certify-from-the-gallery"></a><span data-ttu-id="73a08-123">Adicionando o Certify da galeria</span><span class="sxs-lookup"><span data-stu-id="73a08-123">Adding Certify from the gallery</span></span>
<span data-ttu-id="73a08-124">Para configurar a integração do Certify ao AD do Azure, você precisa adicionar o Certify à sua lista de aplicativos SaaS gerenciados desde a galeria.</span><span class="sxs-lookup"><span data-stu-id="73a08-124">To configure the integration of Certify into Azure AD, you need to add Certify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="73a08-125">**Para adicionar o Certify da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73a08-125">**To add Certify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="73a08-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="73a08-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="73a08-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="73a08-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="73a08-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="73a08-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="73a08-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="73a08-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="73a08-133">Na caixa de pesquisa, digite **Certify**.</span><span class="sxs-lookup"><span data-stu-id="73a08-133">In the search box, type **Certify**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-certify-tutorial/tutorial_certify_search.png)

5. <span data-ttu-id="73a08-135">No painel de resultados, selecione **Certify** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="73a08-135">In the results panel, select **Certify**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-certify-tutorial/tutorial_certify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73a08-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73a08-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="73a08-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Certify, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="73a08-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="73a08-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Certify é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73a08-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Certify is to a user in Azure AD.</span></span> <span data-ttu-id="73a08-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Certify.</span><span class="sxs-lookup"><span data-stu-id="73a08-140">In other words, a link relationship between an Azure AD user and the related user in Certify needs to be established.</span></span>

<span data-ttu-id="73a08-141">No Certify, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="73a08-141">In Certify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="73a08-142">Para configurar e testar o logon único do AD do Azure com o Certify, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="73a08-142">To configure and test Azure AD single sign-on with Certify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="73a08-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="73a08-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="73a08-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="73a08-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73a08-145">**[Criação de um usuário de teste do Certify](#creating-a-certify-test-user)**: para ter um equivalente de Brenda Fernandes no Certify que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73a08-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="73a08-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="73a08-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73a08-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="73a08-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73a08-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="73a08-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73a08-149">Nesta seção, você vai habilitar o logon único do Azure AD no Portal do Azure e configurar o logon único em seu aplicativo Certify.</span><span class="sxs-lookup"><span data-stu-id="73a08-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Certify application.</span></span>

<span data-ttu-id="73a08-150">**Para configurar o logon único do AD do Azure com o Certify, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73a08-150">**To configure Azure AD single sign-on with Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="73a08-151">No portal do Azure, na página de integração do aplicativo **Certify**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="73a08-151">In the Azure portal, on the **Certify** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="73a08-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="73a08-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-certify-tutorial/tutorial_certify_samlbase.png)

3. <span data-ttu-id="73a08-155">Na seção **URLs e Domínio do Certify**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="73a08-155">On the **Certify Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-certify-tutorial/tutorial_certify_url.png)

    <span data-ttu-id="73a08-157">Na caixa de texto **Identificador**, digite a URL: `https://www.certify.com`</span><span class="sxs-lookup"><span data-stu-id="73a08-157">In the **Identifier** textbox, type the URL: `https://www.certify.com`</span></span>

4. <span data-ttu-id="73a08-158">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Bruto)** e, em seguida, salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="73a08-158">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-certify-tutorial/tutorial_certify_certificate.png) 

5. <span data-ttu-id="73a08-160">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="73a08-160">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-certify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73a08-162">Na seção **Configuração do Certify**, clique em **Configurar o Certify** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="73a08-162">On the **Certify Configuration** section, click **Configure Certify** to open **Configure sign-on** window.</span></span> <span data-ttu-id="73a08-163">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="73a08-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-certify-tutorial/tutorial_certify_configure.png) 

7. <span data-ttu-id="73a08-165">Para configurar o logon único no lado do **Certify**, é necessário enviar o **Certificado (Bruto)** baixado, a **URL de Saída, ID da Entidade SAML e URL do Serviço de Logon Único SAML** para a [equipe de suporte do Certify](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="73a08-165">To configure single sign-on on **Certify** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Certify support team](mailto:support@certify.com).</span></span> <span data-ttu-id="73a08-166">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="73a08-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="73a08-167">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="73a08-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="73a08-168">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="73a08-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="73a08-169">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73a08-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73a08-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73a08-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="73a08-171">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="73a08-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="73a08-173">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73a08-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="73a08-174">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="73a08-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-certify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73a08-176">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="73a08-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-certify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73a08-178">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73a08-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-certify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73a08-180">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="73a08-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-certify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73a08-182">a.</span><span class="sxs-lookup"><span data-stu-id="73a08-182">a.</span></span> <span data-ttu-id="73a08-183">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="73a08-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73a08-184">b.</span><span class="sxs-lookup"><span data-stu-id="73a08-184">b.</span></span> <span data-ttu-id="73a08-185">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="73a08-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73a08-186">c.</span><span class="sxs-lookup"><span data-stu-id="73a08-186">c.</span></span> <span data-ttu-id="73a08-187">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="73a08-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="73a08-188">d.</span><span class="sxs-lookup"><span data-stu-id="73a08-188">d.</span></span> <span data-ttu-id="73a08-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="73a08-189">Click **Create**.</span></span>
 
### <a name="creating-a-certify-test-user"></a><span data-ttu-id="73a08-190">Criando um usuário de teste do Certify</span><span class="sxs-lookup"><span data-stu-id="73a08-190">Creating a Certify test user</span></span>

<span data-ttu-id="73a08-191">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Certify.</span><span class="sxs-lookup"><span data-stu-id="73a08-191">The objective of this section is to create a user called Britta Simon in Certify.</span></span> <span data-ttu-id="73a08-192">O Certify dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="73a08-192">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="73a08-193">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="73a08-193">There is no action item for you in this section.</span></span> <span data-ttu-id="73a08-194">Um novo usuário será criado durante uma tentativa de acessar o Certify, caso ela ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="73a08-194">A new user will be created during an attempt to access Certify if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="73a08-195">Se precisar criar um usuário manualmente, entre em contato com a [equipe de suporte do Certify](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="73a08-195">If you need to create an user manually, you need to contact the [Certify support team](mailto:support@certify.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="73a08-196">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73a08-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="73a08-197">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Certify.</span><span class="sxs-lookup"><span data-stu-id="73a08-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Certify.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="73a08-199">**Para atribuir Brenda Fernandes ao Certify, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73a08-199">**To assign Britta Simon to Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="73a08-200">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="73a08-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="73a08-202">Na lista de aplicativos, selecione **Certify**.</span><span class="sxs-lookup"><span data-stu-id="73a08-202">In the applications list, select **Certify**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-certify-tutorial/tutorial_certify_app.png) 

3. <span data-ttu-id="73a08-204">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="73a08-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="73a08-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="73a08-206">Click **Add** button.</span></span> <span data-ttu-id="73a08-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73a08-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="73a08-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="73a08-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="73a08-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73a08-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73a08-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73a08-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73a08-212">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="73a08-212">Testing single sign-on</span></span>

<span data-ttu-id="73a08-213">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="73a08-213">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="73a08-214">Ao clicar no bloco do Certify no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo do Certify.</span><span class="sxs-lookup"><span data-stu-id="73a08-214">When you click the Certify tile in the Access Panel, you should get automatically signed-on to your Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73a08-215">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="73a08-215">Additional resources</span></span>

* [<span data-ttu-id="73a08-216">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="73a08-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73a08-217">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="73a08-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-certify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-certify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-certify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-certify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-certify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-certify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-certify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-certify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-certify-tutorial/tutorial_general_203.png

