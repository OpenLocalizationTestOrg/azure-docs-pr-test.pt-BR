---
title: "Tutorial: Integração do Azure Active Directory ao EverBridge | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: f5a97fc8df978dd55a73ae53516a82f884c14bec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="07b96-103">Tutorial: integração do Azure Active Directory ao Everbridge</span><span class="sxs-lookup"><span data-stu-id="07b96-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="07b96-104">Neste tutorial, você aprenderá a integrar o EverBridge ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="07b96-104">In this tutorial, you learn how to integrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07b96-105">A integração do EverBridge ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="07b96-105">Integrating EverBridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="07b96-106">Você pode controlar no Azure AD quem tem acesso ao EverBridge</span><span class="sxs-lookup"><span data-stu-id="07b96-106">You can control in Azure AD who has access to EverBridge</span></span>
- <span data-ttu-id="07b96-107">Você pode habilitar o logon automático de seus usuários no EverBridge (Logon Único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="07b96-107">You can enable your users to automatically get signed-on to EverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="07b96-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="07b96-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="07b96-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07b96-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07b96-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="07b96-110">Prerequisites</span></span>

<span data-ttu-id="07b96-111">Para configurar a integração do Azure AD ao EverBridge, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="07b96-111">To configure Azure AD integration with EverBridge, you need the following items:</span></span>

- <span data-ttu-id="07b96-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07b96-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07b96-113">Uma assinatura do EverBridge com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="07b96-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07b96-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="07b96-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07b96-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="07b96-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07b96-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="07b96-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07b96-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07b96-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07b96-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="07b96-118">Scenario description</span></span>
<span data-ttu-id="07b96-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="07b96-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07b96-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="07b96-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07b96-121">Adicionar EverBridge da galeria</span><span class="sxs-lookup"><span data-stu-id="07b96-121">Adding EverBridge from the gallery</span></span>
2. <span data-ttu-id="07b96-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07b96-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-the-gallery"></a><span data-ttu-id="07b96-123">Adicionar EverBridge da galeria</span><span class="sxs-lookup"><span data-stu-id="07b96-123">Adding EverBridge from the gallery</span></span>
<span data-ttu-id="07b96-124">Para configurar a integração do EverBridge ao Azure AD, você precisará adicionar o EverBridge da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="07b96-124">To configure the integration of EverBridge into Azure AD, you need to add EverBridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="07b96-125">**Para adicionar o EverBridge da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07b96-125">**To add EverBridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="07b96-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07b96-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="07b96-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="07b96-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="07b96-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="07b96-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="07b96-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07b96-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="07b96-133">Na caixa de pesquisa, digite **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="07b96-133">In the search box, type **EverBridge**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="07b96-135">No painel de resultados, selecione **EverBridge** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07b96-135">In the results panel, select **EverBridge**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="07b96-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07b96-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="07b96-138">Nesta seção, você configurará e testará o logon único do Azure AD com o EverBridge com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="07b96-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="07b96-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do EverBridge é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07b96-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EverBridge is to a user in Azure AD.</span></span> <span data-ttu-id="07b96-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no EverBridge.</span><span class="sxs-lookup"><span data-stu-id="07b96-140">In other words, a link relationship between an Azure AD user and the related user in EverBridge needs to be established.</span></span>

<span data-ttu-id="07b96-141">No EverBridge, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="07b96-141">In EverBridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="07b96-142">Para configurar e testar o logon único do Azure AD com o EverBridge, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="07b96-142">To configure and test Azure AD single sign-on with EverBridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="07b96-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="07b96-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="07b96-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="07b96-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07b96-145">**[Criar um usuário de teste do EverBridge](#creating-an-everbridge-test-user)** – para ter um equivalente de Brenda Fernandes no EverBridge que esteja vinculado à representação desse usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07b96-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - to have a counterpart of Britta Simon in EverBridge that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="07b96-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="07b96-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07b96-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="07b96-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="07b96-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="07b96-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="07b96-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo EverBridge.</span><span class="sxs-lookup"><span data-stu-id="07b96-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="07b96-150">**Para configurar o logon único do Azure AD com o EverBridge, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07b96-150">**To configure Azure AD single sign-on with EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="07b96-151">No portal do Azure, na página de integração de aplicativos do **EverBridge**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="07b96-151">In the Azure portal, on the **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="07b96-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="07b96-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="07b96-155">Na seção **URLs e Domínio do EverBridge**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="07b96-155">On the **EverBridge Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="07b96-157">a.</span><span class="sxs-lookup"><span data-stu-id="07b96-157">a.</span></span> <span data-ttu-id="07b96-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="07b96-158">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="07b96-159">b.</span><span class="sxs-lookup"><span data-stu-id="07b96-159">b.</span></span> <span data-ttu-id="07b96-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="07b96-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="07b96-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="07b96-161">These values are not real.</span></span> <span data-ttu-id="07b96-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="07b96-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="07b96-163">Entre em contato com a [equipe de suporte do EverBridge](mailto:support@everbridge.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="07b96-163">Contact [EverBridge support team](mailto:support@everbridge.com) to get these values.</span></span>
 
4. <span data-ttu-id="07b96-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="07b96-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="07b96-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="07b96-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="07b96-168">Na seção **Configuração do EverBridge**, clique em **Configurar o EverBridge** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="07b96-168">On the **EverBridge Configuration** section, click **Configure EverBridge** to open **Configure sign-on** window.</span></span> <span data-ttu-id="07b96-169">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="07b96-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="07b96-171">Para configurar o SSO para o aplicativo, você precisa entrar no locatário Everbridge como administrador.</span><span class="sxs-lookup"><span data-stu-id="07b96-171">To get SSO configured for your application, you need to sign-on to your Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="07b96-172">No menu na parte superior, clique na guia **Configurações** e selecione **Logon Único** em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="07b96-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="07b96-174">a.</span><span class="sxs-lookup"><span data-stu-id="07b96-174">a.</span></span> <span data-ttu-id="07b96-175">Na caixa de texto **Nome**, digite o nome do Provedor do Identificador (por exemplo: o nome de sua empresa).</span><span class="sxs-lookup"><span data-stu-id="07b96-175">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="07b96-176">b.</span><span class="sxs-lookup"><span data-stu-id="07b96-176">b.</span></span> <span data-ttu-id="07b96-177">Na caixa de texto **Nome da API** , digite o nome da API.</span><span class="sxs-lookup"><span data-stu-id="07b96-177">In the **API Name** textbox, type the name of API.</span></span>
   
    <span data-ttu-id="07b96-178">c.</span><span class="sxs-lookup"><span data-stu-id="07b96-178">c.</span></span> <span data-ttu-id="07b96-179">Clique no botão **Escolher Arquivo** para carregar o arquivo de metadados que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="07b96-179">Click **Choose File** button to upload the metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="07b96-180">d.</span><span class="sxs-lookup"><span data-stu-id="07b96-180">d.</span></span> <span data-ttu-id="07b96-181">No Local de Identidade do SAML, selecione **A identidade está no elemento NameIdentifier da instrução Subject**.</span><span class="sxs-lookup"><span data-stu-id="07b96-181">In the SAML Identity Location, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
   
    <span data-ttu-id="07b96-182">e.</span><span class="sxs-lookup"><span data-stu-id="07b96-182">e.</span></span> <span data-ttu-id="07b96-183">Na caixa de texto **URL de Logon do Provedor de Identidade**, cole o valor da URL do SSO do SAML do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07b96-183">In the **Identity Provider Login URL** textbox, paste the value of SAML SSO URL from Azure AD.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="07b96-185">f.</span><span class="sxs-lookup"><span data-stu-id="07b96-185">f.</span></span> <span data-ttu-id="07b96-186">Na Associação de Solicitação Iniciada pelo Provedor de Serviço, selecione **Redirecionamento HTTP**.</span><span class="sxs-lookup"><span data-stu-id="07b96-186">In the Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="07b96-187">g.</span><span class="sxs-lookup"><span data-stu-id="07b96-187">g.</span></span> <span data-ttu-id="07b96-188">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="07b96-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="07b96-189">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="07b96-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="07b96-190">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="07b96-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="07b96-191">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07b96-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="07b96-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07b96-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="07b96-193">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="07b96-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="07b96-195">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07b96-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="07b96-196">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07b96-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="07b96-198">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="07b96-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="07b96-200">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07b96-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="07b96-202">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="07b96-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="07b96-204">a.</span><span class="sxs-lookup"><span data-stu-id="07b96-204">a.</span></span> <span data-ttu-id="07b96-205">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="07b96-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07b96-206">b.</span><span class="sxs-lookup"><span data-stu-id="07b96-206">b.</span></span> <span data-ttu-id="07b96-207">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="07b96-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="07b96-208">c.</span><span class="sxs-lookup"><span data-stu-id="07b96-208">c.</span></span> <span data-ttu-id="07b96-209">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="07b96-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="07b96-210">d.</span><span class="sxs-lookup"><span data-stu-id="07b96-210">d.</span></span> <span data-ttu-id="07b96-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="07b96-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="07b96-212">Criar um usuário de teste do EverBridge</span><span class="sxs-lookup"><span data-stu-id="07b96-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="07b96-213">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Everbridge.</span><span class="sxs-lookup"><span data-stu-id="07b96-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="07b96-214">Trabalhe com a [equipe de suporte do EverBridge](mailto:support@everbridge.com) para adicionar os usuários na plataforma do Everbridge.</span><span class="sxs-lookup"><span data-stu-id="07b96-214">Work with [EverBridge support team](mailto:support@everbridge.com) to add the users in the Everbridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="07b96-215">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07b96-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="07b96-216">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao EverBridge.</span><span class="sxs-lookup"><span data-stu-id="07b96-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EverBridge.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="07b96-218">**Para atribuir Brenda Fernandes ao EverBridge, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07b96-218">**To assign Britta Simon to EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="07b96-219">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="07b96-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="07b96-221">Na lista de aplicativos, selecione **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="07b96-221">In the applications list, select **EverBridge**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="07b96-223">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="07b96-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="07b96-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="07b96-225">Click **Add** button.</span></span> <span data-ttu-id="07b96-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07b96-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="07b96-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="07b96-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="07b96-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07b96-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07b96-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07b96-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="07b96-231">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="07b96-231">Testing single sign-on</span></span>

<span data-ttu-id="07b96-232">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="07b96-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="07b96-233">Quando você clica no bloco Everbridge no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo Everbridge.</span><span class="sxs-lookup"><span data-stu-id="07b96-233">When you click the Everbridge tile in the Access Panel, you should get automatically signed-on to your Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07b96-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="07b96-234">Additional resources</span></span>

* [<span data-ttu-id="07b96-235">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="07b96-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07b96-236">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07b96-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

