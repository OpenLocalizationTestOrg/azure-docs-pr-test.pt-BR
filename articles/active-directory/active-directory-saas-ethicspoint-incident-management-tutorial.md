---
title: "Tutorial: integração do Azure Active Directory ao EthicsPoint Incident Management (EPIM) | Microsoft Azure"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o EthicsPoint Incident Management (EPIM)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: b5ac3afd973b5765ba151e766754934b49ac0e0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="e287a-103">Tutorial: integração do Azure Active Directory ao EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="e287a-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="e287a-104">Neste tutorial, você aprenderá a integrar o EthicsPoint Incident Management (EPIM) ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e287a-104">In this tutorial, you learn how to integrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e287a-105">A integração do EthicsPoint Incident Management (EPIM) ao Azure AD fornece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e287a-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e287a-106">Você pode controlar no Azure AD, quem tem acesso ao EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="e287a-106">You can control in Azure AD who has access to EthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="e287a-107">Você pode permitir que seus usuários façam logon automaticamente no EthicsPoint Incident Management (EPIM) (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="e287a-107">You can enable your users to automatically get signed-on to EthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e287a-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e287a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e287a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e287a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e287a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e287a-110">Prerequisites</span></span>

<span data-ttu-id="e287a-111">Para configurar a integração do Azure AD com o EthicsPoint Incident Management (EPIM), você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e287a-111">To configure Azure AD integration with EthicsPoint Incident Management (EPIM), you need the following items:</span></span>

- <span data-ttu-id="e287a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e287a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e287a-113">Uma assinatura habilitada para logon único do EPIM (EthicsPoint Incident Management)</span><span class="sxs-lookup"><span data-stu-id="e287a-113">A EthicsPoint Incident Management (EPIM) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e287a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e287a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e287a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e287a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e287a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e287a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e287a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e287a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e287a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e287a-118">Scenario description</span></span>
<span data-ttu-id="e287a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e287a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e287a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e287a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e287a-121">Adicionar o EthicsPoint Incident Management (EPIM) da galeria</span><span class="sxs-lookup"><span data-stu-id="e287a-121">Adding EthicsPoint Incident Management (EPIM) from the gallery</span></span>
2. <span data-ttu-id="e287a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e287a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ethicspoint-incident-management-epim-from-the-gallery"></a><span data-ttu-id="e287a-123">Adicionar o EthicsPoint Incident Management (EPIM) da galeria</span><span class="sxs-lookup"><span data-stu-id="e287a-123">Adding EthicsPoint Incident Management (EPIM) from the gallery</span></span>
<span data-ttu-id="e287a-124">Para configurar a integração do EthicsPoint Incident Management (EPIM) ao Azure AD, você precisa adicionar o EthicsPoint Incident Management (EPIM) da galeria à lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e287a-124">To configure the integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need to add EthicsPoint Incident Management (EPIM) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e287a-125">**Para adicionar o EthicsPoint Incident Management (EPIM) da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e287a-125">**To add EthicsPoint Incident Management (EPIM) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e287a-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e287a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e287a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e287a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e287a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e287a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e287a-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e287a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e287a-133">Na caixa de pesquisa, digite **EPIM (EthicsPoint Incident Management)**.</span><span class="sxs-lookup"><span data-stu-id="e287a-133">In the search box, type **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

5. <span data-ttu-id="e287a-135">No painel de resultados, selecione **EPIM (EthicsPoint Incident Management)** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e287a-135">In the results panel, select **EthicsPoint Incident Management (EPIM)**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e287a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e287a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e287a-138">Nesta seção, você configura e testa o logon único do Azure AD com o EPIM (EthicsPoint Incident Management), com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e287a-138">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e287a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do EthicsPoint Incident Management (EPIM) é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e287a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EthicsPoint Incident Management (EPIM) is to a user in Azure AD.</span></span> <span data-ttu-id="e287a-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="e287a-140">In other words, a link relationship between an Azure AD user and the related user in EthicsPoint Incident Management (EPIM) needs to be established.</span></span>

<span data-ttu-id="e287a-141">No EPIM (EthicsPoint Incident Management), atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="e287a-141">In EthicsPoint Incident Management (EPIM), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e287a-142">Para configurar e testar o logon único do Azure AD com o EthicsPoint Incident Management (EPIM), você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e287a-142">To configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e287a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e287a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e287a-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e287a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e287a-145">**[Criando um usuário de teste do EPIM (EthicsPoint Incident Management)](#creating-a-ethicspoint-incident-management-epim-test-user)** – para ter um equivalente de Brenda Fernandes no EPIM (EthicsPoint Incident Management) que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e287a-145">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-epim-test-user)** - to have a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e287a-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e287a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e287a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e287a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e287a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e287a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e287a-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo EPIM (EthicsPoint Incident Management).</span><span class="sxs-lookup"><span data-stu-id="e287a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>

<span data-ttu-id="e287a-150">**Para configurar o logon único do Azure AD com o EthicsPoint Incident Management (EPIM), execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e287a-150">**To configure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform the following steps:**</span></span>

