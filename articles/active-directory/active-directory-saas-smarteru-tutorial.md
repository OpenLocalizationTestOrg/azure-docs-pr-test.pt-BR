---
title: "Tutorial: integração do Azure Active Directory com o SmarterU | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o SmarterU."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 129d08c8a7b4228d4d5f1a3b7938ab649b2747a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="d1880-103">Tutorial: integração do Azure Active Directory com o SmarterU</span><span class="sxs-lookup"><span data-stu-id="d1880-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="d1880-104">Neste tutorial, você aprenderá a integrar o SmarterU ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d1880-104">In this tutorial, you learn how to integrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1880-105">A integração do SmarterU ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="d1880-105">Integrating SmarterU with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d1880-106">No Azure AD, é possível controlar quem tem acesso ao SmarterU</span><span class="sxs-lookup"><span data-stu-id="d1880-106">You can control in Azure AD who has access to SmarterU</span></span>
- <span data-ttu-id="d1880-107">Você pode permitir que seus usuários façam logon automaticamente no SmarterU (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="d1880-107">You can enable your users to automatically get signed-on to SmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d1880-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d1880-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d1880-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d1880-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1880-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d1880-110">Prerequisites</span></span>

<span data-ttu-id="d1880-111">Para configurar a integração do Azure AD com o SmarterU, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d1880-111">To configure Azure AD integration with SmarterU, you need the following items:</span></span>

- <span data-ttu-id="d1880-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d1880-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d1880-113">Uma assinatura habilitada para logon único do SmarterU</span><span class="sxs-lookup"><span data-stu-id="d1880-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d1880-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d1880-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d1880-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d1880-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d1880-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d1880-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d1880-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d1880-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1880-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d1880-118">Scenario description</span></span>
<span data-ttu-id="d1880-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d1880-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d1880-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="d1880-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1880-121">Adicionar o SmarterU da galeria</span><span class="sxs-lookup"><span data-stu-id="d1880-121">Adding SmarterU from the gallery</span></span>
2. <span data-ttu-id="d1880-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d1880-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-the-gallery"></a><span data-ttu-id="d1880-123">Adicionar o SmarterU da galeria</span><span class="sxs-lookup"><span data-stu-id="d1880-123">Adding SmarterU from the gallery</span></span>
<span data-ttu-id="d1880-124">Para configurar a integração do SmarterU ao Azure AD, você precisará adicionar o SmarterU da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d1880-124">To configure the integration of SmarterU into Azure AD, you need to add SmarterU from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d1880-125">**Para adicionar o SmarterU na galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d1880-125">**To add SmarterU from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d1880-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1880-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d1880-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d1880-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d1880-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d1880-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d1880-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1880-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d1880-133">Na caixa de pesquisa, digite **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="d1880-133">In the search box, type **SmarterU**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="d1880-135">No painel de resultados, selecione **SmarterU** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1880-135">In the results panel, select **SmarterU**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d1880-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d1880-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d1880-138">Nesta seção, você configurará e testará o logon único do Azure AD com o SmarterU, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d1880-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d1880-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SmarterU é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1880-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SmarterU is to a user in Azure AD.</span></span> <span data-ttu-id="d1880-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no SmarterU.</span><span class="sxs-lookup"><span data-stu-id="d1880-140">In other words, a link relationship between an Azure AD user and the related user in SmarterU needs to be established.</span></span>

<span data-ttu-id="d1880-141">No SmarterU, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="d1880-141">In SmarterU, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d1880-142">Para configurar e testar o logon único do Azure AD com o SmarterU, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="d1880-142">To configure and test Azure AD single sign-on with SmarterU, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d1880-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d1880-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d1880-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d1880-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1880-145">**[Criação de um usuário de teste do SmarterU](#creating-a-smarteru-test-user)** – para ter um equivalente de Brenda Fernandes no SmarterU que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1880-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - to have a counterpart of Britta Simon in SmarterU that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d1880-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1880-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d1880-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="d1880-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d1880-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1880-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d1880-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo SmarterU.</span><span class="sxs-lookup"><span data-stu-id="d1880-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="d1880-150">**Para configurar o logon único do Azure AD com o SmarterU, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d1880-150">**To configure Azure AD single sign-on with SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="d1880-151">No portal do Azure, na página de integração de aplicativos do **SmarterU**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="d1880-151">In the Azure portal, on the **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d1880-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="d1880-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="d1880-155">Na seção **URLs e Domínio do SmarterU**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d1880-155">On the **SmarterU Domain and URLs** section, perform the following steps:</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="d1880-157">Na caixa de texto **Identificador**, digite a URL: `https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="d1880-157">In the **Identifier** textbox, type the URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="d1880-158">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d1880-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="d1880-160">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d1880-160">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d1880-162">Em outra janela do navegador da Web, faça logon em seu site de empresa do SmarterU como um administrador.</span><span class="sxs-lookup"><span data-stu-id="d1880-162">In a different web browser window, log in to your SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="d1880-163">Na barra de ferramentas na parte superior, clique em **Configurações da Conta**.</span><span class="sxs-lookup"><span data-stu-id="d1880-163">In the toolbar on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="d1880-164">![Configurações de Conta](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Configurações de Conta")</span><span class="sxs-lookup"><span data-stu-id="d1880-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="d1880-165">Na página de configuração da conta, execute as seguintes etapas: </span><span class="sxs-lookup"><span data-stu-id="d1880-165">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="d1880-166">![Autorização Externa](./media/active-directory-saas-smarteru-tutorial/IC777327.png "Autorização Externa")</span><span class="sxs-lookup"><span data-stu-id="d1880-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="d1880-167">a.</span><span class="sxs-lookup"><span data-stu-id="d1880-167">a.</span></span> <span data-ttu-id="d1880-168">Selecione **Habilitar Autorização Externa**.</span><span class="sxs-lookup"><span data-stu-id="d1880-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="d1880-169">b.</span><span class="sxs-lookup"><span data-stu-id="d1880-169">b.</span></span> <span data-ttu-id="d1880-170">Na seção **Controle de Logon Principal**, selecione a guia **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="d1880-170">In the **Master Login Control** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="d1880-171">c.</span><span class="sxs-lookup"><span data-stu-id="d1880-171">c.</span></span> <span data-ttu-id="d1880-172">Na seção **Logon do Usuário Padrão**, selecione a guia **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="d1880-172">In the **User Default Login** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="d1880-173">d.</span><span class="sxs-lookup"><span data-stu-id="d1880-173">d.</span></span> <span data-ttu-id="d1880-174">Selecione **Habilitar Okta**.</span><span class="sxs-lookup"><span data-stu-id="d1880-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="d1880-175">e.</span><span class="sxs-lookup"><span data-stu-id="d1880-175">e.</span></span> <span data-ttu-id="d1880-176">Copie o conteúdo do arquivo de metadados baixado e cole-o na caixa de texto **Metadados do Okta** .</span><span class="sxs-lookup"><span data-stu-id="d1880-176">Copy the content of the downloaded metadata file, and then paste it into the **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="d1880-177">f.</span><span class="sxs-lookup"><span data-stu-id="d1880-177">f.</span></span> <span data-ttu-id="d1880-178">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d1880-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d1880-179">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="d1880-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d1880-180">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d1880-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d1880-181">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d1880-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d1880-182">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d1880-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="d1880-183">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d1880-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d1880-185">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d1880-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d1880-186">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1880-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d1880-188">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d1880-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d1880-190">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d1880-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d1880-192">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d1880-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d1880-194">a.</span><span class="sxs-lookup"><span data-stu-id="d1880-194">a.</span></span> <span data-ttu-id="d1880-195">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="d1880-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d1880-196">b.</span><span class="sxs-lookup"><span data-stu-id="d1880-196">b.</span></span> <span data-ttu-id="d1880-197">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d1880-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d1880-198">c.</span><span class="sxs-lookup"><span data-stu-id="d1880-198">c.</span></span> <span data-ttu-id="d1880-199">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="d1880-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d1880-200">d.</span><span class="sxs-lookup"><span data-stu-id="d1880-200">d.</span></span> <span data-ttu-id="d1880-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d1880-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="d1880-202">Criar um usuário de teste do SmarterU</span><span class="sxs-lookup"><span data-stu-id="d1880-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="d1880-203">Para permitir que os usuários do Azure AD façam logon no SmarterU, eles deverão ser provisionados no SmarterU.</span><span class="sxs-lookup"><span data-stu-id="d1880-203">To enable Azure AD users to log in to SmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="d1880-204">No caso do SmarterU, o provisionamento será uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="d1880-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="d1880-205">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d1880-205">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d1880-206">Faça logon em seu locatário do **SmarterU** .</span><span class="sxs-lookup"><span data-stu-id="d1880-206">Log in to your **SmarterU** tenant.</span></span>

2. <span data-ttu-id="d1880-207">Vá para **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="d1880-207">Go to **Users**.</span></span>

3. <span data-ttu-id="d1880-208">Na seção do usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d1880-208">In the user section, perform the following steps:</span></span>
   
    <span data-ttu-id="d1880-209">![Novo Usuário](./media/active-directory-saas-smarteru-tutorial/IC777329.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="d1880-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="d1880-210">a.</span><span class="sxs-lookup"><span data-stu-id="d1880-210">a.</span></span> <span data-ttu-id="d1880-211">Clique em **+Usuário**.</span><span class="sxs-lookup"><span data-stu-id="d1880-211">Click **+User**.</span></span>
    
    <span data-ttu-id="d1880-212">b.</span><span class="sxs-lookup"><span data-stu-id="d1880-212">b.</span></span> <span data-ttu-id="d1880-213">Digite os valores de atributo relacionados da conta de usuário do Azure AD nas seguintes caixas de texto: **Email Principal**, **ID do Funcionário**, **Senha**, **Verificar Senha**, **Nome Dado**, **Sobrenome**.</span><span class="sxs-lookup"><span data-stu-id="d1880-213">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="d1880-214">c.</span><span class="sxs-lookup"><span data-stu-id="d1880-214">c.</span></span> <span data-ttu-id="d1880-215">Clique em **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="d1880-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="d1880-216">d.</span><span class="sxs-lookup"><span data-stu-id="d1880-216">d.</span></span> <span data-ttu-id="d1880-217">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d1880-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="d1880-218">É possível usar qualquer outra ferramenta de criação da conta de usuário do SmarterU ou as APIs fornecidas pelo SmarterU para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="d1880-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d1880-219">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d1880-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d1880-220">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao SmarterU.</span><span class="sxs-lookup"><span data-stu-id="d1880-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmarterU.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d1880-222">**Para atribuir Brenda Fernandes ao SmarterU, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d1880-222">**To assign Britta Simon to SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="d1880-223">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d1880-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d1880-225">Na lista de aplicativos, selecione **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="d1880-225">In the applications list, select **SmarterU**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="d1880-227">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d1880-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d1880-229">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d1880-229">Click **Add** button.</span></span> <span data-ttu-id="d1880-230">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d1880-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d1880-232">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d1880-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d1880-233">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d1880-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d1880-234">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d1880-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d1880-235">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d1880-235">Testing single sign-on</span></span>

<span data-ttu-id="d1880-236">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="d1880-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="d1880-237">Ao clicar no bloco do SmarterU no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo SmarterU.</span><span class="sxs-lookup"><span data-stu-id="d1880-237">When you click the SmarterU tile in the Access Panel, you should get automatically signed-on to your SmarterU application.</span></span>
<span data-ttu-id="d1880-238">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1880-238">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="d1880-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d1880-239">Additional resources</span></span>

* [<span data-ttu-id="d1880-240">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d1880-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1880-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d1880-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

