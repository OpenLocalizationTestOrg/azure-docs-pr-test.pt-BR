---
title: "Tutorial: Integração do Azure Active Directory com o QuickHelp | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o QuickHelp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 1c72b0ddee636090129dab7a5c7ec6ffd452434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="83204-103">Tutorial: Integração do Active Directory do Azure com o QuickHelp</span><span class="sxs-lookup"><span data-stu-id="83204-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="83204-104">Neste tutorial, você aprende a integrar o QuickHelp ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="83204-104">In this tutorial, you learn how to integrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83204-105">A integração do QuickHelp ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="83204-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="83204-106">Você pode controlar no AD do Azure quem tem acesso ao QuickHelp</span><span class="sxs-lookup"><span data-stu-id="83204-106">You can control in Azure AD who has access to QuickHelp</span></span>
- <span data-ttu-id="83204-107">Você pode habilitar seus usuários a fazerem logon automaticamente no QuickHelp (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83204-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83204-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="83204-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="83204-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83204-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83204-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="83204-110">Prerequisites</span></span>

<span data-ttu-id="83204-111">Para configurar a integração do AD do Azure ao QuickHelp, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="83204-111">To configure Azure AD integration with QuickHelp, you need the following items:</span></span>

- <span data-ttu-id="83204-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83204-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83204-113">Uma assinatura habilitada para logon único do QuickHelp</span><span class="sxs-lookup"><span data-stu-id="83204-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83204-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="83204-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83204-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="83204-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83204-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="83204-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83204-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83204-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83204-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="83204-118">Scenario description</span></span>
<span data-ttu-id="83204-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="83204-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83204-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="83204-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83204-121">Adicionar QuickHelp a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="83204-121">Adding QuickHelp from the gallery</span></span>
2. <span data-ttu-id="83204-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83204-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-the-gallery"></a><span data-ttu-id="83204-123">Adicionar QuickHelp a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="83204-123">Adding QuickHelp from the gallery</span></span>
<span data-ttu-id="83204-124">Para configurar a integração do QuickHelp ao AD do Azure, você precisa adicionar o QuickHelp a partir da galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="83204-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="83204-125">**Para adicionar o QuickHelp a partir da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="83204-125">**To add QuickHelp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="83204-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83204-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83204-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="83204-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="83204-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="83204-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="83204-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="83204-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="83204-133">Na caixa de pesquisa, digite **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="83204-133">In the search box, type **QuickHelp**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="83204-135">No painel de resultados, selecione **QuickHelp** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="83204-135">In the results panel, select **QuickHelp**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83204-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83204-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83204-138">Nesta seção, você configura e testa o logon único do Azure AD com o QuickHelp, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="83204-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="83204-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do QuickHelp é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83204-139">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp is to a user in Azure AD.</span></span> <span data-ttu-id="83204-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado no QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="83204-140">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="83204-141">No QuickHelp, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="83204-141">In QuickHelp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="83204-142">Para configurar e testar o logon único do AD do Azure com o QuickHelp, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="83204-142">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="83204-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** - para permitir que seus usuários usem esse recurso.</span><span class="sxs-lookup"><span data-stu-id="83204-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="83204-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="83204-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83204-145">**[Criando um usuário de teste do QuickHelp](#creating-a-quickhelp-test-user)** – para ter um equivalente de Brenda Fernandes no QuickHelp que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83204-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="83204-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="83204-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83204-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="83204-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83204-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="83204-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83204-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="83204-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="83204-150">**Para configurar o logon único do AD do Azure com o QuickHelp, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="83204-150">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="83204-151">No portal do Azure, na página de integração do aplicativo **QuickHelp**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="83204-151">In the Azure portal, on the **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="83204-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="83204-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="83204-155">Na seção **Domínio e URLs do QuickHelp**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="83204-155">On the **QuickHelp Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="83204-157">a.</span><span class="sxs-lookup"><span data-stu-id="83204-157">a.</span></span> <span data-ttu-id="83204-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="83204-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="83204-159">b.</span><span class="sxs-lookup"><span data-stu-id="83204-159">b.</span></span> <span data-ttu-id="83204-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="83204-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="83204-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="83204-161">These values are not real.</span></span> <span data-ttu-id="83204-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="83204-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="83204-163">Contate a [equipe de suporte ao Cliente do QuickHelp](https://support.quickhelp.com/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="83204-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="83204-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="83204-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="83204-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="83204-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="83204-168">Faça logon no site do QuickHelp da sua empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="83204-168">Sign-on to your QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="83204-169">No menu na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="83204-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Configurar Logon Único][21]

8. <span data-ttu-id="83204-171">No menu **Administrador do QuickHelp**, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="83204-171">In the **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Configurar o logon único][22]

