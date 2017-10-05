---
title: "Tutorial: Integração do Azure Active Directory com o Lucidchart | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Lucidchart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2dea669f03c893632c08d30feeb3173efc2d8243
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="34bf0-103">Tutorial: Integração do Active Directory do Azure com o Lucidchart</span><span class="sxs-lookup"><span data-stu-id="34bf0-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="34bf0-104">Neste tutorial, você aprenderá como integrar o Lucidchart ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="34bf0-104">In this tutorial, you learn how to integrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34bf0-105">A integração do Lucidchart ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="34bf0-105">Integrating Lucidchart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="34bf0-106">Você pode controlar no Azure AD quem tem acesso ao Lucidchart</span><span class="sxs-lookup"><span data-stu-id="34bf0-106">You can control in Azure AD who has access to Lucidchart</span></span>
- <span data-ttu-id="34bf0-107">Você pode habilitar que usuários façam logon automaticamente no Lucidchart (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="34bf0-107">You can enable your users to automatically get signed-on to Lucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34bf0-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="34bf0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="34bf0-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="34bf0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34bf0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="34bf0-110">Prerequisites</span></span>

<span data-ttu-id="34bf0-111">Para configurar a integração do Azure AD ao Lucidchart, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="34bf0-111">To configure Azure AD integration with Lucidchart, you need the following items:</span></span>

- <span data-ttu-id="34bf0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="34bf0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34bf0-113">Uma assinatura do Lucidchart com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="34bf0-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34bf0-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="34bf0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34bf0-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="34bf0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34bf0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="34bf0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34bf0-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34bf0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34bf0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="34bf0-118">Scenario description</span></span>
<span data-ttu-id="34bf0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="34bf0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34bf0-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="34bf0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34bf0-121">Adicionar o Lucidchart da galeria</span><span class="sxs-lookup"><span data-stu-id="34bf0-121">Adding Lucidchart from the gallery</span></span>
2. <span data-ttu-id="34bf0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="34bf0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-the-gallery"></a><span data-ttu-id="34bf0-123">Adicionar o Lucidchart da galeria</span><span class="sxs-lookup"><span data-stu-id="34bf0-123">Adding Lucidchart from the gallery</span></span>
<span data-ttu-id="34bf0-124">Para configurar a integração do Lucidchart ao Azure AD, você precisará adicionar o Lucidchart da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="34bf0-124">To configure the integration of Lucidchart into Azure AD, you need to add Lucidchart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="34bf0-125">**Para adicionar o Lucidchart da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="34bf0-125">**To add Lucidchart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="34bf0-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="34bf0-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="34bf0-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="34bf0-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="34bf0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="34bf0-133">Na caixa de pesquisa, digite **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-133">In the search box, type **Lucidchart**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="34bf0-135">No painel de resultados, selecione **Lucidchart** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="34bf0-135">In the results panel, select **Lucidchart**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34bf0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="34bf0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34bf0-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Lucidchart, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="34bf0-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="34bf0-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Lucidchart é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34bf0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lucidchart is to a user in Azure AD.</span></span> <span data-ttu-id="34bf0-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="34bf0-140">In other words, a link relationship between an Azure AD user and the related user in Lucidchart needs to be established.</span></span>

<span data-ttu-id="34bf0-141">No Lucidchart, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="34bf0-141">In Lucidchart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="34bf0-142">Para configurar e testar o logon único do Azure AD com o Lucidchart, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="34bf0-142">To configure and test Azure AD single sign-on with Lucidchart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="34bf0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="34bf0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="34bf0-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="34bf0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34bf0-145">**[Criação de um usuário de teste do Lucidchart](#creating-a-lucidchart-test-user)** – para ter um equivalente de Brenda Fernandes no Lucidchart que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34bf0-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - to have a counterpart of Britta Simon in Lucidchart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="34bf0-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="34bf0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34bf0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="34bf0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34bf0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="34bf0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34bf0-149">Nesta seção, você vai habilitar o logon único do Azure AD no portal do Azure e configurar o logon único em seu aplicativo Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="34bf0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="34bf0-150">**Para configurar o logon único do Azure AD com o Lucidchart, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="34bf0-150">**To configure Azure AD single sign-on with Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="34bf0-151">No portal do Azure, na página de integração de aplicativos do **Lucidchart**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-151">In the Azure portal, on the **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="34bf0-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="34bf0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="34bf0-155">Na seção **Domínio e URLs do Lucidchart**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="34bf0-155">On the **Lucidchart Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="34bf0-157">Na caixa de texto **URL de Logon**, digite uma URL como: `https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="34bf0-157">In the **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="34bf0-158">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="34bf0-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="34bf0-160">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="34bf0-160">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="34bf0-162">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Lucidchart como administrador.</span><span class="sxs-lookup"><span data-stu-id="34bf0-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="34bf0-163">No menu na parte superior, clique em **Equipe**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-163">In the menu on the top, click **Team**.</span></span>
   
    <span data-ttu-id="34bf0-164">![Equipe](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Equipe")</span><span class="sxs-lookup"><span data-stu-id="34bf0-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="34bf0-165">Clique em **Aplicativos \> Gerenciar SAML**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="34bf0-166">![Gerenciar SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Gerenciar SAML")</span><span class="sxs-lookup"><span data-stu-id="34bf0-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="34bf0-167">Na página do diálogo **Configurações de Autenticação SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="34bf0-167">On the **SAML Authentication Settings** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="34bf0-168">a.</span><span class="sxs-lookup"><span data-stu-id="34bf0-168">a.</span></span> <span data-ttu-id="34bf0-169">Selecione **Habilitar Autenticação SAML** e clique em **Opcional**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="34bf0-170">![Configurações de Autenticação SAML](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "Configurações de Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="34bf0-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="34bf0-171">b.</span><span class="sxs-lookup"><span data-stu-id="34bf0-171">b.</span></span> <span data-ttu-id="34bf0-172">Na caixa de texto **Domínio**, digite seu domínio e clique em **Alterar Certificado**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-172">In the **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="34bf0-173">![Alterar Certificado](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Alterar Certificado")</span><span class="sxs-lookup"><span data-stu-id="34bf0-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="34bf0-174">c.</span><span class="sxs-lookup"><span data-stu-id="34bf0-174">c.</span></span> <span data-ttu-id="34bf0-175">Abra o arquivo de metadados baixado, copie o conteúdo e cole-o na caixa de texto **Carregar Metadados** .</span><span class="sxs-lookup"><span data-stu-id="34bf0-175">Open your downloaded metadata file, copy the content, and then paste it into the **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="34bf0-176">![Carregar Metadados](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Carregar Metadados")</span><span class="sxs-lookup"><span data-stu-id="34bf0-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="34bf0-177">d.</span><span class="sxs-lookup"><span data-stu-id="34bf0-177">d.</span></span> <span data-ttu-id="34bf0-178">Selecione **Adicionar Automaticamente Novos Usuários à Equipe** e clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-178">Select **Automatically Add new users to the team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="34bf0-179">![Salvar Alterações](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Salvar Alterações")</span><span class="sxs-lookup"><span data-stu-id="34bf0-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="34bf0-180">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="34bf0-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="34bf0-181">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="34bf0-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="34bf0-182">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="34bf0-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34bf0-183">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="34bf0-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="34bf0-184">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="34bf0-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="34bf0-186">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="34bf0-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="34bf0-187">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34bf0-189">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="34bf0-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34bf0-191">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34bf0-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34bf0-193">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="34bf0-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34bf0-195">a.</span><span class="sxs-lookup"><span data-stu-id="34bf0-195">a.</span></span> <span data-ttu-id="34bf0-196">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34bf0-197">b.</span><span class="sxs-lookup"><span data-stu-id="34bf0-197">b.</span></span> <span data-ttu-id="34bf0-198">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="34bf0-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34bf0-199">c.</span><span class="sxs-lookup"><span data-stu-id="34bf0-199">c.</span></span> <span data-ttu-id="34bf0-200">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="34bf0-201">d.</span><span class="sxs-lookup"><span data-stu-id="34bf0-201">d.</span></span> <span data-ttu-id="34bf0-202">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="34bf0-203">Criar um usuário de teste do Lucidchart</span><span class="sxs-lookup"><span data-stu-id="34bf0-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="34bf0-204">Não há nenhum item de ação para a configuração de provisionamento de usuário para o Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="34bf0-204">There is no action item for you to configure user provisioning to Lucidchart.</span></span>  <span data-ttu-id="34bf0-205">Quando um usuário atribuído tenta fazer logon no Lucidchart usando o painel de acesso, o Lucidchart verifica se o usuário existe.</span><span class="sxs-lookup"><span data-stu-id="34bf0-205">When an assigned user tries to log into Lucidchart using the access panel, Lucidchart checks whether the user exists.</span></span>  

<span data-ttu-id="34bf0-206">Se não houver conta de usuário ainda, ela é criada automaticamente pelo Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="34bf0-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="34bf0-207">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="34bf0-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="34bf0-208">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="34bf0-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lucidchart.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="34bf0-210">**Para atribuir Brenda Fernandes ao Lucidchart, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="34bf0-210">**To assign Britta Simon to Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="34bf0-211">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="34bf0-213">Na lista de aplicativos, selecione **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-213">In the applications list, select **Lucidchart**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="34bf0-215">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="34bf0-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="34bf0-217">Click **Add** button.</span></span> <span data-ttu-id="34bf0-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34bf0-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="34bf0-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="34bf0-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="34bf0-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34bf0-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34bf0-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34bf0-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34bf0-223">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="34bf0-223">Testing single sign-on</span></span>

<span data-ttu-id="34bf0-224">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="34bf0-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="34bf0-225">Quando você clica no bloco Lucidchart no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="34bf0-225">When you click the Lucidchart tile in the Access Panel, you should get automatically signed-on to your Lucidchart application.</span></span>
<span data-ttu-id="34bf0-226">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="34bf0-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34bf0-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="34bf0-227">Additional resources</span></span>

* [<span data-ttu-id="34bf0-228">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="34bf0-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34bf0-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34bf0-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

