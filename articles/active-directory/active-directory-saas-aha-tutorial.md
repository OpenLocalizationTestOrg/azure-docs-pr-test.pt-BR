---
title: "Tutorial: Integração do Active Directory do Azure ao Aha! | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Aha!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7723864b2e1ab2d5b69d86f0fa18416b9d3f9aa3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="e05f9-104">Tutorial: Integração do Active Directory do Azure ao Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="e05f9-105">Neste tutorial, você aprende a integrar o Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-105">In this tutorial, you learn how to integrate Aha!</span></span> <span data-ttu-id="e05f9-106">ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e05f9-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e05f9-107">A integração do Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-107">Integrating Aha!</span></span> <span data-ttu-id="e05f9-108">ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e05f9-108">with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e05f9-109">No Azure AD, é possível controlar quem tem acesso ao Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-109">You can control in Azure AD who has access to Aha!</span></span>
- <span data-ttu-id="e05f9-110">É possível permitir que os usuários se conectem automaticamente ao Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-110">You can enable your users to automatically get signed-on to Aha!</span></span> <span data-ttu-id="e05f9-111">(Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e05f9-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e05f9-112">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e05f9-112">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e05f9-113">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e05f9-113">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e05f9-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e05f9-114">Prerequisites</span></span>

<span data-ttu-id="e05f9-115">Para configurar a integração do Azure AD ao Aha!, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e05f9-115">To configure Azure AD integration with Aha!, you need the following items:</span></span>

- <span data-ttu-id="e05f9-116">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e05f9-116">An Azure AD subscription</span></span>
- <span data-ttu-id="e05f9-117">Uma assinatura da Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-117">An Aha!</span></span> <span data-ttu-id="e05f9-118">Uma assinatura habilitada para logon único do Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e05f9-119">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e05f9-119">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e05f9-120">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e05f9-120">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e05f9-121">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e05f9-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e05f9-122">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e05f9-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e05f9-123">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e05f9-123">Scenario description</span></span>
<span data-ttu-id="e05f9-124">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e05f9-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e05f9-125">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e05f9-125">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e05f9-126">Adicionando o Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-126">Adding Aha!</span></span> <span data-ttu-id="e05f9-127">por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="e05f9-127">from the gallery</span></span>
2. <span data-ttu-id="e05f9-128">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e05f9-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-the-gallery"></a><span data-ttu-id="e05f9-129">Adicionando o Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-129">Adding Aha!</span></span> <span data-ttu-id="e05f9-130">por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="e05f9-130">from the gallery</span></span>
<span data-ttu-id="e05f9-131">Para configurar a integração do Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-131">To configure the integration of Aha!</span></span> <span data-ttu-id="e05f9-132">ao Azure AD, você precisa adicionar o Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-132">into Azure AD, you need to add Aha!</span></span> <span data-ttu-id="e05f9-133">à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="e05f9-133">from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e05f9-134">**Para adicionar o Aha! por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e05f9-134">**To add Aha! from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e05f9-135">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-135">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e05f9-137">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-137">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e05f9-138">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-138">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e05f9-140">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e05f9-140">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e05f9-142">Na caixa de pesquisa, digite **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-142">In the search box, type **Aha!**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="e05f9-144">No painel de resultados, selecione **Aha!** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e05f9-144">In the results panel, select **Aha!**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e05f9-146">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e05f9-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e05f9-147">Nesta seção, configura e testa o logon único do Azure AD com o Aha!,</span><span class="sxs-lookup"><span data-stu-id="e05f9-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="e05f9-148">com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e05f9-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e05f9-149">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Aha!</span></span> <span data-ttu-id="e05f9-150">é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e05f9-150">is to a user in Azure AD.</span></span> <span data-ttu-id="e05f9-151">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-151">In other words, a link relationship between an Azure AD user and the related user in Aha!</span></span> <span data-ttu-id="e05f9-152">.</span><span class="sxs-lookup"><span data-stu-id="e05f9-152">needs to be established.</span></span>

