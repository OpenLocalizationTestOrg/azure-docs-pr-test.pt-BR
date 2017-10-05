---
title: "Tutorial: Integração do Azure Active Directory ao Trakstar | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Trakstar."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411cb8c3-95c6-4138-acf2-ffc7f663e89a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 757429aa187e6536489b6636a0a11d122c7f9378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakstar"></a><span data-ttu-id="4c61f-103">Tutorial: Integração do Azure Active Directory ao Trakstar</span><span class="sxs-lookup"><span data-stu-id="4c61f-103">Tutorial: Azure Active Directory integration with Trakstar</span></span>

<span data-ttu-id="4c61f-104">Neste tutorial, você aprenderá a integrar o Trakstar ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4c61f-104">In this tutorial, you learn how to integrate Trakstar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c61f-105">A integração do Trakstar ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4c61f-105">Integrating Trakstar with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c61f-106">No AD do Azure, é possível controlar quem tem acesso ao Trakstar</span><span class="sxs-lookup"><span data-stu-id="4c61f-106">You can control in Azure AD who has access to Trakstar</span></span>
- <span data-ttu-id="4c61f-107">Você pode permitir que os usuários façam logon automaticamente no Trakstar (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c61f-107">You can enable your users to automatically get signed-on to Trakstar (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c61f-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4c61f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4c61f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c61f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c61f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4c61f-110">Prerequisites</span></span>

<span data-ttu-id="4c61f-111">Para configurar a integração do AD do Azure ao Trakstar, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4c61f-111">To configure Azure AD integration with Trakstar, you need the following items:</span></span>

- <span data-ttu-id="4c61f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c61f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c61f-113">Uma assinatura habilitada para logon único do Trakstar</span><span class="sxs-lookup"><span data-stu-id="4c61f-113">A Trakstar single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c61f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4c61f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c61f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4c61f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c61f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4c61f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c61f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c61f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c61f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4c61f-118">Scenario description</span></span>
<span data-ttu-id="4c61f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4c61f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c61f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4c61f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c61f-121">Adicionando o Trakstar da galeria</span><span class="sxs-lookup"><span data-stu-id="4c61f-121">Adding Trakstar from the gallery</span></span>
2. <span data-ttu-id="4c61f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c61f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakstar-from-the-gallery"></a><span data-ttu-id="4c61f-123">Adicionando o Trakstar da galeria</span><span class="sxs-lookup"><span data-stu-id="4c61f-123">Adding Trakstar from the gallery</span></span>
<span data-ttu-id="4c61f-124">Para configurar a integração do Trakstar ao AD do Azure, você precisará adicionar o Trakstar da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4c61f-124">To configure the integration of Trakstar into Azure AD, you need to add Trakstar from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c61f-125">**Para adicionar o Trakstar da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c61f-125">**To add Trakstar from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c61f-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c61f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c61f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4c61f-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4c61f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4c61f-133">Na caixa de pesquisa, digite **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-133">In the search box, type **Trakstar**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_search.png)

5. <span data-ttu-id="4c61f-135">No painel de resultados, selecione **Trakstar** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4c61f-135">In the results panel, select **Trakstar**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c61f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c61f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c61f-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Trakstar, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="4c61f-138">In this section, you configure and test Azure AD single sign-on with Trakstar based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4c61f-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Trakstar é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c61f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakstar is to a user in Azure AD.</span></span> <span data-ttu-id="4c61f-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do AD do Azure e o usuário relacionado no Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4c61f-140">In other words, a link relationship between an Azure AD user and the related user in Trakstar needs to be established.</span></span>

<span data-ttu-id="4c61f-141">No Trakstar, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="4c61f-141">In Trakstar, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4c61f-142">Para configurar e testar o logon único do AD do Azure com o Trakstar, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4c61f-142">To configure and test Azure AD single sign-on with Trakstar, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c61f-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4c61f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4c61f-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4c61f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c61f-145">**[Criando um usuário de teste do Trakstar](#creating-a-trakstar-test-user)** – para ter um equivalente de Brenda Fernandes no Trakstar que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c61f-145">**[Creating a Trakstar test user](#creating-a-trakstar-test-user)** - to have a counterpart of Britta Simon in Trakstar that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c61f-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c61f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c61f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4c61f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c61f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c61f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c61f-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4c61f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trakstar application.</span></span>

<span data-ttu-id="4c61f-150">**Para configurar o logon único do AD do Azure com o Trakstar, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c61f-150">**To configure Azure AD single sign-on with Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="4c61f-151">No Portal do Azure, na página de integração de aplicativos do **Trakstar**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-151">In the Azure portal, on the **Trakstar** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4c61f-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4c61f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_samlbase.png)

3. <span data-ttu-id="4c61f-155">Na seção **Domínio e URLs do Trakstar**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4c61f-155">On the **Trakstar Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_url.png)

    <span data-ttu-id="4c61f-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c61f-157">a.</span></span> <span data-ttu-id="4c61f-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`</span><span class="sxs-lookup"><span data-stu-id="4c61f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`</span></span>

    <span data-ttu-id="4c61f-159">b.</span><span class="sxs-lookup"><span data-stu-id="4c61f-159">b.</span></span> <span data-ttu-id="4c61f-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.trakstar.com`</span><span class="sxs-lookup"><span data-stu-id="4c61f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.trakstar.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c61f-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4c61f-161">These values are not real.</span></span> <span data-ttu-id="4c61f-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="4c61f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4c61f-163">Entre em contato com a [equipe de suporte ao cliente do Trakstar](mailto:integrations@trakstar.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="4c61f-163">Contact [Trakstar Client support team](mailto:integrations@trakstar.com) to get these values.</span></span> 
 
4. <span data-ttu-id="4c61f-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4c61f-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_certificate.png) 

5. <span data-ttu-id="4c61f-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4c61f-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakstar-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c61f-168">Na seção **Configuração do Trakstar**, clique em **Configurar Trakstar** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-168">On the **Trakstar Configuration** section, click **Configure Trakstar** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4c61f-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="4c61f-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_configure.png) 

