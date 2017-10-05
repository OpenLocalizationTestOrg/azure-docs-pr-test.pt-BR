---
title: "Tutorial: Integração do Azure Active Directory ao itslearning | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o itslearning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 60587ba3-1396-4b8a-9ac1-e22a98e5e0ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 32c8a8dff533f726784fb52b9496c2cb50ecfde7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itslearning"></a><span data-ttu-id="0aba0-103">Tutorial: Integração do Azure Active Directory ao itslearning</span><span class="sxs-lookup"><span data-stu-id="0aba0-103">Tutorial: Azure Active Directory integration with itslearning</span></span>

<span data-ttu-id="0aba0-104">Neste tutorial, você aprende a integrar o itslearning ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0aba0-104">In this tutorial, you learn how to integrate itslearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0aba0-105">A integração do itslearning ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="0aba0-105">Integrating itslearning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0aba0-106">Você pode controlar no Azure AD quem terá acesso ao itslearning</span><span class="sxs-lookup"><span data-stu-id="0aba0-106">You can control in Azure AD who has access to itslearning</span></span>
- <span data-ttu-id="0aba0-107">Você pode permitir que seus usuários façam logon automaticamente no itslearning (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0aba0-107">You can enable your users to automatically get signed-on to itslearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0aba0-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0aba0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0aba0-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0aba0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0aba0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0aba0-110">Prerequisites</span></span>

<span data-ttu-id="0aba0-111">Para configurar a integração do Azure AD ao itslearning, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0aba0-111">To configure Azure AD integration with itslearning, you need the following items:</span></span>

- <span data-ttu-id="0aba0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0aba0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0aba0-113">Uma assinatura habilitada para logon único do itslearning</span><span class="sxs-lookup"><span data-stu-id="0aba0-113">An itslearning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0aba0-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0aba0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0aba0-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0aba0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0aba0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0aba0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0aba0-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0aba0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0aba0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0aba0-118">Scenario description</span></span>
<span data-ttu-id="0aba0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0aba0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0aba0-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="0aba0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0aba0-121">Adicionando itslearning da galeria</span><span class="sxs-lookup"><span data-stu-id="0aba0-121">Adding itslearning from the gallery</span></span>
2. <span data-ttu-id="0aba0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0aba0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itslearning-from-the-gallery"></a><span data-ttu-id="0aba0-123">Adicionando itslearning da galeria</span><span class="sxs-lookup"><span data-stu-id="0aba0-123">Adding itslearning from the gallery</span></span>
<span data-ttu-id="0aba0-124">Para configurar a integração do itslearning ao Azure AD, você precisará adicionar o itslearning da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0aba0-124">To configure the integration of itslearning into Azure AD, you need to add itslearning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0aba0-125">**Para adicionar o itslearning da galera, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0aba0-125">**To add itslearning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0aba0-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0aba0-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0aba0-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0aba0-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0aba0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0aba0-133">Na caixa de pesquisa, digite **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-133">In the search box, type **itslearning**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_search.png)

5. <span data-ttu-id="0aba0-135">No painel de resultados, selecione **itslearning** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0aba0-135">In the results panel, select **itslearning**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0aba0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0aba0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0aba0-138">Nesta seção, você configura e testa o logon único do Azure AD com o itslearning com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="0aba0-138">In this section, you configure and test Azure AD single sign-on with itslearning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0aba0-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do itslearning é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aba0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in itslearning is to a user in Azure AD.</span></span> <span data-ttu-id="0aba0-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do itslearning.</span><span class="sxs-lookup"><span data-stu-id="0aba0-140">In other words, a link relationship between an Azure AD user and the related user in itslearning needs to be established.</span></span>

<span data-ttu-id="0aba0-141">No itslearning, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="0aba0-141">In itslearning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0aba0-142">Para configurar e testar o logon único do Azure AD com o itslearning, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="0aba0-142">To configure and test Azure AD single sign-on with itslearning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0aba0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0aba0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0aba0-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0aba0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0aba0-145">**[Como criar um usuário de teste do itslearning](#creating-an-itslearning-test-user)** – para ter um equivalente de Brenda Fernandes no itslearning que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aba0-145">**[Creating an itslearning test user](#creating-an-itslearning-test-user)** - to have a counterpart of Britta Simon in itslearning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0aba0-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0aba0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0aba0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="0aba0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0aba0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0aba0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0aba0-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo itslearning.</span><span class="sxs-lookup"><span data-stu-id="0aba0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your itslearning application.</span></span>

<span data-ttu-id="0aba0-150">**Para configurar o logon único do Azure AD com o itslearning, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0aba0-150">**To configure Azure AD single sign-on with itslearning, perform the following steps:**</span></span>

1. <span data-ttu-id="0aba0-151">No portal do Azure, na página de integração de aplicativos do **itslearning**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-151">In the Azure portal, on the **itslearning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0aba0-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="0aba0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_samlbase.png)

3. <span data-ttu-id="0aba0-155">Na seção **URLs e Domínio do itslearning**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0aba0-155">On the **itslearning Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_url.png)

    <span data-ttu-id="0aba0-157">a.</span><span class="sxs-lookup"><span data-stu-id="0aba0-157">a.</span></span> <span data-ttu-id="0aba0-158">Na caixa de texto **URL de Logon**, digite uma URL como:</span><span class="sxs-lookup"><span data-stu-id="0aba0-158">In the **Sign-on URL** textbox, type a URL as:</span></span>
    | |
    |--| 
    | `https://www.itslearning.com/index.aspx`|
    | `https://us1.itslearning.com/index.aspx`|

    <span data-ttu-id="0aba0-159">b.</span><span class="sxs-lookup"><span data-stu-id="0aba0-159">b.</span></span> <span data-ttu-id="0aba0-160">Na caixa de texto **Identificador**, digite uma URL como: `urn:mace:saml2v2.no:services:com.itslearning`</span><span class="sxs-lookup"><span data-stu-id="0aba0-160">In the **Identifier** textbox, type a URL as: `urn:mace:saml2v2.no:services:com.itslearning`</span></span>

4. <span data-ttu-id="0aba0-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0aba0-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_certificate.png) 

5. <span data-ttu-id="0aba0-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0aba0-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itslearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0aba0-165">Para configurar o lado do **itslearning** de logon único, você precisa enviar o **XML de Metadados** baixado para [a equipe de suporte do itslearning](mailto:support@itslearning.com).</span><span class="sxs-lookup"><span data-stu-id="0aba0-165">To configure single sign-on on **itslearning** side, you need to send the downloaded **Metadata XML** to [itslearning support team](mailto:support@itslearning.com).</span></span> <span data-ttu-id="0aba0-166">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="0aba0-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0aba0-167">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="0aba0-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0aba0-168">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0aba0-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0aba0-169">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0aba0-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0aba0-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0aba0-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="0aba0-171">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0aba0-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0aba0-173">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0aba0-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0aba0-174">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0aba0-176">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0aba0-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0aba0-178">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0aba0-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0aba0-180">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0aba0-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0aba0-182">a.</span><span class="sxs-lookup"><span data-stu-id="0aba0-182">a.</span></span> <span data-ttu-id="0aba0-183">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0aba0-184">b.</span><span class="sxs-lookup"><span data-stu-id="0aba0-184">b.</span></span> <span data-ttu-id="0aba0-185">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0aba0-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0aba0-186">c.</span><span class="sxs-lookup"><span data-stu-id="0aba0-186">c.</span></span> <span data-ttu-id="0aba0-187">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0aba0-188">d.</span><span class="sxs-lookup"><span data-stu-id="0aba0-188">d.</span></span> <span data-ttu-id="0aba0-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-189">Click **Create**.</span></span>
 
### <a name="creating-an-itslearning-test-user"></a><span data-ttu-id="0aba0-190">Como criar um usuário de teste do itslearning</span><span class="sxs-lookup"><span data-stu-id="0aba0-190">Creating an itslearning test user</span></span>

<span data-ttu-id="0aba0-191">Nesta seção, você cria um usuário chamado Brenda Fernandes no itslearning.</span><span class="sxs-lookup"><span data-stu-id="0aba0-191">In this section, you create a user called Britta Simon in itslearning.</span></span> <span data-ttu-id="0aba0-192">Trabalhe com a [equipe de suporte ao cliente do itslearning](mailto:support@itslearning.com) para adicionar os usuários na plataforma do itslearning.</span><span class="sxs-lookup"><span data-stu-id="0aba0-192">Work with [itslearning Client support team](mailto:support@itslearning.com) to add the users in the itslearning platform.</span></span> <span data-ttu-id="0aba0-193">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="0aba0-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0aba0-194">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0aba0-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0aba0-195">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao itslearning.</span><span class="sxs-lookup"><span data-stu-id="0aba0-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to itslearning.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0aba0-197">**Para atribuir Brenda Fernandes ao itslearning, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0aba0-197">**To assign Britta Simon to itslearning, perform the following steps:**</span></span>

1. <span data-ttu-id="0aba0-198">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0aba0-200">Na lista de aplicativos, selecione **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-200">In the applications list, select **itslearning**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_app.png) 

3. <span data-ttu-id="0aba0-202">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0aba0-204">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0aba0-204">Click **Add** button.</span></span> <span data-ttu-id="0aba0-205">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0aba0-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0aba0-207">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0aba0-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0aba0-208">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0aba0-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0aba0-209">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0aba0-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0aba0-210">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0aba0-210">Testing single sign-on</span></span>

<span data-ttu-id="0aba0-211">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="0aba0-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0aba0-212">Quando você clicar no bloco do itslearning no painel de acesso, deverá obter a página de logon do aplicativo itslearning.</span><span class="sxs-lookup"><span data-stu-id="0aba0-212">When you click the itslearning tile in the Access Panel, you should get login page of itslearning application.</span></span> <span data-ttu-id="0aba0-213">Clique em **Fazer logon com o Microsoft Azure ACS1** para fazer logon com êxito no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0aba0-213">Click **Log in with Windows Azure ACS1** for successful login into the application.</span></span>

  ![Logon](./media/active-directory-saas-itslearning-tutorial/login.png)

<span data-ttu-id="0aba0-215">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0aba0-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0aba0-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0aba0-216">Additional resources</span></span>

* [<span data-ttu-id="0aba0-217">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0aba0-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0aba0-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0aba0-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_203.png

