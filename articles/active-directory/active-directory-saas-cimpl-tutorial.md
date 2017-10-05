---
title: "Tutorial: integração do Azure Active Directory ao Cimpl | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Cimpl."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58ee5481-ae40-4e4a-a3c9-86343851fc9a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 24a0c89966c83e1b32367d4519ead98d76f5ac6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cimpl"></a><span data-ttu-id="ac718-103">Tutorial: Integração do Active Directory do Azure com o Cimpl</span><span class="sxs-lookup"><span data-stu-id="ac718-103">Tutorial: Azure Active Directory integration with Cimpl</span></span>

<span data-ttu-id="ac718-104">Neste tutorial, você aprende a integrar o Cimpl ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ac718-104">In this tutorial, you learn how to integrate Cimpl with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ac718-105">A integração do Cimpl ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="ac718-105">Integrating Cimpl with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ac718-106">Controlar no AD do Azure quem terá acesso ao Cimpl</span><span class="sxs-lookup"><span data-stu-id="ac718-106">You can control in Azure AD who has access to Cimpl</span></span>
- <span data-ttu-id="ac718-107">Permitir que seus usuários façam logon automaticamente no Cimpl (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac718-107">You can enable your users to automatically get signed-on to Cimpl (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ac718-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ac718-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ac718-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ac718-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac718-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ac718-110">Prerequisites</span></span>

<span data-ttu-id="ac718-111">Para configurar a integração do AD do Azure ao Cimpl, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ac718-111">To configure Azure AD integration with Cimpl, you need the following items:</span></span>

- <span data-ttu-id="ac718-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ac718-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ac718-113">Uma assinatura habilitada para logon único do Cimpl</span><span class="sxs-lookup"><span data-stu-id="ac718-113">A Cimpl single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ac718-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ac718-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ac718-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ac718-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ac718-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ac718-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ac718-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac718-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ac718-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ac718-118">Scenario description</span></span>
<span data-ttu-id="ac718-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ac718-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ac718-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="ac718-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ac718-121">Adicionar Cimpl a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="ac718-121">Adding Cimpl from the gallery</span></span>
2. <span data-ttu-id="ac718-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ac718-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cimpl-from-the-gallery"></a><span data-ttu-id="ac718-123">Adicionar Cimpl a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="ac718-123">Adding Cimpl from the gallery</span></span>
<span data-ttu-id="ac718-124">Para configurar a integração do Cimpl ao AD do Azure, você precisará adicionar o Cimpl da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ac718-124">To configure the integration of Cimpl into Azure AD, you need to add Cimpl from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ac718-125">**Para adicionar o Cimpl da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ac718-125">**To add Cimpl from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ac718-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ac718-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ac718-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ac718-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ac718-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ac718-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ac718-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ac718-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ac718-133">Na caixa de pesquisa, digite **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="ac718-133">In the search box, type **Cimpl**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_search.png)

5. <span data-ttu-id="ac718-135">No painel de resultados, selecione **Cimpl** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ac718-135">In the results panel, select **Cimpl**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ac718-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ac718-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ac718-138">Nesta seção, você configura e testa o logon único do Azure AD com o Cimpl com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ac718-138">In this section, you configure and test Azure AD single sign-on with Cimpl based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ac718-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Cimpl é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac718-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cimpl is to a user in Azure AD.</span></span> <span data-ttu-id="ac718-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Cimpl.</span><span class="sxs-lookup"><span data-stu-id="ac718-140">In other words, a link relationship between an Azure AD user and the related user in Cimpl needs to be established.</span></span>

<span data-ttu-id="ac718-141">No Cimpl, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="ac718-141">In Cimpl, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ac718-142">Para configurar e testar o logon único do AD do Azure com o Cimpl, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="ac718-142">To configure and test Azure AD single sign-on with Cimpl, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ac718-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ac718-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ac718-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ac718-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ac718-145">**[Como criar de um usuário de teste do Cimpl](#creating-a-cimpl-test-user)** – para ter um equivalente de Brenda Fernandes no Cimpl que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac718-145">**[Creating a Cimpl test user](#creating-a-cimpl-test-user)** - to have a counterpart of Britta Simon in Cimpl that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ac718-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac718-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ac718-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="ac718-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ac718-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac718-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ac718-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Cimpl.</span><span class="sxs-lookup"><span data-stu-id="ac718-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cimpl application.</span></span>

<span data-ttu-id="ac718-150">**Para configurar o logon único do AD do Azure com o Cimpl, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ac718-150">**To configure Azure AD single sign-on with Cimpl, perform the following steps:**</span></span>

1. <span data-ttu-id="ac718-151">No portal do Azure, na página de integração de aplicativos do **Cimpl**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="ac718-151">In the Azure portal, on the **Cimpl** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ac718-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ac718-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_samlbase.png)

