---
title: "Tutorial: integração do Azure Active Directory com o TalentLMS | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: f28d6fbfad9dae578a20db7218b7e3b174ed859c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="a96ba-103">Tutorial: integração do Azure Active Directory com o TalentLMS</span><span class="sxs-lookup"><span data-stu-id="a96ba-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="a96ba-104">Neste tutorial, você aprenderá a integrar o TalentLMS ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a96ba-104">In this tutorial, you learn how to integrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a96ba-105">A integração do TalentLMS com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a96ba-105">Integrating TalentLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a96ba-106">No Azure AD, é possível controlar quem tem acesso ao TalentLMS</span><span class="sxs-lookup"><span data-stu-id="a96ba-106">You can control in Azure AD who has access to TalentLMS</span></span>
- <span data-ttu-id="a96ba-107">É possível permitir que seus usuários entrem automaticamente no TalentLMS (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a96ba-107">You can enable your users to automatically get signed-on to TalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a96ba-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a96ba-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a96ba-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a96ba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a96ba-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a96ba-110">Prerequisites</span></span>

<span data-ttu-id="a96ba-111">Para configurar a integração do Azure AD com o TalentLMS, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a96ba-111">To configure Azure AD integration with TalentLMS, you need the following items:</span></span>

- <span data-ttu-id="a96ba-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a96ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a96ba-113">Uma assinatura habilitada para logon único do TalentLMS</span><span class="sxs-lookup"><span data-stu-id="a96ba-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a96ba-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a96ba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a96ba-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a96ba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a96ba-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a96ba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a96ba-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a96ba-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a96ba-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a96ba-118">Scenario description</span></span>
<span data-ttu-id="a96ba-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a96ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a96ba-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a96ba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a96ba-121">Adicionar o TalentLMS da galeria</span><span class="sxs-lookup"><span data-stu-id="a96ba-121">Adding TalentLMS from the gallery</span></span>
2. <span data-ttu-id="a96ba-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a96ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-the-gallery"></a><span data-ttu-id="a96ba-123">Adicionar o TalentLMS da galeria</span><span class="sxs-lookup"><span data-stu-id="a96ba-123">Adding TalentLMS from the gallery</span></span>
<span data-ttu-id="a96ba-124">Para configurar a integração do TalentLMS com o Azure AD, é necessário adicionar o TalentLMS da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a96ba-124">To configure the integration of TalentLMS into Azure AD, you need to add TalentLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a96ba-125">**Para adicionar o TalentLMS da galeria, siga as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a96ba-125">**To add TalentLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a96ba-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a96ba-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a96ba-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a96ba-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a96ba-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a96ba-133">Na caixa de pesquisa, digite **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-133">In the search box, type **TalentLMS**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="a96ba-135">No painel de resultados, selecione **TalentLMS** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a96ba-135">In the results panel, select **TalentLMS**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a96ba-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a96ba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a96ba-138">Nesta seção, você configurará e testará o logon único do Azure AD com o TalentLMS, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="a96ba-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a96ba-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do TalentLMS é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a96ba-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TalentLMS is to a user in Azure AD.</span></span> <span data-ttu-id="a96ba-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="a96ba-140">In other words, a link relationship between an Azure AD user and the related user in TalentLMS needs to be established.</span></span>

<span data-ttu-id="a96ba-141">No TalentLMS, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="a96ba-141">In TalentLMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a96ba-142">Para configurar e testar o logon único do Azure AD com o TalentLMS, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="a96ba-142">To configure and test Azure AD single sign-on with TalentLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a96ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a96ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a96ba-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a96ba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a96ba-145">**[Criação de um usuário de teste do TalentLMS](#creating-a-talentlms-test-user)** – para ter um equivalente de Brenda Fernandes no TalentLMS que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a96ba-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - to have a counterpart of Britta Simon in TalentLMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a96ba-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a96ba-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a96ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="a96ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a96ba-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a96ba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a96ba-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="a96ba-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="a96ba-150">**Para configurar o logon único do Azure AD com o TalentLMS, siga as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a96ba-150">**To configure Azure AD single sign-on with TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="a96ba-151">No Portal do Azure, na página de integração de aplicativos do **TalentLMS**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-151">In the Azure portal, on the **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a96ba-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a96ba-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="a96ba-155">Na seção **URLs e Domínio do TalentLMS**, siga as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a96ba-155">On the **TalentLMS Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="a96ba-157">a.</span><span class="sxs-lookup"><span data-stu-id="a96ba-157">a.</span></span> <span data-ttu-id="a96ba-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="a96ba-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="a96ba-159">b.</span><span class="sxs-lookup"><span data-stu-id="a96ba-159">b.</span></span> <span data-ttu-id="a96ba-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="a96ba-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a96ba-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="a96ba-161">These values are not real.</span></span> <span data-ttu-id="a96ba-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="a96ba-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a96ba-163">Contate a [equipe de suporte ao Cliente do TalentLMS](https://www.talentlms.com/contact) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="a96ba-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="a96ba-164">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="a96ba-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="a96ba-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a96ba-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a96ba-168">Na seção **Configuração do TalentLMS**, clique em **Configurar o TalentLMS** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-168">On the **TalentLMS Configuration** section, click **Configure TalentLMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a96ba-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="a96ba-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="a96ba-171">Em outra janela do navegador da Web, faça logon em seu site da empresa TalentLMS como administrador.</span><span class="sxs-lookup"><span data-stu-id="a96ba-171">In a different web browser window, log in to your TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="a96ba-172">Na seção **Conta e Configurações**, clique na guia **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-172">In the **Account & Settings** section, click the **Users** tab.</span></span>
   
    <span data-ttu-id="a96ba-173">![Conta e Configurações](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Conta e Configurações")</span><span class="sxs-lookup"><span data-stu-id="a96ba-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="a96ba-174">Clique em **SSO (Logon Único)**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="a96ba-175">Na seção de Configurações de Logon Único, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a96ba-175">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="a96ba-176">![Logon Único](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="a96ba-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="a96ba-177">a.</span><span class="sxs-lookup"><span data-stu-id="a96ba-177">a.</span></span> <span data-ttu-id="a96ba-178">Na lista **Tipo de integração de SSO**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-178">From the **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="a96ba-179">b.</span><span class="sxs-lookup"><span data-stu-id="a96ba-179">b.</span></span> <span data-ttu-id="a96ba-180">Na caixa de texto **IDP (Provedor de Identidade)**, cole o valor da **ID da entidade SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a96ba-180">In the **Identity provider (IDP)** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="a96ba-181">c.</span><span class="sxs-lookup"><span data-stu-id="a96ba-181">c.</span></span> <span data-ttu-id="a96ba-182">Cole o valor da **Impressão digital** do Portal do Azure na caixa de texto **Impressão digital do certificado**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-182">Paste the **Thumbprint** value from Azure portal into the **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="a96ba-183">d.</span><span class="sxs-lookup"><span data-stu-id="a96ba-183">d.</span></span>  <span data-ttu-id="a96ba-184">Na caixa de texto **URL de Entrada Remota**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a96ba-184">In the **Remote sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="a96ba-185">e.</span><span class="sxs-lookup"><span data-stu-id="a96ba-185">e.</span></span> <span data-ttu-id="a96ba-186">Na caixa de texto **URL de Saída Remota**, cole o valor da **URL de Saída** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a96ba-186">In the **Remote sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a96ba-187">f.</span><span class="sxs-lookup"><span data-stu-id="a96ba-187">f.</span></span> <span data-ttu-id="a96ba-188">Preencha o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a96ba-188">Fill in the following:</span></span> 

    * <span data-ttu-id="a96ba-189">Na caixa de texto **TargetedID**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="a96ba-189">In the **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="a96ba-190">Na caixa de texto **Nome**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="a96ba-190">In the **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="a96ba-191">Na caixa de texto **Sobrenome**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="a96ba-191">In the **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="a96ba-192">Na caixa de texto **Email**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="a96ba-192">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="a96ba-193">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="a96ba-194">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="a96ba-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a96ba-195">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a96ba-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a96ba-196">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a96ba-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a96ba-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a96ba-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="a96ba-198">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a96ba-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a96ba-200">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a96ba-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a96ba-201">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a96ba-203">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a96ba-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a96ba-205">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a96ba-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a96ba-207">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a96ba-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a96ba-209">a.</span><span class="sxs-lookup"><span data-stu-id="a96ba-209">a.</span></span> <span data-ttu-id="a96ba-210">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a96ba-211">b.</span><span class="sxs-lookup"><span data-stu-id="a96ba-211">b.</span></span> <span data-ttu-id="a96ba-212">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a96ba-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a96ba-213">c.</span><span class="sxs-lookup"><span data-stu-id="a96ba-213">c.</span></span> <span data-ttu-id="a96ba-214">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a96ba-215">d.</span><span class="sxs-lookup"><span data-stu-id="a96ba-215">d.</span></span> <span data-ttu-id="a96ba-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="a96ba-217">Criação de um usuário de teste do TalentLMS</span><span class="sxs-lookup"><span data-stu-id="a96ba-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="a96ba-218">Para permitir que os usuários do Azure AD façam logon no TalentLMS, eles devem ser provisionados no TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="a96ba-218">To enable Azure AD users to log in to TalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="a96ba-219">No caso do TalentLMS, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="a96ba-219">In the case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="a96ba-220">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a96ba-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a96ba-221">Faça logon em seu locatário do **TalentLMS** .</span><span class="sxs-lookup"><span data-stu-id="a96ba-221">Log in to your **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="a96ba-222">Clique em **Usuários** e em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="a96ba-223">Na página do diálogo **Adicionar usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a96ba-223">On the **Add user** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="a96ba-224">![Adicionar Usuário](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="a96ba-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="a96ba-225">a.</span><span class="sxs-lookup"><span data-stu-id="a96ba-225">a.</span></span> <span data-ttu-id="a96ba-226">Na caixa de texto **Nome**, digite o nome do usuário, como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-226">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="a96ba-227">b.</span><span class="sxs-lookup"><span data-stu-id="a96ba-227">b.</span></span> <span data-ttu-id="a96ba-228">Na caixa de texto **Sobrenome**, digite o sobrenome do usuário como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-228">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="a96ba-229">c.</span><span class="sxs-lookup"><span data-stu-id="a96ba-229">c.</span></span> <span data-ttu-id="a96ba-230">Na caixa de texto **Endereço de email**, insira o email do usuário como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-230">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="a96ba-231">d.</span><span class="sxs-lookup"><span data-stu-id="a96ba-231">d.</span></span> <span data-ttu-id="a96ba-232">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="a96ba-233">É possível usar qualquer outra ferramenta de criação da conta de usuário do TalentLMS ou as APIs fornecidas pelo TalentLMS para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="a96ba-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a96ba-234">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a96ba-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a96ba-235">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="a96ba-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TalentLMS.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a96ba-237">**Para atribuir Brenda Fernandes ao TalentLMS, siga as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a96ba-237">**To assign Britta Simon to TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="a96ba-238">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a96ba-240">Na lista de aplicativos, selecione **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-240">In the applications list, select **TalentLMS**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="a96ba-242">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a96ba-244">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a96ba-244">Click **Add** button.</span></span> <span data-ttu-id="a96ba-245">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a96ba-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a96ba-247">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a96ba-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a96ba-248">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a96ba-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a96ba-249">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a96ba-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a96ba-250">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a96ba-250">Testing single sign-on</span></span>

<span data-ttu-id="a96ba-251">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a96ba-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a96ba-252">Quando você clicar no bloco TalentLMS no Painel de Acesso, você deverá entrar automaticamente no seu aplicativo TalentLMS</span><span class="sxs-lookup"><span data-stu-id="a96ba-252">When you click the TalentLMS tile in the Access Panel, you should get automatically signed-on to your TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a96ba-253">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a96ba-253">Additional resources</span></span>

* [<span data-ttu-id="a96ba-254">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a96ba-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a96ba-255">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a96ba-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

