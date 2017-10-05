---
title: "Tutorial: Integração do Azure Active Directory com o PostBeyond | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o PostBeyond."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 09992f08-ec50-4472-997f-ccbe719039e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 80b920dc99619795cbc86e8cb2e3ac2a78a71932
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-postbeyond"></a><span data-ttu-id="1f36d-103">Tutorial: Integração do Azure Active Directory com o PostBeyond</span><span class="sxs-lookup"><span data-stu-id="1f36d-103">Tutorial: Azure Active Directory integration with PostBeyond</span></span>

<span data-ttu-id="1f36d-104">Neste tutorial, você aprenderá a integrar o PostBeyond ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1f36d-104">In this tutorial, you learn how to integrate PostBeyond with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f36d-105">A integração do PostBeyond ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="1f36d-105">Integrating PostBeyond with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1f36d-106">Você pode controlar no Azure AD quem tem acesso ao PostBeyond</span><span class="sxs-lookup"><span data-stu-id="1f36d-106">You can control in Azure AD who has access to PostBeyond</span></span>
- <span data-ttu-id="1f36d-107">Você pode permitir que os usuários façam logon automaticamente no PostBeyond (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f36d-107">You can enable your users to automatically get signed-on to PostBeyond (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f36d-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1f36d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1f36d-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f36d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f36d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1f36d-110">Prerequisites</span></span>

<span data-ttu-id="1f36d-111">Para configurar a integração do Azure AD ao PostBeyond, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1f36d-111">To configure Azure AD integration with PostBeyond, you need the following items:</span></span>

- <span data-ttu-id="1f36d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f36d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f36d-113">Uma assinatura habilitada para logon único do PostBeyond</span><span class="sxs-lookup"><span data-stu-id="1f36d-113">A PostBeyond single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f36d-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1f36d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f36d-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1f36d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f36d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1f36d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f36d-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f36d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f36d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1f36d-118">Scenario description</span></span>
<span data-ttu-id="1f36d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1f36d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f36d-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="1f36d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f36d-121">Adicionando o PostBeyond da galeria</span><span class="sxs-lookup"><span data-stu-id="1f36d-121">Adding PostBeyond from the gallery</span></span>
2. <span data-ttu-id="1f36d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f36d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-postbeyond-from-the-gallery"></a><span data-ttu-id="1f36d-123">Adicionando o PostBeyond da galeria</span><span class="sxs-lookup"><span data-stu-id="1f36d-123">Adding PostBeyond from the gallery</span></span>
<span data-ttu-id="1f36d-124">Para configurar a integração do PostBeyond ao Azure AD, você precisa adicionar o PostBeyond por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1f36d-124">To configure the integration of PostBeyond into Azure AD, you need to add PostBeyond from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1f36d-125">**Para adicionar o PostBeyond da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1f36d-125">**To add PostBeyond from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1f36d-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f36d-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1f36d-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1f36d-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f36d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1f36d-133">Na caixa de pesquisa, digite **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-133">In the search box, type **PostBeyond**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_search.png)

5. <span data-ttu-id="1f36d-135">No painel de resultados, selecione **PostBeyond** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f36d-135">In the results panel, select **PostBeyond**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f36d-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f36d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f36d-138">Nesta seção, você configurará e testará o logon único do Azure AD com o PostBeyond, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1f36d-138">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1f36d-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do PostBeyond é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f36d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PostBeyond is to a user in Azure AD.</span></span> <span data-ttu-id="1f36d-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="1f36d-140">In other words, a link relationship between an Azure AD user and the related user in PostBeyond needs to be established.</span></span>

<span data-ttu-id="1f36d-141">No PostBeyond, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="1f36d-141">In PostBeyond, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1f36d-142">Para configurar e testar o logon único do Azure AD com o PostBeyond, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="1f36d-142">To configure and test Azure AD single sign-on with PostBeyond, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1f36d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1f36d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1f36d-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1f36d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f36d-145">**[Criação de um usuário de teste do PostBeyond](#creating-a-postbeyond-test-user)** – para ter um equivalente de Brenda Fernandes no PostBeyond que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f36d-145">**[Creating a PostBeyond test user](#creating-a-postbeyond-test-user)** - to have a counterpart of Britta Simon in PostBeyond that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f36d-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f36d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f36d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="1f36d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f36d-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f36d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f36d-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="1f36d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PostBeyond application.</span></span>

<span data-ttu-id="1f36d-150">**Para configurar o logon único do Azure AD com o PostBeyond, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1f36d-150">**To configure Azure AD single sign-on with PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="1f36d-151">No Portal do Azure, na página de integração de aplicativos do **PostBeyond**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-151">In the Azure portal, on the **PostBeyond** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1f36d-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="1f36d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_samlbase.png)

3. <span data-ttu-id="1f36d-155">Na seção **URLs e Domínio do PostBeyond**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1f36d-155">On the **PostBeyond Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_url.png)

    <span data-ttu-id="1f36d-157">a.</span><span class="sxs-lookup"><span data-stu-id="1f36d-157">a.</span></span> <span data-ttu-id="1f36d-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="1f36d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    <span data-ttu-id="1f36d-159">b.</span><span class="sxs-lookup"><span data-stu-id="1f36d-159">b.</span></span> <span data-ttu-id="1f36d-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="1f36d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1f36d-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="1f36d-161">These values are not real.</span></span> <span data-ttu-id="1f36d-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="1f36d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1f36d-163">Entre em contato com a [equipe de suporte ao cliente do PostBeyond](mailto:sso@postbeyond.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="1f36d-163">Contact [PostBeyond Client support team](mailto:sso@postbeyond.com) to get these values.</span></span> 
 
4. <span data-ttu-id="1f36d-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="1f36d-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_certificate.png) 

5. <span data-ttu-id="1f36d-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1f36d-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-postbeyond-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1f36d-168">Na seção **Configuração do PostBeyond**, clique em **Configurar o PostBeyond** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-168">On the **PostBeyond Configuration** section, click **Configure PostBeyond** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1f36d-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="1f36d-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_configure.png) 