3. <span data-ttu-id="ac718-155">Na seção **URLs e Domínio do Cimpl**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ac718-155">On the **Cimpl Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_url.png)

    <span data-ttu-id="ac718-157">a.</span><span class="sxs-lookup"><span data-stu-id="ac718-157">a.</span></span> <span data-ttu-id="ac718-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="ac718-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    <span data-ttu-id="ac718-159">b.</span><span class="sxs-lookup"><span data-stu-id="ac718-159">b.</span></span> <span data-ttu-id="ac718-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="ac718-160">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ac718-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="ac718-161">These values are not real.</span></span> <span data-ttu-id="ac718-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="ac718-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ac718-163">Entre em contato com a equipe do Cimpl pelo telefone **+1 866-982-8250** para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="ac718-163">Contact Cimpl team at **+1 866-982-8250** to get these values.</span></span> 
 
4. <span data-ttu-id="ac718-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ac718-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_certificate.png) 

5. <span data-ttu-id="ac718-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ac718-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cimpl-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ac718-168">Na seção **Configuração do Cimpl**, clique em **Configurar Cimpl** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="ac718-168">On the **Cimpl Configuration** section, click **Configure Cimpl** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ac718-169">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="ac718-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_configure.png) 

7. <span data-ttu-id="ac718-171">Para configurar o logon único no lado do **Cimpl**, é necessário enviar o **Certificado (Base64)** baixado, a **ID da Entidade do SAML e a URL do Serviço de Logon Único do SAML** ao suporte do Cimpl no telefone **+1 866-982-8250**.</span><span class="sxs-lookup"><span data-stu-id="ac718-171">To configure single sign-on on **Cimpl** side, you need to send the downloaded **Certificate (Base64)**, **SAML Entity ID, and SAML Single Sign-On Service URL** to Cimpl support at **+1 866-982-8250**.</span></span>


> [!TIP]
> <span data-ttu-id="ac718-172">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="ac718-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ac718-173">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ac718-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ac718-174">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ac718-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ac718-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ac718-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="ac718-176">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ac718-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ac718-178">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ac718-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ac718-179">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ac718-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cimpl-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ac718-181">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ac718-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cimpl-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ac718-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ac718-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cimpl-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ac718-185">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ac718-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cimpl-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ac718-187">a.</span><span class="sxs-lookup"><span data-stu-id="ac718-187">a.</span></span> <span data-ttu-id="ac718-188">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="ac718-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ac718-189">b.</span><span class="sxs-lookup"><span data-stu-id="ac718-189">b.</span></span> <span data-ttu-id="ac718-190">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ac718-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ac718-191">c.</span><span class="sxs-lookup"><span data-stu-id="ac718-191">c.</span></span> <span data-ttu-id="ac718-192">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="ac718-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ac718-193">d.</span><span class="sxs-lookup"><span data-stu-id="ac718-193">d.</span></span> <span data-ttu-id="ac718-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ac718-194">Click **Create**.</span></span>
 
### <a name="creating-a-cimpl-test-user"></a><span data-ttu-id="ac718-195">Criação de um usuário de teste do Cimpl</span><span class="sxs-lookup"><span data-stu-id="ac718-195">Creating a Cimpl test user</span></span>

<span data-ttu-id="ac718-196">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Cimpl.</span><span class="sxs-lookup"><span data-stu-id="ac718-196">The objective of this section is to create a user called Britta Simon in Cimpl.</span></span> <span data-ttu-id="ac718-197">Trabalhe com o suporte do Cimpl pelo telefone **+1 866-982-8250** para adicionar os usuários à conta do Cimpl.</span><span class="sxs-lookup"><span data-stu-id="ac718-197">Work with Cimpl support at **+1 866-982-8250** to add the users in the Cimpl account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ac718-198">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ac718-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ac718-199">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Cimpl.</span><span class="sxs-lookup"><span data-stu-id="ac718-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cimpl.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ac718-201">**Para atribuir Brenda Fernandes ao Cimpl, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ac718-201">**To assign Britta Simon to Cimpl, perform the following steps:**</span></span>

1. <span data-ttu-id="ac718-202">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ac718-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ac718-204">Na lista de aplicativos, escolha **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="ac718-204">In the applications list, select **Cimpl**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_app.png) 

3. <span data-ttu-id="ac718-206">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ac718-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ac718-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ac718-208">Click **Add** button.</span></span> <span data-ttu-id="ac718-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ac718-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ac718-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ac718-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ac718-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ac718-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ac718-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ac718-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ac718-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ac718-214">Testing single sign-on</span></span>

<span data-ttu-id="ac718-215">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="ac718-215">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  <span data-ttu-id="ac718-216">Ao clicar no bloco do Cimpl no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Cimpl.</span><span class="sxs-lookup"><span data-stu-id="ac718-216">When you click the Cimpl tile in the Access Panel, you should get automatically signed-on to your Cimpl application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ac718-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ac718-217">Additional resources</span></span>

* [<span data-ttu-id="ac718-218">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ac718-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ac718-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ac718-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_203.png

