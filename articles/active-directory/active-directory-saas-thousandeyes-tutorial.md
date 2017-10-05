---
title: "Tutorial: Integração do Azure Active Directory ao ThousandEyes | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ThousandEyes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 392add7d5f0a55598b8b90760f5c3f2d1e67ac02
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="b9912-103">Tutorial: Integração do Active Directory do Azure ao ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="b9912-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="b9912-104">Neste tutorial, você aprenderá a integrar o ThousandEyes ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="b9912-104">In this tutorial, you learn how to integrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9912-105">A integração do ThousandEyes com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="b9912-105">Integrating ThousandEyes with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b9912-106">No Azure AD, é possível controlar quem tem acesso ao ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="b9912-106">You can control in Azure AD who has access to ThousandEyes</span></span>
- <span data-ttu-id="b9912-107">É possível permitir que os usuários entrem automaticamente no ThousandEyes (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9912-107">You can enable your users to automatically get signed-on to ThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9912-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b9912-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b9912-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9912-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9912-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b9912-110">Prerequisites</span></span>

<span data-ttu-id="b9912-111">Para configurar a integração do Azure AD com o ThousandEyes, serão necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b9912-111">To configure Azure AD integration with ThousandEyes, you need the following items:</span></span>

- <span data-ttu-id="b9912-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9912-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9912-113">Uma assinatura do ThousandEyes habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="b9912-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9912-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b9912-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9912-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b9912-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9912-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b9912-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9912-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9912-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9912-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b9912-118">Scenario description</span></span>
<span data-ttu-id="b9912-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b9912-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9912-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="b9912-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9912-121">Adicionar o ThousandEyes da galeria</span><span class="sxs-lookup"><span data-stu-id="b9912-121">Adding ThousandEyes from the gallery</span></span>
2. <span data-ttu-id="b9912-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9912-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-the-gallery"></a><span data-ttu-id="b9912-123">Adicionar o ThousandEyes da galeria</span><span class="sxs-lookup"><span data-stu-id="b9912-123">Adding ThousandEyes from the gallery</span></span>
<span data-ttu-id="b9912-124">Para configurar a integração do ThousandEyes com o Azure AD, é necessário adicionar o ThousandEyes da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b9912-124">To configure the integration of ThousandEyes into Azure AD, you need to add ThousandEyes from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b9912-125">**Para adicionar o ThousandEyes da galeria, siga as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b9912-125">**To add ThousandEyes from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b9912-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9912-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9912-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b9912-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b9912-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b9912-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="b9912-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9912-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="b9912-133">Na caixa de pesquisa, digite **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="b9912-133">In the search box, type **ThousandEyes**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="b9912-135">No painel de resultados, selecione **ThousandEyes** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9912-135">In the results panel, select **ThousandEyes**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9912-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9912-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9912-138">Nesta seção, você configurará e testará o logon único do Azure AD com o ThousandEyes, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="b9912-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9912-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ThousandEyes é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9912-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThousandEyes is to a user in Azure AD.</span></span> <span data-ttu-id="b9912-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="b9912-140">In other words, a link relationship between an Azure AD user and the related user in ThousandEyes needs to be established.</span></span>

<span data-ttu-id="b9912-141">No ThousandEyes, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="b9912-141">In ThousandEyes, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b9912-142">Para configurar e testar o logon único do Azure AD com o ThousandEyes, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="b9912-142">To configure and test Azure AD single sign-on with ThousandEyes, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b9912-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b9912-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b9912-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b9912-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9912-145">**[Criação de um usuário de teste do ThousandEyes](#creating-a-thousandeyes-test-user)** – para ter um equivalente de Brenda Fernandes no ThousandEyes que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9912-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - to have a counterpart of Britta Simon in ThousandEyes that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9912-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9912-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9912-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="b9912-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9912-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9912-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9912-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="b9912-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="b9912-150">**Para configurar o logon único do Azure AD com o ThousandEyes, siga estas etapas:**</span><span class="sxs-lookup"><span data-stu-id="b9912-150">**To configure Azure AD single sign-on with ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="b9912-151">No Portal do Azure, na página de integração de aplicativos do **ThousandEyes**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="b9912-151">In the Azure portal, on the **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="b9912-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="b9912-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="b9912-155">Na seção **URLs e Domínio do ThousandEyes**, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="b9912-155">On the **ThousandEyes Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="b9912-157">Na caixa de texto **URL de Logon**, digite uma URL como: `https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="b9912-157">In the **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="b9912-158">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="b9912-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="b9912-160">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b9912-160">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9912-162">Na seção **Configuração do ThousandEyes**, clique em **Configurar ThousandEyes** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="b9912-162">On the **ThousandEyes Configuration** section, click **Configure ThousandEyes** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b9912-163">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="b9912-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="b9912-165">Em outra janela do navegador da Web, entre em seu site de empresa do **ThousandEyes** como administrador.</span><span class="sxs-lookup"><span data-stu-id="b9912-165">In a different web browser window, sign on to your **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="b9912-166">No menu na parte superior, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="b9912-166">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="b9912-167">![Configurações](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="b9912-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="b9912-168">Clique em **Conta**</span><span class="sxs-lookup"><span data-stu-id="b9912-168">Click **Account**</span></span>
   
    <span data-ttu-id="b9912-169">![Conta](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Conta")</span><span class="sxs-lookup"><span data-stu-id="b9912-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="b9912-170">Clique na guia **Segurança e Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="b9912-170">Click the **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="b9912-171">![Segurança e autenticação](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Segurança e autenticação")</span><span class="sxs-lookup"><span data-stu-id="b9912-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="b9912-172">Na seção **Configurações de Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b9912-172">In the **Setup Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b9912-173">![Configurar o logon único](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Configurar o logon único")</span><span class="sxs-lookup"><span data-stu-id="b9912-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="b9912-174">a.</span><span class="sxs-lookup"><span data-stu-id="b9912-174">a.</span></span> <span data-ttu-id="b9912-175">Selecione **Habilitar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="b9912-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="b9912-176">b.</span><span class="sxs-lookup"><span data-stu-id="b9912-176">b.</span></span> <span data-ttu-id="b9912-177">Na caixa de texto **URL de Página de Logon**, cole a **URL do Serviço de Logon Único SAML** copiada do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9912-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="b9912-178">c.</span><span class="sxs-lookup"><span data-stu-id="b9912-178">c.</span></span> <span data-ttu-id="b9912-179">Na caixa de texto **URL de Página de Logoff**, cole a **URL de Saída** copiada do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9912-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="b9912-180">d.</span><span class="sxs-lookup"><span data-stu-id="b9912-180">d.</span></span> <span data-ttu-id="b9912-181">Na caixa de texto **Emissor do Provedor de Identidade**, cole a **ID de Entidade SAML** copiada do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9912-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="b9912-182">e.</span><span class="sxs-lookup"><span data-stu-id="b9912-182">e.</span></span> <span data-ttu-id="b9912-183">Em **Certificado de Verificação**, clique em **Escolher Arquivo** e carregue o certificado que você baixou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9912-183">In **Verification Certificate**, click **Choose file**, and then upload the certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="b9912-184">f.</span><span class="sxs-lookup"><span data-stu-id="b9912-184">f.</span></span> <span data-ttu-id="b9912-185">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b9912-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="b9912-186">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="b9912-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b9912-187">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="b9912-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b9912-188">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9912-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9912-189">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9912-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9912-190">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b9912-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="b9912-192">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b9912-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b9912-193">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9912-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9912-195">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="b9912-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9912-197">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9912-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9912-199">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b9912-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9912-201">a.</span><span class="sxs-lookup"><span data-stu-id="b9912-201">a.</span></span> <span data-ttu-id="b9912-202">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="b9912-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9912-203">b.</span><span class="sxs-lookup"><span data-stu-id="b9912-203">b.</span></span> <span data-ttu-id="b9912-204">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b9912-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9912-205">c.</span><span class="sxs-lookup"><span data-stu-id="b9912-205">c.</span></span> <span data-ttu-id="b9912-206">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="b9912-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b9912-207">d.</span><span class="sxs-lookup"><span data-stu-id="b9912-207">d.</span></span> <span data-ttu-id="b9912-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b9912-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="b9912-209">Criação de um usuário de teste do ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="b9912-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="b9912-210">Para permitir que os usuários do AD do Azure façam logon no ThousandEyes, eles devem ser provisionados no ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="b9912-210">In order to enable Azure AD users to log into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="b9912-211">No caso do ThousandEyes, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="b9912-211">In the case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="b9912-212">É possível usar qualquer outra ferramenta de criação da conta de usuário do ThousandEyes ou as APIs fornecidas pelo ThousandEyes para provisionar as contas de usuário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b9912-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="b9912-213">**Para provisionar uma conta de usuário no ThousandEyes, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b9912-213">**To provision a user account to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="b9912-214">Faça logon em seu site de empresa ThousandEyes como um administrador.</span><span class="sxs-lookup"><span data-stu-id="b9912-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="b9912-215">Clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="b9912-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="b9912-216">![Configurações](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="b9912-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="b9912-217">Clique em **Conta**.</span><span class="sxs-lookup"><span data-stu-id="b9912-217">Click **Account**.</span></span>
   
    <span data-ttu-id="b9912-218">![Conta](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Conta")</span><span class="sxs-lookup"><span data-stu-id="b9912-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="b9912-219">Clique na guia **Contas e Usuários**.</span><span class="sxs-lookup"><span data-stu-id="b9912-219">Click the **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="b9912-220">![Contas e usuários](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Contas e usuários")</span><span class="sxs-lookup"><span data-stu-id="b9912-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="b9912-221">Na seção **Adicionar Usuários e Contas**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b9912-221">In the **Add Users & Accounts** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b9912-222">![Adicionar contas de usuário](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Adicionar contas de usuário")</span><span class="sxs-lookup"><span data-stu-id="b9912-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="b9912-223">a.</span><span class="sxs-lookup"><span data-stu-id="b9912-223">a.</span></span> <span data-ttu-id="b9912-224">Na caixa de texto **Nome**, digite o nome do usuário como **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="b9912-224">In **Name** textbox, type the name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="b9912-225">b.</span><span class="sxs-lookup"><span data-stu-id="b9912-225">b.</span></span> <span data-ttu-id="b9912-226">Na caixa de texto **Email**, digite o email do usuário como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b9912-226">In **Email** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="b9912-227">b.</span><span class="sxs-lookup"><span data-stu-id="b9912-227">b.</span></span> <span data-ttu-id="b9912-228">Clique em **Adicionar Novo Usuário à Conta**.</span><span class="sxs-lookup"><span data-stu-id="b9912-228">Click **Add New User to Account**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="b9912-229">O titular da conta do Azure Active Directory receberá um email com um link para confirmar e ativar a conta.</span><span class="sxs-lookup"><span data-stu-id="b9912-229">The Azure Active Directory account holder will get an email including a link to confirm and activate the account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b9912-230">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9912-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b9912-231">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="b9912-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThousandEyes.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="b9912-233">**Para atribuir Brenda Fernandes ao ThousandEyes, siga estas etapas:**</span><span class="sxs-lookup"><span data-stu-id="b9912-233">**To assign Britta Simon to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="b9912-234">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b9912-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b9912-236">Na lista de aplicativos, escolha **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="b9912-236">In the applications list, select **ThousandEyes**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="b9912-238">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b9912-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="b9912-240">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b9912-240">Click **Add** button.</span></span> <span data-ttu-id="b9912-241">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9912-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="b9912-243">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="b9912-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b9912-244">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9912-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9912-245">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9912-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9912-246">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="b9912-246">Testing single sign-on</span></span>

<span data-ttu-id="b9912-247">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="b9912-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b9912-248">Ao clicar no bloco ThousandEyes no Painel de Acesso, você deverá entrará automaticamente no seu aplicativo ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="b9912-248">When you click the ThousandEyes tile in the Access Panel, you should get automatically signed-on to your ThousandEyes application.</span></span>

<span data-ttu-id="b9912-249">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9912-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9912-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b9912-250">Additional resources</span></span>

* [<span data-ttu-id="b9912-251">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b9912-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9912-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9912-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

