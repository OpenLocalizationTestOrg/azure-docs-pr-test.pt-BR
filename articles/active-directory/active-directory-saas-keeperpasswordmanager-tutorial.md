---
title: "Tutorial: Integração do Azure Active Directory ao Gerenciador de Senhas Protetor e Cofre Digital | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Gerenciador de Senhas Protetor e Cofre Digital."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 36504a281756b980e3348e7f892ba08821873b52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="9f6b8-103">Tutorial: integração do Azure Active Directory ao Gerenciador de Senhas Protetor e Cofre Digital</span><span class="sxs-lookup"><span data-stu-id="9f6b8-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="9f6b8-104">Neste tutorial, você aprenderá a integrar o Gerenciador de Senhas Protetor e o Cofre Digital ao Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9f6b8-104">In this tutorial, you learn how to integrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f6b8-105">Integrar do Gerenciador de Senhas Protetor e do Cofre Digital ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="9f6b8-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9f6b8-106">Você pode controlar no Azure AD quem tem acesso ao Gerenciador de Senhas Protetor e Cofre Digital</span><span class="sxs-lookup"><span data-stu-id="9f6b8-106">You can control in Azure AD who has access to Keeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="9f6b8-107">Você pode habilitar os usuários para serem automaticamente conectados ao Gerenciador de Senhas Protetor e Cofre Digital (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f6b8-107">You can enable your users to automatically get signed-on to Keeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f6b8-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6b8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9f6b8-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f6b8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f6b8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9f6b8-110">Prerequisites</span></span>

<span data-ttu-id="9f6b8-111">Para configurar a integração do Azure AD ao Gerenciador de Senhas Protetor e Cofre Digital, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9f6b8-111">To configure Azure AD integration with Keeper Password Manager & Digital Vault, you need the following items:</span></span>

- <span data-ttu-id="9f6b8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f6b8-113">Uma assinatura habilitada para logon único do Gerenciador de Senhas Protetor e Cofre Digital</span><span class="sxs-lookup"><span data-stu-id="9f6b8-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f6b8-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f6b8-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9f6b8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f6b8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f6b8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f6b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f6b8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9f6b8-118">Scenario description</span></span>
<span data-ttu-id="9f6b8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f6b8-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="9f6b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f6b8-121">Adicionando Gerenciador de Senhas Protetor e Cofre Digital da galeria</span><span class="sxs-lookup"><span data-stu-id="9f6b8-121">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
2. <span data-ttu-id="9f6b8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6b8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-the-gallery"></a><span data-ttu-id="9f6b8-123">Adicionando Gerenciador de Senhas Protetor e Cofre Digital da galeria</span><span class="sxs-lookup"><span data-stu-id="9f6b8-123">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
<span data-ttu-id="9f6b8-124">Para configurar a integração do Gerenciador de Senhas Protetor e Cofre Digital no Azure AD, você precisa adicionar o Gerenciador de Senhas Protetor e Cofre Digital da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-124">To configure the integration of Keeper Password Manager & Digital Vault into Azure AD, you need to add Keeper Password Manager & Digital Vault from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9f6b8-125">**Para adicionar o Gerenciador de Senhas Protetor e Cofre Digital da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f6b8-125">**To add Keeper Password Manager & Digital Vault from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9f6b8-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9f6b8-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9f6b8-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9f6b8-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9f6b8-133">Na caixa de pesquisa, digite **Gerenciador de Senhas Protetor e Cofre Digital**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-133">In the search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="9f6b8-135">No painel de resultados, selecione **Gerenciador de Senhas Protetor e Cofre Digital** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-135">In the results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f6b8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f6b8-138">Nesta seção, você pode configurar e testar o logon único do Azure AD com o Gerenciador de Senhas Protetor e Cofre Digital com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="9f6b8-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9f6b8-139">Para o logon único funcionar, o Azure AD precisa saber qual é o usuário correspondente no Gerenciador de Senhas Protetor e Cofre Digital para um usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Keeper Password Manager & Digital Vault is to a user in Azure AD.</span></span> <span data-ttu-id="9f6b8-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Gerenciador de Senhas Protetor e Cofre Digital.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-140">In other words, a link relationship between an Azure AD user and the related user in Keeper Password Manager & Digital Vault needs to be established.</span></span>

