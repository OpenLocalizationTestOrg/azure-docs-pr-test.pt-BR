---
title: "Tutorial: Integração do Azure Active Directory com o Nomadesk | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Nomadesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d261b776-b48e-45f0-9722-0297adefabb8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 1d652d562f4c5caffded18d928e2395e537f59f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadesk"></a><span data-ttu-id="6d9d9-103">Tutorial: Integração do Active Directory do Azure com o Nomadesk</span><span class="sxs-lookup"><span data-stu-id="6d9d9-103">Tutorial: Azure Active Directory integration with Nomadesk</span></span>

<span data-ttu-id="6d9d9-104">Neste tutorial, você aprenderá a integrar o Nomadesk ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6d9d9-104">In this tutorial, you learn how to integrate Nomadesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d9d9-105">A integração do Nomadesk ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="6d9d9-105">Integrating Nomadesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6d9d9-106">No AD do Azure, você pode controlar quem tem acesso ao Nomadesk</span><span class="sxs-lookup"><span data-stu-id="6d9d9-106">You can control in Azure AD who has access to Nomadesk</span></span>
- <span data-ttu-id="6d9d9-107">Você pode permitir que os usuários façam logon automaticamente no Nomadesk (Logon Único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d9d9-107">You can enable your users to automatically get signed-on to Nomadesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6d9d9-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6d9d9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6d9d9-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d9d9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d9d9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6d9d9-110">Prerequisites</span></span>

<span data-ttu-id="6d9d9-111">Para configurar a integração do AD do Azure com o Nomadesk, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6d9d9-111">To configure Azure AD integration with Nomadesk, you need the following items:</span></span>

- <span data-ttu-id="6d9d9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d9d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d9d9-113">Uma assinatura habilitada para logon único do Nomadesk</span><span class="sxs-lookup"><span data-stu-id="6d9d9-113">A Nomadesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6d9d9-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d9d9-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6d9d9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d9d9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d9d9-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d9d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d9d9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6d9d9-118">Scenario description</span></span>
<span data-ttu-id="6d9d9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d9d9-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="6d9d9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d9d9-121">Adicionando o Nomadesk por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="6d9d9-121">Adding Nomadesk from the gallery</span></span>
2. <span data-ttu-id="6d9d9-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d9d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nomadesk-from-the-gallery"></a><span data-ttu-id="6d9d9-123">Adicionando o Nomadesk por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="6d9d9-123">Adding Nomadesk from the gallery</span></span>
<span data-ttu-id="6d9d9-124">Para configurar a integração do Nomadesk ao AD do Azure, você precisa adicionar o Nomadesk por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-124">To configure the integration of Nomadesk into Azure AD, you need to add Nomadesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6d9d9-125">**Para adicionar o Nomadesk por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6d9d9-125">**To add Nomadesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6d9d9-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6d9d9-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6d9d9-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="6d9d9-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="6d9d9-133">Na caixa de pesquisa, digite **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-133">In the search box, type **Nomadesk**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_search.png)

5. <span data-ttu-id="6d9d9-135">No painel de resultados, selecione **Nomadesk** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-135">In the results panel, select **Nomadesk**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6d9d9-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d9d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6d9d9-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Nomadesk, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-138">In this section, you configure and test Azure AD single sign-on with Nomadesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6d9d9-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Nomadesk é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadesk is to a user in Azure AD.</span></span> <span data-ttu-id="6d9d9-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado no Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-140">In other words, a link relationship between an Azure AD user and the related user in Nomadesk needs to be established.</span></span>

<span data-ttu-id="6d9d9-141">No Nomadesk, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-141">In Nomadesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6d9d9-142">Para configurar e testar o logon único do AD do Azure com o Nomadesk, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="6d9d9-142">To configure and test Azure AD single sign-on with Nomadesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6d9d9-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6d9d9-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d9d9-145">**[Criar um usuário de teste do Nomadesk](#creating-a-nomadesk-test-user)** – para ter um equivalente de Brenda Fernandes no Nomadesk vinculado à representação desse usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-145">**[Creating a Nomadesk test user](#creating-a-nomadesk-test-user)** - to have a counterpart of Britta Simon in Nomadesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6d9d9-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d9d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6d9d9-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d9d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6d9d9-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadesk application.</span></span>

<span data-ttu-id="6d9d9-150">**Para configurar o logon único do AD do Azure com o Nomadesk, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6d9d9-150">**To configure Azure AD single sign-on with Nomadesk, perform the following steps:**</span></span>

1. <span data-ttu-id="6d9d9-151">No Portal do Azure, na página de integração de aplicativos do **Nomadesk**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-151">In the Azure portal, on the **Nomadesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="6d9d9-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_samlbase.png)

3. <span data-ttu-id="6d9d9-155">Na seção **URLs e Domínio do Nomadesk**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6d9d9-155">On the **Nomadesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_url.png)

    <span data-ttu-id="6d9d9-157">a.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-157">a.</span></span> <span data-ttu-id="6d9d9-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://mynomadesk.com/logon/saml/<TENANTID>`</span><span class="sxs-lookup"><span data-stu-id="6d9d9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mynomadesk.com/logon/saml/<TENANTID>`</span></span>

    <span data-ttu-id="6d9d9-159">b.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-159">b.</span></span> <span data-ttu-id="6d9d9-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://secure.nomadesk.com/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="6d9d9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://secure.nomadesk.com/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6d9d9-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-161">These values are not real.</span></span> <span data-ttu-id="6d9d9-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="6d9d9-163">Contate a [equipe de suporte do Cliente Nomadesk](mailto:support@nomadesk.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-163">Contact [Nomadesk Client support team](mailto:support@nomadesk.com) to get these values.</span></span> 
 
4. <span data-ttu-id="6d9d9-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_certificate.png) 

5. <span data-ttu-id="6d9d9-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6d9d9-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nomadesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6d9d9-168">Na seção **Configuração do Nomadesk**, clique em **Configurar o Nomadesk** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-168">On the **Nomadesk Configuration** section, click **Configure Nomadesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6d9d9-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="6d9d9-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_configure.png) 

