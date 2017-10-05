---
title: "Tutorial: integração do Azure Active Directory ao HireVue | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o HireVue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 682d88d3010f5781948a9adde0e1351471608a5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="e9486-103">Tutorial: Integração do Azure Active Directory com o HireVue</span><span class="sxs-lookup"><span data-stu-id="e9486-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="e9486-104">Neste tutorial, você aprenderá como integrar o HireVue ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e9486-104">In this tutorial, you learn how to integrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9486-105">A integração do HireVue ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e9486-105">Integrating HireVue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e9486-106">No Azure AD, é possível controlar quem tem acesso ao HireVue</span><span class="sxs-lookup"><span data-stu-id="e9486-106">You can control in Azure AD who has access to HireVue</span></span>
- <span data-ttu-id="e9486-107">Você pode permitir que os usuários façam logon automaticamente no HireVue (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9486-107">You can enable your users to automatically get signed-on to HireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e9486-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e9486-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e9486-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9486-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9486-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e9486-110">Prerequisites</span></span>

<span data-ttu-id="e9486-111">Para configurar a integração do Azure AD ao HireVue, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e9486-111">To configure Azure AD integration with HireVue, you need the following items:</span></span>

- <span data-ttu-id="e9486-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e9486-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9486-113">Uma assinatura habilitada para logon único do HireVue</span><span class="sxs-lookup"><span data-stu-id="e9486-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9486-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e9486-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9486-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e9486-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9486-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e9486-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9486-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9486-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9486-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e9486-118">Scenario description</span></span>
<span data-ttu-id="e9486-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e9486-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9486-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e9486-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9486-121">Adicionar HireVue da galeria</span><span class="sxs-lookup"><span data-stu-id="e9486-121">Adding HireVue from the gallery</span></span>
2. <span data-ttu-id="e9486-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e9486-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-the-gallery"></a><span data-ttu-id="e9486-123">Adicionar HireVue da galeria</span><span class="sxs-lookup"><span data-stu-id="e9486-123">Adding HireVue from the gallery</span></span>
<span data-ttu-id="e9486-124">Para configurar a integração do HireVue ao Azure AD, você precisará adicionar o HireVue da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e9486-124">To configure the integration of HireVue into Azure AD, you need to add HireVue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9486-125">**Para adicionar o HireVue por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e9486-125">**To add HireVue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9486-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9486-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e9486-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e9486-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e9486-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e9486-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e9486-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9486-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e9486-133">Na caixa de pesquisa, digite **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="e9486-133">In the search box, type **HireVue**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="e9486-135">No painel de resultados, selecione **HireVue** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9486-135">In the results panel, select **HireVue**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e9486-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e9486-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e9486-138">Nesta seção, você configurará e testará o logon único do Azure AD com o HireVue, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="e9486-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9486-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do HireVue é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9486-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HireVue is to a user in Azure AD.</span></span> <span data-ttu-id="e9486-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do HireVue.</span><span class="sxs-lookup"><span data-stu-id="e9486-140">In other words, a link relationship between an Azure AD user and the related user in HireVue needs to be established.</span></span>

<span data-ttu-id="e9486-141">No HireVue, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="e9486-141">In HireVue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e9486-142">Para configurar e testar o logon único do Azure AD com o HireVue, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e9486-142">To configure and test Azure AD single sign-on with HireVue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9486-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e9486-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e9486-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e9486-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9486-145">**[Como criar um usuário de teste do HireVue](#creating-a-hirevue-test-user)** – para ter um equivalente de Brenda Fernandes no HireVue que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9486-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - to have a counterpart of Britta Simon in HireVue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9486-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9486-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9486-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e9486-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e9486-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9486-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e9486-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo HireVue.</span><span class="sxs-lookup"><span data-stu-id="e9486-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="e9486-150">**Para configurar o logon único do Azure AD com o HireVue, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e9486-150">**To configure Azure AD single sign-on with HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="e9486-151">No portal do Azure, na página de integração de aplicativos do **HireVue**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e9486-151">In the Azure portal, on the **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e9486-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e9486-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="e9486-155">Na seção **URLs e Domínio do HireVue**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e9486-155">On the **HireVue Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="e9486-157">a.</span><span class="sxs-lookup"><span data-stu-id="e9486-157">a.</span></span> <span data-ttu-id="e9486-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="e9486-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>

    | <span data-ttu-id="e9486-159">Ambiente</span><span class="sxs-lookup"><span data-stu-id="e9486-159">Environment</span></span> | <span data-ttu-id="e9486-160">URL</span><span class="sxs-lookup"><span data-stu-id="e9486-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="e9486-161">Produção</span><span class="sxs-lookup"><span data-stu-id="e9486-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="e9486-162">Staging</span><span class="sxs-lookup"><span data-stu-id="e9486-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="e9486-163">b.</span><span class="sxs-lookup"><span data-stu-id="e9486-163">b.</span></span> <span data-ttu-id="e9486-164">Na caixa de texto **Identificador**, digite uma URL como:</span><span class="sxs-lookup"><span data-stu-id="e9486-164">In the **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="e9486-165">Ambiente</span><span class="sxs-lookup"><span data-stu-id="e9486-165">Environment</span></span> | <span data-ttu-id="e9486-166">URN</span><span class="sxs-lookup"><span data-stu-id="e9486-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="e9486-167">Produção</span><span class="sxs-lookup"><span data-stu-id="e9486-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="e9486-168">Staging</span><span class="sxs-lookup"><span data-stu-id="e9486-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="e9486-169">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e9486-169">These values are not real.</span></span> <span data-ttu-id="e9486-170">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="e9486-170">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e9486-171">Contate a [equipe de suporte ao Cliente do HireVue](mailto:samlsupport@hirevue.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="e9486-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) to get these values.</span></span> 
 
4. <span data-ttu-id="e9486-172">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="e9486-172">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="e9486-174">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e9486-174">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e9486-176">Na seção **Configuração do HireVue**, clique em **Configurar HireVue** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="e9486-176">On the **HireVue Configuration** section, click **Configure HireVue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e9486-177">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="e9486-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="e9486-179">Para configurar o logon único no lado do **HireVue**, é necessário enviar o **Certificado (Base64)** baixado, a **URL de Saída, ID da Entidade SAML e URL do Serviço de Logon Único SAML** para a [equipe de suporte do HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="e9486-179">To configure single sign-on on **HireVue** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="e9486-180">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="e9486-180">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e9486-181">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="e9486-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e9486-182">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e9486-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e9486-183">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e9486-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e9486-184">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e9486-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="e9486-185">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e9486-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e9486-187">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e9486-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9486-188">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9486-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e9486-190">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e9486-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e9486-192">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9486-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e9486-194">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e9486-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e9486-196">a.</span><span class="sxs-lookup"><span data-stu-id="e9486-196">a.</span></span> <span data-ttu-id="e9486-197">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e9486-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9486-198">b.</span><span class="sxs-lookup"><span data-stu-id="e9486-198">b.</span></span> <span data-ttu-id="e9486-199">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e9486-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e9486-200">c.</span><span class="sxs-lookup"><span data-stu-id="e9486-200">c.</span></span> <span data-ttu-id="e9486-201">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="e9486-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e9486-202">d.</span><span class="sxs-lookup"><span data-stu-id="e9486-202">d.</span></span> <span data-ttu-id="e9486-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e9486-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="e9486-204">Como criar um usuário de teste do HireVue</span><span class="sxs-lookup"><span data-stu-id="e9486-204">Creating a HireVue test user</span></span>

<span data-ttu-id="e9486-205">Nesta seção, você criará uma usuária chamada Brenda Fernandes no HireVue.</span><span class="sxs-lookup"><span data-stu-id="e9486-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="e9486-206">Trabalhe com a [equipe de suporte do HireVue](mailto:samlsupport@hirevue.com) para adicionar usuários à plataforma do HireVue.</span><span class="sxs-lookup"><span data-stu-id="e9486-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) to add the users in the HireVue platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e9486-207">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e9486-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e9486-208">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao HireVue.</span><span class="sxs-lookup"><span data-stu-id="e9486-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HireVue.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e9486-210">**Para atribuir Brenda Fernandes ao HireVue, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e9486-210">**To assign Britta Simon to HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="e9486-211">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e9486-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e9486-213">Na lista de aplicativos, escolha **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="e9486-213">In the applications list, select **HireVue**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="e9486-215">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e9486-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e9486-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e9486-217">Click **Add** button.</span></span> <span data-ttu-id="e9486-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9486-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e9486-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e9486-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e9486-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9486-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9486-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9486-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e9486-223">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e9486-223">Testing single sign-on</span></span>

<span data-ttu-id="e9486-224">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e9486-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e9486-225">Ao clicar no bloco do HireVue no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo HireVue.</span><span class="sxs-lookup"><span data-stu-id="e9486-225">When you click the HireVue tile in the Access Panel, you should get automatically signed-on to your HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e9486-226">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e9486-226">Additional resources</span></span>

* [<span data-ttu-id="e9486-227">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e9486-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9486-228">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9486-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png

