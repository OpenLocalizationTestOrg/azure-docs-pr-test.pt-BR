---
title: "Tutorial: integração do Azure Active Directory com o Adaptive Suite | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Adaptive Suite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 5d7ba2f4c7d814e3aaa1bf804ddc5030380ccb2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="999d2-103">Tutorial: Integração do Active Directory do Azure ao Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="999d2-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="999d2-104">Neste tutorial, você aprenderá a integrar o Adaptive Suite ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="999d2-104">In this tutorial, you learn how to integrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="999d2-105">A integração do Adaptive Suite ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="999d2-105">Integrating Adaptive Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="999d2-106">No Azure AD, é possível controlar quem tem acesso ao Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="999d2-106">You can control in Azure AD who has access to Adaptive Suite</span></span>
- <span data-ttu-id="999d2-107">Você pode habilitar seus usuários a fazer logon automaticamente no Adaptive Suite (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="999d2-107">You can enable your users to automatically get signed-on to Adaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="999d2-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="999d2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="999d2-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="999d2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="999d2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="999d2-110">Prerequisites</span></span>

<span data-ttu-id="999d2-111">Para configurar a integração do Azure AD com o Adaptive Suite, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="999d2-111">To configure Azure AD integration with Adaptive Suite, you need the following items:</span></span>

- <span data-ttu-id="999d2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="999d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="999d2-113">Uma assinatura habilitada para logon único do Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="999d2-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="999d2-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="999d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="999d2-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="999d2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="999d2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="999d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="999d2-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="999d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="999d2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="999d2-118">Scenario description</span></span>
<span data-ttu-id="999d2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="999d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="999d2-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="999d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="999d2-121">Adicionando o Adaptive Suite da galeria</span><span class="sxs-lookup"><span data-stu-id="999d2-121">Adding Adaptive Suite from the gallery</span></span>
2. <span data-ttu-id="999d2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="999d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-the-gallery"></a><span data-ttu-id="999d2-123">Adicionando o Adaptive Suite da galeria</span><span class="sxs-lookup"><span data-stu-id="999d2-123">Adding Adaptive Suite from the gallery</span></span>
<span data-ttu-id="999d2-124">Para configurar a integração do Adaptive Suite com o Azure AD, você precisa adicionar o Adaptive Suite por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="999d2-124">To configure the integration of Adaptive Suite into Azure AD, you need to add Adaptive Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="999d2-125">**Para adicionar o Adaptive Suite por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="999d2-125">**To add Adaptive Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="999d2-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="999d2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="999d2-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="999d2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="999d2-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="999d2-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="999d2-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="999d2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="999d2-133">Na caixa de pesquisa, digite **Adaptive Suite**.</span><span class="sxs-lookup"><span data-stu-id="999d2-133">In the search box, type **Adaptive Suite**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="999d2-135">No painel de resultados, selecione **Adaptive Suite** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="999d2-135">In the results panel, select **Adaptive Suite**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="999d2-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="999d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="999d2-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Adaptive Suite, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="999d2-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="999d2-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Adaptive Suite é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="999d2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adaptive Suite is to a user in Azure AD.</span></span> <span data-ttu-id="999d2-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="999d2-140">In other words, a link relationship between an Azure AD user and the related user in Adaptive Suite needs to be established.</span></span>

<span data-ttu-id="999d2-141">No Adaptive Suite, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="999d2-141">In Adaptive Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="999d2-142">Para configurar e testar o logon único do Azure AD com o Adaptive Suite, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="999d2-142">To configure and test Azure AD single sign-on with Adaptive Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="999d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="999d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="999d2-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="999d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="999d2-145">**[Criando um usuário de teste do Adaptive Suite](#creating-an-adaptive-suite-test-user)** – para ter um equivalente de Brenda Fernandes no Adaptive Suite que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="999d2-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - to have a counterpart of Britta Simon in Adaptive Suite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="999d2-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="999d2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="999d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="999d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="999d2-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="999d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="999d2-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="999d2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="999d2-150">**Para configurar o logon único do Azure AD com o Adaptive Suite, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="999d2-150">**To configure Azure AD single sign-on with Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="999d2-151">No Portal do Azure, na página de integração do aplicativo **Adaptive Suite**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="999d2-151">In the Azure portal, on the **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="999d2-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="999d2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="999d2-155">Na seção **URLs e Domínio do Adaptive Suite**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="999d2-155">On the **Adaptive Suite Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="999d2-157">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="999d2-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="999d2-158">Você pode obter esse valor na página **Configurações de SSO do SAML** do Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="999d2-158">You can get this value from the Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="999d2-159">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="999d2-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="999d2-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="999d2-161">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="999d2-163">Na seção **Configuração do Adaptive Suite**, clique em **Configurar o Adaptive Suite** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="999d2-163">On the **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="999d2-164">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="999d2-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="999d2-166">Em outra janela do navegador da Web, faça logon em seu site de empresa Adaptive Suite como administrador.</span><span class="sxs-lookup"><span data-stu-id="999d2-166">In a different web browser window, log in to your Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="999d2-167">Vá para **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="999d2-167">Go to **Admin**.</span></span>
   
    <span data-ttu-id="999d2-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="999d2-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="999d2-169">Na seção **Usuários e Funções**, clique em **Gerenciar Configurações de SSO do SAML**.</span><span class="sxs-lookup"><span data-stu-id="999d2-169">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="999d2-170">![Gerenciar Configurações de SSO do SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Gerenciar Configurações de SSO do SAML")</span><span class="sxs-lookup"><span data-stu-id="999d2-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="999d2-171">Na página **Configurações de SSO do SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="999d2-171">On the **SAML SSO Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="999d2-172">![Configurações de SSO do SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "Configurações de SSO do SAML")</span><span class="sxs-lookup"><span data-stu-id="999d2-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="999d2-173">a.</span><span class="sxs-lookup"><span data-stu-id="999d2-173">a.</span></span> <span data-ttu-id="999d2-174">Na caixa de texto **Nome do provedor de identidade** , digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="999d2-174">In the **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="999d2-175">b.</span><span class="sxs-lookup"><span data-stu-id="999d2-175">b.</span></span> <span data-ttu-id="999d2-176">Cole a **ID da Entidade SAML** copiada do Portal do Azure na caixa de texto **ID da entidade do provedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="999d2-176">Paste the **SAML Entity ID** value copied from Azure portal into the **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="999d2-177">c.</span><span class="sxs-lookup"><span data-stu-id="999d2-177">c.</span></span> <span data-ttu-id="999d2-178">Cole o valor da **URL de Entrada do Provedor de Identidade** copiado do Portal do Azure na caixa de texto **URL de SSO do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="999d2-178">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="999d2-179">d.</span><span class="sxs-lookup"><span data-stu-id="999d2-179">d.</span></span> <span data-ttu-id="999d2-180">Cole o valor da **URL de Entrada do Provedor de Identidade** copiado do Portal do Azure na caixa de texto **URL de Logoff Personalizado**.</span><span class="sxs-lookup"><span data-stu-id="999d2-180">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="999d2-181">e.</span><span class="sxs-lookup"><span data-stu-id="999d2-181">e.</span></span> <span data-ttu-id="999d2-182">Para carregar seu certificado baixado, clique em **Escolher arquivo**.</span><span class="sxs-lookup"><span data-stu-id="999d2-182">To upload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="999d2-183">f.</span><span class="sxs-lookup"><span data-stu-id="999d2-183">f.</span></span> <span data-ttu-id="999d2-184">Selecione as seguintes opções para:</span><span class="sxs-lookup"><span data-stu-id="999d2-184">Select the following, for:</span></span>
    * <span data-ttu-id="999d2-185">**ID de usuário do SAML**, selecione **Nome de usuário do Adaptive Insights do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="999d2-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="999d2-186">**Local da ID de usuário do SAML**, selecione **ID de usuário em NameID da Entidade**.</span><span class="sxs-lookup"><span data-stu-id="999d2-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="999d2-187">**Formato de NameID do SAML**, selecione **Endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="999d2-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="999d2-188">**Habilitar SAML**, selecione **Permitir SSO do SAML e direcionar logon do Adaptive Insights**.</span><span class="sxs-lookup"><span data-stu-id="999d2-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="999d2-189">g.</span><span class="sxs-lookup"><span data-stu-id="999d2-189">g.</span></span> <span data-ttu-id="999d2-190">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="999d2-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="999d2-191">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="999d2-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="999d2-192">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="999d2-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="999d2-193">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="999d2-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="999d2-194">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="999d2-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="999d2-195">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="999d2-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="999d2-197">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="999d2-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="999d2-198">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="999d2-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="999d2-200">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="999d2-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="999d2-202">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="999d2-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="999d2-204">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="999d2-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="999d2-206">a.</span><span class="sxs-lookup"><span data-stu-id="999d2-206">a.</span></span> <span data-ttu-id="999d2-207">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="999d2-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="999d2-208">b.</span><span class="sxs-lookup"><span data-stu-id="999d2-208">b.</span></span> <span data-ttu-id="999d2-209">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="999d2-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="999d2-210">c.</span><span class="sxs-lookup"><span data-stu-id="999d2-210">c.</span></span> <span data-ttu-id="999d2-211">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="999d2-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="999d2-212">d.</span><span class="sxs-lookup"><span data-stu-id="999d2-212">d.</span></span> <span data-ttu-id="999d2-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="999d2-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="999d2-214">Criando de um usuário de teste do Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="999d2-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="999d2-215">Para permitir que os usuários do Azure AD façam logon no Adaptive Suite, eles devem ser provisionados no Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="999d2-215">To enable Azure AD users to log in to Adaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="999d2-216">No caso do Adaptive Suite, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="999d2-216">In the case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="999d2-217">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="999d2-217">**To configure user provisioning, perform the following steps:**</span></span> 

1. <span data-ttu-id="999d2-218">Faça logon em seu site de empresa do **Adaptive Suite** como administrador.</span><span class="sxs-lookup"><span data-stu-id="999d2-218">Log in to your **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="999d2-219">Vá para **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="999d2-219">Go to **Admin**.</span></span>
   
   <span data-ttu-id="999d2-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="999d2-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="999d2-221">Na seção **Usuários e Funções**, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="999d2-221">In the **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="999d2-222">![Adicionar Usuário](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="999d2-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="999d2-223">Na seção **Novo Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="999d2-223">In the **New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="999d2-224">![Enviar](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Enviar")</span><span class="sxs-lookup"><span data-stu-id="999d2-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="999d2-225">a.</span><span class="sxs-lookup"><span data-stu-id="999d2-225">a.</span></span> <span data-ttu-id="999d2-226">Digite o **Nome**, **Logon**, **Email** e **Senha** de um usuário válido do Azure Active Directory que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="999d2-226">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span></span>
  
   <span data-ttu-id="999d2-227">b.</span><span class="sxs-lookup"><span data-stu-id="999d2-227">b.</span></span> <span data-ttu-id="999d2-228">Selecione uma **Função**.</span><span class="sxs-lookup"><span data-stu-id="999d2-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="999d2-229">c.</span><span class="sxs-lookup"><span data-stu-id="999d2-229">c.</span></span> <span data-ttu-id="999d2-230">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="999d2-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="999d2-231">É possível usar qualquer outra ferramenta de criação da conta de usuário do Adaptive Suite ou as APIs fornecidas pelo Adaptive Suite para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="999d2-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="999d2-232">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="999d2-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="999d2-233">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="999d2-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adaptive Suite.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="999d2-235">**Para atribuir Brenda Fernandes ao Adaptive Suite, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="999d2-235">**To assign Britta Simon to Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="999d2-236">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="999d2-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="999d2-238">Na lista de aplicativos, escolha **Adaptive Suite**.</span><span class="sxs-lookup"><span data-stu-id="999d2-238">In the applications list, select **Adaptive Suite**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="999d2-240">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="999d2-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="999d2-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="999d2-242">Click **Add** button.</span></span> <span data-ttu-id="999d2-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="999d2-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="999d2-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="999d2-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="999d2-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="999d2-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="999d2-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="999d2-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="999d2-248">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="999d2-248">Testing single sign-on</span></span>

<span data-ttu-id="999d2-249">O objetivo desta seção é testar sua configuração de logon único do Microsoft Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="999d2-249">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="999d2-250">Quando clica no bloco Adaptive Suite no Painel de Acesso, você deve ser conectado automaticamente ao seu aplicativo Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="999d2-250">When you click the Adaptive Suite tile in the Access Panel, you should get automatically signed-on to your Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="999d2-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="999d2-251">Additional resources</span></span>

* [<span data-ttu-id="999d2-252">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="999d2-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="999d2-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="999d2-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

