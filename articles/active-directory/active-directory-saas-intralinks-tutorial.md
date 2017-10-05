---
title: "Tutorial: integração do Azure Active Directory com o Intralinks | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ee7fd5b88ac806104002ffb41af11bab4fd1b2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="da582-103">Tutorial: Integração do Azure Active Directory com o Intralinks</span><span class="sxs-lookup"><span data-stu-id="da582-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="da582-104">Neste tutorial, você aprenderá como integrar o Intralinks ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="da582-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da582-105">A integração do Intralinks ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="da582-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="da582-106">Você pode controlar no Azure AD quem terá acesso ao Intralinks</span><span class="sxs-lookup"><span data-stu-id="da582-106">You can control in Azure AD who has access to Intralinks</span></span>
- <span data-ttu-id="da582-107">Você pode permitir que seus usuários façam logon automaticamente no Intralinks (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="da582-107">You can enable your users to automatically get signed-on to Intralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="da582-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="da582-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="da582-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="da582-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da582-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="da582-110">Prerequisites</span></span>

<span data-ttu-id="da582-111">Para configurar a integração do Azure AD ao Intralinks, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="da582-111">To configure Azure AD integration with Intralinks, you need the following items:</span></span>

- <span data-ttu-id="da582-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="da582-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da582-113">Uma assinatura habilitada para logon único do Intralinks</span><span class="sxs-lookup"><span data-stu-id="da582-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="da582-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="da582-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="da582-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="da582-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da582-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="da582-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="da582-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="da582-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="da582-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="da582-118">Scenario description</span></span>
<span data-ttu-id="da582-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="da582-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da582-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="da582-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da582-121">Adicionando o Intralinks da galeria</span><span class="sxs-lookup"><span data-stu-id="da582-121">Adding Intralinks from the gallery</span></span>
2. <span data-ttu-id="da582-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="da582-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-the-gallery"></a><span data-ttu-id="da582-123">Adicionando o Intralinks da galeria</span><span class="sxs-lookup"><span data-stu-id="da582-123">Adding Intralinks from the gallery</span></span>
<span data-ttu-id="da582-124">Para configurar a integração do Intralinks ao Azure AD, você precisará adicionar o Intralinks da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="da582-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="da582-125">**Para adicionar o Intralinks da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="da582-125">**To add Intralinks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="da582-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="da582-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="da582-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="da582-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="da582-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="da582-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="da582-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da582-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="da582-133">Na caixa de pesquisa, digite **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="da582-133">In the search box, type **Intralinks**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="da582-135">No painel de resultados, selecione **Intralinks** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da582-135">In the results panel, select **Intralinks**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="da582-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="da582-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="da582-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Intralinks, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="da582-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="da582-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Intralinks é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da582-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span></span> <span data-ttu-id="da582-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Intralinks.</span><span class="sxs-lookup"><span data-stu-id="da582-140">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span></span>

<span data-ttu-id="da582-141">No Intralinks, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="da582-141">In Intralinks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="da582-142">Para configurar e testar o logon único do Azure AD com o Intralinks, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="da582-142">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="da582-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="da582-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="da582-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="da582-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da582-145">**[Criando um usuário de teste do Intralinks](#creating-an-intralinks-test-user)** – para ter um equivalente de Brenda Fernandes no Intralinks que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da582-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="da582-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="da582-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da582-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="da582-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="da582-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="da582-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="da582-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Intralinks.</span><span class="sxs-lookup"><span data-stu-id="da582-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="da582-150">**Para configurar o logon único do Azure AD com o Intralinks, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="da582-150">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="da582-151">No portal do Azure, na página de integração do aplicativo **Intralinks**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="da582-151">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="da582-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="da582-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="da582-155">Na seção **Domínio e URLs do Intralinks**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="da582-155">On the **Intralinks Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="da582-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="da582-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="da582-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="da582-158">This value is not real.</span></span> <span data-ttu-id="da582-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="da582-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="da582-160">Contate a [equipe de suporte ao Cliente do Intralinks](https://www.intralinks.com/contact-1) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="da582-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) to get this value.</span></span> 
 