7. <span data-ttu-id="4c61f-171">Para configurar o logon único no lado do **Trakstar**, é necessário enviar o **Certificado (Base64)** baixado, a **URL de Saída, ID da Entidade SAML e URL do Serviço de Logon Único SAML** para a [equipe de suporte do Trakstar](mailto:integrations@trakstar.com).</span><span class="sxs-lookup"><span data-stu-id="4c61f-171">To configure single sign-on on **Trakstar** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Trakstar support team](mailto:integrations@trakstar.com).</span></span> 

> [!TIP]
> <span data-ttu-id="4c61f-172">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4c61f-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4c61f-173">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4c61f-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4c61f-174">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4c61f-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c61f-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c61f-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c61f-176">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4c61f-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4c61f-178">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c61f-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c61f-179">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakstar-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c61f-181">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4c61f-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakstar-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c61f-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c61f-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakstar-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c61f-185">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4c61f-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakstar-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c61f-187">a.</span><span class="sxs-lookup"><span data-stu-id="4c61f-187">a.</span></span> <span data-ttu-id="4c61f-188">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c61f-189">b.</span><span class="sxs-lookup"><span data-stu-id="4c61f-189">b.</span></span> <span data-ttu-id="4c61f-190">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4c61f-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c61f-191">c.</span><span class="sxs-lookup"><span data-stu-id="4c61f-191">c.</span></span> <span data-ttu-id="4c61f-192">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4c61f-193">d.</span><span class="sxs-lookup"><span data-stu-id="4c61f-193">d.</span></span> <span data-ttu-id="4c61f-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-194">Click **Create**.</span></span>
 
### <a name="creating-a-trakstar-test-user"></a><span data-ttu-id="4c61f-195">Criando um usuário de teste do Trakstar</span><span class="sxs-lookup"><span data-stu-id="4c61f-195">Creating a Trakstar test user</span></span>

<span data-ttu-id="4c61f-196">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4c61f-196">The objective of this section is to create a user called Britta Simon in Trakstar.</span></span> <span data-ttu-id="4c61f-197">Trabalhe com a [equipe de suporte do Trakstar](mailto:integrations@trakstar.com) para adicionar usuários na conta do Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4c61f-197">Work with [Trakstar support team](mailto:integrations@trakstar.com) to add the users in the Trakstar account.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4c61f-198">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c61f-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4c61f-199">Nesta seção, você habilitará a Brenda Fernandes a usar o logon único do Azure através da concessão de acesso ao Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4c61f-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trakstar.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4c61f-201">**Para atribuir Brenda Fernandes ao Trakstar, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c61f-201">**To assign Britta Simon to Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="4c61f-202">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4c61f-204">Na lista de aplicativos, selecione **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-204">In the applications list, select **Trakstar**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_app.png) 

3. <span data-ttu-id="4c61f-206">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4c61f-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4c61f-208">Click **Add** button.</span></span> <span data-ttu-id="4c61f-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c61f-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4c61f-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4c61f-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4c61f-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c61f-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c61f-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c61f-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c61f-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4c61f-214">Testing single sign-on</span></span>

<span data-ttu-id="4c61f-215">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4c61f-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="4c61f-216">Ao clicar no bloco do Trakstar no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4c61f-216">When you click the Trakstar tile in the Access Panel, you should get automatically signed-on to your Trakstar application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4c61f-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4c61f-217">Additional resources</span></span>

* [<span data-ttu-id="4c61f-218">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4c61f-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c61f-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c61f-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_203.png

