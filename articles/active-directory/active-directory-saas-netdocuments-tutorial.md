---
title: "Tutorial: Integração do Azure Active Directory ao NetDocuments | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o NetDocuments."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 87c3338d611daa837aa5f079c4b68e0e6fc58455
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="c3e32-103">Tutorial: Integração do Active Directory do Azure com o NetDocuments</span><span class="sxs-lookup"><span data-stu-id="c3e32-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="c3e32-104">Neste tutorial, você aprenderá a integrar o NetDocuments ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c3e32-104">In this tutorial, you learn how to integrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3e32-105">A integração do NetDocuments ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c3e32-105">Integrating NetDocuments with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c3e32-106">No Azure AD, é possível controlar quem tem acesso ao NetDocuments</span><span class="sxs-lookup"><span data-stu-id="c3e32-106">You can control in Azure AD who has access to NetDocuments</span></span>
- <span data-ttu-id="c3e32-107">Você pode permitir que seus usuários façam logon automaticamente no NetDocuments (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3e32-107">You can enable your users to automatically get signed-on to NetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c3e32-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c3e32-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c3e32-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3e32-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3e32-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c3e32-110">Prerequisites</span></span>

<span data-ttu-id="c3e32-111">Para configurar a integração do Azure AD ao NetDocuments, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c3e32-111">To configure Azure AD integration with NetDocuments, you need the following items:</span></span>

- <span data-ttu-id="c3e32-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c3e32-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3e32-113">Uma assinatura habilitada para logon único do NetDocuments</span><span class="sxs-lookup"><span data-stu-id="c3e32-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3e32-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c3e32-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3e32-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c3e32-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3e32-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c3e32-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3e32-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3e32-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3e32-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c3e32-118">Scenario description</span></span>
<span data-ttu-id="c3e32-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c3e32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3e32-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c3e32-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3e32-121">Adicionar o NetDocuments da galeria</span><span class="sxs-lookup"><span data-stu-id="c3e32-121">Adding NetDocuments from the gallery</span></span>
2. <span data-ttu-id="c3e32-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c3e32-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-the-gallery"></a><span data-ttu-id="c3e32-123">Adicionar o NetDocuments da galeria</span><span class="sxs-lookup"><span data-stu-id="c3e32-123">Adding NetDocuments from the gallery</span></span>
<span data-ttu-id="c3e32-124">Para configurar a integração do NetDocuments ao Azure AD, você precisará adicionar o NetDocuments da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c3e32-124">To configure the integration of NetDocuments into Azure AD, you need to add NetDocuments from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c3e32-125">**Para adicionar o NetDocuments da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c3e32-125">**To add NetDocuments from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c3e32-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c3e32-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c3e32-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c3e32-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c3e32-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c3e32-133">Na caixa de pesquisa, digite **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-133">In the search box, type **NetDocuments**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="c3e32-135">No painel de resultados, selecione **NetDocuments** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c3e32-135">In the results panel, select **NetDocuments**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c3e32-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c3e32-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c3e32-138">Nesta seção, você configurará e testará o logon único do Azure AD com o NetDocuments, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c3e32-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c3e32-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do NetDocuments é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3e32-139">For single sign-on to work, Azure AD needs to know what the counterpart user in NetDocuments is to a user in Azure AD.</span></span> <span data-ttu-id="c3e32-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="c3e32-140">In other words, a link relationship between an Azure AD user and the related user in NetDocuments needs to be established.</span></span>

<span data-ttu-id="c3e32-141">No NetDocuments, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="c3e32-141">In NetDocuments, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c3e32-142">Para configurar e testar o logon único do Azure AD com o NetDocuments, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c3e32-142">To configure and test Azure AD single sign-on with NetDocuments, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c3e32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c3e32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c3e32-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c3e32-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3e32-145">**[Criar um usuário de teste do NetDocuments](#creating-a-netdocuments-test-user)** – para ter um equivalente de Brenda Fernandes no NetDocuments que esteja vinculado à representação desse usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3e32-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - to have a counterpart of Britta Simon in NetDocuments that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3e32-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e32-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3e32-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c3e32-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c3e32-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3e32-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c3e32-149">Nesta seção, você vai habilitar o logon único do Azure AD no Portal do Azure e configurar o logon único em seu aplicativo NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="c3e32-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="c3e32-150">**Para configurar o logon único do Azure AD com o NetDocuments, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c3e32-150">**To configure Azure AD single sign-on with NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="c3e32-151">No Portal do Azure, na página de integração de aplicativos do **NetDocuments**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-151">In the Azure portal, on the **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c3e32-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c3e32-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="c3e32-155">Na seção **URLs e Domínio do NetDocuments**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c3e32-155">On the **NetDocuments Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="c3e32-157">a.</span><span class="sxs-lookup"><span data-stu-id="c3e32-157">a.</span></span> <span data-ttu-id="c3e32-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="c3e32-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="c3e32-159">b.</span><span class="sxs-lookup"><span data-stu-id="c3e32-159">b.</span></span> <span data-ttu-id="c3e32-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="c3e32-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c3e32-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c3e32-161">These values are not real.</span></span> <span data-ttu-id="c3e32-162">Atualize esses valores com a URL de Resposta e a URL de Logon reais.</span><span class="sxs-lookup"><span data-stu-id="c3e32-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="c3e32-163">Entre em contato com a [equipe de suporte do NetDocuments](https://support.netdocuments.com/hc/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="c3e32-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) to get these values.</span></span>
 
4. <span data-ttu-id="c3e32-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c3e32-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="c3e32-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c3e32-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c3e32-168">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do NetDocuments como administrador.</span><span class="sxs-lookup"><span data-stu-id="c3e32-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="c3e32-169">Vá para **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-169">Go to **Admin**.</span></span>

8. <span data-ttu-id="c3e32-170">Clique em **Adicionar e remover usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="c3e32-171">![Repositório](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repositório")</span><span class="sxs-lookup"><span data-stu-id="c3e32-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="c3e32-172">Clique em **Configurar opções de autenticação avançadas**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="c3e32-173">![Configurar opções de autenticação avançadas](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configurar opções de autenticação avançadas")</span><span class="sxs-lookup"><span data-stu-id="c3e32-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="c3e32-174">Na caixa de diálogo **Identidade Federada**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c3e32-174">On the **Federated Identity** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="c3e32-175">![Identidade Federada](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identidade Federada")</span><span class="sxs-lookup"><span data-stu-id="c3e32-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="c3e32-176">a.</span><span class="sxs-lookup"><span data-stu-id="c3e32-176">a.</span></span> <span data-ttu-id="c3e32-177">Para **Tipo de servidor de identidade federada**, selecione **Serviços de Federação do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="c3e32-178">b.</span><span class="sxs-lookup"><span data-stu-id="c3e32-178">b.</span></span> <span data-ttu-id="c3e32-179">Clique em **Escolher arquivo**para carregar o arquivo de metadados que você baixou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e32-179">Click **Choose file**, to upload the downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="c3e32-180">c.</span><span class="sxs-lookup"><span data-stu-id="c3e32-180">c.</span></span> <span data-ttu-id="c3e32-181">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="c3e32-182">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c3e32-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c3e32-183">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c3e32-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c3e32-184">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c3e32-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c3e32-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c3e32-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="c3e32-186">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c3e32-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c3e32-188">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c3e32-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c3e32-189">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c3e32-191">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c3e32-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c3e32-193">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c3e32-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c3e32-195">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c3e32-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c3e32-197">a.</span><span class="sxs-lookup"><span data-stu-id="c3e32-197">a.</span></span> <span data-ttu-id="c3e32-198">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3e32-199">b.</span><span class="sxs-lookup"><span data-stu-id="c3e32-199">b.</span></span> <span data-ttu-id="c3e32-200">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c3e32-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c3e32-201">c.</span><span class="sxs-lookup"><span data-stu-id="c3e32-201">c.</span></span> <span data-ttu-id="c3e32-202">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c3e32-203">d.</span><span class="sxs-lookup"><span data-stu-id="c3e32-203">d.</span></span> <span data-ttu-id="c3e32-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="c3e32-205">Criar um usuário de teste do NetDocuments</span><span class="sxs-lookup"><span data-stu-id="c3e32-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="c3e32-206">Para permitir que os usuários do Azure AD façam logon no NetDocuments, eles devem ser provisionados no NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="c3e32-206">To enable Azure AD users to log in to NetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="c3e32-207">No caso do NetDocuments, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="c3e32-207">In the case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="c3e32-208">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c3e32-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c3e32-209">Faça logon em seu site de empresa do **NetDocuments** como administrador.</span><span class="sxs-lookup"><span data-stu-id="c3e32-209">Sing on to your **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="c3e32-210">No menu na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-210">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="c3e32-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c3e32-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="c3e32-212">Clique em **Adicionar e remover usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="c3e32-213">![Repositório](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repositório")</span><span class="sxs-lookup"><span data-stu-id="c3e32-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="c3e32-214">Na caixa de texto **Endereço de Email**, digite o endereço de email de uma conta válida do Azure Active Directory que você deseja provisionar e clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-214">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="c3e32-215">![Endereço de Email](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Endereço de Email")</span><span class="sxs-lookup"><span data-stu-id="c3e32-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="c3e32-216">O titular da conta do Active Directory do Azure receberá um email com um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="c3e32-216">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span></span> <span data-ttu-id="c3e32-217">É possível usar qualquer outra ferramenta de criação da conta de usuário do NetDocuments ou as APIs fornecidas pelo NetDocuments para provisionar as contas de usuário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3e32-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c3e32-218">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c3e32-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c3e32-219">Nesta seção, você concederá a Brenda Fernandes acesso ao NetDocuments para que ela fique habilitada a usar o logon único do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e32-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetDocuments.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c3e32-221">**Para atribuir Brenda Fernandes ao NetDocuments, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c3e32-221">**To assign Britta Simon to NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="c3e32-222">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c3e32-224">Na lista de aplicativos, selecione **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-224">In the applications list, select **NetDocuments**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="c3e32-226">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c3e32-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c3e32-228">Click **Add** button.</span></span> <span data-ttu-id="c3e32-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c3e32-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c3e32-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c3e32-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c3e32-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c3e32-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3e32-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c3e32-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c3e32-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c3e32-234">Testing single sign-on</span></span>

<span data-ttu-id="c3e32-235">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c3e32-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c3e32-236">Quando você clicar no bloco NetDocuments no Painel de Acesso, você deverá ser automaticamente conectado ao seu aplicativo NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="c3e32-236">When you click the NetDocuments tile in the Access Panel, you should get automatically signed-on to your NetDocuments application.</span></span>
<span data-ttu-id="c3e32-237">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c3e32-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3e32-238">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c3e32-238">Additional resources</span></span>

* [<span data-ttu-id="c3e32-239">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c3e32-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3e32-240">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c3e32-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

