---
title: "Tutorial: Integração do Azure Active Directory com o Salesforce | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 639e40ca7e406a1726033e9f5c5363c289087589
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="7b691-103">Tutorial: Integração do Azure Active Directory com o Salesforce</span><span class="sxs-lookup"><span data-stu-id="7b691-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="7b691-104">Neste tutorial, você aprenderá a integrar o Salesforce ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7b691-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b691-105">A integração do Salesforce ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7b691-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7b691-106">No Azure AD, é possível controlar quem tem acesso ao Salesforce</span><span class="sxs-lookup"><span data-stu-id="7b691-106">You can control in Azure AD who has access to Salesforce</span></span>
- <span data-ttu-id="7b691-107">Você pode permitir que seus usuários façam logon automaticamente no Salesforce (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="7b691-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b691-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7b691-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7b691-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b691-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b691-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7b691-110">Prerequisites</span></span>

<span data-ttu-id="7b691-111">Para configurar a integração do Azure AD ao Salesforce, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7b691-111">To configure Azure AD integration with Salesforce, you need the following items:</span></span>

- <span data-ttu-id="7b691-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7b691-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b691-113">Uma assinatura do Salesforce com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="7b691-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b691-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7b691-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b691-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7b691-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b691-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7b691-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b691-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b691-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b691-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7b691-118">Scenario description</span></span>
<span data-ttu-id="7b691-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7b691-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b691-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7b691-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b691-121">Adicionar Salesforce da galeria</span><span class="sxs-lookup"><span data-stu-id="7b691-121">Adding Salesforce from the gallery</span></span>
2. <span data-ttu-id="7b691-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7b691-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-the-gallery"></a><span data-ttu-id="7b691-123">Adicionar Salesforce da galeria</span><span class="sxs-lookup"><span data-stu-id="7b691-123">Adding Salesforce from the gallery</span></span>
<span data-ttu-id="7b691-124">Para configurar a integração do Salesforce ao Azure AD, você precisará adicionar o Salesforce da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7b691-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7b691-125">**Para adicionar o Salesforce na galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7b691-125">**To add Salesforce from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7b691-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7b691-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7b691-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7b691-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7b691-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7b691-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7b691-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b691-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7b691-133">Na caixa de pesquisa, digite **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="7b691-133">In the search box, type **Salesforce**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="7b691-135">No painel de resultados, selecione **Salesforce** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7b691-135">In the results panel, select **Salesforce**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7b691-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7b691-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7b691-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Salesforce, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7b691-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7b691-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Salesforce é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b691-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span></span> <span data-ttu-id="7b691-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7b691-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span></span>

<span data-ttu-id="7b691-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como sendo o valor de **Nome de Usuário** no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7b691-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce.</span></span>

<span data-ttu-id="7b691-142">Para configurar e testar o logon único do Azure AD com o Salesforce, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="7b691-142">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7b691-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7b691-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7b691-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7b691-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b691-145">**[Criação de um usuário de teste do Salesforce](#creating-a-salesforce-test-user)** – para ter um equivalente de Brenda Fernandes no Salesforce que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b691-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b691-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b691-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b691-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7b691-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7b691-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b691-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7b691-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7b691-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="7b691-150">**Para configurar o logon único do Azure AD com o Salesforce, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7b691-150">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="7b691-151">No portal do Azure, na página de integração de aplicativos do **Salesforce**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7b691-151">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7b691-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7b691-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="7b691-155">Na seção **URLs e Domínio do Salesforce**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7b691-155">On the **Salesforce Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="7b691-157">Na caixa de texto **URL de Logon**, digite o valor usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="7b691-157">In the **Sign-on URL** textbox, type the value using the following pattern:</span></span> 
   * <span data-ttu-id="7b691-158">Conta empresarial: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="7b691-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="7b691-159">Conta de desenvolvedor: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="7b691-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b691-160">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="7b691-160">These values are not the real.</span></span> <span data-ttu-id="7b691-161">Atualize esses valores com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="7b691-161">Update these values with the actual Sign-on URL.</span></span> <span data-ttu-id="7b691-162">Contate a [equipe de suporte do Cliente Salesforce](https://help.salesforce.com/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="7b691-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="7b691-163">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7b691-163">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="7b691-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7b691-165">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7b691-167">Na seção **configuração do Salesforce**, clique em **Configurar Salesforce** para abrir a janela **Configurar Logon**.</span><span class="sxs-lookup"><span data-stu-id="7b691-167">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7b691-168">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="7b691-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    <span data-ttu-id="7b691-169">![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="7b691-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="7b691-170">Abra uma nova guia no navegador e faça logon em sua conta de administrador do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7b691-170">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>

8.  <span data-ttu-id="7b691-171">No painel de navegação **Administrador**, clique em **Controles de Segurança** para expandir a seção correspondente.</span><span class="sxs-lookup"><span data-stu-id="7b691-171">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span></span> <span data-ttu-id="7b691-172">Em seguida, clique em **Configurações de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="7b691-172">Then click **Single Sign-On Settings**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="7b691-174">Na página **Configurações de Logon Único**, clique no botão **Editar**.</span><span class="sxs-lookup"><span data-stu-id="7b691-174">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>
    <span data-ttu-id="7b691-175">![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="7b691-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="7b691-176">Se não for possível habilitar as configurações de Logon Único para a conta do Salesforce, talvez seja necessário entrar em contato com a [equipe de suporte do Cliente Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="7b691-176">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="7b691-177">Selecione **SAML Habilitado** e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7b691-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="7b691-179">Para definir as configurações de logon único do SAML, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="7b691-179">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="7b691-181">Na página **Edição de Configuração de Logon Único do SAML** , realize as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="7b691-181">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="7b691-183">a.</span><span class="sxs-lookup"><span data-stu-id="7b691-183">a.</span></span> <span data-ttu-id="7b691-184">Para o campo **Nome** , digite um nome amigável para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="7b691-184">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="7b691-185">Fornecer um valor para **Nome** preenche automaticamente a caixa de texto **Nome da API**.</span><span class="sxs-lookup"><span data-stu-id="7b691-185">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>

    <span data-ttu-id="7b691-186">b.</span><span class="sxs-lookup"><span data-stu-id="7b691-186">b.</span></span> <span data-ttu-id="7b691-187">Cole o valor **ID da Entidade de SAML** no campo **Emissor** em Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7b691-187">Paste **SMAL Entity ID** value into the **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="7b691-188">c.</span><span class="sxs-lookup"><span data-stu-id="7b691-188">c.</span></span> <span data-ttu-id="7b691-189">Na **caixa de texto Id da Entidade**, digite seu nome de domínio do Salesforce usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="7b691-189">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>
      
      * <span data-ttu-id="7b691-190">Conta empresarial: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="7b691-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="7b691-191">Conta de desenvolvedor: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="7b691-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="7b691-192">d.</span><span class="sxs-lookup"><span data-stu-id="7b691-192">d.</span></span> <span data-ttu-id="7b691-193">Clique em **Procurar** ou **Escolher Arquivo** para abrir a caixa de diálogo **Escolher Arquivo para Carregar**, selecione seu certificado do Salesforce e, em seguida, clique em **Abrir** para carregar o certificado.</span><span class="sxs-lookup"><span data-stu-id="7b691-193">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="7b691-194">e.</span><span class="sxs-lookup"><span data-stu-id="7b691-194">e.</span></span> <span data-ttu-id="7b691-195">Para **Tipo de Identidade do SAML**, selecione **A declaração contém o nome de usuário salesforce.com do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="7b691-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="7b691-196">f.</span><span class="sxs-lookup"><span data-stu-id="7b691-196">f.</span></span> <span data-ttu-id="7b691-197">Para **Local de Identidade do SAML**, selecione **A identidade está no elemento NameIdentifier da instrução de assunto**</span><span class="sxs-lookup"><span data-stu-id="7b691-197">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span></span>

    <span data-ttu-id="7b691-198">g.</span><span class="sxs-lookup"><span data-stu-id="7b691-198">g.</span></span> <span data-ttu-id="7b691-199">Cole a **URL de Serviço de Logon Único** no campo **URL de Logon do Provedor de Identidade** no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7b691-199">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="7b691-200">h.</span><span class="sxs-lookup"><span data-stu-id="7b691-200">h.</span></span> <span data-ttu-id="7b691-201">Para **Associação de Solicitação Iniciada do Provedor de Serviço**, selecione **Redirecionamento HTTP**.</span><span class="sxs-lookup"><span data-stu-id="7b691-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="7b691-202">i.</span><span class="sxs-lookup"><span data-stu-id="7b691-202">i.</span></span> <span data-ttu-id="7b691-203">Finalmente, clique em **Salvar** para aplicar as configurações de logon único do SAML.</span><span class="sxs-lookup"><span data-stu-id="7b691-203">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="7b691-204">No painel de navegação à esquerda no Salesforce, clique em **Gerenciamento de Domínio** para expandir a seção correspondente e, em seguida, clique em **Meu Domínio**.</span><span class="sxs-lookup"><span data-stu-id="7b691-204">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="7b691-206">Role para baixo até a seção **Configuração de Autenticação** e, em seguida, clique no botão **Editar**.</span><span class="sxs-lookup"><span data-stu-id="7b691-206">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="7b691-208">Na seção **Serviço de Autenticação**, selecione o nome amigável da sua configuração de SSO de SAML e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7b691-208">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="7b691-210">Se mais de um serviço de autenticação estiver selecionado, quando os usuários tentarem iniciar o logon único em seu ambiente do Salesforce, serão solicitados a selecionar o serviço de autenticação com o qual desejam entrar.</span><span class="sxs-lookup"><span data-stu-id="7b691-210">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span></span> <span data-ttu-id="7b691-211">Se você não quiser que isso aconteça, deverá **deixar todos os outros serviços de autenticação desmarcados**.</span><span class="sxs-lookup"><span data-stu-id="7b691-211">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="7b691-212">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="7b691-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7b691-213">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, simplesmente clique na guia **Logon Único** e acesse a documentação inserida através da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7b691-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7b691-214">Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b691-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7b691-215">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7b691-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="7b691-216">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7b691-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7b691-218">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7b691-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7b691-219">No painel de navegação esquerdo no **Portal do Azure**, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7b691-219">On the left navigation pane in the **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b691-221">Vá para **Usuários e Grupos** e clique em **Todos os Usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7b691-221">To display the list of users, Go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b691-223">Na parte superior da caixa de diálogo, clique em **Adicionar** para abrir a caixa de diálogo **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="7b691-223">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b691-225">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7b691-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b691-227">a.</span><span class="sxs-lookup"><span data-stu-id="7b691-227">a.</span></span> <span data-ttu-id="7b691-228">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="7b691-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b691-229">b.</span><span class="sxs-lookup"><span data-stu-id="7b691-229">b.</span></span> <span data-ttu-id="7b691-230">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7b691-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7b691-231">c.</span><span class="sxs-lookup"><span data-stu-id="7b691-231">c.</span></span> <span data-ttu-id="7b691-232">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="7b691-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7b691-233">d.</span><span class="sxs-lookup"><span data-stu-id="7b691-233">d.</span></span> <span data-ttu-id="7b691-234">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7b691-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="7b691-235">Criar um usuário de teste do Salesforce</span><span class="sxs-lookup"><span data-stu-id="7b691-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="7b691-236">Nesta seção, é criado um usuário denominado Brenda Fernandes no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7b691-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="7b691-237">O Salesforce dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="7b691-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="7b691-238">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="7b691-238">There is no action item for you in this section.</span></span> <span data-ttu-id="7b691-239">Se um usuário ainda não existir no Salesforce, um novo será criado quando você tentar acessar o Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7b691-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7b691-240">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7b691-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7b691-241">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7b691-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7b691-243">**Para atribuir Brenda Fernandes ao Salesforce, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7b691-243">**To assign Britta Simon to Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="7b691-244">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7b691-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7b691-246">Na lista de aplicativos, selecione **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="7b691-246">In the applications list, select **Salesforce**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="7b691-248">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7b691-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7b691-250">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7b691-250">Click **Add** button.</span></span> <span data-ttu-id="7b691-251">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b691-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7b691-253">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7b691-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7b691-254">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b691-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b691-255">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b691-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7b691-256">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7b691-256">Testing single sign-on</span></span>

<span data-ttu-id="7b691-257">Para testar suas configurações de logon único, abra o Painel de Acesso em [https://myapps.microsoft.com](https://myapps.microsoft.com/), depois entre na conta de teste e clique em **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="7b691-257">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b691-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7b691-258">Additional resources</span></span>

* [<span data-ttu-id="7b691-259">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7b691-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b691-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b691-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7b691-261">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="7b691-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

