---
title: "Tutorial: integração do Azure Active Directory ao Expensify | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Expensify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: e45576fd92706881121469ccd82150b3d48059cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="cb577-103">Tutorial: integração do Azure Active Directory com o Expensify</span><span class="sxs-lookup"><span data-stu-id="cb577-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="cb577-104">Neste tutorial, você aprenderá como integrar o Expensify com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb577-104">In this tutorial, you learn how to integrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb577-105">A integração do Expensify com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="cb577-105">Integrating Expensify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cb577-106">No Azure AD, é possível controlar quem tem acesso ao Expensify</span><span class="sxs-lookup"><span data-stu-id="cb577-106">You can control in Azure AD who has access to Expensify</span></span>
- <span data-ttu-id="cb577-107">Você pode permitir que seus usuários façam logon automaticamente no Expensify (Logon Único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb577-107">You can enable your users to automatically get signed-on to Expensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb577-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cb577-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cb577-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb577-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb577-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cb577-110">Prerequisites</span></span>

<span data-ttu-id="cb577-111">Para configurar a integração do Azure AD com o Expensify, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="cb577-111">To configure Azure AD integration with Expensify, you need the following items:</span></span>

- <span data-ttu-id="cb577-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb577-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb577-113">Uma assinatura habilitada para logon único do Expensify</span><span class="sxs-lookup"><span data-stu-id="cb577-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb577-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cb577-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb577-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cb577-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb577-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cb577-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb577-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb577-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb577-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cb577-118">Scenario description</span></span>
<span data-ttu-id="cb577-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cb577-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb577-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="cb577-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb577-121">Adicionando o Expensify da galeria</span><span class="sxs-lookup"><span data-stu-id="cb577-121">Adding Expensify from the gallery</span></span>
2. <span data-ttu-id="cb577-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb577-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-the-gallery"></a><span data-ttu-id="cb577-123">Adicionando o Expensify da galeria</span><span class="sxs-lookup"><span data-stu-id="cb577-123">Adding Expensify from the gallery</span></span>
<span data-ttu-id="cb577-124">Para configurar a integração do Expensify ao Azure AD, você precisa adicionar o Expensify da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cb577-124">To configure the integration of Expensify into Azure AD, you need to add Expensify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cb577-125">**Para adicionar o Expensify da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cb577-125">**To add Expensify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cb577-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb577-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb577-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cb577-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cb577-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cb577-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cb577-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb577-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cb577-133">Na caixa de pesquisa, digite **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="cb577-133">In the search box, type **Expensify**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="cb577-135">No painel de resultados, selecione **Expensify** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb577-135">In the results panel, select **Expensify**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb577-137">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb577-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb577-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Expensify, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cb577-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cb577-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Expensify é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb577-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Expensify is to a user in Azure AD.</span></span> <span data-ttu-id="cb577-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Expensify.</span><span class="sxs-lookup"><span data-stu-id="cb577-140">In other words, a link relationship between an Azure AD user and the related user in Expensify needs to be established.</span></span>

<span data-ttu-id="cb577-141">No Expensify, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="cb577-141">In Expensify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cb577-142">Para configurar e testar o logon único do Azure AD com o Expensify, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="cb577-142">To configure and test Azure AD single sign-on with Expensify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cb577-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** - para permitir que seus usuários usem esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cb577-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cb577-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cb577-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb577-145">**[Criando um usuário de teste do Expensify](#creating-an-expensify-test-user)** – para ter um equivalente de Brenda Fernandes no Expensify que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb577-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - to have a counterpart of Britta Simon in Expensify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb577-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb577-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb577-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="cb577-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb577-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb577-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb577-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo Expensify.</span><span class="sxs-lookup"><span data-stu-id="cb577-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="cb577-150">**Para configurar o logon único do Azure AD com o Expensify, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cb577-150">**To configure Azure AD single sign-on with Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="cb577-151">No portal do Azure, na página de integração de aplicativos do **Expensify**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="cb577-151">In the Azure portal, on the **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cb577-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="cb577-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="cb577-155">Na seção **Domínio e URLs do Expensify**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cb577-155">On the **Expensify Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="cb577-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb577-157">a.</span></span> <span data-ttu-id="cb577-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="cb577-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="cb577-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb577-159">b.</span></span> <span data-ttu-id="cb577-160">Na caixa de texto **URL do Identificador**, digite uma URL usando o seguinte padrão: `https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="cb577-160">In the **Identifier URL** textbox, type a URL using the following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="cb577-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="cb577-161">These values are not real.</span></span> <span data-ttu-id="cb577-162">Atualize esses valores com a URL de Entrada e a URL do Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="cb577-162">Update these values with the actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="cb577-163">Entre em contato com [equipe de suporte ao Cliente do Expensify](mailto:help@expensify.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="cb577-163">Contact [Expensify Client support team](mailto:help@expensify.com) to get these values.</span></span> 
 
4. <span data-ttu-id="cb577-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cb577-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="cb577-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="cb577-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cb577-168">Para habilitar o SSO no Expensify, primeiro habilite o **Controle de Domínio** no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb577-168">To enable SSO in Expensify, you first need to enable **Domain Control** in the application.</span></span> <span data-ttu-id="cb577-169">Você pode habilitar o Controle de Domínio no aplicativo por meio das etapas listadas [aqui](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="cb577-169">You can enable Domain Control in the application through the steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="cb577-170">Para obter suporte adicional, trabalhe com a [equipe de suporte ao Cliente do Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="cb577-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="cb577-171">Depois que o Controle de Domínio estiver habilitado, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="cb577-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="cb577-173">a.</span><span class="sxs-lookup"><span data-stu-id="cb577-173">a.</span></span> <span data-ttu-id="cb577-174">Faça logon no seu aplicativo Expensify.</span><span class="sxs-lookup"><span data-stu-id="cb577-174">Sign on to your Expensify application.</span></span>
    
    <span data-ttu-id="cb577-175">b.</span><span class="sxs-lookup"><span data-stu-id="cb577-175">b.</span></span> <span data-ttu-id="cb577-176">Na barra de ferramentas na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="cb577-176">In the toolbar on the top, click **Admin**.</span></span>
    
    <span data-ttu-id="cb577-177">c.</span><span class="sxs-lookup"><span data-stu-id="cb577-177">c.</span></span> <span data-ttu-id="cb577-178">No painel esquerdo, clique em **Domínio**.</span><span class="sxs-lookup"><span data-stu-id="cb577-178">In the left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="cb577-179">d.</span><span class="sxs-lookup"><span data-stu-id="cb577-179">d.</span></span> <span data-ttu-id="cb577-180">Clique no nome do domínio verificado.</span><span class="sxs-lookup"><span data-stu-id="cb577-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="cb577-181">e.</span><span class="sxs-lookup"><span data-stu-id="cb577-181">e.</span></span> <span data-ttu-id="cb577-182">No painel esquerdo, clique em **SAML** e selecione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="cb577-182">In the left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="cb577-183">f.</span><span class="sxs-lookup"><span data-stu-id="cb577-183">f.</span></span> <span data-ttu-id="cb577-184">Abra os Metadados de Federação baixados do Azure AD no bloco de notas, copie o conteúdo e cole-o na caixa de texto **Metadados do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="cb577-184">Open the downloaded Federation Metadata from Azure AD in notepad, copy the content, and then paste it into the **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="cb577-185">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="cb577-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cb577-186">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="cb577-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cb577-187">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb577-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb577-188">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb577-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb577-189">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cb577-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cb577-191">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cb577-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cb577-192">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb577-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb577-194">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cb577-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb577-196">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb577-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb577-198">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cb577-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb577-200">a.</span><span class="sxs-lookup"><span data-stu-id="cb577-200">a.</span></span> <span data-ttu-id="cb577-201">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="cb577-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb577-202">b.</span><span class="sxs-lookup"><span data-stu-id="cb577-202">b.</span></span> <span data-ttu-id="cb577-203">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cb577-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb577-204">c.</span><span class="sxs-lookup"><span data-stu-id="cb577-204">c.</span></span> <span data-ttu-id="cb577-205">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="cb577-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cb577-206">d.</span><span class="sxs-lookup"><span data-stu-id="cb577-206">d.</span></span> <span data-ttu-id="cb577-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cb577-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="cb577-208">Criando um usuário de teste do Expensify</span><span class="sxs-lookup"><span data-stu-id="cb577-208">Creating an Expensify test user</span></span>

<span data-ttu-id="cb577-209">Nesta seção, você criará um usuário chamado Brenda Fernandes no Expensify.</span><span class="sxs-lookup"><span data-stu-id="cb577-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="cb577-210">Trabalhe com a [equipe de suporte ao Cliente do Expensify](mailto:help@expensify.com) para adicionar usuários na plataforma do Expensify.</span><span class="sxs-lookup"><span data-stu-id="cb577-210">Work with [Expensify Client support team](mailto:help@expensify.com) to add the users in the Expensify platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cb577-211">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb577-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cb577-212">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Expensify.</span><span class="sxs-lookup"><span data-stu-id="cb577-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Expensify.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cb577-214">**Para atribuir Brenda Fernandes ao Expensify, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cb577-214">**To assign Britta Simon to Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="cb577-215">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cb577-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cb577-217">Na lista de aplicativos, selecione **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="cb577-217">In the applications list, select **Expensify**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="cb577-219">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cb577-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cb577-221">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cb577-221">Click **Add** button.</span></span> <span data-ttu-id="cb577-222">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb577-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cb577-224">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cb577-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cb577-225">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb577-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb577-226">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb577-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb577-227">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cb577-227">Testing single sign-on</span></span>

<span data-ttu-id="cb577-228">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="cb577-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="cb577-229">Ao clicar no bloco do Expensify no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo Expensify.</span><span class="sxs-lookup"><span data-stu-id="cb577-229">When you click the Expensify tile in the Access Panel, you should get automatically signed-on to your Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb577-230">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cb577-230">Additional resources</span></span>

* [<span data-ttu-id="cb577-231">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cb577-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb577-232">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cb577-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