<span data-ttu-id="9f6b8-141">No Gerenciador de Senhas Protetor e Cofre Digital, atribua o valor do **nome de usuário** no Azure AD como o valor de **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-141">In Keeper Password Manager & Digital Vault, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9f6b8-142">Para configurar e testar o logon único do Azure AD com o Gerenciador de Senhas Protetor e Cofre Digital, você precisa concluir os blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6b8-142">To configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9f6b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9f6b8-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f6b8-145">**[Como criar um usuário de teste do Gerenciador de Senhas Protetor e Cofre Digital](#creating-a-keeperpasswordmanager-test-user)** – para ter um equivalente de Brenda Fernandes no Gerenciador de Senhas Protetor e Cofre Digital vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - to have a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f6b8-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f6b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f6b8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f6b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f6b8-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Gerenciador de Senhas Protetor e Cofre Digital.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="9f6b8-150">**Para configurar o logon único do Azure AD com o Gerenciador de Senhas Protetor e Cofre Digital, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f6b8-150">**To configure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="9f6b8-151">No portal do Azure, na página de integração do aplicativo do **Gerenciador de Senhas Protetor e Cofre Digital**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-151">In the Azure portal, on the **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9f6b8-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="9f6b8-155">Na seção **Gerenciador de Senhas Protetor e Domínio do Cofre Digital e URLs**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9f6b8-155">On the **Keeper Password Manager & Digital Vault Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="9f6b8-157">a.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-157">a.</span></span> <span data-ttu-id="9f6b8-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="9f6b8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="9f6b8-159">b.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-159">b.</span></span> <span data-ttu-id="9f6b8-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="9f6b8-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="9f6b8-161">c.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-161">c.</span></span> <span data-ttu-id="9f6b8-162">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="9f6b8-162">In the **Identifier** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9f6b8-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-163">These values are not real.</span></span> <span data-ttu-id="9f6b8-164">Atualize esses valores com a URL de Resposta real e a URL de Logon.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9f6b8-165">Entre em contato com a [equipe de suporte do Gerenciador de Senhas Protetor e Cliente do Cofre Digital](https://keepersecurity.com/contact.html) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) to get these values.</span></span> 

4. <span data-ttu-id="9f6b8-166">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="9f6b8-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9f6b8-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="9f6b8-170">Na seção **Configuração do Gerenciador de Senhas Protetor e Cofre Digital**, clique em **Configurar Gerenciador de Senhas Protetor e Cofre Digital** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-170">On the **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9f6b8-171">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="9f6b8-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="9f6b8-173">Para configurar o logon único no lado da **Configuração do Gerenciador de Senhas Protetor e Cofre Digital**, siga as orientações fornecidas no [Guia de Suporte do Protetor](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span><span class="sxs-lookup"><span data-stu-id="9f6b8-173">To configure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow the guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="9f6b8-174">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="9f6b8-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9f6b8-175">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9f6b8-176">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f6b8-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f6b8-177">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6b8-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f6b8-178">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9f6b8-180">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f6b8-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9f6b8-181">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f6b8-183">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f6b8-185">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f6b8-187">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9f6b8-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f6b8-189">a.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-189">a.</span></span> <span data-ttu-id="9f6b8-190">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f6b8-191">b.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-191">b.</span></span> <span data-ttu-id="9f6b8-192">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f6b8-193">c.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-193">c.</span></span> <span data-ttu-id="9f6b8-194">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9f6b8-195">d.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-195">d.</span></span> <span data-ttu-id="9f6b8-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="9f6b8-197">Como criar um usuário de teste do Gerenciador de Senhas Protetor Cofre Digital</span><span class="sxs-lookup"><span data-stu-id="9f6b8-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="9f6b8-198">Para permitir que os usuários do Azure AD fazer logon no Gerenciador de Senhas Protetor e Cofre Digital, eles devem ser provisionados no Gerenciador de Senhas Protetor e Cofre Digital.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-198">To enable Azure AD users to log in to Keeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="9f6b8-199">O aplicativo dá suporte ao provisionamento de usuário just-in-time e, após a autenticação, os usuários serão automaticamente criados no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-199">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="9f6b8-200">Você poderá contatar [Suporte Protetor](https://keepersecurity.com/contact.html) se quiser configurar usuários manualmente.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want to setup users manually.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9f6b8-201">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6b8-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9f6b8-202">Nesta seção, você habilita Brenda Fernandes a usar logon único do Azure concedendo acesso ao Gerenciador de Senhas Protetor e Cofre Digital.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Keeper Password Manager & Digital Vault.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9f6b8-204">**Para atribuir Brenda Fernandes ao Gerenciador de Senhas Protetor e Cofre Digital, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f6b8-204">**To assign Britta Simon to Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="9f6b8-205">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9f6b8-207">Na lista de aplicativos, selecione **Gerenciador de Senhas Protetor e Cofre Digital**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-207">In the applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="9f6b8-209">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9f6b8-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-211">Click **Add** button.</span></span> <span data-ttu-id="9f6b8-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9f6b8-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9f6b8-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f6b8-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f6b8-217">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9f6b8-217">Testing single sign-on</span></span>

<span data-ttu-id="9f6b8-218">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9f6b8-219">Quando você clicar no bloco Gerenciador de Senhas Protetor e Cofre Digital no Painel de Acesso, deverá obter a página de logon do aplicativo Gerenciador de Senhas Protetor e Cofre Digital.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-219">When you click the Keeper Password Manager & Digital Vault tile in the Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="9f6b8-220">Após a autenticação bem-sucedida, você deverá entrar no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f6b8-220">Upon successful authentication, you should get into the application.</span></span> <span data-ttu-id="9f6b8-221">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9f6b8-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9f6b8-222">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9f6b8-222">Additional resources</span></span>

* [<span data-ttu-id="9f6b8-223">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6b8-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f6b8-224">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f6b8-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