7. <span data-ttu-id="6d9d9-171">Para configurar o logon único no lado do **Nomadesk**, é necessário enviar o **Certificado** baixado, a **URL de Saída, ID da Entidade SAML e URL do Serviço de Logon Único SAML** para a [equipe de suporte do Nomadesk](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="6d9d9-171">To configure single sign-on on **Nomadesk** side, you need to send the downloaded **Certificate**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Nomadesk support team](mailto:support@nomadesk.com).</span></span> <span data-ttu-id="6d9d9-172">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6d9d9-173">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="6d9d9-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6d9d9-174">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6d9d9-175">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6d9d9-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6d9d9-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d9d9-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="6d9d9-177">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="6d9d9-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6d9d9-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6d9d9-180">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6d9d9-182">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6d9d9-184">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6d9d9-186">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6d9d9-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6d9d9-188">a.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-188">a.</span></span> <span data-ttu-id="6d9d9-189">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d9d9-190">b.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-190">b.</span></span> <span data-ttu-id="6d9d9-191">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6d9d9-192">c.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-192">c.</span></span> <span data-ttu-id="6d9d9-193">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6d9d9-194">d.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-194">d.</span></span> <span data-ttu-id="6d9d9-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-195">Click **Create**.</span></span>
 
### <a name="creating-a-nomadesk-test-user"></a><span data-ttu-id="6d9d9-196">Criar um usuário de teste do Nomadesk</span><span class="sxs-lookup"><span data-stu-id="6d9d9-196">Creating a Nomadesk test user</span></span>

<span data-ttu-id="6d9d9-197">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-197">The objective of this section is to create a user called Britta Simon in Nomadesk.</span></span> <span data-ttu-id="6d9d9-198">O Nomadesk dá suporte ao provisionamento just-in-time, que é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-198">Nomadesk supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="6d9d9-199">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-199">There is no action item for you in this section.</span></span> <span data-ttu-id="6d9d9-200">Um novo usuário será criado durante uma tentativa de acessar o Nomadesk, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-200">A new user is created during an attempt to access Nomadesk if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="6d9d9-201">Se precisar criar um usuário manualmente, entre em contato com a [equipe de suporte do Nomadesk](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="6d9d9-201">If you need to create a user manually, you need to contact the [Nomadesk support team](mailto:support@nomadesk.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6d9d9-202">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d9d9-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6d9d9-203">Nesta seção, você concederá a Brenda Fernandes acesso ao Nomadesk para que ela fique habilitada a usar o logon único do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadesk.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="6d9d9-205">**Para atribuir Brenda Fernandes ao Nomadesk, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6d9d9-205">**To assign Britta Simon to Nomadesk, perform the following steps:**</span></span>

1. <span data-ttu-id="6d9d9-206">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="6d9d9-208">Na lista de aplicativos, selecione **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-208">In the applications list, select **Nomadesk**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_app.png) 

3. <span data-ttu-id="6d9d9-210">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="6d9d9-212">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-212">Click **Add** button.</span></span> <span data-ttu-id="6d9d9-213">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="6d9d9-215">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6d9d9-216">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d9d9-217">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6d9d9-218">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="6d9d9-218">Testing single sign-on</span></span>

<span data-ttu-id="6d9d9-219">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6d9d9-220">Quando você clicar no bloco Nomadesk no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="6d9d9-220">When you click the Nomadesk tile in the Access Panel,  you should get automatically signed-on to your Nomadesk application.</span></span>
<span data-ttu-id="6d9d9-221">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6d9d9-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6d9d9-222">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6d9d9-222">Additional resources</span></span>

* [<span data-ttu-id="6d9d9-223">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6d9d9-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d9d9-224">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6d9d9-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_203.png