<span data-ttu-id="e05f9-153">No Aha!, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="e05f9-153">In Aha!, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e05f9-154">Para configurar e testar o logon único do Azure AD com o Aha!, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e05f9-154">To configure and test Azure AD single sign-on with Aha!, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e05f9-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e05f9-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e05f9-156">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e05f9-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e05f9-157">**[Criando um usuário de teste do Aha!](#creating-an-aha-test-user)** – para ter um equivalente de Brenda Fernandes no Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - to have a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="e05f9-158">que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e05f9-158">that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e05f9-159">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e05f9-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e05f9-160">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e05f9-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e05f9-161">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e05f9-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e05f9-162">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="e05f9-163">.</span><span class="sxs-lookup"><span data-stu-id="e05f9-163">application.</span></span>

<span data-ttu-id="e05f9-164">**Para configurar o logon único do Azure AD com o Aha!, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e05f9-164">**To configure Azure AD single sign-on with Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="e05f9-165">No portal do Azure, na página de integração do aplicativo **Aha!**,</span><span class="sxs-lookup"><span data-stu-id="e05f9-165">In the Azure portal, on the **Aha!**</span></span> <span data-ttu-id="e05f9-166">clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-166">application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e05f9-168">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e05f9-168">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="e05f9-170">Na seção **Domínio e URLs do Aha!**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e05f9-170">On the **Aha! Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="e05f9-172">a.</span><span class="sxs-lookup"><span data-stu-id="e05f9-172">a.</span></span> <span data-ttu-id="e05f9-173">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="e05f9-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="e05f9-174">b.</span><span class="sxs-lookup"><span data-stu-id="e05f9-174">b.</span></span> <span data-ttu-id="e05f9-175">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="e05f9-175">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e05f9-176">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e05f9-176">These values are not real.</span></span> <span data-ttu-id="e05f9-177">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="e05f9-177">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e05f9-178">Contate a [equipe de suporte ao Cliente do Aha!](https://www.aha.io/company/contact) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="e05f9-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="e05f9-179">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e05f9-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="e05f9-181">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e05f9-181">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e05f9-183">Em outra janela do navegador da Web, faça logon em seu site de empresa do Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-183">In a different web browser window, log in to your Aha!</span></span> <span data-ttu-id="e05f9-184">como um administrador.</span><span class="sxs-lookup"><span data-stu-id="e05f9-184">company site as an administrator.</span></span>

7. <span data-ttu-id="e05f9-185">No menu na parte superior, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-185">In the menu on the top, click **Settings**.</span></span>

    <span data-ttu-id="e05f9-186">![Configurações](./media/active-directory-saas-aha-tutorial/IC798950.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="e05f9-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="e05f9-187">Clique em **Conta**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-187">Click **Account**.</span></span>
   
    <span data-ttu-id="e05f9-188">![Perfil](./media/active-directory-saas-aha-tutorial/IC798951.png "Perfil")</span><span class="sxs-lookup"><span data-stu-id="e05f9-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="e05f9-189">Clique em **Segurança e logon único**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="e05f9-190">![Segurança e logon único](./media/active-directory-saas-aha-tutorial/IC798952.png "Segurança e logon único")</span><span class="sxs-lookup"><span data-stu-id="e05f9-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="e05f9-191">Na seção **Logon Único**, como **Provedor de Identidade**, selecione **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="e05f9-192">![Segurança e logon único](./media/active-directory-saas-aha-tutorial/IC798953.png "Segurança e logon único")</span><span class="sxs-lookup"><span data-stu-id="e05f9-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="e05f9-193">Na página de configuração **Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e05f9-193">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
    
    <span data-ttu-id="e05f9-194">![Logon Único](./media/active-directory-saas-aha-tutorial/IC798954.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="e05f9-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="e05f9-195">a.</span><span class="sxs-lookup"><span data-stu-id="e05f9-195">a.</span></span> <span data-ttu-id="e05f9-196">Na caixa de texto **Nome** , digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="e05f9-196">In the **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="e05f9-197">b.</span><span class="sxs-lookup"><span data-stu-id="e05f9-197">b.</span></span> <span data-ttu-id="e05f9-198">Para **Configurar usando**, selecione **Arquivo de Metadados**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="e05f9-199">c.</span><span class="sxs-lookup"><span data-stu-id="e05f9-199">c.</span></span> <span data-ttu-id="e05f9-200">Para carregar seu arquivo de metadados baixado, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-200">To upload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="e05f9-201">d.</span><span class="sxs-lookup"><span data-stu-id="e05f9-201">d.</span></span> <span data-ttu-id="e05f9-202">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="e05f9-203">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="e05f9-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e05f9-204">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e05f9-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e05f9-205">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e05f9-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e05f9-206">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e05f9-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="e05f9-207">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e05f9-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e05f9-209">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e05f9-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e05f9-210">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e05f9-212">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e05f9-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e05f9-214">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e05f9-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e05f9-216">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e05f9-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e05f9-218">a.</span><span class="sxs-lookup"><span data-stu-id="e05f9-218">a.</span></span> <span data-ttu-id="e05f9-219">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e05f9-220">b.</span><span class="sxs-lookup"><span data-stu-id="e05f9-220">b.</span></span> <span data-ttu-id="e05f9-221">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e05f9-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e05f9-222">c.</span><span class="sxs-lookup"><span data-stu-id="e05f9-222">c.</span></span> <span data-ttu-id="e05f9-223">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e05f9-224">d.</span><span class="sxs-lookup"><span data-stu-id="e05f9-224">d.</span></span> <span data-ttu-id="e05f9-225">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="e05f9-226">Criando um usuário de teste</span><span class="sxs-lookup"><span data-stu-id="e05f9-226">Creating an Aha!</span></span> <span data-ttu-id="e05f9-227">do Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-227">test user</span></span>

<span data-ttu-id="e05f9-228">Para permitir que os usuários do Azure AD façam logon no Aha!, eles devem ser provisionados no Aha!.</span><span class="sxs-lookup"><span data-stu-id="e05f9-228">To enable Azure AD users to log in to Aha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="e05f9-229">No caso do Aha!, o provisionamento é uma tarefa automatizada.</span><span class="sxs-lookup"><span data-stu-id="e05f9-229">In the case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="e05f9-230">Não há nenhum item de ação para você.</span><span class="sxs-lookup"><span data-stu-id="e05f9-230">There is no action item for you.</span></span>

<span data-ttu-id="e05f9-231">Os usuários são criados automaticamente, se necessário, durante a primeira tentativa de logon único.</span><span class="sxs-lookup"><span data-stu-id="e05f9-231">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="e05f9-232">É possível usar qualquer outra ferramenta de criação da conta de usuário do Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-232">You can use any other Aha!</span></span> <span data-ttu-id="e05f9-233">ou as APIs fornecidas pelo Aha!</span><span class="sxs-lookup"><span data-stu-id="e05f9-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="e05f9-234">para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="e05f9-234">to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e05f9-235">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e05f9-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e05f9-236">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Aha!.</span><span class="sxs-lookup"><span data-stu-id="e05f9-236">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aha!.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e05f9-238">**Para atribuir Brenda Fernandes ao Aha!, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e05f9-238">**To assign Britta Simon to Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="e05f9-239">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-239">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e05f9-241">Na lista de aplicativos, selecione **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-241">In the applications list, select **Aha!**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="e05f9-243">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e05f9-245">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e05f9-245">Click **Add** button.</span></span> <span data-ttu-id="e05f9-246">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e05f9-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e05f9-248">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e05f9-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e05f9-249">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e05f9-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e05f9-250">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e05f9-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e05f9-251">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e05f9-251">Testing single sign-on</span></span>

<span data-ttu-id="e05f9-252">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e05f9-252">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="e05f9-253">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e05f9-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e05f9-254">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e05f9-254">Additional resources</span></span>

* [<span data-ttu-id="e05f9-255">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e05f9-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e05f9-256">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e05f9-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

