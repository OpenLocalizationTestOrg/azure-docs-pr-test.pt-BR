---
title: "Tutorial: Integração do Azure Active Directory ao Tableau Server | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Tableau Server."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 6b35609d88fbbf649e15863901d521886db2a4d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="913d7-103">Tutorial: Integração do Azure Active Directory ao Tableau Server</span><span class="sxs-lookup"><span data-stu-id="913d7-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="913d7-104">Neste tutorial, você aprenderá a integrar o Tableau Server ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="913d7-104">In this tutorial, you learn how to integrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="913d7-105">A integração do Tableau Server ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="913d7-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="913d7-106">Você pode controlar no Azure AD quem tem acesso ao Tableau Server</span><span class="sxs-lookup"><span data-stu-id="913d7-106">You can control in Azure AD who has access to Tableau Server</span></span>
- <span data-ttu-id="913d7-107">Você pode habilitar os usuários a entrar automaticamente no Tableau Server (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="913d7-107">You can enable your users to automatically get signed-on to Tableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="913d7-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="913d7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="913d7-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="913d7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="913d7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="913d7-110">Prerequisites</span></span>

<span data-ttu-id="913d7-111">Para configurar a integração do Azure AD ao Tableau Server, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="913d7-111">To configure Azure AD integration with Tableau Server, you need the following items:</span></span>

- <span data-ttu-id="913d7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="913d7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="913d7-113">Uma assinatura habilitada para logon único do Tableau Server</span><span class="sxs-lookup"><span data-stu-id="913d7-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="913d7-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="913d7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="913d7-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="913d7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="913d7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="913d7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="913d7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="913d7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="913d7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="913d7-118">Scenario description</span></span>
<span data-ttu-id="913d7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="913d7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="913d7-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="913d7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="913d7-121">Adição do Tableau Server a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="913d7-121">Adding Tableau Server from the gallery</span></span>
2. <span data-ttu-id="913d7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="913d7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-the-gallery"></a><span data-ttu-id="913d7-123">Adição do Tableau Server a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="913d7-123">Adding Tableau Server from the gallery</span></span>
<span data-ttu-id="913d7-124">Para configurar a integração do Tableau Server ao Azure AD, você precisa adicionar o Tableau Server da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="913d7-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="913d7-125">**Para adicionar o Tableau Server por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="913d7-125">**To add Tableau Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="913d7-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="913d7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="913d7-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="913d7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="913d7-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="913d7-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="913d7-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="913d7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="913d7-133">Na caixa de pesquisa, digite **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="913d7-133">In the search box, type **Tableau Server**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="913d7-135">No painel de resultados, selecione **Tableau Server** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="913d7-135">In the results panel, select **Tableau Server**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="913d7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="913d7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="913d7-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Tableau Server, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="913d7-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="913d7-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Tableau Server é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="913d7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Server is to a user in Azure AD.</span></span> <span data-ttu-id="913d7-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="913d7-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span></span>

<span data-ttu-id="913d7-141">No Tableau Server, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="913d7-141">In Tableau Server, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="913d7-142">Para configurar e testar o logon único do Azure AD com o Tableau Server, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="913d7-142">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="913d7-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="913d7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="913d7-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="913d7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="913d7-145">**[Criação de um usuário de teste do Tableau Server](#creating-a-tableau-server-test-user)** – para ter um equivalente de Brenda Fernandes no Tableau Server que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="913d7-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="913d7-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="913d7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="913d7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="913d7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="913d7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="913d7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="913d7-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="913d7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="913d7-150">**Para configurar o logon único do Azure AD com o Tableau Server, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="913d7-150">**To configure Azure AD single sign-on with Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="913d7-151">No portal do Azure, na página de integração do aplicativo do **Tableau Server**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="913d7-151">In the Azure portal, on the **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="913d7-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="913d7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="913d7-155">Na seção **Domínio e URLs do Tableau Server**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="913d7-155">On the **Tableau Server Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="913d7-157">a.</span><span class="sxs-lookup"><span data-stu-id="913d7-157">a.</span></span> <span data-ttu-id="913d7-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="913d7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="913d7-159">b.</span><span class="sxs-lookup"><span data-stu-id="913d7-159">b.</span></span> <span data-ttu-id="913d7-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="913d7-160">In the **Identifier** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="913d7-161">c.</span><span class="sxs-lookup"><span data-stu-id="913d7-161">c.</span></span> <span data-ttu-id="913d7-162">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="913d7-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="913d7-163">Os valores anteriores não são valores reais.</span><span class="sxs-lookup"><span data-stu-id="913d7-163">The preceding values are not real values.</span></span> <span data-ttu-id="913d7-164">Posteriormente, você deve atualizar os valores com a URL e o identificador reais da página de configuração do Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="913d7-164">Later, you update the values with the actual URL and identifier from the Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="913d7-165">O aplicativo Tableau Server espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="913d7-165">Tableau Server application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="913d7-166">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="913d7-166">Configure the following claims for this application.</span></span> <span data-ttu-id="913d7-167">Você pode gerenciar os valores desses atributos da seção **“Atributos de Usuário”** na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="913d7-167">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="913d7-168">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="913d7-168">The following screenshot shows an example for the same.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="913d7-170">Na seção **Atributos do usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML na imagem acima e siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="913d7-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="913d7-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="913d7-171">Attribute Name</span></span> | <span data-ttu-id="913d7-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="913d7-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="913d7-173">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="913d7-173">username</span></span> | <span data-ttu-id="913d7-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="913d7-174">*user.displayname*</span></span> |

    <span data-ttu-id="913d7-175">a.</span><span class="sxs-lookup"><span data-stu-id="913d7-175">a.</span></span> <span data-ttu-id="913d7-176">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="913d7-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="913d7-179">b.</span><span class="sxs-lookup"><span data-stu-id="913d7-179">b.</span></span> <span data-ttu-id="913d7-180">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="913d7-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="913d7-181">c.</span><span class="sxs-lookup"><span data-stu-id="913d7-181">c.</span></span> <span data-ttu-id="913d7-182">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="913d7-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="913d7-183">d.</span><span class="sxs-lookup"><span data-stu-id="913d7-183">d.</span></span> <span data-ttu-id="913d7-184">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="913d7-184">Click **Ok**</span></span>


6. <span data-ttu-id="913d7-185">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="913d7-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="913d7-187">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="913d7-187">Click **Save** button.</span></span>

    <span data-ttu-id="913d7-188">![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="913d7-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="913d7-189">Para configurar o SSO para o aplicativo, você precisa entrar no locatário Tableau Server como administrador.</span><span class="sxs-lookup"><span data-stu-id="913d7-189">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="913d7-190">a.</span><span class="sxs-lookup"><span data-stu-id="913d7-190">a.</span></span> <span data-ttu-id="913d7-191">Na configuração do Tableau Server, clique na guia **SAML** .</span><span class="sxs-lookup"><span data-stu-id="913d7-191">In the Tableau Server configuration, click the **SAML** tab.</span></span>
  
    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="913d7-193">b.</span><span class="sxs-lookup"><span data-stu-id="913d7-193">b.</span></span> <span data-ttu-id="913d7-194">Marque a caixa de seleção **Usar SAML para logon único**.</span><span class="sxs-lookup"><span data-stu-id="913d7-194">Select the checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="913d7-195">c.</span><span class="sxs-lookup"><span data-stu-id="913d7-195">c.</span></span> <span data-ttu-id="913d7-196">URL de retorno do Tableau Server — a URL que os usuários do Tableau Server acessarão, por exemplo, http://tableau_server.</span><span class="sxs-lookup"><span data-stu-id="913d7-196">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="913d7-197">Não é recomendável usar http://localhost.</span><span class="sxs-lookup"><span data-stu-id="913d7-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="913d7-198">O uso de URL com barra à direita (por exemplo, http://tableau_server/) não é aceito.</span><span class="sxs-lookup"><span data-stu-id="913d7-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="913d7-199">Copie a **URL de retorno do Tableau Server** e cole-a na caixa de texto **URL de Logon** do Azure AD, na seção **URLs e Domínio do Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="913d7-199">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="913d7-200">d.</span><span class="sxs-lookup"><span data-stu-id="913d7-200">d.</span></span> <span data-ttu-id="913d7-201">ID de entidade SAML - a ID de entidade identifica com exclusividade sua instalação do Tableau Server para o IdP.</span><span class="sxs-lookup"><span data-stu-id="913d7-201">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span></span> <span data-ttu-id="913d7-202">Você pode digitar a URL do Tableau Server novamente aqui, se desejar, mas ela não precisa ser sua URL do Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="913d7-202">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span></span> <span data-ttu-id="913d7-203">Copie a **ID de Entidade do SAML** e cole-a na caixa de texto **Identificador** do Azure AD, na seção **URLs e Domínio do Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="913d7-203">Copy **SAML entity ID** and paste it to Azure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="913d7-204">e.</span><span class="sxs-lookup"><span data-stu-id="913d7-204">e.</span></span> <span data-ttu-id="913d7-205">Clique em **Exportar Arquivo de Metadados** e abra-o no aplicativo de editor de texto.</span><span class="sxs-lookup"><span data-stu-id="913d7-205">Click the **Export Metadata File** and open it in the text editor application.</span></span> <span data-ttu-id="913d7-206">Localize a URL do Serviço de Declaração do Consumidor com Http Post e Índice 0 e copie a URL.</span><span class="sxs-lookup"><span data-stu-id="913d7-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span></span> <span data-ttu-id="913d7-207">Agora a cole na caixa de texto **URL de Resposta** do Azure AD, na seção **URLs e Domínio do Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="913d7-207">Now paste it to Azure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="913d7-208">f.</span><span class="sxs-lookup"><span data-stu-id="913d7-208">f.</span></span> <span data-ttu-id="913d7-209">Localize o arquivo de Metadados de Federação baixado do portal do Azure e carregue-o no **arquivo de metadados do IDP do SAML**.</span><span class="sxs-lookup"><span data-stu-id="913d7-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in the **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="913d7-210">g.</span><span class="sxs-lookup"><span data-stu-id="913d7-210">g.</span></span> <span data-ttu-id="913d7-211">Clique no botão **OK** na página Configuração do Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="913d7-211">Click the **OK** button in the Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="913d7-212">O cliente precisa carregar um certificado na configuração de SSO do SAML do Tableau Server e ele será ignorado no fluxo de SSO.</span><span class="sxs-lookup"><span data-stu-id="913d7-212">Customer have to upload any certificate in the Tableau Server SAML SSO configuration and it will get ignored in the SSO flow.</span></span>
    ><span data-ttu-id="913d7-213">Se precisar de ajuda para configurar o SAML no Tableau Server, consulte o artigo [Configurar SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="913d7-213">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="913d7-214">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="913d7-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="913d7-215">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="913d7-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="913d7-216">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="913d7-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="913d7-217">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="913d7-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="913d7-218">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="913d7-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="913d7-220">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="913d7-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="913d7-221">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="913d7-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="913d7-223">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="913d7-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="913d7-225">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="913d7-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="913d7-227">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="913d7-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="913d7-229">a.</span><span class="sxs-lookup"><span data-stu-id="913d7-229">a.</span></span> <span data-ttu-id="913d7-230">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="913d7-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="913d7-231">b.</span><span class="sxs-lookup"><span data-stu-id="913d7-231">b.</span></span> <span data-ttu-id="913d7-232">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="913d7-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="913d7-233">c.</span><span class="sxs-lookup"><span data-stu-id="913d7-233">c.</span></span> <span data-ttu-id="913d7-234">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="913d7-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="913d7-235">d.</span><span class="sxs-lookup"><span data-stu-id="913d7-235">d.</span></span> <span data-ttu-id="913d7-236">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="913d7-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="913d7-237">Criação de um usuário de teste do Tableau Server</span><span class="sxs-lookup"><span data-stu-id="913d7-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="913d7-238">O objetivo desta seção é criar uma usuária chamada Brenda Fernandes no Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="913d7-238">The objective of this section is to create a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="913d7-239">Será necessário provisionar todos os usuários no Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="913d7-239">You need to provision all the users in the Tableau server.</span></span> 

<span data-ttu-id="913d7-240">O nome de usuário deve corresponder ao valor que você configurou no atributo personalizado **username** do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="913d7-240">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="913d7-241">Com o mapeamento correto, a integração deve funcionar, conforme [Configuração do Logon Único do Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="913d7-241">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="913d7-242">Se precisar criar um usuário manualmente, entre em contato com o administrador do Tableau Server em sua organização.</span><span class="sxs-lookup"><span data-stu-id="913d7-242">If you need to create a user manually, you need to contact the Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="913d7-243">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="913d7-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="913d7-244">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="913d7-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Server.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="913d7-246">**Para atribuir Brenda Fernandes ao Tableau Server, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="913d7-246">**To assign Britta Simon to Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="913d7-247">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="913d7-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="913d7-249">Na lista de aplicativos, selecione **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="913d7-249">In the applications list, select **Tableau Server**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="913d7-251">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="913d7-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="913d7-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="913d7-253">Click **Add** button.</span></span> <span data-ttu-id="913d7-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="913d7-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="913d7-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="913d7-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="913d7-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="913d7-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="913d7-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="913d7-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="913d7-259">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="913d7-259">Testing single sign-on</span></span>

<span data-ttu-id="913d7-260">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="913d7-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="913d7-261">Ao clicar no bloco Tableau Server no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="913d7-261">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span></span>
<span data-ttu-id="913d7-262">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="913d7-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="913d7-263">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="913d7-263">Additional resources</span></span>

* [<span data-ttu-id="913d7-264">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="913d7-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="913d7-265">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="913d7-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

