---
title: "Tutorial: integração do Azure Active Directory com o ThirdLight | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ThirdLight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ee7710cfea3a13907c0cc940a98c875bf83607a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="c837e-103">Tutorial: integração do Azure Active Directory com o ThirdLight</span><span class="sxs-lookup"><span data-stu-id="c837e-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="c837e-104">Neste tutorial, você aprenderá como integrar o ThirdLight com o Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c837e-104">In this tutorial, you learn how to integrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c837e-105">A integração do ThirdLight com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c837e-105">Integrating ThirdLight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c837e-106">No Azure AD, é possível controlar quem tem acesso ao ThirdLight</span><span class="sxs-lookup"><span data-stu-id="c837e-106">You can control in Azure AD who has access to ThirdLight</span></span>
- <span data-ttu-id="c837e-107">Você pode habilitar os usuários a entrarem automaticamente no ThirdLight (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c837e-107">You can enable your users to automatically get signed-on to ThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c837e-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c837e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c837e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c837e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c837e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c837e-110">Prerequisites</span></span>

<span data-ttu-id="c837e-111">Para configurar a integração do Azure AD com o ThirdLight, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c837e-111">To configure Azure AD integration with ThirdLight, you need the following items:</span></span>

- <span data-ttu-id="c837e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c837e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c837e-113">Uma assinatura habilitada para logon único do ThirdLight</span><span class="sxs-lookup"><span data-stu-id="c837e-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c837e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c837e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c837e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c837e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c837e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c837e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c837e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c837e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c837e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c837e-118">Scenario description</span></span>
<span data-ttu-id="c837e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c837e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c837e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c837e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c837e-121">Adicionando o ThirdLight da Galeria</span><span class="sxs-lookup"><span data-stu-id="c837e-121">Adding ThirdLight from the gallery</span></span>
2. <span data-ttu-id="c837e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c837e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-the-gallery"></a><span data-ttu-id="c837e-123">Adicionando o ThirdLight da Galeria</span><span class="sxs-lookup"><span data-stu-id="c837e-123">Adding ThirdLight from the gallery</span></span>
<span data-ttu-id="c837e-124">Para configurar a integração do ThirdLight ao Azure AD, você precisará adicionar o ThirdLight da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c837e-124">To configure the integration of ThirdLight into Azure AD, you need to add ThirdLight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c837e-125">**Para adicionar o ThirdLight da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c837e-125">**To add ThirdLight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c837e-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c837e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c837e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c837e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c837e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c837e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c837e-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c837e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c837e-133">Na caixa de pesquisa, digite **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="c837e-133">In the search box, type **ThirdLight**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="c837e-135">No painel de resultados, selecione **ThirdLight** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c837e-135">In the results panel, select **ThirdLight**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c837e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c837e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c837e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o ThirdLight, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="c837e-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c837e-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ThirdLight é equivalente a um usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c837e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdLight is to a user in Azure AD.</span></span> <span data-ttu-id="c837e-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="c837e-140">In other words, a link relationship between an Azure AD user and the related user in ThirdLight needs to be established.</span></span>

<span data-ttu-id="c837e-141">Essa relação de vínculo é estabelecida por meio da atribuição do valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="c837e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ThirdLight.</span></span>

<span data-ttu-id="c837e-142">Para configurar e testar o logon único do Azure AD com o ThirdLight, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c837e-142">To configure and test Azure AD single sign-on with ThirdLight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c837e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c837e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c837e-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c837e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c837e-145">**[Criação de um usuário de teste do ThirdLight](#creating-a-thirdlight-test-user)** – para ter um equivalente de Brenda Fernandes no ThirdLight que seja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c837e-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - to have a counterpart of Britta Simon in ThirdLight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c837e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c837e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c837e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c837e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c837e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c837e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c837e-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="c837e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="c837e-150">**Para configurar o logon único do Azure AD com o ThirdLight, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c837e-150">**To configure Azure AD single sign-on with ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="c837e-151">No Portal do Azure, na página de integração de aplicativos do **ThirdLight**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c837e-151">In the Azure portal, on the **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c837e-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c837e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="c837e-155">Na seção **URLs e Domínio do ThirdLight**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c837e-155">On the **ThirdLight Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="c837e-157">a.</span><span class="sxs-lookup"><span data-stu-id="c837e-157">a.</span></span> <span data-ttu-id="c837e-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="c837e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="c837e-159">b.</span><span class="sxs-lookup"><span data-stu-id="c837e-159">b.</span></span> <span data-ttu-id="c837e-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="c837e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c837e-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c837e-161">These values are not real.</span></span> <span data-ttu-id="c837e-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="c837e-162">Update these values with the actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="c837e-163">Contate a [equipe de suporte ao cliente do ThirdLight](https://www.thirdlight.com/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="c837e-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="c837e-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c837e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="c837e-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c837e-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c837e-168">Em outra janela do navegador da Web, faça logon em seu site de empresa ThirdLight como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c837e-168">In a different web browser window, log in to your ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="c837e-169">Vá para **Configuração \> Administração do Sistema** e clique em **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="c837e-169">Go to **Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="c837e-170">![Administração do Sistema](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Administração do Sistema")</span><span class="sxs-lookup"><span data-stu-id="c837e-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="c837e-171">Na seção de configuração do SAML2, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c837e-171">In the SAML2 configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="c837e-172">![Logon Único do SAML](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="c837e-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="c837e-173">a.</span><span class="sxs-lookup"><span data-stu-id="c837e-173">a.</span></span> <span data-ttu-id="c837e-174">Selecione **Habilitar Logon Único do SAML2**.</span><span class="sxs-lookup"><span data-stu-id="c837e-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="c837e-175">b.</span><span class="sxs-lookup"><span data-stu-id="c837e-175">b.</span></span> <span data-ttu-id="c837e-176">Como **Fonte de metadados do IdP**, selecione **Carregar Metadados do IdP do XML**.</span><span class="sxs-lookup"><span data-stu-id="c837e-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="c837e-177">c.</span><span class="sxs-lookup"><span data-stu-id="c837e-177">c.</span></span> <span data-ttu-id="c837e-178">Abra o arquivo de metadados baixado, copie o conteúdo e cole-o na caixa de texto **XML de Metadados do IdP** .</span><span class="sxs-lookup"><span data-stu-id="c837e-178">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="c837e-179">d.</span><span class="sxs-lookup"><span data-stu-id="c837e-179">d.</span></span> <span data-ttu-id="c837e-180">Clique em **Salvar configurações do SAML2**.</span><span class="sxs-lookup"><span data-stu-id="c837e-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="c837e-181">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c837e-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c837e-182">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c837e-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c837e-183">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c837e-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c837e-184">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c837e-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="c837e-185">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c837e-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c837e-187">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c837e-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c837e-188">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c837e-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c837e-190">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c837e-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c837e-192">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c837e-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c837e-194">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c837e-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c837e-196">a.</span><span class="sxs-lookup"><span data-stu-id="c837e-196">a.</span></span> <span data-ttu-id="c837e-197">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c837e-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c837e-198">b.</span><span class="sxs-lookup"><span data-stu-id="c837e-198">b.</span></span> <span data-ttu-id="c837e-199">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c837e-199">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="c837e-200">c.</span><span class="sxs-lookup"><span data-stu-id="c837e-200">c.</span></span> <span data-ttu-id="c837e-201">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="c837e-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c837e-202">d.</span><span class="sxs-lookup"><span data-stu-id="c837e-202">d.</span></span> <span data-ttu-id="c837e-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c837e-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="c837e-204">Criação de um usuário de teste do ThirdLight</span><span class="sxs-lookup"><span data-stu-id="c837e-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="c837e-205">Para permitir que os usuários do Azure AD façam logon no ThirdLight, eles devem ser provisionados no ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="c837e-205">To enable Azure AD users to log in to ThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="c837e-206">No caso do ThirdLight, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="c837e-206">In the case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="c837e-207">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c837e-207">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c837e-208">Faça logon em seu site de empresa do **ThirdLight** como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c837e-208">Log in to your **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="c837e-209">Vá para a guia **Usuários** .</span><span class="sxs-lookup"><span data-stu-id="c837e-209">Go to **Users** tab.</span></span>

3. <span data-ttu-id="c837e-210">Selecione **Usuários e Grupos**.</span><span class="sxs-lookup"><span data-stu-id="c837e-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="c837e-211">Clique no botão **Adicionar novo Usuário** .</span><span class="sxs-lookup"><span data-stu-id="c837e-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="c837e-212">Digite os valores de **Nome de usuário, Nome ou Descrição, Email, Escolher uma Predefinição ou Grupo de Novos Membros** de uma conta válida do AAD que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="c837e-212">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span></span>

6. <span data-ttu-id="c837e-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c837e-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="c837e-214">É possível usar qualquer outra ferramenta de criação da conta de usuário do Thirdlight ou as APIs fornecidas pelo Thirdlight para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="c837e-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c837e-215">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c837e-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c837e-216">Nesta seção, você habilita a Brenda Fernandes a usar o logon único do Azure através da concessão de acesso ao ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="c837e-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdLight.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c837e-218">**Para atribuir Brenda Fernandes ao ThirdLight, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c837e-218">**To assign Britta Simon to ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="c837e-219">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c837e-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c837e-221">Na lista de aplicativos, selecione **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="c837e-221">In the applications list, select **ThirdLight**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="c837e-223">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c837e-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c837e-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c837e-225">Click **Add** button.</span></span> <span data-ttu-id="c837e-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c837e-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c837e-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c837e-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c837e-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c837e-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c837e-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c837e-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c837e-231">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c837e-231">Testing single sign-on</span></span>

<span data-ttu-id="c837e-232">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c837e-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c837e-233">Ao clicar no bloco ThirdLight no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="c837e-233">When you click the ThirdLight tile in the Access Panel, you should get automatically signed-on to your ThirdLight application.</span></span>
<span data-ttu-id="c837e-234">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c837e-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c837e-235">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c837e-235">Additional resources</span></span>

* [<span data-ttu-id="c837e-236">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c837e-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c837e-237">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c837e-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

