---
title: "Tutorial: Integração do Azure Active Directory com o Heroku | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Heroku."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: d30605e4757b484f327a784b73f939b62ef59373
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="3446f-103">Tutorial: Integração do Azure Active Directory ao Heroku</span><span class="sxs-lookup"><span data-stu-id="3446f-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="3446f-104">Neste tutorial, você aprenderá como integrar o Heroku ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3446f-104">In this tutorial, you learn how to integrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3446f-105">A integração do Heroku ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3446f-105">Integrating Heroku with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3446f-106">No Azure AD, você pode controlar quem tem acesso ao Heroku</span><span class="sxs-lookup"><span data-stu-id="3446f-106">You can control in Azure AD who has access to Heroku</span></span>
- <span data-ttu-id="3446f-107">Você pode permitir que seus usuários façam logon automaticamente no Heroku (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3446f-107">You can enable your users to automatically get signed-on to Heroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3446f-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3446f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3446f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3446f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3446f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3446f-110">Prerequisites</span></span>

<span data-ttu-id="3446f-111">Para configurar a integração do Azure AD ao Heroku, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3446f-111">To configure Azure AD integration with Heroku, you need the following items:</span></span>

- <span data-ttu-id="3446f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3446f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3446f-113">Uma assinatura habilitada para logon único do Heroku</span><span class="sxs-lookup"><span data-stu-id="3446f-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3446f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3446f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3446f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3446f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3446f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3446f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3446f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3446f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3446f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3446f-118">Scenario description</span></span>
<span data-ttu-id="3446f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3446f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3446f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="3446f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3446f-121">Adicionando o Heroku da galeria</span><span class="sxs-lookup"><span data-stu-id="3446f-121">Adding Heroku from the gallery</span></span>
2. <span data-ttu-id="3446f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3446f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-the-gallery"></a><span data-ttu-id="3446f-123">Adicionando o Heroku da galeria</span><span class="sxs-lookup"><span data-stu-id="3446f-123">Adding Heroku from the gallery</span></span>
<span data-ttu-id="3446f-124">Para configurar a integração do Heroku ao Azure AD, você precisa adicionar o Heroku da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3446f-124">To configure the integration of Heroku into Azure AD, you need to add Heroku from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3446f-125">**Para adicionar o Heroku da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3446f-125">**To add Heroku from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3446f-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3446f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3446f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3446f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3446f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3446f-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3446f-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3446f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3446f-133">Na caixa de pesquisa, digite **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="3446f-133">In the search box, type **Heroku**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="3446f-135">No painel de resultados, selecione **Heroku** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3446f-135">In the results panel, select **Heroku**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3446f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3446f-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="3446f-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Heroku, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3446f-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3446f-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Heroku é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3446f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Heroku is to a user in Azure AD.</span></span> <span data-ttu-id="3446f-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Heroku.</span><span class="sxs-lookup"><span data-stu-id="3446f-140">In other words, a link relationship between an Azure AD user and the related user in Heroku needs to be established.</span></span>

<span data-ttu-id="3446f-141">No Heroku, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="3446f-141">In Heroku, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3446f-142">Para configurar e testar o logon único do Azure AD com o Heroku, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="3446f-142">To configure and test Azure AD single sign-on with Heroku, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3446f-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3446f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3446f-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3446f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3446f-145">**[Criação de um usuário de teste do Heroku](#creating-a-heroku-test-user)**: para ter um equivalente de Brenda Fernandes no Heroku que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3446f-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - to have a counterpart of Britta Simon in Heroku that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3446f-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3446f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3446f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="3446f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3446f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3446f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3446f-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Heroku.</span><span class="sxs-lookup"><span data-stu-id="3446f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="3446f-150">**Para configurar o logon único do Azure AD com o Heroku, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3446f-150">**To configure Azure AD single sign-on with Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="3446f-151">No Portal do Azure, na página de integração de aplicativos do **Heroku**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="3446f-151">In the Azure portal, on the **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3446f-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="3446f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="3446f-155">Na seção **URLs e Domínio do Heroku**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3446f-155">On the **Heroku Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="3446f-157">a.</span><span class="sxs-lookup"><span data-stu-id="3446f-157">a.</span></span> <span data-ttu-id="3446f-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="3446f-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="3446f-159">b.</span><span class="sxs-lookup"><span data-stu-id="3446f-159">b.</span></span> <span data-ttu-id="3446f-160">Na caixa de texto **URL do Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="3446f-160">In the **Identifier URL** textbox, type a URL using the following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="3446f-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="3446f-161">These values are not real.</span></span> <span data-ttu-id="3446f-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="3446f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3446f-163">Você obtém esses valores da equipe do Heroku, o que é descrito nas próximas seções deste artigo.</span><span class="sxs-lookup"><span data-stu-id="3446f-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="3446f-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3446f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="3446f-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3446f-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3446f-168">Para habilitar o SSO no Heroku, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3446f-168">To enable SSO in Heroku, perform the following steps:</span></span>
   
    <span data-ttu-id="3446f-169">a.</span><span class="sxs-lookup"><span data-stu-id="3446f-169">a.</span></span> <span data-ttu-id="3446f-170">Faça logon na conta do Heroku como administrador.</span><span class="sxs-lookup"><span data-stu-id="3446f-170">Log in to the Heroku account as an administrator.</span></span>

    <span data-ttu-id="3446f-171">b.</span><span class="sxs-lookup"><span data-stu-id="3446f-171">b.</span></span> <span data-ttu-id="3446f-172">Clique na guia **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="3446f-172">Click the **Settings** tab.</span></span>

    <span data-ttu-id="3446f-173">c.</span><span class="sxs-lookup"><span data-stu-id="3446f-173">c.</span></span> <span data-ttu-id="3446f-174">Na **Página de Logon Único**, clique em **Carregar Metadados**.</span><span class="sxs-lookup"><span data-stu-id="3446f-174">On the **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="3446f-175">d.</span><span class="sxs-lookup"><span data-stu-id="3446f-175">d.</span></span> <span data-ttu-id="3446f-176">Carregue o arquivo de metadados, que você baixou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3446f-176">Upload the metadata file, which you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="3446f-177">e.</span><span class="sxs-lookup"><span data-stu-id="3446f-177">e.</span></span> <span data-ttu-id="3446f-178">Quando a instalação for bem-sucedida, os administradores verão uma caixa de diálogo de confirmação e a URL do Logon de SSO para usuários finais será exibida.</span><span class="sxs-lookup"><span data-stu-id="3446f-178">When the setup is successful, administrators see a confirmation dialog and the URL of the SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="3446f-179">f.</span><span class="sxs-lookup"><span data-stu-id="3446f-179">f.</span></span> <span data-ttu-id="3446f-180">Copie os valores da **URL de Logon do Heroku** e da **ID da Entidade do Heroku**, retorne à seção **URLs e Domínio do Heroku** no Portal do Azure e cole esses valores nas caixas de texto **URL de Logon** e **Identificador**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="3446f-180">Copy the **Heroku Login URL** and **Heroku Entity ID** values and go back to **Heroku Domain and URLs** section in Azure portal and paste these values into the **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="3446f-182">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="3446f-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="3446f-183">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="3446f-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3446f-184">Depois de adicionar esse aplicativo da seção **Aplicativos Empresariais do Active Directory**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3446f-184">After adding this app from the **Active Directory Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3446f-185">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3446f-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3446f-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3446f-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="3446f-187">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3446f-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3446f-189">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3446f-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3446f-190">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3446f-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3446f-192">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3446f-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3446f-194">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3446f-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3446f-196">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3446f-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3446f-198">a.</span><span class="sxs-lookup"><span data-stu-id="3446f-198">a.</span></span> <span data-ttu-id="3446f-199">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="3446f-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3446f-200">b.</span><span class="sxs-lookup"><span data-stu-id="3446f-200">b.</span></span> <span data-ttu-id="3446f-201">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3446f-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3446f-202">c.</span><span class="sxs-lookup"><span data-stu-id="3446f-202">c.</span></span> <span data-ttu-id="3446f-203">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="3446f-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3446f-204">d.</span><span class="sxs-lookup"><span data-stu-id="3446f-204">d.</span></span> <span data-ttu-id="3446f-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3446f-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="3446f-206">Criação de um usuário de teste do Heroku</span><span class="sxs-lookup"><span data-stu-id="3446f-206">Creating a Heroku test user</span></span>

<span data-ttu-id="3446f-207">Nesta seção, você criará um usuário chamado Brenda Fernandes no Heroku.</span><span class="sxs-lookup"><span data-stu-id="3446f-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="3446f-208">O Heroku dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="3446f-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="3446f-209">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="3446f-209">There is no action item for you in this section.</span></span> <span data-ttu-id="3446f-210">Um novo usuário será criado ao acessar o Heroku se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="3446f-210">A new user is created when accessing Heroku if the user doesn't exist yet.</span></span> <span data-ttu-id="3446f-211">Depois que a conta for provisionada, o usuário final receberá um email de verificação e precisará clicar no link de confirmação.</span><span class="sxs-lookup"><span data-stu-id="3446f-211">After the account is provisioned, the end user receives a verification email and needs to click the acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="3446f-212">Se seja necessário criar um usuário manualmente, você precisará entrar em contato com a [equipe de suporte do Cliente Heroku](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="3446f-212">If you need to create a user manually, you need to contact the [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3446f-213">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3446f-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3446f-214">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Heroku.</span><span class="sxs-lookup"><span data-stu-id="3446f-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Heroku.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3446f-216">**Para atribuir Brenda Fernandes ao Heroku, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3446f-216">**To assign Britta Simon to Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="3446f-217">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3446f-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3446f-219">Na lista de aplicativos, escolha **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="3446f-219">In the applications list, select **Heroku**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="3446f-221">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3446f-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3446f-223">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3446f-223">Click **Add** button.</span></span> <span data-ttu-id="3446f-224">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3446f-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3446f-226">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3446f-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3446f-227">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3446f-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3446f-228">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3446f-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3446f-229">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3446f-229">Testing single sign-on</span></span>

<span data-ttu-id="3446f-230">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3446f-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3446f-231">Quando você clicar no bloco Heroku no Painel de Acesso, deverá fazer logon automaticamente no seu aplicativo Heroku.</span><span class="sxs-lookup"><span data-stu-id="3446f-231">When you click the Heroku tile in the Access Panel, you should get automatically signed-on to your Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3446f-232">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3446f-232">Additional resources</span></span>

* [<span data-ttu-id="3446f-233">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3446f-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3446f-234">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3446f-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
