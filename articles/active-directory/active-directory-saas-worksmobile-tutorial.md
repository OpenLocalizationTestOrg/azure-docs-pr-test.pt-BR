---
title: "Tutorial: Integração do Azure Active Directory com o WORKS MOBILE | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o WORKS MOBILE."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 139a1968a59424eae278de3e7fa227ad340a1eb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="8e0f7-103">Tutorial: Integração do Azure Active Directory com o WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="8e0f7-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="8e0f7-104">Neste tutorial, você aprenderá a integrar o WORKS MOBILE ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8e0f7-104">In this tutorial, you learn how to integrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e0f7-105">A integração do WORKS MOBILE ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="8e0f7-105">Integrating WORKS MOBILE with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8e0f7-106">Você pode controlar no Azure AD quem tem acesso ao WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="8e0f7-106">You can control in Azure AD who has access to WORKS MOBILE</span></span>
- <span data-ttu-id="8e0f7-107">Você pode permitir que seus usuários façam logon automaticamente no WORKS MOBILE (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e0f7-107">You can enable your users to automatically get signed-on to WORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e0f7-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8e0f7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8e0f7-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e0f7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e0f7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8e0f7-110">Prerequisites</span></span>

<span data-ttu-id="8e0f7-111">Para configurar a integração do Azure AD ao WORKS MOBILE, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8e0f7-111">To configure Azure AD integration with WORKS MOBILE, you need the following items:</span></span>

- <span data-ttu-id="8e0f7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8e0f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e0f7-113">Uma assinatura do WORKS MOBILE com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="8e0f7-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e0f7-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e0f7-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8e0f7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e0f7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e0f7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e0f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e0f7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8e0f7-118">Scenario description</span></span>
<span data-ttu-id="8e0f7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e0f7-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="8e0f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e0f7-121">Adicionar o WORKS MOBILE a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="8e0f7-121">Adding WORKS MOBILE from the gallery</span></span>
2. <span data-ttu-id="8e0f7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8e0f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-the-gallery"></a><span data-ttu-id="8e0f7-123">Adicionar o WORKS MOBILE a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="8e0f7-123">Adding WORKS MOBILE from the gallery</span></span>
<span data-ttu-id="8e0f7-124">Para configurar a integração do WORKS MOBILE ao Azure AD, você precisa adicionar o WORKS MOBILE a partir da galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-124">To configure the integration of WORKS MOBILE into Azure AD, you need to add WORKS MOBILE from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8e0f7-125">**Para adicionar o WORKS MOBILE a partir da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8e0f7-125">**To add WORKS MOBILE from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8e0f7-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e0f7-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8e0f7-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8e0f7-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8e0f7-133">Na caixa de pesquisa, digite **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-133">In the search box, type **WORKS MOBILE**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="8e0f7-135">No painel de resultados, selecione **WORKS MOBILE** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-135">In the results panel, select **WORKS MOBILE**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e0f7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8e0f7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e0f7-138">Nesta seção, você configurará e testará o logon único do Azure AD com o WORKS MOBILE, com base em uma usuária de teste chamada “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8e0f7-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do WORKS MOBILE é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in WORKS MOBILE is to a user in Azure AD.</span></span> <span data-ttu-id="8e0f7-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-140">In other words, a link relationship between an Azure AD user and the related user in WORKS MOBILE needs to be established.</span></span>

<span data-ttu-id="8e0f7-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no AD do Azure ao valor do **Nome de Usuário** no WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="8e0f7-142">Para configurar e testar o logon único do Azure AD com o WORKS MOBILE, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="8e0f7-142">To configure and test Azure AD single sign-on with WORKS MOBILE, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8e0f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8e0f7-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e0f7-145">**[Criação de um usuário de teste do WORKS MOBILE](#creating-a-works-mobile-test-user)**: para ter um equivalente de Brenda Fernandes no WORKS MOBILE que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in WORKS MOBILE that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e0f7-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e0f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e0f7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e0f7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e0f7-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="8e0f7-150">**Para configurar o logon único do Azure AD com o WORKS MOBILE, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8e0f7-150">**To configure Azure AD single sign-on with WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="8e0f7-151">No Portal do Azure, na página de integração de aplicativos do **WORKS MOBILE**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-151">In the Azure portal, on the **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8e0f7-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="8e0f7-155">Na seção **URLs e Domínio do WORKS MOBILE**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8e0f7-155">On the **WORKS MOBILE Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="8e0f7-157">a.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-157">a.</span></span> <span data-ttu-id="8e0f7-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="8e0f7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="8e0f7-159">b.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-159">b.</span></span> <span data-ttu-id="8e0f7-160">Na caixa de texto **Identificador**, digite o valor como `worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="8e0f7-160">In the **Identifier** textbox, type the value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8e0f7-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-161">This value is not real.</span></span> <span data-ttu-id="8e0f7-162">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="8e0f7-163">Entre em contato com a [equipe de suporte ao cliente do WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) to get this value.</span></span> 
 
4. <span data-ttu-id="8e0f7-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Bruto)** e, em seguida, salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="8e0f7-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8e0f7-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e0f7-168">Na seção **Configuração do WORKS MOBILE**, clique em **Configurar WORKS MOBILE** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-168">On the **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8e0f7-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="8e0f7-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="8e0f7-171">Para que o SSO seja configurado para seu aplicativo, entre em contato com a [equipe de suporte do WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) e forneça as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="8e0f7-171">To get SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with the following information:</span></span> 

    <span data-ttu-id="8e0f7-172">• O **Arquivo de certificado** baixado</span><span class="sxs-lookup"><span data-stu-id="8e0f7-172">• The downloaded **Certificate file**</span></span>

    <span data-ttu-id="8e0f7-173">• A **URL do Serviço de Logon Único SAML**</span><span class="sxs-lookup"><span data-stu-id="8e0f7-173">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="8e0f7-174">• A **ID da entidade SAML**</span><span class="sxs-lookup"><span data-stu-id="8e0f7-174">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="8e0f7-175">• A **URL de Saída**</span><span class="sxs-lookup"><span data-stu-id="8e0f7-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="8e0f7-176">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="8e0f7-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8e0f7-177">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8e0f7-178">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e0f7-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e0f7-179">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8e0f7-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e0f7-180">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8e0f7-182">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8e0f7-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8e0f7-183">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e0f7-185">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e0f7-187">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e0f7-189">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8e0f7-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e0f7-191">a.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-191">a.</span></span> <span data-ttu-id="8e0f7-192">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e0f7-193">b.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-193">b.</span></span> <span data-ttu-id="8e0f7-194">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e0f7-195">c.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-195">c.</span></span> <span data-ttu-id="8e0f7-196">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8e0f7-197">d.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-197">d.</span></span> <span data-ttu-id="8e0f7-198">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="8e0f7-199">Criar um usuário de teste do WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="8e0f7-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="8e0f7-200">Nesta seção, você criará uma usuária chamada Britta Simon no WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="8e0f7-201">Trabalhe com a [equipe de suporte do WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) para adicionar usuários à plataforma WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the WORKS MOBILE platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8e0f7-202">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8e0f7-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8e0f7-203">Nesta seção, você habilitará a Brenda Fernandes a usar o logon único do Azure através da concessão de acesso ao WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to WORKS MOBILE.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8e0f7-205">**Para atribuir Britta Simon ao WORKS MOBILE, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8e0f7-205">**To assign Britta Simon to WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="8e0f7-206">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8e0f7-208">Na lista de aplicativos, selecione **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-208">In the applications list, select **WORKS MOBILE**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="8e0f7-210">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8e0f7-212">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-212">Click **Add** button.</span></span> <span data-ttu-id="8e0f7-213">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8e0f7-215">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8e0f7-216">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e0f7-217">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e0f7-218">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8e0f7-218">Testing single sign-on</span></span>

<span data-ttu-id="8e0f7-219">Nesta seção, você testará sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8e0f7-220">Ao clicar no bloco WORKS MOBILE no Painel de Acesso, você será automaticamente conectado ao seu aplicativo WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="8e0f7-220">When you click the WORKS MOBILE tile in the Access Panel, you should get automatically signed-on to your WORKS MOBILE application.</span></span>
<span data-ttu-id="8e0f7-221">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8e0f7-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8e0f7-222">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8e0f7-222">Additional resources</span></span>

* [<span data-ttu-id="8e0f7-223">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8e0f7-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e0f7-224">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e0f7-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