9. <span data-ttu-id="83204-173">Clique em **Configurações da Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="83204-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="83204-174">Na página **Configurações de Autenticação** , execute as etapas a seguir</span><span class="sxs-lookup"><span data-stu-id="83204-174">On the **Authentication Settings** page, perform the following steps</span></span>
   
    ![Configurar Logon Único][23]
   
    <span data-ttu-id="83204-176">a.</span><span class="sxs-lookup"><span data-stu-id="83204-176">a.</span></span> <span data-ttu-id="83204-177">Como **Tipo de SSO**, selecione **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="83204-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="83204-178">b.</span><span class="sxs-lookup"><span data-stu-id="83204-178">b.</span></span> <span data-ttu-id="83204-179">Para carregar o arquivo de metadados do Azure baixado, clique em **Procurar**, navegue até o arquivo e clique em **Carregar Metadados**.</span><span class="sxs-lookup"><span data-stu-id="83204-179">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="83204-180">c.</span><span class="sxs-lookup"><span data-stu-id="83204-180">c.</span></span> <span data-ttu-id="83204-181">Na caixa de texto **Email**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="83204-181">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="83204-182">d.</span><span class="sxs-lookup"><span data-stu-id="83204-182">d.</span></span> <span data-ttu-id="83204-183">Na caixa de texto **Nome**, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="83204-183">In the **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="83204-184">e.</span><span class="sxs-lookup"><span data-stu-id="83204-184">e.</span></span> <span data-ttu-id="83204-185">Na caixa de texto **Sobrenome**, digite `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="83204-185">In the **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="83204-186">f.</span><span class="sxs-lookup"><span data-stu-id="83204-186">f.</span></span> <span data-ttu-id="83204-187">Na **Barra de Ações**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="83204-187">In the **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="83204-188">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="83204-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="83204-189">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="83204-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="83204-190">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="83204-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83204-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83204-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="83204-192">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="83204-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="83204-194">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="83204-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="83204-195">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83204-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83204-197">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="83204-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83204-199">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="83204-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83204-201">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="83204-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83204-203">a.</span><span class="sxs-lookup"><span data-stu-id="83204-203">a.</span></span> <span data-ttu-id="83204-204">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="83204-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83204-205">b.</span><span class="sxs-lookup"><span data-stu-id="83204-205">b.</span></span> <span data-ttu-id="83204-206">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="83204-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83204-207">c.</span><span class="sxs-lookup"><span data-stu-id="83204-207">c.</span></span> <span data-ttu-id="83204-208">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="83204-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="83204-209">d.</span><span class="sxs-lookup"><span data-stu-id="83204-209">d.</span></span> <span data-ttu-id="83204-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="83204-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="83204-211">Criando um usuário de teste do QuickHelp</span><span class="sxs-lookup"><span data-stu-id="83204-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="83204-212">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="83204-212">The objective of this section is to create a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="83204-213">Para que o logon único funcione, o Azure AD precisa saber qual usuário do QuickHelp é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83204-213">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to a user in Azure AD is.</span></span> <span data-ttu-id="83204-214">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado no QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="83204-214">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="83204-215">O QuickHelp dá suporte ao provisionamento just-in-time.</span><span class="sxs-lookup"><span data-stu-id="83204-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="83204-216">Isso significa que, se necessário, uma conta de usuário é criada automaticamente no QuickHelp e a conta é vinculada à conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83204-216">This means, if necessary, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span></span>

<span data-ttu-id="83204-217">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="83204-217">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="83204-218">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="83204-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="83204-219">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="83204-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QuickHelp.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="83204-221">**Para atribuir Brenda Fernandes ao QuickHelp, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="83204-221">**To assign Britta Simon to QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="83204-222">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="83204-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="83204-224">Na lista de aplicativos, selecione **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="83204-224">In the applications list, select **QuickHelp**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="83204-226">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="83204-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="83204-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="83204-228">Click **Add** button.</span></span> <span data-ttu-id="83204-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="83204-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="83204-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="83204-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="83204-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="83204-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83204-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="83204-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83204-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="83204-234">Testing single sign-on</span></span>

<span data-ttu-id="83204-235">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="83204-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="83204-236">Quando você clica no bloco QuickHelp no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="83204-236">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="83204-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="83204-237">Additional resources</span></span>

* [<span data-ttu-id="83204-238">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="83204-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83204-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83204-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
