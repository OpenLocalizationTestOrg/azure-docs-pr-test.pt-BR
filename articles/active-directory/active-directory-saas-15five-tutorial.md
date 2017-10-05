---
title: "Tutorial: Integração do Azure Active Directory ao 15Five | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o 15Five."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: ea36774747a0fcfa4ace1aefb2d46dba815d92c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="e5aa8-103">Tutorial: Integração do Active Directory do Azure ao 15Five</span><span class="sxs-lookup"><span data-stu-id="e5aa8-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="e5aa8-104">Neste tutorial, você aprenderá a integrar o 15Five ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e5aa8-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e5aa8-105">A integração do 15Five ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e5aa8-105">Integrating 15Five with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e5aa8-106">Você pode controlar no Azure AD quem terá acesso ao 15Five</span><span class="sxs-lookup"><span data-stu-id="e5aa8-106">You can control in Azure AD who has access to 15Five</span></span>
- <span data-ttu-id="e5aa8-107">Você pode permitir que usuários façam logon automaticamente no 15Five (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5aa8-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e5aa8-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e5aa8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e5aa8-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e5aa8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5aa8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e5aa8-110">Prerequisites</span></span>

<span data-ttu-id="e5aa8-111">Para configurar a integração do Azure AD com 15Five, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e5aa8-111">To configure Azure AD integration with 15Five, you need the following items:</span></span>

- <span data-ttu-id="e5aa8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5aa8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e5aa8-113">Uma assinatura habilitada para logon único do 15Five</span><span class="sxs-lookup"><span data-stu-id="e5aa8-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e5aa8-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e5aa8-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e5aa8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e5aa8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e5aa8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5aa8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e5aa8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e5aa8-118">Scenario description</span></span>
<span data-ttu-id="e5aa8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e5aa8-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e5aa8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e5aa8-121">Adicionar 15Five da galeria</span><span class="sxs-lookup"><span data-stu-id="e5aa8-121">Adding 15Five from the gallery</span></span>
2. <span data-ttu-id="e5aa8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5aa8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-the-gallery"></a><span data-ttu-id="e5aa8-123">Adicionar 15Five da galeria</span><span class="sxs-lookup"><span data-stu-id="e5aa8-123">Adding 15Five from the gallery</span></span>
<span data-ttu-id="e5aa8-124">Para configurar a integração do 15Five ao Azure AD, você precisará adicionar o 15Five da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e5aa8-125">**Para adicionar o 15Five por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e5aa8-125">**To add 15Five from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e5aa8-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e5aa8-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e5aa8-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e5aa8-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e5aa8-133">Na caixa de pesquisa, digite **15Five**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-133">In the search box, type **15Five**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="e5aa8-135">No painel de resultados, selecione **15Five** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e5aa8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5aa8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e5aa8-138">Nesta seção, você configurará e testará o logon único do Azure AD com o 15Five, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e5aa8-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do 15Five é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span></span> <span data-ttu-id="e5aa8-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do 15Five.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span></span>

<span data-ttu-id="e5aa8-141">No 15Five, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e5aa8-142">Para configurar e testar o logon único do Azure AD com o 15Five, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e5aa8-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e5aa8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e5aa8-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e5aa8-145">**[Criar um usuário de teste do 15Five](#creating-a-15five-test-user)** – para ter um equivalente de Brenda Fernandes no 15Five que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e5aa8-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e5aa8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e5aa8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5aa8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e5aa8-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo 15Five.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="e5aa8-150">**Para configurar o logon único do Azure AD com o 15Five, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e5aa8-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="e5aa8-151">No Portal do Azure, na página de integração de aplicativos do **15Five**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e5aa8-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="e5aa8-155">Na seção **URLs e Domínio do 15Five**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e5aa8-155">On the **15Five Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="e5aa8-157">a.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-157">a.</span></span> <span data-ttu-id="e5aa8-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="e5aa8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="e5aa8-159">b.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-159">b.</span></span> <span data-ttu-id="e5aa8-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="e5aa8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e5aa8-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-161">These values are not real.</span></span> <span data-ttu-id="e5aa8-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e5aa8-163">Contate a [equipe de suporte ao Cliente do 15Five](https://www.15five.com/contact/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="e5aa8-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="e5aa8-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e5aa8-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e5aa8-168">Para configurar o logon único no lado do **15Five**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte 15Five](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="e5aa8-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="e5aa8-169">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="e5aa8-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e5aa8-170">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e5aa8-171">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e5aa8-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e5aa8-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5aa8-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="e5aa8-173">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e5aa8-175">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e5aa8-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e5aa8-176">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e5aa8-178">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e5aa8-180">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e5aa8-182">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e5aa8-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e5aa8-184">a.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-184">a.</span></span> <span data-ttu-id="e5aa8-185">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e5aa8-186">b.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-186">b.</span></span> <span data-ttu-id="e5aa8-187">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e5aa8-188">c.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-188">c.</span></span> <span data-ttu-id="e5aa8-189">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e5aa8-190">d.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-190">d.</span></span> <span data-ttu-id="e5aa8-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="e5aa8-192">Criação de um usuário de teste do 15Five</span><span class="sxs-lookup"><span data-stu-id="e5aa8-192">Creating a 15Five test user</span></span>

<span data-ttu-id="e5aa8-193">Para permitir que os usuários do Azure AD façam logon no 15Five, eles devem ser provisionados no 15Five.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="e5aa8-194">No caso do 15Five, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="e5aa8-195">Para configurar o provisionamento de usuários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e5aa8-195">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="e5aa8-196">Faça logon em seu site de empresa do **15Five** como administrador.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-196">Log in to your **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="e5aa8-197">Vá para **Gerenciar Empresa**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-197">Go to **Manage Company**.</span></span>
   
    <span data-ttu-id="e5aa8-198">![Gerenciar Empresa](./media/active-directory-saas-15five-tutorial/IC784675.png "Gerenciar Empresa")</span><span class="sxs-lookup"><span data-stu-id="e5aa8-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="e5aa8-199">Vá para **Pessoas \> Adicionar Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-199">Go to **People \> Add People**.</span></span>
   
    <span data-ttu-id="e5aa8-200">![Pessoas](./media/active-directory-saas-15five-tutorial/IC784676.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="e5aa8-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="e5aa8-201">Na seção Adicionar Nova Pessoa, execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5aa8-201">In the Add New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="e5aa8-202">![Adicionar Nova Pessoa](./media/active-directory-saas-15five-tutorial/IC784677.png "Adicionar Nova Pessoa")</span><span class="sxs-lookup"><span data-stu-id="e5aa8-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="e5aa8-203">a.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-203">a.</span></span> <span data-ttu-id="e5aa8-204">Digite o **Nome**, **Sobrenome**, **Título** e **Endereço de email** de uma conta válida do Azure Active Directory que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="e5aa8-205">b.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-205">b.</span></span> <span data-ttu-id="e5aa8-206">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="e5aa8-207">O titular da conta do Azure AD recebe um email com um link de confirmação de conta para que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span></span>
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e5aa8-208">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5aa8-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e5aa8-209">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao 15Five.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e5aa8-211">**Para atribuir Brenda Fernandes ao 15Five, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e5aa8-211">**To assign Britta Simon to 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="e5aa8-212">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e5aa8-214">Na lista de aplicativos, selecione **15Five**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-214">In the applications list, select **15Five**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="e5aa8-216">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e5aa8-218">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-218">Click **Add** button.</span></span> <span data-ttu-id="e5aa8-219">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e5aa8-221">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e5aa8-222">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e5aa8-223">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e5aa8-224">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e5aa8-224">Testing single sign-on</span></span>

<span data-ttu-id="e5aa8-225">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e5aa8-226">Ao clicar no bloco 15Five no Painel de Acesso, você deve acessar a página de logon do aplicativo 15Five.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="e5aa8-227">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e5aa8-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e5aa8-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e5aa8-228">Additional resources</span></span>

* [<span data-ttu-id="e5aa8-229">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e5aa8-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e5aa8-230">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e5aa8-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

