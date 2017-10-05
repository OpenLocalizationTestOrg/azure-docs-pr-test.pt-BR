---
title: "Tutorial: integração do Azure Active Directory com o Zscaler ZSCloud | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 2b6eb113e5725260bc04f50e9218939bf28b1ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="e147c-103">Tutorial: integração do Azure Active Directory com o Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="e147c-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="e147c-104">Neste tutorial, você aprenderá a integrar o Zscaler ZSCloud com o Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e147c-104">In this tutorial, you learn how to integrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e147c-105">A integração do Zscaler ZSCloud com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e147c-105">Integrating Zscaler ZSCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e147c-106">No Azure AD, é possível controlar quem tem acesso ao Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="e147c-106">You can control in Azure AD who has access to Zscaler ZSCloud</span></span>
- <span data-ttu-id="e147c-107">Você pode habilitar os usuários a entrar automaticamente no Zscaler ZSCloud (Logon Único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e147c-107">You can enable your users to automatically get signed-on to Zscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e147c-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e147c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e147c-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e147c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e147c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e147c-110">Prerequisites</span></span>

<span data-ttu-id="e147c-111">Para configurar a integração do Azure AD com o Zscaler ZSCloud, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e147c-111">To configure Azure AD integration with Zscaler ZSCloud, you need the following items:</span></span>

- <span data-ttu-id="e147c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e147c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e147c-113">Uma assinatura habilitada para logon único do Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="e147c-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e147c-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e147c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e147c-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e147c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e147c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e147c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e147c-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e147c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e147c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e147c-118">Scenario description</span></span>
<span data-ttu-id="e147c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e147c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e147c-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e147c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e147c-121">Adicionando o Zscaler ZSCloud por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="e147c-121">Adding Zscaler ZSCloud from the gallery</span></span>
2. <span data-ttu-id="e147c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e147c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-the-gallery"></a><span data-ttu-id="e147c-123">Adicionando o Zscaler ZSCloud por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="e147c-123">Adding Zscaler ZSCloud from the gallery</span></span>
<span data-ttu-id="e147c-124">Para configurar a integração do Zscaler ZSCloud ao Azure AD, você precisa adicionar o Zscaler ZSCloud da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e147c-124">To configure the integration of Zscaler ZSCloud into Azure AD, you need to add Zscaler ZSCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e147c-125">**Para adicionar o Zscaler ZSCloud da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e147c-125">**To add Zscaler ZSCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e147c-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e147c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e147c-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e147c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e147c-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e147c-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e147c-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e147c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e147c-133">Na caixa de pesquisa, digite **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="e147c-133">In the search box, type **Zscaler ZSCloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="e147c-135">No painel de resultados, selecione **Zscaler ZSCloud** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e147c-135">In the results panel, select **Zscaler ZSCloud**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e147c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e147c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e147c-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Zscaler ZSCloud, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e147c-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e147c-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Zscaler ZSCloud é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e147c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler ZSCloud is to a user in Azure AD.</span></span> <span data-ttu-id="e147c-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e147c-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler ZSCloud needs to be established.</span></span>

<span data-ttu-id="e147c-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e147c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="e147c-142">Para configurar e testar o logon único do Azure AD com o Zscaler ZSCloud, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e147c-142">To configure and test Azure AD single sign-on with Zscaler ZSCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e147c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e147c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e147c-144">**[Definir configurações de proxy](#configuring-proxy-settings)** – para definir as configurações de proxy no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="e147c-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="e147c-145">**[Criação de um usuário de teste do Azure AD](#creating-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e147c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e147c-146">**[Criar um usuário de teste do Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)** – para ter um equivalente de Brenda Fernandes no Zscaler ZSCloud que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e147c-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - to have a counterpart of Britta Simon in Zscaler ZSCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e147c-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e147c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e147c-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e147c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e147c-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e147c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e147c-150">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e147c-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="e147c-151">**Para configurar o logon único do Azure AD com o Zscaler ZSCloud, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e147c-151">**To configure Azure AD single sign-on with Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="e147c-152">No Portal do Azure, na página de integração de aplicativos do **Zscaler ZSCloud**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e147c-152">In the Azure portal, on the **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e147c-154">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e147c-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="e147c-156">Na seção **URLs e Domínio do Zscaler ZSCloud**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e147c-156">On the **Zscaler ZSCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="e147c-158">Na caixa de texto **URL de Entrada**, digite a URL usada pelos usuários para se conectar ao aplicativo ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e147c-158">In the **Sign-on URL** textbox, type the URL used by your users to sign-on to your ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="e147c-159">Você precisa atualizar esse valor com a URL de Entrada real.</span><span class="sxs-lookup"><span data-stu-id="e147c-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e147c-160">Entre em contato com a [equipe de suporte ao cliente do Zscaler ZSCloud](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="e147c-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) to get this value.</span></span> 
 
4. <span data-ttu-id="e147c-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e147c-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="e147c-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e147c-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e147c-165">Na seção **Configuração do Zscaler ZSCloud**, clique em **Configurar Zscaler ZSCloud** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="e147c-165">On the **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e147c-166">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="e147c-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="e147c-168">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa Zscaler ZSCloud como administrador.</span><span class="sxs-lookup"><span data-stu-id="e147c-168">In a different web browser window, log in to your ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="e147c-169">No menu na parte superior, clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="e147c-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="e147c-170">![Administração](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="e147c-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="e147c-171">Em **Gerenciar Administradores e Funções**, clique em **Gerenciar Usuários e Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="e147c-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="e147c-172">![Gerenciar usuários e autenticação](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Gerenciar usuários e autenticação")</span><span class="sxs-lookup"><span data-stu-id="e147c-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="e147c-173">Na seção **Escolher Opções de Autenticação para a sua Organização** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e147c-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="e147c-174">![Autenticação](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Autenticação")</span><span class="sxs-lookup"><span data-stu-id="e147c-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="e147c-175">a.</span><span class="sxs-lookup"><span data-stu-id="e147c-175">a.</span></span> <span data-ttu-id="e147c-176">Selecione **Autenticar usando o Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="e147c-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="e147c-177">b.</span><span class="sxs-lookup"><span data-stu-id="e147c-177">b.</span></span> <span data-ttu-id="e147c-178">Clique em **Configurar Parâmetros de Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="e147c-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="e147c-179">Na página da caixa de diálogo **Configurar Parâmetros de Logon Único do SAML**, execute as seguintes etapas e, em seguida, clique em **Concluído**</span><span class="sxs-lookup"><span data-stu-id="e147c-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="e147c-180">![Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="e147c-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="e147c-181">a.</span><span class="sxs-lookup"><span data-stu-id="e147c-181">a.</span></span> <span data-ttu-id="e147c-182">Cole o valor **URL de serviço de logon único do SAML** na caixa de texto **URL do Portal SAML para o qual os usuários são enviados para autenticação**.</span><span class="sxs-lookup"><span data-stu-id="e147c-182">Paste the **SAML Single Sign-On Service URL** value into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="e147c-183">b.</span><span class="sxs-lookup"><span data-stu-id="e147c-183">b.</span></span> <span data-ttu-id="e147c-184">Na caixa de texto **Atributo que contém o Nome de Logon**, digite **NameID**.</span><span class="sxs-lookup"><span data-stu-id="e147c-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="e147c-185">c.</span><span class="sxs-lookup"><span data-stu-id="e147c-185">c.</span></span> <span data-ttu-id="e147c-186">Para carregar seu certificado baixado, clique em **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="e147c-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="e147c-187">d.</span><span class="sxs-lookup"><span data-stu-id="e147c-187">d.</span></span> <span data-ttu-id="e147c-188">Selecione **Habilitar Provisionamento Automático do SAML**.</span><span class="sxs-lookup"><span data-stu-id="e147c-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="e147c-189">Na página de caixa de diálogo **Configurar Autenticação de Usuário** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e147c-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="e147c-190">![Administração](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="e147c-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="e147c-191">a.</span><span class="sxs-lookup"><span data-stu-id="e147c-191">a.</span></span> <span data-ttu-id="e147c-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e147c-192">Click **Save**.</span></span>

    <span data-ttu-id="e147c-193">b.</span><span class="sxs-lookup"><span data-stu-id="e147c-193">b.</span></span> <span data-ttu-id="e147c-194">Clique em **Ativar Agora**.</span><span class="sxs-lookup"><span data-stu-id="e147c-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="e147c-195">Definindo as configurações de proxy</span><span class="sxs-lookup"><span data-stu-id="e147c-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="e147c-196">Para definir as configurações de proxy no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="e147c-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="e147c-197">Inicie o **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e147c-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="e147c-198">Selecione **Opções da Internet** no menu **Ferramentas** para abrir a caixa de diálogo **Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="e147c-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="e147c-199">![Opções da Internet](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Opções da Internet")</span><span class="sxs-lookup"><span data-stu-id="e147c-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="e147c-200">Clique na guia **Conexões** .</span><span class="sxs-lookup"><span data-stu-id="e147c-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="e147c-201">![Conexões](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Conexões")</span><span class="sxs-lookup"><span data-stu-id="e147c-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="e147c-202">Clique em **Configurações da LAN** para abrir a caixa de diálogo **Configurações da LAN**.</span><span class="sxs-lookup"><span data-stu-id="e147c-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="e147c-203">Na seção Servidor de proxy, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e147c-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="e147c-204">![Servidor proxy](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Servidor proxy")</span><span class="sxs-lookup"><span data-stu-id="e147c-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="e147c-205">a.</span><span class="sxs-lookup"><span data-stu-id="e147c-205">a.</span></span> <span data-ttu-id="e147c-206">Selecione **Usar um servidor proxy para LAN**.</span><span class="sxs-lookup"><span data-stu-id="e147c-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="e147c-207">b.</span><span class="sxs-lookup"><span data-stu-id="e147c-207">b.</span></span> <span data-ttu-id="e147c-208">Na caixa de texto Endereço, digite **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="e147c-208">In the Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="e147c-209">c.</span><span class="sxs-lookup"><span data-stu-id="e147c-209">c.</span></span> <span data-ttu-id="e147c-210">Na caixa de texto Porta, digite **80**.</span><span class="sxs-lookup"><span data-stu-id="e147c-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="e147c-211">d.</span><span class="sxs-lookup"><span data-stu-id="e147c-211">d.</span></span> <span data-ttu-id="e147c-212">Selecione **Ignorar servidor proxy para endereços locais**.</span><span class="sxs-lookup"><span data-stu-id="e147c-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="e147c-213">e.</span><span class="sxs-lookup"><span data-stu-id="e147c-213">e.</span></span> <span data-ttu-id="e147c-214">Clique em **OK** para fechar a caixa de diálogo **Configurações da Rede Local (LAN)**.</span><span class="sxs-lookup"><span data-stu-id="e147c-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="e147c-215">Clique em **OK** para fechar a caixa de diálogo **Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="e147c-215">Click **OK** to close the **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e147c-216">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e147c-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="e147c-217">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e147c-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e147c-219">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e147c-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e147c-220">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e147c-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e147c-222">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e147c-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e147c-224">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e147c-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e147c-226">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e147c-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e147c-228">a.</span><span class="sxs-lookup"><span data-stu-id="e147c-228">a.</span></span> <span data-ttu-id="e147c-229">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e147c-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e147c-230">b.</span><span class="sxs-lookup"><span data-stu-id="e147c-230">b.</span></span> <span data-ttu-id="e147c-231">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e147c-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e147c-232">c.</span><span class="sxs-lookup"><span data-stu-id="e147c-232">c.</span></span> <span data-ttu-id="e147c-233">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="e147c-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e147c-234">d.</span><span class="sxs-lookup"><span data-stu-id="e147c-234">d.</span></span> <span data-ttu-id="e147c-235">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e147c-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="e147c-236">Criar um usuário de teste do Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="e147c-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="e147c-237">Para permitir que os usuários do Azure AD façam logon no ZScaler ZSCloud, eles devem ser provisionados no ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e147c-237">To enable Azure AD users to log in to ZScaler ZSCloud, they must be provisioned to ZScaler ZSCloud.</span></span>  
<span data-ttu-id="e147c-238">No caso do Zscaler ZSCloud, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="e147c-238">In the case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="e147c-239">Para configurar o provisionamento de usuários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e147c-239">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="e147c-240">Faça login no seu locatário do **Zscaler** .</span><span class="sxs-lookup"><span data-stu-id="e147c-240">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="e147c-241">Clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="e147c-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="e147c-242">![Administração](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="e147c-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="e147c-243">Clique em **Gerenciamento de Usuários**.</span><span class="sxs-lookup"><span data-stu-id="e147c-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="e147c-244">![Adicionar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="e147c-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="e147c-245">Na guia **Usuários**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e147c-245">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="e147c-246">![Adicionar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="e147c-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="e147c-247">Na seção Adicionar Usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e147c-247">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="e147c-248">![Adicionar Usuário](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="e147c-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="e147c-249">a.</span><span class="sxs-lookup"><span data-stu-id="e147c-249">a.</span></span> <span data-ttu-id="e147c-250">Digite **UserID**, **Nome de Exibição do Usuário**, **Senha**, **Confirmar Senha** e selecione **Grupos** e o **Departamento** de uma conta válida do AAD que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="e147c-250">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="e147c-251">b.</span><span class="sxs-lookup"><span data-stu-id="e147c-251">b.</span></span> <span data-ttu-id="e147c-252">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e147c-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="e147c-253">É possível usar qualquer outra ferramenta de criação da conta de usuário do Zscaler ZSCloud ou APIs fornecidas pelo Zscaler ZSCloud para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="e147c-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e147c-254">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e147c-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e147c-255">Nesta seção, você habilitará a Brenda Fernandes a usar o logon único do Azure através da concessão de acesso ao Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e147c-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler ZSCloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e147c-257">**Para atribuir Brenda Fernandes ao Zscaler ZSCloud, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e147c-257">**To assign Britta Simon to Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="e147c-258">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e147c-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e147c-260">Na lista de aplicativos, selecione **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="e147c-260">In the applications list, select **Zscaler ZSCloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="e147c-262">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e147c-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e147c-264">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e147c-264">Click **Add** button.</span></span> <span data-ttu-id="e147c-265">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e147c-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e147c-267">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e147c-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e147c-268">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e147c-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e147c-269">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e147c-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e147c-270">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e147c-270">Testing single sign-on</span></span>

<span data-ttu-id="e147c-271">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e147c-271">If you want to test your single sign-on settings, open the Access Panel.</span></span>

<span data-ttu-id="e147c-272">Ao clicar no bloco Zscaler ZSCloud no Painel de Acesso, você deve entrar automaticamente no aplicativo Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="e147c-272">When you click the Zscaler ZSCloud tile in the Access Panel, you should get automatically signed-on to your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="e147c-273">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e147c-273">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e147c-274">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e147c-274">Additional resources</span></span>

* [<span data-ttu-id="e147c-275">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e147c-275">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e147c-276">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e147c-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

