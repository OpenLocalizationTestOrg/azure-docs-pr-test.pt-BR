---
title: "Tutorial: integração do Azure Active Directory com o Jobscience | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 66bec35a8f17482433dbf02827b90620d1cff378
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="ba620-103">Tutorial: Integração do Active Directory do Azure com o Jobscience</span><span class="sxs-lookup"><span data-stu-id="ba620-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="ba620-104">Neste tutorial, você aprende a integrar o Jobscience ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ba620-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba620-105">A integração do Jobscience ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="ba620-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ba620-106">No Azure AD, é possível controlar quem tem acesso ao Jobscience</span><span class="sxs-lookup"><span data-stu-id="ba620-106">You can control in Azure AD who has access to Jobscience</span></span>
- <span data-ttu-id="ba620-107">É possível permitir que os usuários se conectem automaticamente ao Jobscience (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba620-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ba620-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ba620-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ba620-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ba620-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba620-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ba620-110">Prerequisites</span></span>

<span data-ttu-id="ba620-111">Para configurar a integração do Azure AD ao Jobscience, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ba620-111">To configure Azure AD integration with Jobscience, you need the following items:</span></span>

- <span data-ttu-id="ba620-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ba620-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba620-113">Uma assinatura habilitada para logon único do Jobscience</span><span class="sxs-lookup"><span data-stu-id="ba620-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba620-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ba620-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba620-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ba620-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba620-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ba620-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba620-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba620-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba620-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ba620-118">Scenario description</span></span>
<span data-ttu-id="ba620-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ba620-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ba620-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="ba620-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba620-121">Adicionando o Jobscience por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="ba620-121">Adding Jobscience from the gallery</span></span>
2. <span data-ttu-id="ba620-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ba620-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-the-gallery"></a><span data-ttu-id="ba620-123">Adicionando o Jobscience por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="ba620-123">Adding Jobscience from the gallery</span></span>
<span data-ttu-id="ba620-124">Para configurar a integração do Jobscience ao Azure AD, é necessário adicionar o Jobscience à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="ba620-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ba620-125">**Para adicionar o Jobscience por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ba620-125">**To add Jobscience from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ba620-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ba620-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ba620-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ba620-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ba620-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ba620-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ba620-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba620-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ba620-133">Na caixa de pesquisa, digite **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="ba620-133">In the search box, type **Jobscience**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="ba620-135">No painel de resultados, selecione **Jobscience** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba620-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ba620-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ba620-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ba620-138">Nesta seção, você configura e testa o logon único do Azure AD com o Jobscience, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ba620-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ba620-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Jobscience é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba620-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span></span> <span data-ttu-id="ba620-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ba620-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span></span>

<span data-ttu-id="ba620-141">No Jobscience, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="ba620-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ba620-142">Para configurar e testar o logon único do Azure AD com o Jobscience, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="ba620-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ba620-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ba620-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ba620-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ba620-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba620-145">**[Criando um usuário de teste do Jobscience](#creating-a-jobscience-test-user)** – para ter um equivalente de Brenda Fernandes no Jobscience que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba620-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ba620-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba620-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ba620-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="ba620-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ba620-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba620-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ba620-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ba620-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="ba620-150">**Para configurar o logon único do Azure AD com o Jobscience, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ba620-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="ba620-151">No portal do Azure, na página de integração do aplicativo **Jobscience**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="ba620-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ba620-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ba620-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="ba620-155">Na seção **Domínio e URLs do Jobscience**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ba620-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="ba620-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="ba620-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ba620-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="ba620-158">This value is not real.</span></span> <span data-ttu-id="ba620-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="ba620-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ba620-160">Obtenha esse valor com a [equipe de suporte ao Cliente do Jobscience](https://www.jobscience.com/support) ou no perfil de SSO que você criará, explicado adiante no tutorial.</span><span class="sxs-lookup"><span data-stu-id="ba620-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span></span> 
 
4. <span data-ttu-id="ba620-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ba620-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="ba620-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ba620-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ba620-165">Na seção **Configuração do Jobscience**, clique em **Configurar o Jobscience** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="ba620-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ba620-166">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="ba620-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="ba620-168">Faça logon no site da sua empresa Jobscience como um administrador.</span><span class="sxs-lookup"><span data-stu-id="ba620-168">Log in to your Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="ba620-169">Vá para **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="ba620-169">Go to **Setup**.</span></span>
   
   <span data-ttu-id="ba620-170">![Configuração](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="ba620-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="ba620-171">No painel de navegação à esquerda, na seção **Administrador**, clique em **Gerenciamento de Domínio** para expandir a seção correspondente e clique em **Meu Domínio** para abrir a página **Meu Domínio**.</span><span class="sxs-lookup"><span data-stu-id="ba620-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="ba620-172">![Meu Domínio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="ba620-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="ba620-173">Para confirmar se o domínio foi configurado corretamente, verifique se ele está em “**Etapa 4 Implantado nos Usuários**” e examine “**Minhas Configurações de Domínio**”.</span><span class="sxs-lookup"><span data-stu-id="ba620-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="ba620-174">![Domínio Implantado no Usuário](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domínio Implantado no Usuário")</span><span class="sxs-lookup"><span data-stu-id="ba620-174">![Domain Deployed to User](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="ba620-175">No site de empresa do Jobscience, clique em **Controles de Segurança** e clique em **Configurações de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="ba620-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="ba620-176">![Controles de Segurança](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Controles de Segurança")</span><span class="sxs-lookup"><span data-stu-id="ba620-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="ba620-177">Na seção **Configurações de Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ba620-177">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="ba620-178">![Configurações de Logon Único](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="ba620-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="ba620-179">a.</span><span class="sxs-lookup"><span data-stu-id="ba620-179">a.</span></span> <span data-ttu-id="ba620-180">Selecione **SAML Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="ba620-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="ba620-181">b.</span><span class="sxs-lookup"><span data-stu-id="ba620-181">b.</span></span> <span data-ttu-id="ba620-182">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="ba620-182">Click **New**.</span></span>

13. <span data-ttu-id="ba620-183">No diálogo **Editar Configuração de Logon Único do SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ba620-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="ba620-184">![Configurações de Logon Único do SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Configurações de Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="ba620-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="ba620-185">a.</span><span class="sxs-lookup"><span data-stu-id="ba620-185">a.</span></span> <span data-ttu-id="ba620-186">Na caixa de texto **Nome** , digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="ba620-186">In the **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="ba620-187">b.</span><span class="sxs-lookup"><span data-stu-id="ba620-187">b.</span></span> <span data-ttu-id="ba620-188">Na caixa de texto **Emissor**, cole o valor da **ID da Entidade SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba620-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ba620-189">c.</span><span class="sxs-lookup"><span data-stu-id="ba620-189">c.</span></span> <span data-ttu-id="ba620-190">Na caixa de texto **ID da Entidade**, digite `https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="ba620-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="ba620-191">d.</span><span class="sxs-lookup"><span data-stu-id="ba620-191">d.</span></span> <span data-ttu-id="ba620-192">Clique em **Procurar** para carregar o certificado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba620-192">Click **Browse** to upload your Azure AD certificate.</span></span>

    <span data-ttu-id="ba620-193">e.</span><span class="sxs-lookup"><span data-stu-id="ba620-193">e.</span></span> <span data-ttu-id="ba620-194">Para o **Tipo de Identidade SAML**, selecione **A declaração contém a ID de Federação do objeto de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="ba620-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>

    <span data-ttu-id="ba620-195">f.</span><span class="sxs-lookup"><span data-stu-id="ba620-195">f.</span></span> <span data-ttu-id="ba620-196">Para **Local de Identidade do SAML**, selecione **A identidade está contida no elemento NameIdentifier da instrução Subject**.</span><span class="sxs-lookup"><span data-stu-id="ba620-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>

    <span data-ttu-id="ba620-197">g.</span><span class="sxs-lookup"><span data-stu-id="ba620-197">g.</span></span> <span data-ttu-id="ba620-198">Na caixa de texto **URL de Logon do Provedor de Identidade**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba620-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ba620-199">h.</span><span class="sxs-lookup"><span data-stu-id="ba620-199">h.</span></span> <span data-ttu-id="ba620-200">Na caixa de texto **URL de Logoff do Provedor de Identidade**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba620-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ba620-201">i.</span><span class="sxs-lookup"><span data-stu-id="ba620-201">i.</span></span> <span data-ttu-id="ba620-202">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ba620-202">Click **Save**.</span></span>

14. <span data-ttu-id="ba620-203">No painel de navegação à esquerda, na seção **Administrador**, clique em **Gerenciamento de Domínio** para expandir a seção correspondente e clique em **Meu Domínio** para abrir a página **Meu Domínio**.</span><span class="sxs-lookup"><span data-stu-id="ba620-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="ba620-204">![Meu Domínio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="ba620-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="ba620-205">Na página **Meu Domínio**, na seção **Identidade Visual da Página de Logon**, clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="ba620-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="ba620-206">![Identidade Visual da Página de Logon](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Identidade Visual da Página de Logon")</span><span class="sxs-lookup"><span data-stu-id="ba620-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="ba620-207">Na página **Identidade Visual da Página de Logon**, na seção **Serviço de Autenticação**, o nome das **Configurações de SSO do SAML** é exibido.</span><span class="sxs-lookup"><span data-stu-id="ba620-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="ba620-208">Selecione-o e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ba620-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="ba620-209">![Identidade Visual da Página de Logon](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Identidade Visual da Página de Logon")</span><span class="sxs-lookup"><span data-stu-id="ba620-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="ba620-210">Para obter a URL de Logon Único iniciada pelo SP, clique em **Configurações de Logon Único** na seção do menu **Controles de Segurança**.</span><span class="sxs-lookup"><span data-stu-id="ba620-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

    <span data-ttu-id="ba620-211">![Controles de Segurança](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Controles de Segurança")</span><span class="sxs-lookup"><span data-stu-id="ba620-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="ba620-212">Clique no perfil SSO que você criou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="ba620-212">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="ba620-213">Essa página mostra a URL de Logon Único de sua empresa (por exemplo, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid)).</span><span class="sxs-lookup"><span data-stu-id="ba620-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="ba620-214">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="ba620-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ba620-215">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ba620-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ba620-216">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ba620-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ba620-217">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ba620-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="ba620-218">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ba620-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ba620-220">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ba620-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ba620-221">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ba620-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ba620-223">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ba620-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ba620-225">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ba620-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ba620-227">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ba620-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ba620-229">a.</span><span class="sxs-lookup"><span data-stu-id="ba620-229">a.</span></span> <span data-ttu-id="ba620-230">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="ba620-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba620-231">b.</span><span class="sxs-lookup"><span data-stu-id="ba620-231">b.</span></span> <span data-ttu-id="ba620-232">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ba620-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ba620-233">c.</span><span class="sxs-lookup"><span data-stu-id="ba620-233">c.</span></span> <span data-ttu-id="ba620-234">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="ba620-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ba620-235">d.</span><span class="sxs-lookup"><span data-stu-id="ba620-235">d.</span></span> <span data-ttu-id="ba620-236">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ba620-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="ba620-237">Criando um usuário de teste do Jobscience</span><span class="sxs-lookup"><span data-stu-id="ba620-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="ba620-238">Para permitir que os usuários do Azure AD façam logon no Jobscience, eles devem ser provisionados no Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ba620-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="ba620-239">No caso do Jobscience, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="ba620-239">In the case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="ba620-240">Você pode usar qualquer outra ferramenta de criação de conta de usuário do Jobscience ou as APIs fornecidas pelo Jobscience para provisionar contas de usuário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ba620-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="ba620-241">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ba620-241">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="ba620-242">Faça logon em seu site de empresa do **Jobscience** como administrador.</span><span class="sxs-lookup"><span data-stu-id="ba620-242">Log in to your **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="ba620-243">Vá para a Configuração.</span><span class="sxs-lookup"><span data-stu-id="ba620-243">Go to Setup.</span></span>
   
   <span data-ttu-id="ba620-244">![Configuração](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="ba620-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="ba620-245">Vá para **Gerenciar Usuários \> Usuários**.</span><span class="sxs-lookup"><span data-stu-id="ba620-245">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="ba620-246">![Usuários](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="ba620-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="ba620-247">Clique em **Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="ba620-247">Click **New User**.</span></span>
   
   <span data-ttu-id="ba620-248">![Todos os Usuários](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Todos os Usuários")</span><span class="sxs-lookup"><span data-stu-id="ba620-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="ba620-249">No diálogo **Editar Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ba620-249">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="ba620-250">![Editar Usuário](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Editar Usuário")</span><span class="sxs-lookup"><span data-stu-id="ba620-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="ba620-251">a.</span><span class="sxs-lookup"><span data-stu-id="ba620-251">a.</span></span> <span data-ttu-id="ba620-252">Na caixa de texto **Nome**, digite um nome do usuário, como Brenda.</span><span class="sxs-lookup"><span data-stu-id="ba620-252">In the **First Name** textbox, type a first name of the user like Britta.</span></span>
   
   <span data-ttu-id="ba620-253">b.</span><span class="sxs-lookup"><span data-stu-id="ba620-253">b.</span></span> <span data-ttu-id="ba620-254">Na caixa de texto **Sobrenome**, digite um sobrenome do usuário, como Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ba620-254">In the **Last Name** textbox, type a last name of the user like Simon.</span></span>
   
   <span data-ttu-id="ba620-255">c.</span><span class="sxs-lookup"><span data-stu-id="ba620-255">c.</span></span> <span data-ttu-id="ba620-256">Na caixa de texto **Alias**, digite um nome de alias do usuário, como brendaf.</span><span class="sxs-lookup"><span data-stu-id="ba620-256">In the **Alias** textbox, type an alias name of the user like brittas.</span></span>

   <span data-ttu-id="ba620-257">d.</span><span class="sxs-lookup"><span data-stu-id="ba620-257">d.</span></span> <span data-ttu-id="ba620-258">Na caixa de texto **Email**, digite o endereço de email do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ba620-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="ba620-259">e.</span><span class="sxs-lookup"><span data-stu-id="ba620-259">e.</span></span> <span data-ttu-id="ba620-260">Na caixa de texto **Nome de Usuário**, digite um nome de usuário do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ba620-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="ba620-261">f.</span><span class="sxs-lookup"><span data-stu-id="ba620-261">f.</span></span> <span data-ttu-id="ba620-262">Na caixa de texto **Apelido**, digite um apelido do usuário, como Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ba620-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="ba620-263">g.</span><span class="sxs-lookup"><span data-stu-id="ba620-263">g.</span></span> <span data-ttu-id="ba620-264">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ba620-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="ba620-265">O titular da conta do Azure Active Directory recebe um email e segue um link para confirmar sua conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="ba620-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ba620-266">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ba620-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ba620-267">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ba620-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ba620-269">**Para atribuir Brenda Fernandes ao Jobscience, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ba620-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="ba620-270">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ba620-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ba620-272">Na lista de aplicativos, selecione **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="ba620-272">In the applications list, select **Jobscience**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="ba620-274">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ba620-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ba620-276">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ba620-276">Click **Add** button.</span></span> <span data-ttu-id="ba620-277">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ba620-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ba620-279">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ba620-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ba620-280">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ba620-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba620-281">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ba620-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ba620-282">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ba620-282">Testing single sign-on</span></span>

<span data-ttu-id="ba620-283">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="ba620-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ba620-284">Quando você clicar no bloco do Jobscience no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ba620-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span></span>
<span data-ttu-id="ba620-285">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ba620-285">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ba620-286">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ba620-286">Additional resources</span></span>

* [<span data-ttu-id="ba620-287">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ba620-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba620-288">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ba620-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

