---
title: "Tutorial: Integração do Azure Active Directory com o Syncplicity | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 1321fa71bcd625d6ea754432bfb402d3919e38f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="a719a-103">Tutorial: Integração do Active Directory do Azure com o Syncplicity</span><span class="sxs-lookup"><span data-stu-id="a719a-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="a719a-104">Neste tutorial, você aprenderá a integrar o Syncplicity ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a719a-104">In this tutorial, you learn how to integrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a719a-105">A integração do Syncplicity ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a719a-105">Integrating Syncplicity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a719a-106">No Azure AD, é possível controlar quem tem acesso ao Syncplicity</span><span class="sxs-lookup"><span data-stu-id="a719a-106">You can control in Azure AD who has access to Syncplicity</span></span>
- <span data-ttu-id="a719a-107">Você pode permitir que seus usuários façam logon automaticamente no Syncplicity (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="a719a-107">You can enable your users to automatically get signed-on to Syncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a719a-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a719a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a719a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a719a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a719a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a719a-110">Prerequisites</span></span>

<span data-ttu-id="a719a-111">Para configurar a integração do Azure AD ao Syncplicity, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a719a-111">To configure Azure AD integration with Syncplicity, you need the following items:</span></span>

- <span data-ttu-id="a719a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a719a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a719a-113">Uma assinatura habilitada para logon único do Syncplicity</span><span class="sxs-lookup"><span data-stu-id="a719a-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a719a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a719a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a719a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a719a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a719a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a719a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a719a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a719a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a719a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a719a-118">Scenario description</span></span>
<span data-ttu-id="a719a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a719a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a719a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a719a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a719a-121">Adicionar o Syncplicity da galeria</span><span class="sxs-lookup"><span data-stu-id="a719a-121">Adding Syncplicity from the gallery</span></span>
2. <span data-ttu-id="a719a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a719a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-the-gallery"></a><span data-ttu-id="a719a-123">Adicionar o Syncplicity da galeria</span><span class="sxs-lookup"><span data-stu-id="a719a-123">Adding Syncplicity from the gallery</span></span>
<span data-ttu-id="a719a-124">Para configurar a integração do Syncplicity ao Azure AD, você precisará adicionar o Syncplicity da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a719a-124">To configure the integration of Syncplicity into Azure AD, you need to add Syncplicity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a719a-125">**Para adicionar o Syncplicity da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a719a-125">**To add Syncplicity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a719a-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a719a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a719a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a719a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a719a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a719a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a719a-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a719a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a719a-133">Na caixa de pesquisa, digite **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="a719a-133">In the search box, type **Syncplicity**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="a719a-135">No painel de resultados, selecione **Syncplicity** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a719a-135">In the results panel, select **Syncplicity**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a719a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a719a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a719a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Syncplicity, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a719a-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a719a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Syncplicity é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a719a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Syncplicity is to a user in Azure AD.</span></span> <span data-ttu-id="a719a-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="a719a-140">In other words, a link relationship between an Azure AD user and the related user in Syncplicity needs to be established.</span></span>

<span data-ttu-id="a719a-141">No Syncplicity, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="a719a-141">In Syncplicity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a719a-142">Para configurar e testar o logon único do Azure AD com o Syncplicity, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="a719a-142">To configure and test Azure AD single sign-on with Syncplicity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a719a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a719a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a719a-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a719a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a719a-145">**[Criação de um usuário de teste do Syncplicity](#creating-a-syncplicity-test-user)** – para ter um equivalente de Brenda Fernandes no Syncplicity que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a719a-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - to have a counterpart of Britta Simon in Syncplicity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a719a-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a719a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a719a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="a719a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a719a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a719a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a719a-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="a719a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="a719a-150">**Para configurar o logon único do Azure AD com o Syncplicity, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a719a-150">**To configure Azure AD single sign-on with Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="a719a-151">No portal do Azure, na página de integração de aplicativos do **Syncplicity**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a719a-151">In the Azure portal, on the **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a719a-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a719a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="a719a-155">Na seção **URLs e Domínio do Syncplicity**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a719a-155">On the **Syncplicity Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="a719a-157">a.</span><span class="sxs-lookup"><span data-stu-id="a719a-157">a.</span></span> <span data-ttu-id="a719a-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="a719a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="a719a-159">b.</span><span class="sxs-lookup"><span data-stu-id="a719a-159">b.</span></span> <span data-ttu-id="a719a-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="a719a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a719a-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="a719a-161">These values are not real.</span></span> <span data-ttu-id="a719a-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="a719a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a719a-163">Contate a [equipe de suporte do cliente Syncplicity](https://www.syncplicity.com/contact-us) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="a719a-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values.</span></span> 
 

4. <span data-ttu-id="a719a-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a719a-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="a719a-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a719a-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a719a-168">Na seção **Configuração do Syncplicity**, clique em **Configurar Syncplicity** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="a719a-168">On the **Syncplicity Configuration** section, click **Configure Syncplicity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a719a-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="a719a-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="a719a-171">Entre no locatário do **Syncplicity** .</span><span class="sxs-lookup"><span data-stu-id="a719a-171">Sign in to your **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="a719a-172">No menu, na parte superior, clique em **administrador**, selecione **configurações** e clique em **Domínio personalizado e logon único**.</span><span class="sxs-lookup"><span data-stu-id="a719a-172">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="a719a-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="a719a-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="a719a-174">Na página do diálogo **SSO (Logon Único)** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a719a-174">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="a719a-175">![Logon Único \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="a719a-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="a719a-176">a.</span><span class="sxs-lookup"><span data-stu-id="a719a-176">a.</span></span> <span data-ttu-id="a719a-177">Na caixa de texto **Domínio Personalizado** , digite o nome do seu domínio.</span><span class="sxs-lookup"><span data-stu-id="a719a-177">In the **Custom Domain** textbox, type the name of your domain.</span></span>
  
    <span data-ttu-id="a719a-178">b.</span><span class="sxs-lookup"><span data-stu-id="a719a-178">b.</span></span> <span data-ttu-id="a719a-179">Selecione **Habilitado** como **Status do Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="a719a-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="a719a-180">c.</span><span class="sxs-lookup"><span data-stu-id="a719a-180">c.</span></span> <span data-ttu-id="a719a-181">Na caixa de texto **ID da Entidade**, cole o valor da **ID da Entidade do SAML** copiado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a719a-181">In the **Entity Id** textbox, Paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a719a-182">d.</span><span class="sxs-lookup"><span data-stu-id="a719a-182">d.</span></span> <span data-ttu-id="a719a-183">Na caixa de texto **URL da página de entrada**, cole o valor da **URL do Serviço de Logon Único do SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a719a-183">In the **Sign-in page URL** textbox, Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a719a-184">e.</span><span class="sxs-lookup"><span data-stu-id="a719a-184">e.</span></span> <span data-ttu-id="a719a-185">Na caixa de texto **URL da Página de Logoff**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a719a-185">In the **Logout page URL** textbox, Paste the **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a719a-186">f.</span><span class="sxs-lookup"><span data-stu-id="a719a-186">f.</span></span> <span data-ttu-id="a719a-187">Em **Certificado do Provedor de Identidade**, clique em **Escolher Arquivo** e carregue o certificado que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a719a-187">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate which you have downloaded from the Azure portal.</span></span> 

    <span data-ttu-id="a719a-188">g.</span><span class="sxs-lookup"><span data-stu-id="a719a-188">g.</span></span> <span data-ttu-id="a719a-189">Clique em **SALVAR ALTERAÇÕES**.</span><span class="sxs-lookup"><span data-stu-id="a719a-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="a719a-190">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="a719a-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a719a-191">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a719a-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a719a-192">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a719a-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a719a-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a719a-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="a719a-194">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a719a-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a719a-196">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a719a-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a719a-197">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a719a-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a719a-199">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a719a-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a719a-201">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a719a-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a719a-203">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a719a-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a719a-205">a.</span><span class="sxs-lookup"><span data-stu-id="a719a-205">a.</span></span> <span data-ttu-id="a719a-206">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a719a-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a719a-207">b.</span><span class="sxs-lookup"><span data-stu-id="a719a-207">b.</span></span> <span data-ttu-id="a719a-208">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a719a-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a719a-209">c.</span><span class="sxs-lookup"><span data-stu-id="a719a-209">c.</span></span> <span data-ttu-id="a719a-210">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="a719a-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a719a-211">d.</span><span class="sxs-lookup"><span data-stu-id="a719a-211">d.</span></span> <span data-ttu-id="a719a-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a719a-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="a719a-213">Criar um usuário de teste do Syncplicity</span><span class="sxs-lookup"><span data-stu-id="a719a-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="a719a-214">Para que os usuários do AAD possam fazer logon, eles devem ser provisionados no aplicativo Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="a719a-214">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span></span> <span data-ttu-id="a719a-215">Esta seção descreve como criar contas de usuário do AAD no Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="a719a-215">This section describes how to create AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="a719a-216">**Para provisionar uma conta de usuário no Syncplicity, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a719a-216">**To provision a user account to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="a719a-217">Faça logon no locatário do **Syncplicity** (por exemplo, `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="a719a-217">Log in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="a719a-218">Clique em **Administrador** e selecione **Contas de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="a719a-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="a719a-219">Clique em **ADICIONAR UM USUÁRIO**.</span><span class="sxs-lookup"><span data-stu-id="a719a-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="a719a-220">![Gerenciar Usuários](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="a719a-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="a719a-221">Digite os **Endereços de Email** da conta do AAD que você deseja provisionar, selecione **Usuário** como **Função** e clique em **AVANÇAR**.</span><span class="sxs-lookup"><span data-stu-id="a719a-221">Type the **Email addressess** of an AAD account you want to provision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="a719a-222">![Dados da Conta](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Dados da Conta")</span><span class="sxs-lookup"><span data-stu-id="a719a-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="a719a-223">O titular da conta do AAD receberá um email incluindo um link para confirmar e ativar a conta.</span><span class="sxs-lookup"><span data-stu-id="a719a-223">The AAD account holder  gets an email including a link to confirm and activate the account.</span></span> 
    > 

5. <span data-ttu-id="a719a-224">Selecione um grupo em sua empresa do qual o novo usuário deverá se tornar membro e clique em **AVANÇAR**.</span><span class="sxs-lookup"><span data-stu-id="a719a-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="a719a-225">![Associação a um Grupo](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Associação a um Grupo")</span><span class="sxs-lookup"><span data-stu-id="a719a-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="a719a-226">Se não houver nenhum grupo listado, basta clicar em **AVANÇAR**.</span><span class="sxs-lookup"><span data-stu-id="a719a-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="a719a-227">Selecione as pastas que você gostaria de colocar sob o controle do Syncplicity no computador do usuário e clique em **AVANÇAR**.</span><span class="sxs-lookup"><span data-stu-id="a719a-227">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="a719a-228">![Pastas do Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Pastas do Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="a719a-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="a719a-229">É possível usar qualquer outra ferramenta de criação da conta de usuário do Syncplicity ou as APIs fornecidas pelo Syncplicity para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="a719a-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a719a-230">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a719a-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a719a-231">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="a719a-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Syncplicity.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a719a-233">**Para atribuir Brenda Fernandes ao Syncplicity, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a719a-233">**To assign Britta Simon to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="a719a-234">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a719a-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a719a-236">Na lista de aplicativos, selecione **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="a719a-236">In the applications list, select **Syncplicity**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="a719a-238">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a719a-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a719a-240">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a719a-240">Click **Add** button.</span></span> <span data-ttu-id="a719a-241">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a719a-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a719a-243">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a719a-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a719a-244">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a719a-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a719a-245">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a719a-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a719a-246">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a719a-246">Testing single sign-on</span></span>

<span data-ttu-id="a719a-247">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a719a-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a719a-248">Quando você clicar no bloco Syncplicity no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="a719a-248">When you click the Syncplicity tile in the Access Panel, you should get automatically signed-on to your Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="a719a-249">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a719a-249">Additional resources</span></span>

* [<span data-ttu-id="a719a-250">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a719a-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a719a-251">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a719a-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