4. <span data-ttu-id="da582-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="da582-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="da582-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="da582-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="da582-165">Para configurar o logon único no lado do **Intralinks**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Intralinks](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="da582-165">To configure single sign-on on **Intralinks** side, you need to send the downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="da582-166">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="da582-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="da582-167">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="da582-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="da582-168">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="da582-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="da582-169">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="da582-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="da582-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="da582-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="da582-171">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="da582-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="da582-173">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="da582-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="da582-174">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="da582-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="da582-176">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="da582-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="da582-178">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="da582-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="da582-180">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="da582-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="da582-182">a.</span><span class="sxs-lookup"><span data-stu-id="da582-182">a.</span></span> <span data-ttu-id="da582-183">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="da582-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da582-184">b.</span><span class="sxs-lookup"><span data-stu-id="da582-184">b.</span></span> <span data-ttu-id="da582-185">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="da582-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da582-186">c.</span><span class="sxs-lookup"><span data-stu-id="da582-186">c.</span></span> <span data-ttu-id="da582-187">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="da582-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="da582-188">d.</span><span class="sxs-lookup"><span data-stu-id="da582-188">d.</span></span> <span data-ttu-id="da582-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="da582-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="da582-190">Criação de um usuário de teste do Intralinks</span><span class="sxs-lookup"><span data-stu-id="da582-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="da582-191">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Intralinks.</span><span class="sxs-lookup"><span data-stu-id="da582-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="da582-192">Trabalhe com a [equipe de suporte do Intralinks](https://www.intralinks.com/contact-1) para adicionar os usuários à plataforma Intralinks.</span><span class="sxs-lookup"><span data-stu-id="da582-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) to add the users in the Intralinks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="da582-193">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="da582-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="da582-194">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Intralinks.</span><span class="sxs-lookup"><span data-stu-id="da582-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intralinks.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="da582-196">**Para atribuir Brenda Fernandes ao Intralinks, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="da582-196">**To assign Britta Simon to Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="da582-197">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="da582-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="da582-199">Na lista de aplicativos, selecione **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="da582-199">In the applications list, select **Intralinks**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="da582-201">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="da582-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="da582-203">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="da582-203">Click **Add** button.</span></span> <span data-ttu-id="da582-204">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="da582-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="da582-206">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="da582-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="da582-207">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="da582-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da582-208">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="da582-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="da582-209">Adicionar o aplicativo Intralinks VIA ou Elite</span><span class="sxs-lookup"><span data-stu-id="da582-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="da582-210">O Intralinks usa a mesma plataforma de Identidade de SSO para todos os outros aplicativos Intralinks excluindo o aplicativo Deal Nexus.</span><span class="sxs-lookup"><span data-stu-id="da582-210">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="da582-211">Portanto, se você planeja usar qualquer outro aplicativo Intralinks, primeiro você precisa configurar o SSO para um aplicativo Intralinks primário usando o procedimento descrito acima.</span><span class="sxs-lookup"><span data-stu-id="da582-211">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span></span>

<span data-ttu-id="da582-212">Depois disso, você pode seguir o procedimento abaixo para adicionar outro aplicativo Intralinks em seu locatário, que pode aproveitar esse aplicativo principal para o SSO.</span><span class="sxs-lookup"><span data-stu-id="da582-212">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="da582-213">Esse recurso está disponível somente para clientes de SKU do Azure AD Premium e não está disponível para clientes de SKU Gratuito ou Básico.</span><span class="sxs-lookup"><span data-stu-id="da582-213">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="da582-214">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="da582-214">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="da582-216">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="da582-216">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="da582-217">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="da582-217">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="da582-219">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da582-219">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="da582-221">Na caixa de pesquisa, digite **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="da582-221">In the search box, type **Intralinks**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="da582-223">No **aplicativo Intralinks Add**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="da582-223">On **Intralinks Add app** perform the following steps:</span></span>

    ![Adicionar o aplicativo Intralinks VIA ou Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="da582-225">a.</span><span class="sxs-lookup"><span data-stu-id="da582-225">a.</span></span> <span data-ttu-id="da582-226">Na caixa de texto **Nome**, insira o nome apropriado do aplicativo, por exemplo, **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="da582-226">In **Name** textbox, enter appropriate name of the application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="da582-227">b.</span><span class="sxs-lookup"><span data-stu-id="da582-227">b.</span></span> <span data-ttu-id="da582-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="da582-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="da582-229">No portal do Azure, na página de integração do aplicativo **Intralinks**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="da582-229">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

7. <span data-ttu-id="da582-231">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon vinculado**.</span><span class="sxs-lookup"><span data-stu-id="da582-231">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="da582-233">Obtenha a URL de SSO Iniciada pelo SP da [equipe do Intralinks](https://www.intralinks.com/contact-1) para o outro aplicativo Intralinks e insira-a em **Configurar URL de Logon**, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="da582-233">Get the the SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for the other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="da582-235">Na caixa de texto URL de Logon, digite a URL usada pelos usuários para fazer logon no aplicativo Intralinks usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="da582-235">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="da582-236">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="da582-236">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="da582-238">Atribua o aplicativo para usuários ou grupos, como mostrado na seção **[Atribuição do usuário de teste do Azure AD](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="da582-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="da582-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="da582-239">Testing single sign-on</span></span>

<span data-ttu-id="da582-240">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="da582-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="da582-241">Ao clicar no bloco Intralinks no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Intralinks.</span><span class="sxs-lookup"><span data-stu-id="da582-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span></span>
<span data-ttu-id="da582-242">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="da582-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="da582-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="da582-243">Additional resources</span></span>

* [<span data-ttu-id="da582-244">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="da582-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da582-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="da582-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

