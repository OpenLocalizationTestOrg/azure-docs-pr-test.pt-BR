---
title: "Tutorial: integração do Azure Active Directory com o Zscaler Beta | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Zscaler Beta."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 72b4efc6b3bb58e63a399ab26c42984f070d9307
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a><span data-ttu-id="6d7f6-103">Tutorial: integração do Azure Active Directory com o Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="6d7f6-103">Tutorial: Azure Active Directory integration with Zscaler Beta</span></span>

<span data-ttu-id="6d7f6-104">Neste tutorial, você aprenderá como integrar o Zscaler Beta ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6d7f6-104">In this tutorial, you learn how to integrate Zscaler Beta with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d7f6-105">A integração do Zscaler Beta com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-105">Integrating Zscaler Beta with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6d7f6-106">No Azure AD, é possível controlar quem tem acesso ao Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="6d7f6-106">You can control in Azure AD who has access to Zscaler Beta</span></span>
- <span data-ttu-id="6d7f6-107">É possível permitir que seus usuários entrem automaticamente no Zscaler Beta (Logon Único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d7f6-107">You can enable your users to automatically get signed-on to Zscaler Beta (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6d7f6-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6d7f6-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d7f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d7f6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6d7f6-110">Prerequisites</span></span>

<span data-ttu-id="6d7f6-111">Para configurar a integração do Azure AD com o Zscaler Beta, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-111">To configure Azure AD integration with Zscaler Beta, you need the following items:</span></span>

- <span data-ttu-id="6d7f6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d7f6-113">Uma assinatura do Zscaler Beta habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="6d7f6-113">A Zscaler Beta single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6d7f6-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d7f6-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d7f6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d7f6-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d7f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d7f6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6d7f6-118">Scenario description</span></span>
<span data-ttu-id="6d7f6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d7f6-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d7f6-121">Adicionar o Zscaler Beta da galeria</span><span class="sxs-lookup"><span data-stu-id="6d7f6-121">Adding Zscaler Beta from the gallery</span></span>
2. <span data-ttu-id="6d7f6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-beta-from-the-gallery"></a><span data-ttu-id="6d7f6-123">Adicionar o Zscaler Beta da galeria</span><span class="sxs-lookup"><span data-stu-id="6d7f6-123">Adding Zscaler Beta from the gallery</span></span>
<span data-ttu-id="6d7f6-124">Para configurar a integração do Zscaler Beta com o Azure AD, é necessário adicionar o Zscaler Beta da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-124">To configure the integration of Zscaler Beta into Azure AD, you need to add Zscaler Beta from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6d7f6-125">**Para adicionar o Zscaler Beta da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="6d7f6-125">**To add Zscaler Beta from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6d7f6-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6d7f6-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6d7f6-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="6d7f6-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="6d7f6-133">Na caixa de pesquisa, digite **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-133">In the search box, type **Zscaler Beta**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

5. <span data-ttu-id="6d7f6-135">No painel de resultados, selecione **Zscaler Beta** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-135">In the results panel, select **Zscaler Beta**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6d7f6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6d7f6-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Zscaler Beta com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-138">In this section, you configure and test Azure AD single sign-on with Zscaler Beta based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6d7f6-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Zscaler Beta é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Beta is to a user in Azure AD.</span></span> <span data-ttu-id="6d7f6-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Beta needs to be established.</span></span>

<span data-ttu-id="6d7f6-141">No Zscaler Beta, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-141">In Zscaler Beta, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6d7f6-142">Para configurar e testar o logon único do Azure AD com o Zscaler Beta, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-142">To configure and test Azure AD single sign-on with Zscaler Beta, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6d7f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6d7f6-144">**[Definir configurações de proxy](#configuring-proxy-settings)** – para definir as configurações de proxy no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="6d7f6-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="6d7f6-145">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="6d7f6-146">**[Criação de um usuário de teste do Zscaler Beta](#creating-a-zscaler-beta-test-user)** – para ter um equivalente de Brenda Fernandes no Zscaler Beta que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-146">**[Creating a Zscaler Beta test user](#creating-a-zscaler-beta-test-user)** - to have a counterpart of Britta Simon in Zscaler Beta that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="6d7f6-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="6d7f6-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6d7f6-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d7f6-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6d7f6-150">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler Beta application.</span></span>

<span data-ttu-id="6d7f6-151">**Para configurar o logon único do Azure AD com o Zscaler Beta, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="6d7f6-151">**To configure Azure AD single sign-on with Zscaler Beta, perform the following steps:**</span></span>

1. <span data-ttu-id="6d7f6-152">No Portal do Azure, na página de integração de aplicativos do **Zscaler Beta**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-152">In the Azure portal, on the **Zscaler Beta** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="6d7f6-154">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

3. <span data-ttu-id="6d7f6-156">Na seção **URLs e Domínio do Zscaler Beta**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-156">On the **Zscaler Beta Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    <span data-ttu-id="6d7f6-158">Na caixa de texto URL de Entrada, digite a URL usada pelos usuários para entrar no aplicativo Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-158">In the Sign-on URL textbox, type the URL used by your users to sign-on to your Zscaler Beta application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6d7f6-159">Você precisa atualizar esse valor com a URL de Entrada real.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="6d7f6-160">Contate a [equipe de suporte ao cliente do Zscaler Beta](https://www.zscaler.com/company/contact) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-160">Contact [Zscaler Beta Client support team](https://www.zscaler.com/company/contact) to get this value.</span></span> 

4. <span data-ttu-id="6d7f6-161">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

5. <span data-ttu-id="6d7f6-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6d7f6-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6d7f6-165">Na seção **Configuração do Zscaler Beta**, clique em **Configurar o Zscaler Beta** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-165">On the **Zscaler Beta Configuration** section, click **Configure Zscaler Beta** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6d7f6-166">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="6d7f6-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

7. <span data-ttu-id="6d7f6-168">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa Zscaler Beta como administrador.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-168">In a different web browser window, log in to your Zscaler Beta company site as an administrator.</span></span>

8. <span data-ttu-id="6d7f6-169">No menu na parte superior, clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="6d7f6-170">![Administração](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-170">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="6d7f6-171">Em **Gerenciar Administradores e Funções**, clique em **Gerenciar Usuários e Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="6d7f6-172">![Gerenciar usuários e autenticação](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Gerenciar usuários e autenticação")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="6d7f6-173">Na seção **Escolher Opções de Autenticação para a sua Organização** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="6d7f6-174">![Autenticação](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Autenticação")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-174">![Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="6d7f6-175">a.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-175">a.</span></span> <span data-ttu-id="6d7f6-176">Selecione **Autenticar usando o Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="6d7f6-177">b.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-177">b.</span></span> <span data-ttu-id="6d7f6-178">Clique em **Configurar Parâmetros de Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="6d7f6-179">Na página da caixa de diálogo **Configurar Parâmetros de Logon Único do SAML**, execute as seguintes etapas e, em seguida, clique em **Concluído**</span><span class="sxs-lookup"><span data-stu-id="6d7f6-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="6d7f6-180">![Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-180">![Single Sign-On](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="6d7f6-181">a.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-181">a.</span></span> <span data-ttu-id="6d7f6-182">Cole o valor **URL do Serviço de Logon Único SAML**, copiado do Portal do Azure para a caixa de texto **URL do Portal SAML ao qual os usuários são enviados para autenticação**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-182">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="6d7f6-183">b.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-183">b.</span></span> <span data-ttu-id="6d7f6-184">Na caixa de texto **Atributo que contém o Nome de Logon**, digite **NameID**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="6d7f6-185">c.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-185">c.</span></span> <span data-ttu-id="6d7f6-186">Para carregar seu certificado baixado, clique em **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="6d7f6-187">d.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-187">d.</span></span> <span data-ttu-id="6d7f6-188">Selecione **Habilitar Provisionamento Automático do SAML**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="6d7f6-189">Na página de caixa de diálogo **Configurar Autenticação de Usuário** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="6d7f6-190">![Administração](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-190">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="6d7f6-191">a.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-191">a.</span></span> <span data-ttu-id="6d7f6-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-192">Click **Save**.</span></span>

    <span data-ttu-id="6d7f6-193">b.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-193">b.</span></span> <span data-ttu-id="6d7f6-194">Clique em **Ativar Agora**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="6d7f6-195">Definindo as configurações de proxy</span><span class="sxs-lookup"><span data-stu-id="6d7f6-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="6d7f6-196">Para definir as configurações de proxy no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="6d7f6-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="6d7f6-197">Inicie o **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="6d7f6-198">Selecione **Opções da Internet** no menu **Ferramentas** para abrir a caixa de diálogo **Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="6d7f6-199">![Opções da Internet](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Opções da Internet")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-199">![Internet Options](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="6d7f6-200">Clique na guia **Conexões** .</span><span class="sxs-lookup"><span data-stu-id="6d7f6-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="6d7f6-201">![Conexões](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Conexões")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-201">![Connections](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="6d7f6-202">Clique em **Configurações da LAN** para abrir a caixa de diálogo **Configurações da LAN**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="6d7f6-203">Na seção Servidor de proxy, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="6d7f6-204">![Servidor proxy](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Servidor proxy")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-204">![Proxy server](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="6d7f6-205">a.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-205">a.</span></span> <span data-ttu-id="6d7f6-206">Selecione **Usar um servidor proxy para LAN**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="6d7f6-207">b.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-207">b.</span></span> <span data-ttu-id="6d7f6-208">Na caixa de texto Endereço, digite **gateway.zscalerbeta.net**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-208">In the Address textbox, type **gateway.zscalerbeta.net**.</span></span>

    <span data-ttu-id="6d7f6-209">c.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-209">c.</span></span> <span data-ttu-id="6d7f6-210">Na caixa de texto Porta, digite **80**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="6d7f6-211">d.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-211">d.</span></span> <span data-ttu-id="6d7f6-212">Selecione **Ignorar servidor proxy para endereços locais**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="6d7f6-213">e.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-213">e.</span></span> <span data-ttu-id="6d7f6-214">Clique em **OK** para fechar a caixa de diálogo **Configurações da Rede Local (LAN)**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="6d7f6-215">Clique em **OK** para fechar a caixa de diálogo **Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-215">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="6d7f6-216">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="6d7f6-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6d7f6-217">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6d7f6-218">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6d7f6-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6d7f6-219">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f6-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="6d7f6-220">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="6d7f6-222">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6d7f6-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6d7f6-223">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6d7f6-225">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6d7f6-227">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6d7f6-229">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6d7f6-231">a.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-231">a.</span></span> <span data-ttu-id="6d7f6-232">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d7f6-233">b.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-233">b.</span></span> <span data-ttu-id="6d7f6-234">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6d7f6-235">c.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-235">c.</span></span> <span data-ttu-id="6d7f6-236">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6d7f6-237">d.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-237">d.</span></span> <span data-ttu-id="6d7f6-238">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-beta-test-user"></a><span data-ttu-id="6d7f6-239">Criação de um usuário de teste do Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="6d7f6-239">Creating a Zscaler Beta test user</span></span>

<span data-ttu-id="6d7f6-240">Para permitir que os usuários do Azure AD façam logon no Zscaler Beta, eles devem ser provisionados no Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-240">To enable Azure AD users to log in to Zscaler Beta, they must be provisioned to Zscaler Beta.</span></span> <span data-ttu-id="6d7f6-241">No caso do Zscaler Beta, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-241">In the case of Zscaler Beta, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="6d7f6-242">Para configurar o provisionamento de usuários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-242">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="6d7f6-243">Faça logon no seu locatário do **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-243">Log in to your **Zscaler Beta** tenant.</span></span>

2. <span data-ttu-id="6d7f6-244">Clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="6d7f6-245">![Administração](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-245">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="6d7f6-246">Clique em **Gerenciamento de Usuários**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="6d7f6-247">![Adicionar](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-247">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="6d7f6-248">Na guia **Usuários**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-248">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="6d7f6-249">![Adicionar](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-249">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="6d7f6-250">Na seção Adicionar Usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-250">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="6d7f6-251">![Adicionar Usuário](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="6d7f6-251">![Add User](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="6d7f6-252">a.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-252">a.</span></span> <span data-ttu-id="6d7f6-253">Digite **UserID**, **Nome de Exibição do Usuário**, **Senha**, **Confirmar Senha** e, em seguida, selecione **Grupos** e o **Departamento** de uma conta válida do Azure AD que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-253">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="6d7f6-254">b.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-254">b.</span></span> <span data-ttu-id="6d7f6-255">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="6d7f6-256">É possível usar qualquer outra ferramenta de criação de conta de usuário do Zscaler Beta ou APIs fornecidas pelo Zscaler Beta para provisionar as contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-256">You can use any other Zscaler Beta user account creation tools or APIs provided by Zscaler Beta to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6d7f6-257">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f6-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6d7f6-258">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler Beta.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="6d7f6-260">**Para atribuir Brenda Fernandes ao Zscaler Beta, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="6d7f6-260">**To assign Britta Simon to Zscaler Beta, perform the following steps:**</span></span>

1. <span data-ttu-id="6d7f6-261">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="6d7f6-263">Na lista de aplicativos, selecione **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-263">In the applications list, select **Zscaler Beta**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

3. <span data-ttu-id="6d7f6-265">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="6d7f6-267">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-267">Click **Add** button.</span></span> <span data-ttu-id="6d7f6-268">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="6d7f6-270">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6d7f6-271">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d7f6-272">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6d7f6-273">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="6d7f6-273">Testing single sign-on</span></span>

<span data-ttu-id="6d7f6-274">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6d7f6-275">Ao clicar no bloco Zscaler Beta no Painel de Acesso, você deverá entrar automaticamente no aplicativo Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-275">When you click the Zscaler Beta tile in the Access Panel, you should get automatically signed-on to your Zscaler Beta application.</span></span>
<span data-ttu-id="6d7f6-276">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6d7f6-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6d7f6-277">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6d7f6-277">Additional resources</span></span>

* [<span data-ttu-id="6d7f6-278">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f6-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d7f6-279">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6d7f6-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_203.png