7. <span data-ttu-id="1f36d-171">Para configurar o logon único no lado do **PostBeyond**, é necessário enviar o **Certificado (Base64)** baixado, a **ID da Entidade SAML**, a **URL do Serviço de Logon Único** e a **URL de Saída** para a [equipe de suporte do PostBeyond](mailto:sso@postbeyond.com).</span><span class="sxs-lookup"><span data-stu-id="1f36d-171">To configure single sign-on on **PostBeyond** side, you need to send the downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** to [PostBeyond support team](mailto:sso@postbeyond.com).</span></span> <span data-ttu-id="1f36d-172">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="1f36d-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1f36d-173">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="1f36d-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1f36d-174">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1f36d-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1f36d-175">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f36d-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f36d-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f36d-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f36d-177">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1f36d-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1f36d-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1f36d-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1f36d-180">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f36d-182">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1f36d-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f36d-184">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f36d-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f36d-186">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1f36d-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f36d-188">a.</span><span class="sxs-lookup"><span data-stu-id="1f36d-188">a.</span></span> <span data-ttu-id="1f36d-189">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f36d-190">b.</span><span class="sxs-lookup"><span data-stu-id="1f36d-190">b.</span></span> <span data-ttu-id="1f36d-191">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1f36d-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f36d-192">c.</span><span class="sxs-lookup"><span data-stu-id="1f36d-192">c.</span></span> <span data-ttu-id="1f36d-193">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1f36d-194">d.</span><span class="sxs-lookup"><span data-stu-id="1f36d-194">d.</span></span> <span data-ttu-id="1f36d-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-195">Click **Create**.</span></span>
 
### <a name="creating-a-postbeyond-test-user"></a><span data-ttu-id="1f36d-196">Criando um usuário de teste do PostBeyond</span><span class="sxs-lookup"><span data-stu-id="1f36d-196">Creating a PostBeyond test user</span></span>

<span data-ttu-id="1f36d-197">Nesta seção, você criará uma usuária chamada Brenda Fernandes no PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="1f36d-197">In this section, you create a user called Britta Simon in PostBeyond.</span></span> <span data-ttu-id="1f36d-198">Se você não souber como adicionar Brenda Fernandes ao PostBeyond, trabalhe com a [equipe de suporte do PostBeyond](mailto:sso@postbeyond.com) para adicionar o usuário de teste e habilitar o SSO.</span><span class="sxs-lookup"><span data-stu-id="1f36d-198">If you don't know how to add Britta Simon in PostBeyond, please work with [PostBeyond support team](mailto:sso@postbeyond.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1f36d-199">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f36d-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1f36d-200">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="1f36d-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PostBeyond.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1f36d-202">**Para atribuir Brenda Fernandes ao PostBeyond, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1f36d-202">**To assign Britta Simon to PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="1f36d-203">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1f36d-205">Na lista de aplicativos, selecione **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-205">In the applications list, select **PostBeyond**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_app.png) 

3. <span data-ttu-id="1f36d-207">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1f36d-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-209">Click **Add** button.</span></span> <span data-ttu-id="1f36d-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f36d-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1f36d-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1f36d-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1f36d-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f36d-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f36d-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f36d-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f36d-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1f36d-215">Testing single sign-on</span></span>

<span data-ttu-id="1f36d-216">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="1f36d-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1f36d-217">Quando você clica no bloco PostBeyond no Painel de Acesso, deve acessar a página de entrada do PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="1f36d-217">When you click the PostBeyond tile in the Access Panel, you should get to the PostBeyond sign in page.</span></span> <span data-ttu-id="1f36d-218">Clique em **Entrar com o Office 365**, insira suas credenciais do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f36d-218">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span></span> <span data-ttu-id="1f36d-219">Em seguida, você deve estar conectado ao PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="1f36d-219">Then, you should be logged in into PostBeyond.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f36d-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1f36d-220">Additional resources</span></span>

* [<span data-ttu-id="1f36d-221">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1f36d-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f36d-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f36d-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_203.png

