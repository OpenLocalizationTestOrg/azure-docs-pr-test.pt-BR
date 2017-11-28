---
title: "Tutorial: Integração do Azure Active Directory ao Sprinklr | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 6e1622cd55e3b0e8063604ac9dc0cb0673fa9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="36a7d-103">Tutorial: Integração do Active Directory do Azure com o Sprinklr</span><span class="sxs-lookup"><span data-stu-id="36a7d-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="36a7d-104">Neste tutorial, você aprenderá a integrar o Sprinklr ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="36a7d-104">In this tutorial, you learn how to integrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36a7d-105">A integração do Sprinklr ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="36a7d-105">Integrating Sprinklr with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="36a7d-106">No Azure AD, é possível controlar quem tem acesso ao Sprinklr</span><span class="sxs-lookup"><span data-stu-id="36a7d-106">You can control in Azure AD who has access to Sprinklr</span></span>
- <span data-ttu-id="36a7d-107">Você pode permitir que seus usuários façam logon automaticamente no Sprinklr (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="36a7d-107">You can enable your users to automatically get signed-on to Sprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36a7d-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="36a7d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="36a7d-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="36a7d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36a7d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="36a7d-110">Prerequisites</span></span>

<span data-ttu-id="36a7d-111">Para configurar a integração do Azure AD ao Sprinklr, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="36a7d-111">To configure Azure AD integration with Sprinklr, you need the following items:</span></span>

- <span data-ttu-id="36a7d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="36a7d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36a7d-113">Uma assinatura habilitada para logon único do Sprinklr</span><span class="sxs-lookup"><span data-stu-id="36a7d-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36a7d-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="36a7d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36a7d-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="36a7d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36a7d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="36a7d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36a7d-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36a7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36a7d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="36a7d-118">Scenario description</span></span>
<span data-ttu-id="36a7d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="36a7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36a7d-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="36a7d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36a7d-121">Adicionar o Sprinklr da galeria</span><span class="sxs-lookup"><span data-stu-id="36a7d-121">Adding Sprinklr from the gallery</span></span>
2. <span data-ttu-id="36a7d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="36a7d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-the-gallery"></a><span data-ttu-id="36a7d-123">Adicionar o Sprinklr da galeria</span><span class="sxs-lookup"><span data-stu-id="36a7d-123">Adding Sprinklr from the gallery</span></span>
<span data-ttu-id="36a7d-124">Para configurar a integração do Sprinklr ao Azure AD, você precisará adicionar o Sprinklr da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="36a7d-124">To configure the integration of Sprinklr into Azure AD, you need to add Sprinklr from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="36a7d-125">**Para adicionar o Sprinklr da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="36a7d-125">**To add Sprinklr from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="36a7d-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="36a7d-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="36a7d-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="36a7d-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36a7d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="36a7d-133">Na caixa de pesquisa, digite **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-133">In the search box, type **Sprinklr**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="36a7d-135">No painel de resultados, selecione **Sprinklr** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36a7d-135">In the results panel, select **Sprinklr**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="36a7d-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="36a7d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="36a7d-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Sprinklr, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="36a7d-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="36a7d-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Sprinklr é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36a7d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sprinklr is to a user in Azure AD.</span></span> <span data-ttu-id="36a7d-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="36a7d-140">In other words, a link relationship between an Azure AD user and the related user in Sprinklr needs to be established.</span></span>

<span data-ttu-id="36a7d-141">No Sprinklr, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="36a7d-141">In Sprinklr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="36a7d-142">Para configurar e testar o logon único do Azure AD com o Sprinklr, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="36a7d-142">To configure and test Azure AD single sign-on with Sprinklr, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="36a7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="36a7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="36a7d-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="36a7d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36a7d-145">**[Criação de um usuário de teste do Sprinklr](#creating-a-sprinklr-test-user)** – para ter um equivalente de Brenda Fernandes no Sprinklr que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36a7d-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - to have a counterpart of Britta Simon in Sprinklr that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="36a7d-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="36a7d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36a7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="36a7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="36a7d-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="36a7d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="36a7d-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="36a7d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="36a7d-150">**Para configurar o logon único do Azure AD com o Sprinklr, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="36a7d-150">**To configure Azure AD single sign-on with Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="36a7d-151">No portal do Azure, na página de integração de aplicativos do **Sprinklr**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-151">In the Azure portal, on the **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="36a7d-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="36a7d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="36a7d-155">Na seção **URLs e Domínio do Sprinklr**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="36a7d-155">On the **Sprinklr Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="36a7d-157">a.</span><span class="sxs-lookup"><span data-stu-id="36a7d-157">a.</span></span> <span data-ttu-id="36a7d-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="36a7d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="36a7d-159">b.</span><span class="sxs-lookup"><span data-stu-id="36a7d-159">b.</span></span> <span data-ttu-id="36a7d-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="36a7d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="36a7d-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="36a7d-161">These values are not real.</span></span> <span data-ttu-id="36a7d-162">Atualize esses valores com a URL de Logon e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="36a7d-162">Update the value with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="36a7d-163">Contate a [equipe de suporte do cliente Sprinklr](https://www.sprinklr.com/contact-us/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="36a7d-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="36a7d-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="36a7d-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="36a7d-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="36a7d-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="36a7d-168">Na seção **Configuração do Sprinklr**, clique em **Configurar Sprinklr** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-168">On the **Sprinklr Configuration** section, click **Configure Sprinklr** to open **Configure sign-on** window.</span></span> <span data-ttu-id="36a7d-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="36a7d-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

7. <span data-ttu-id="36a7d-170">Em outra janela do navegador da Web, faça logon em seu site de empresa do Sprinklr como um administrador.</span><span class="sxs-lookup"><span data-stu-id="36a7d-170">In a different web browser window, log in to your Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="36a7d-171">Vá para **Administração \> Configurações**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-171">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="36a7d-172">![Administração](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="36a7d-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="36a7d-173">Vá para **Gerenciar Parceiro \> Logon Único** no painel à esquerda.</span><span class="sxs-lookup"><span data-stu-id="36a7d-173">Go to **Manage Partner \> Single Sign** on from the left pane.</span></span>
   
    <span data-ttu-id="36a7d-174">![Gerenciar Parceiro](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Gerenciar Parceiro")</span><span class="sxs-lookup"><span data-stu-id="36a7d-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="36a7d-175">Clique em **+Adicionar Logons Únicos**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="36a7d-176">![Logons Únicos](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Logons Únicos")</span><span class="sxs-lookup"><span data-stu-id="36a7d-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="36a7d-177">Na página **Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="36a7d-177">On the **Single Sign on** page, perform the following steps:</span></span>
   
    <span data-ttu-id="36a7d-178">![Logons Únicos](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Logons Únicos")</span><span class="sxs-lookup"><span data-stu-id="36a7d-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="36a7d-179">a.</span><span class="sxs-lookup"><span data-stu-id="36a7d-179">a.</span></span> <span data-ttu-id="36a7d-180">Na caixa de texto **Nome**, digite um nome para a sua configuração (por exemplo: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="36a7d-180">In the **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="36a7d-181">b.</span><span class="sxs-lookup"><span data-stu-id="36a7d-181">b.</span></span> <span data-ttu-id="36a7d-182">Selecione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-182">Select **Enabled**.</span></span>

    <span data-ttu-id="36a7d-183">c.</span><span class="sxs-lookup"><span data-stu-id="36a7d-183">c.</span></span> <span data-ttu-id="36a7d-184">Selecione **Usar novo Certificado de SSO**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="36a7d-185">e.</span><span class="sxs-lookup"><span data-stu-id="36a7d-185">e.</span></span> <span data-ttu-id="36a7d-186">Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-186">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="36a7d-187">f.</span><span class="sxs-lookup"><span data-stu-id="36a7d-187">f.</span></span> <span data-ttu-id="36a7d-188">Cole a **ID de Entidade do SAML** copiada no portal do Azure para a caixa de texto **ID da Entidade**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-188">Paste the **SAML Entity ID** value which you have copied from Azure Portal into the **Entity Id** textbox.</span></span>

    <span data-ttu-id="36a7d-189">g.</span><span class="sxs-lookup"><span data-stu-id="36a7d-189">g.</span></span> <span data-ttu-id="36a7d-190">Na caixa de texto **URL de Logon do Provedor de Identidade**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="36a7d-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="36a7d-191">h.</span><span class="sxs-lookup"><span data-stu-id="36a7d-191">h.</span></span> <span data-ttu-id="36a7d-192">Na caixa de texto **URL de Logoff do Provedor de Identidade**, cole o valor da **URL de Saída** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="36a7d-192">Paste the **Sign-Out URL** value which you have copied from Azure Portal into the **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="36a7d-193">i.</span><span class="sxs-lookup"><span data-stu-id="36a7d-193">i.</span></span> <span data-ttu-id="36a7d-194">Para **Tipo de ID de Usuário do SAML**, selecione **A declaração contém o nome de usuário de sprinklr.com do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="36a7d-195">j.</span><span class="sxs-lookup"><span data-stu-id="36a7d-195">j.</span></span> <span data-ttu-id="36a7d-196">Para **Local da ID de Usuário do SAML**, selecione **A ID de Usuário está contida no elemento Identificador de Nome da instrução Subject**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-196">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span></span>

    <span data-ttu-id="36a7d-197">k.</span><span class="sxs-lookup"><span data-stu-id="36a7d-197">k.</span></span> <span data-ttu-id="36a7d-198">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-198">Click **Save**.</span></span>
       
    <span data-ttu-id="36a7d-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="36a7d-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="36a7d-200">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="36a7d-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="36a7d-201">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="36a7d-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="36a7d-202">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36a7d-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="36a7d-203">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="36a7d-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="36a7d-204">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="36a7d-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="36a7d-206">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="36a7d-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="36a7d-207">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="36a7d-209">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="36a7d-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="36a7d-211">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36a7d-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="36a7d-213">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="36a7d-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36a7d-215">a.</span><span class="sxs-lookup"><span data-stu-id="36a7d-215">a.</span></span> <span data-ttu-id="36a7d-216">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36a7d-217">b.</span><span class="sxs-lookup"><span data-stu-id="36a7d-217">b.</span></span> <span data-ttu-id="36a7d-218">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="36a7d-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36a7d-219">c.</span><span class="sxs-lookup"><span data-stu-id="36a7d-219">c.</span></span> <span data-ttu-id="36a7d-220">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="36a7d-221">d.</span><span class="sxs-lookup"><span data-stu-id="36a7d-221">d.</span></span> <span data-ttu-id="36a7d-222">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="36a7d-223">Criar um usuário de teste do Sprinklr</span><span class="sxs-lookup"><span data-stu-id="36a7d-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="36a7d-224">Faça logon em seu site de empresa do Sprinklr como um administrador.</span><span class="sxs-lookup"><span data-stu-id="36a7d-224">Log in to your Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="36a7d-225">Vá para **Administração \> Configurações**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-225">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="36a7d-226">![Administração](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="36a7d-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="36a7d-227">Vá para **Gerenciar Cliente \> Usuários** no painel à esquerda.</span><span class="sxs-lookup"><span data-stu-id="36a7d-227">Go to **Manage Client \> Users** from the left pane.</span></span>
   
    <span data-ttu-id="36a7d-228">![Configurações](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="36a7d-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="36a7d-229">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="36a7d-230">![Configurações](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="36a7d-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="36a7d-231">No diálogo **Editar usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="36a7d-231">On the **Edit user** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="36a7d-232">![Editar usuário](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Editar usuário")</span><span class="sxs-lookup"><span data-stu-id="36a7d-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="36a7d-233">a.</span><span class="sxs-lookup"><span data-stu-id="36a7d-233">a.</span></span> <span data-ttu-id="36a7d-234">Nas caixas de texto **Email**, **Nome** e **Sobrenome**, digite as informações de uma conta de usuário do Azure AD que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="36a7d-234">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span></span>

    <span data-ttu-id="36a7d-235">b.</span><span class="sxs-lookup"><span data-stu-id="36a7d-235">b.</span></span> <span data-ttu-id="36a7d-236">Selecione **Senha Desabilitada**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="36a7d-237">c.</span><span class="sxs-lookup"><span data-stu-id="36a7d-237">c.</span></span> <span data-ttu-id="36a7d-238">Selecione **Idioma**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-238">Select **Language**.</span></span>

    <span data-ttu-id="36a7d-239">d.</span><span class="sxs-lookup"><span data-stu-id="36a7d-239">d.</span></span> <span data-ttu-id="36a7d-240">Selecione **Tipo de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-240">Select **User Type**.</span></span>

    <span data-ttu-id="36a7d-241">e.</span><span class="sxs-lookup"><span data-stu-id="36a7d-241">e.</span></span> <span data-ttu-id="36a7d-242">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="36a7d-243">**Senha Desabilitada** deve ser marcada para permitir que um usuário faça logon por meio de um Provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="36a7d-243">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="36a7d-244">Vá para **Função**e realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="36a7d-244">Go to **Role**, and then perform the following steps:</span></span>
   
    <span data-ttu-id="36a7d-245">![Funções de Parceiro](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Funções de Parceiro")</span><span class="sxs-lookup"><span data-stu-id="36a7d-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="36a7d-246">a.</span><span class="sxs-lookup"><span data-stu-id="36a7d-246">a.</span></span> <span data-ttu-id="36a7d-247">Na lista **Global**, selecione **ALL\_Permissions**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-247">From the **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="36a7d-248">b.</span><span class="sxs-lookup"><span data-stu-id="36a7d-248">b.</span></span> <span data-ttu-id="36a7d-249">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="36a7d-250">Você pode usar qualquer outra ferramenta de criação da conta de usuário do Sprinklr ou APIs fornecidas pelo Sprinklr para provisionar contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="36a7d-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="36a7d-251">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="36a7d-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="36a7d-252">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="36a7d-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sprinklr.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="36a7d-254">**Para atribuir Brenda Fernandes ao Sprinklr, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="36a7d-254">**To assign Britta Simon to Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="36a7d-255">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="36a7d-257">Na lista de aplicativos, selecione **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-257">In the applications list, select **Sprinklr**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="36a7d-259">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="36a7d-261">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="36a7d-261">Click **Add** button.</span></span> <span data-ttu-id="36a7d-262">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36a7d-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="36a7d-264">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="36a7d-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="36a7d-265">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36a7d-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36a7d-266">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36a7d-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="36a7d-267">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="36a7d-267">Testing single sign-on</span></span>

<span data-ttu-id="36a7d-268">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="36a7d-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="36a7d-269">Quando clicar no bloco do Sprinklr no Painel de Acesso, você deverá ser automaticamente conectado ao seu aplicativo Sprinklr. Para obter mais informações sobre o Painel de Acesso, consulte [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="36a7d-269">When you click the Sprinklr tile in the Access Panel, you should get automatically signed-on to your Sprinklr application For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="36a7d-270">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="36a7d-270">Additional resources</span></span>

* [<span data-ttu-id="36a7d-271">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="36a7d-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36a7d-272">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="36a7d-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