1. <span data-ttu-id="e287a-151">No portal do Azure, na página de integração do aplicativo **EPIM (EthicsPoint Incident Management)**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e287a-151">In the Azure portal, on the **EthicsPoint Incident Management (EPIM)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e287a-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e287a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

3. <span data-ttu-id="e287a-155">Na seção **Domínio e URLs do EPIM (EthicsPoint Incident Management)**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e287a-155">On the **EthicsPoint Incident Management (EPIM) Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    <span data-ttu-id="e287a-157">a.</span><span class="sxs-lookup"><span data-stu-id="e287a-157">a.</span></span> <span data-ttu-id="e287a-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="e287a-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    <span data-ttu-id="e287a-159">b.</span><span class="sxs-lookup"><span data-stu-id="e287a-159">b.</span></span> <span data-ttu-id="e287a-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.navexglobal.com/adfs/services/trust`</span><span class="sxs-lookup"><span data-stu-id="e287a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.navexglobal.com/adfs/services/trust`</span></span>

    <span data-ttu-id="e287a-161">c.</span><span class="sxs-lookup"><span data-stu-id="e287a-161">c.</span></span> <span data-ttu-id="e287a-162">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<servername>.navexglobal.com/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="e287a-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e287a-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e287a-163">These values are not real.</span></span> <span data-ttu-id="e287a-164">Atualize esses valores com a URL de Resposta, o Identificador e a URL de Logon reais.</span><span class="sxs-lookup"><span data-stu-id="e287a-164">Update these values with the actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="e287a-165">Contate a [equipe de suporte ao Cliente do EPIM (EthicsPoint Incident Management)](http://www.navexglobal.com/company/contact-us) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="e287a-165">Contact [EthicsPoint Incident Management (EPIM) Client support team](http://www.navexglobal.com/company/contact-us) to get these values.</span></span> 

4. <span data-ttu-id="e287a-166">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e287a-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

5. <span data-ttu-id="e287a-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e287a-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="e287a-170">Para configurar o logon único no lado do **EPIM (EthicsPoint Incident Management)**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do EPIM (EthicsPoint Incident Management)](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="e287a-170">To configure single sign-on on **EthicsPoint Incident Management (EPIM)** side, you need to send the downloaded **Metadata XML** to [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="e287a-171">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="e287a-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e287a-172">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e287a-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e287a-173">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e287a-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e287a-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e287a-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="e287a-175">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e287a-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e287a-177">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e287a-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e287a-178">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e287a-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e287a-180">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e287a-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e287a-182">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e287a-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e287a-184">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e287a-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e287a-186">a.</span><span class="sxs-lookup"><span data-stu-id="e287a-186">a.</span></span> <span data-ttu-id="e287a-187">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e287a-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e287a-188">b.</span><span class="sxs-lookup"><span data-stu-id="e287a-188">b.</span></span> <span data-ttu-id="e287a-189">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e287a-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e287a-190">c.</span><span class="sxs-lookup"><span data-stu-id="e287a-190">c.</span></span> <span data-ttu-id="e287a-191">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="e287a-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e287a-192">d.</span><span class="sxs-lookup"><span data-stu-id="e287a-192">d.</span></span> <span data-ttu-id="e287a-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e287a-193">Click **Create**.</span></span>
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="e287a-194">Criando um usuário de teste do EPIM (EthicsPoint Incident Management)</span><span class="sxs-lookup"><span data-stu-id="e287a-194">Creating a EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="e287a-195">Nesta seção, você deve criar uma usuária chamada Brenda Fernandes no EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="e287a-195">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="e287a-196">Trabalhe com a [equipe de suporte do EPIM (EthicsPoint Incident Management)](http://www.navexglobal.com/company/contact-us) para adicionar os usuários à plataforma EPIM (EthicsPoint Incident Management).</span><span class="sxs-lookup"><span data-stu-id="e287a-196">Please work with [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us) to add the users in the EthicsPoint Incident Management (EPIM) platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e287a-197">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e287a-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e287a-198">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao EPIM (EthicsPoint Incident Management).</span><span class="sxs-lookup"><span data-stu-id="e287a-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EthicsPoint Incident Management (EPIM).</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e287a-200">**Para adicionar Brenda Fernandes ao EthicsPoint Incident Management (EPIM), execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e287a-200">**To assign Britta Simon to EthicsPoint Incident Management (EPIM), perform the following steps:**</span></span>

1. <span data-ttu-id="e287a-201">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e287a-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e287a-203">Na lista de aplicativos, selecione **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="e287a-203">In the applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

3. <span data-ttu-id="e287a-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e287a-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e287a-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e287a-207">Click **Add** button.</span></span> <span data-ttu-id="e287a-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e287a-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e287a-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e287a-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e287a-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e287a-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e287a-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e287a-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e287a-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e287a-213">Testing single sign-on</span></span>

<span data-ttu-id="e287a-214">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e287a-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="e287a-215">Ao clicar no bloco EthicsPoint Incident Management (EPIM) no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="e287a-215">When you click the EthicsPoint Incident Management (EPIM) tile in the Access Panel, you should get automatically signed-on to your EthicsPoint Incident Management (EPIM) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e287a-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e287a-216">Additional resources</span></span>

* [<span data-ttu-id="e287a-217">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e287a-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e287a-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e287a-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png

