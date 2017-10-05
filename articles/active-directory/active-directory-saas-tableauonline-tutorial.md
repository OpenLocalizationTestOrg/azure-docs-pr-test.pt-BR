---
title: "Tutorial: Integração do Azure Active Directory com o Tableau Online | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Tableau Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 443fab1198a91a4d5749e6421f7b8603fc75a81e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="ff5f0-103">Tutorial: Integração do Azure Active Directory com o Tableau Online</span><span class="sxs-lookup"><span data-stu-id="ff5f0-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="ff5f0-104">Neste tutorial, você aprenderá a integrar o Tableau Online ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ff5f0-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff5f0-105">A integração do Tableau Online ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="ff5f0-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ff5f0-106">Você pode controlar no Azure AD quem tem acesso ao Tableau Online</span><span class="sxs-lookup"><span data-stu-id="ff5f0-106">You can control in Azure AD who has access to Tableau Online</span></span>
- <span data-ttu-id="ff5f0-107">Você pode habilitar os usuários a entrar automaticamente no Tableau Online (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff5f0-107">You can enable your users to automatically get signed-on to Tableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff5f0-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ff5f0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ff5f0-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff5f0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff5f0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ff5f0-110">Prerequisites</span></span>

<span data-ttu-id="ff5f0-111">Para configurar a integração do Azure AD ao Tableau Online, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ff5f0-111">To configure Azure AD integration with Tableau Online, you need the following items:</span></span>

- <span data-ttu-id="ff5f0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ff5f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff5f0-113">Uma assinatura habilitada para logon único do Tableau Online</span><span class="sxs-lookup"><span data-stu-id="ff5f0-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff5f0-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff5f0-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ff5f0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff5f0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff5f0-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff5f0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff5f0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ff5f0-118">Scenario description</span></span>
<span data-ttu-id="ff5f0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff5f0-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="ff5f0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff5f0-121">Adição do Tableau Online da galeria</span><span class="sxs-lookup"><span data-stu-id="ff5f0-121">Adding Tableau Online from the gallery</span></span>
2. <span data-ttu-id="ff5f0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ff5f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="ff5f0-123">Adição do Tableau Online da galeria</span><span class="sxs-lookup"><span data-stu-id="ff5f0-123">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="ff5f0-124">Para configurar a integração do Tableau Online ao Azure AD, você precisa adicionar o Tableau Online da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff5f0-125">**Para adicionar o Tableau Online por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ff5f0-125">**To add Tableau Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff5f0-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ff5f0-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ff5f0-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ff5f0-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ff5f0-133">Na caixa de pesquisa, digite **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-133">In the search box, type **Tableau Online**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="ff5f0-135">No painel de resultados, selecione **Tableau Online** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-135">In the results panel, select **Tableau Online**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff5f0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ff5f0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff5f0-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Tableau Online, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ff5f0-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Tableau Online é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span></span> <span data-ttu-id="ff5f0-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span></span>

<span data-ttu-id="ff5f0-141">No Tableau Online, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-141">In Tableau Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ff5f0-142">Para configurar e testar o logon único do Azure AD com o Tableau Online, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="ff5f0-142">To configure and test Azure AD single sign-on with Tableau Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff5f0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ff5f0-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff5f0-145">**[Criação de um usuário de teste do Tableau Online](#creating-a-tableau-online-test-user)** – para ter um equivalente de Brenda Fernandes no Tableau Online que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ff5f0-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff5f0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff5f0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff5f0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff5f0-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="ff5f0-150">**Para configurar o logon único do Azure AD com o Tableau Online, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ff5f0-150">**To configure Azure AD single sign-on with Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="ff5f0-151">No portal do Azure, na página de integração do aplicativo do **Tableau Online**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-151">In the Azure portal, on the **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ff5f0-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="ff5f0-155">Na seção **Domínio e URLs do Tableau Online**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ff5f0-155">On the **Tableau Online Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="ff5f0-157">a.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-157">a.</span></span> <span data-ttu-id="ff5f0-158">Na caixa de texto **URL de Logon**, digite a URL: `https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="ff5f0-158">In the **Sign-on URL** textbox, type the URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="ff5f0-159">b.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-159">b.</span></span> <span data-ttu-id="ff5f0-160">Na caixa de texto **Identificador**, digite a URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ff5f0-160">In the **Identifier** textbox, type the URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="ff5f0-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="ff5f0-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ff5f0-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ff5f0-165">Em uma janela de navegador diferente, entre no seu aplicativo Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-165">In a different browser window, sign-on to your Tableau Online application.</span></span> <span data-ttu-id="ff5f0-166">Vá para **Settings** e para **Authentication**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-166">Go to **Settings** and then **Authentication**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="ff5f0-168">Para habilitar SAML, na seção **Tipos de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-168">To enable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="ff5f0-169">Marque a caixa de seleção **Logon Único com SAML**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-169">Check the **Single sign-on with SAML** checkbox.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="ff5f0-171">Role para baixo até a seção **Import metadata file into Tableau Online** .</span><span class="sxs-lookup"><span data-stu-id="ff5f0-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="ff5f0-172">Clique em Browser e importe o arquivo de metadados que você baixou do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-172">Click Browse and import the metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="ff5f0-173">Em seguida, clique em **Apply**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-173">Then, click **Apply**.</span></span>
   
   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="ff5f0-175">Na seção **Corresponder Instruções de Declaração**, insira o nome de instrução de declaração do Provedor de Identidade correspondente para **endereço de email**, **nome** e **sobrenome**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-175">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="ff5f0-176">Para obter essas informações do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="ff5f0-176">To get this information from Azure AD:</span></span> 
  
    <span data-ttu-id="ff5f0-177">a.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-177">a.</span></span> <span data-ttu-id="ff5f0-178">No portal do Azure, acesse a página de integração de aplicativos do **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-178">In the Azure portal, go on the **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="ff5f0-179">b.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-179">b.</span></span> <span data-ttu-id="ff5f0-180">Na seção Atributos, marque a caixa de seleção **“Exibir e editar todos os outros atributos de usuário”**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-180">In the attributes section, Select the **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="ff5f0-182">c.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-182">c.</span></span> <span data-ttu-id="ff5f0-183">Copie o valor de namespace para esses atributos: nome, email e sobrenome usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ff5f0-183">Copy the namespace value for these attributes: givenname, email and surname by using the following steps:</span></span>

   ![Logon Único do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="ff5f0-185">d.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-185">d.</span></span> <span data-ttu-id="ff5f0-186">Clique no valor **user.givenname**</span><span class="sxs-lookup"><span data-stu-id="ff5f0-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="ff5f0-187">e.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-187">e.</span></span> <span data-ttu-id="ff5f0-188">Copie o valor da caixa de texto **namespace**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-188">Copy the value from the **namespace** textbox.</span></span>

   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="ff5f0-190">f.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-190">f.</span></span> <span data-ttu-id="ff5f0-191">Para copiar os valores de namespace para o email e o sobrenome, siga as etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-191">To copy the namesapce values for the email and surname follow the preceding steps.</span></span>

    <span data-ttu-id="ff5f0-192">g.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-192">g.</span></span> <span data-ttu-id="ff5f0-193">Alterne para o aplicativo Tableau Online e defina a seção **Atributos do Tableau Online** como a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff5f0-193">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="ff5f0-194">Email: **mail** ou **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="ff5f0-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="ff5f0-195">Nome: **givenname**</span><span class="sxs-lookup"><span data-stu-id="ff5f0-195">First name: **givenname**</span></span>
     * <span data-ttu-id="ff5f0-196">Sobrenome: **surname**</span><span class="sxs-lookup"><span data-stu-id="ff5f0-196">Last name: **surname**</span></span>
   
   ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="ff5f0-198">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="ff5f0-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ff5f0-199">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ff5f0-200">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ff5f0-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff5f0-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ff5f0-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff5f0-202">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ff5f0-204">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ff5f0-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff5f0-205">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ff5f0-207">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ff5f0-209">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff5f0-211">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ff5f0-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ff5f0-213">a.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-213">a.</span></span> <span data-ttu-id="ff5f0-214">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff5f0-215">b.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-215">b.</span></span> <span data-ttu-id="ff5f0-216">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff5f0-217">c.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-217">c.</span></span> <span data-ttu-id="ff5f0-218">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ff5f0-219">d.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-219">d.</span></span> <span data-ttu-id="ff5f0-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="ff5f0-221">Criação de um usuário de teste do Tableau Online</span><span class="sxs-lookup"><span data-stu-id="ff5f0-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="ff5f0-222">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="ff5f0-223">No **Tableau Online**, clique em **Configurações** e na seção **Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="ff5f0-224">Role para baixo até a seção **Selecionar Usuários** .</span><span class="sxs-lookup"><span data-stu-id="ff5f0-224">Scroll down to **Select Users** section.</span></span> <span data-ttu-id="ff5f0-225">Clique em **Adicionar Usuários** e em **Inserir Endereços de Email**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="ff5f0-227">Selecione **Adicionar usuários para autenticação de logon único (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="ff5f0-228">Na caixa de texto **Inserir Endereços de Email**, adicione britta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="ff5f0-228">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="ff5f0-230">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-230">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ff5f0-231">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ff5f0-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ff5f0-232">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Online.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ff5f0-234">**Para atribuir Brenda Fernandes ao Tableau Online, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ff5f0-234">**To assign Britta Simon to Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="ff5f0-235">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ff5f0-237">Na lista de aplicativos, selecione **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-237">In the applications list, select **Tableau Online**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="ff5f0-239">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ff5f0-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-241">Click **Add** button.</span></span> <span data-ttu-id="ff5f0-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ff5f0-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ff5f0-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff5f0-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ff5f0-247">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ff5f0-247">Testing single sign-on</span></span>

<span data-ttu-id="ff5f0-248">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ff5f0-249">Ao clicar no bloco Tableau Online no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="ff5f0-249">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff5f0-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ff5f0-250">Additional resources</span></span>

* [<span data-ttu-id="ff5f0-251">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ff5f0-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff5f0-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff5f0-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

