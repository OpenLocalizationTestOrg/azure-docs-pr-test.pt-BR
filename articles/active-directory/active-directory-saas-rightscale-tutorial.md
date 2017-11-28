---
title: "Tutorial: Integração do Azure Active Directory ao Rightscale | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 222c4414a9f736a3589b4cdd0ed934696f6c31ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="1ff79-103">Tutorial: Integração do Azure Active Directory ao Rightscale</span><span class="sxs-lookup"><span data-stu-id="1ff79-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="1ff79-104">Neste tutorial, você aprende a integrar o Rightscale ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1ff79-104">In this tutorial, you learn how to integrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ff79-105">A integração do Rightscale ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="1ff79-105">Integrating Rightscale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1ff79-106">No Azure AD, é possível controlar quem tem acesso ao Rightscale</span><span class="sxs-lookup"><span data-stu-id="1ff79-106">You can control in Azure AD who has access to Rightscale</span></span>
- <span data-ttu-id="1ff79-107">É possível permitir que os usuários se conectem automaticamente ao Rightscale (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ff79-107">You can enable your users to automatically get signed-on to Rightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1ff79-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1ff79-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1ff79-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1ff79-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ff79-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1ff79-110">Prerequisites</span></span>

<span data-ttu-id="1ff79-111">Para configurar a integração do Azure AD ao Rightscale, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1ff79-111">To configure Azure AD integration with Rightscale, you need the following items:</span></span>

- <span data-ttu-id="1ff79-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1ff79-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ff79-113">Uma assinatura habilitada para logon único do Rightscale</span><span class="sxs-lookup"><span data-stu-id="1ff79-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ff79-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1ff79-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ff79-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1ff79-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ff79-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1ff79-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ff79-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ff79-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ff79-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1ff79-118">Scenario description</span></span>
<span data-ttu-id="1ff79-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1ff79-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ff79-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="1ff79-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ff79-121">Adicionando o Rightscale por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="1ff79-121">Adding Rightscale from the gallery</span></span>
2. <span data-ttu-id="1ff79-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1ff79-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-the-gallery"></a><span data-ttu-id="1ff79-123">Adicionando o Rightscale por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="1ff79-123">Adding Rightscale from the gallery</span></span>
<span data-ttu-id="1ff79-124">Para configurar a integração do Rightscale ao Azure AD, é necessário adicionar o Rightscale à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="1ff79-124">To configure the integration of Rightscale into Azure AD, you need to add Rightscale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1ff79-125">**Para adicionar o Rightscale por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1ff79-125">**To add Rightscale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1ff79-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1ff79-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1ff79-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1ff79-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ff79-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1ff79-133">Na caixa de pesquisa, digite **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-133">In the search box, type **Rightscale**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="1ff79-135">No painel de resultados, selecione **Rightscale** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ff79-135">In the results panel, select **Rightscale**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1ff79-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1ff79-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1ff79-138">Nesta seção, você configura e testa o logon único do Azure AD com o Rightscale, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1ff79-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1ff79-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Rightscale é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ff79-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Rightscale is to a user in Azure AD.</span></span> <span data-ttu-id="1ff79-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Rightscale.</span><span class="sxs-lookup"><span data-stu-id="1ff79-140">In other words, a link relationship between an Azure AD user and the related user in Rightscale needs to be established.</span></span>

<span data-ttu-id="1ff79-141">No Rightscale, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="1ff79-141">In Rightscale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1ff79-142">Para configurar e testar o logon único do Azure AD com o Rightscale, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="1ff79-142">To configure and test Azure AD single sign-on with Rightscale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1ff79-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1ff79-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1ff79-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1ff79-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ff79-145">**[Criando um usuário de teste do Rightscale](#creating-a-rightscale-test-user)** – para ter um equivalente de Brenda Fernandes no Rightscale que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ff79-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - to have a counterpart of Britta Simon in Rightscale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ff79-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ff79-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ff79-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="1ff79-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1ff79-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ff79-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1ff79-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Rightscale.</span><span class="sxs-lookup"><span data-stu-id="1ff79-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="1ff79-150">**Para configurar o logon único do Azure AD com o Rightscale, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1ff79-150">**To configure Azure AD single sign-on with Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="1ff79-151">No portal do Azure, na página de integração do aplicativo **Rightscale**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-151">In the Azure portal, on the **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1ff79-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="1ff79-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="1ff79-155">Na seção **Domínio e URLs do Rightscale**, se você desejar configurar o aplicativo no **modo iniciado pelo IDP**, não precisará realizar nenhuma etapa, pois o aplicativo já é pré-integrado ao Azure.</span><span class="sxs-lookup"><span data-stu-id="1ff79-155">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **IDP initiated mode** you do not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="1ff79-157">Na seção **Domínio e URLs do Rightscale**, se desejar configurar o aplicativo no **modo iniciado pelo SP**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1ff79-157">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="1ff79-159">a.</span><span class="sxs-lookup"><span data-stu-id="1ff79-159">a.</span></span> <span data-ttu-id="1ff79-160">Clique em **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-160">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="1ff79-161">b.</span><span class="sxs-lookup"><span data-stu-id="1ff79-161">b.</span></span> <span data-ttu-id="1ff79-162">Na caixa de texto **URL de Logon**, digite a URL: `https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="1ff79-162">In the **Sign On URL** textbox, type the URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="1ff79-163">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1ff79-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="1ff79-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1ff79-165">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="1ff79-167">Na seção **Configuração do Rightscale**, clique em **Configurar o Rightscale** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-167">On the **Rightscale Configuration** section, click **Configure Rightscale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1ff79-168">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="1ff79-168">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="1ff79-169">![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="1ff79-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="1ff79-170">Para configurar o SSO para o aplicativo, você precisa entrar no locatário do RightScale como administrador.</span><span class="sxs-lookup"><span data-stu-id="1ff79-170">To get SSO configured for your application, you need to sign-on to your RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="1ff79-171">a.</span><span class="sxs-lookup"><span data-stu-id="1ff79-171">a.</span></span> <span data-ttu-id="1ff79-172">No menu na parte superior, clique na guia **Configurações** e selecione **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="1ff79-174">b.</span><span class="sxs-lookup"><span data-stu-id="1ff79-174">b.</span></span> <span data-ttu-id="1ff79-175">Clique no botão "**novo**" para adicionar **Seus Provedores de Identidade do SAML**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-175">Click the "**new**" button to add **Your SAML Identity Providers**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="1ff79-177">c.</span><span class="sxs-lookup"><span data-stu-id="1ff79-177">c.</span></span> <span data-ttu-id="1ff79-178">Na caixa de texto do **Nome de Exibição**, insira o nome da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="1ff79-178">In the textbox of **Display Name**, input your company name.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="1ff79-180">d.</span><span class="sxs-lookup"><span data-stu-id="1ff79-180">d.</span></span> <span data-ttu-id="1ff79-181">Selecione **Permitir o SSO iniciado pelo RightScale usando uma dica de descoberta** e insira seu **nome de domínio** na caixa de texto abaixo.</span><span class="sxs-lookup"><span data-stu-id="1ff79-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in the below textbox.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="1ff79-183">e.</span><span class="sxs-lookup"><span data-stu-id="1ff79-183">e.</span></span> <span data-ttu-id="1ff79-184">Cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure no **Ponto de Extremidade do SSO do SAML** no RightScale.</span><span class="sxs-lookup"><span data-stu-id="1ff79-184">Paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="1ff79-186">f.</span><span class="sxs-lookup"><span data-stu-id="1ff79-186">f.</span></span> <span data-ttu-id="1ff79-187">Cole o valor da **ID da Entidade SAML** copiado do portal do Azure na **EntityID SAML** no RightScale.</span><span class="sxs-lookup"><span data-stu-id="1ff79-187">Paste the value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="1ff79-189">g.</span><span class="sxs-lookup"><span data-stu-id="1ff79-189">g.</span></span> <span data-ttu-id="1ff79-190">Clique no botão **Navegador** para carregar o certificado baixado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ff79-190">Click **Browser** button to upload the certificate which you downloaded from Azure portal.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="1ff79-192">h.</span><span class="sxs-lookup"><span data-stu-id="1ff79-192">h.</span></span> <span data-ttu-id="1ff79-193">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="1ff79-194">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="1ff79-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1ff79-195">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1ff79-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1ff79-196">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1ff79-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1ff79-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1ff79-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="1ff79-198">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1ff79-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1ff79-200">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1ff79-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1ff79-201">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1ff79-203">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1ff79-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1ff79-205">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1ff79-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1ff79-207">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1ff79-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1ff79-209">a.</span><span class="sxs-lookup"><span data-stu-id="1ff79-209">a.</span></span> <span data-ttu-id="1ff79-210">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ff79-211">b.</span><span class="sxs-lookup"><span data-stu-id="1ff79-211">b.</span></span> <span data-ttu-id="1ff79-212">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1ff79-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1ff79-213">c.</span><span class="sxs-lookup"><span data-stu-id="1ff79-213">c.</span></span> <span data-ttu-id="1ff79-214">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1ff79-215">d.</span><span class="sxs-lookup"><span data-stu-id="1ff79-215">d.</span></span> <span data-ttu-id="1ff79-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="1ff79-217">Criando um usuário de teste do Rightscale</span><span class="sxs-lookup"><span data-stu-id="1ff79-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="1ff79-218">Nesta seção, você criará um usuário chamado Brenda Fernandes no RightScale.</span><span class="sxs-lookup"><span data-stu-id="1ff79-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="1ff79-219">Trabalhe com a [equipe de suporte ao Cliente do Rightscale](mailto:support@rightscale.com) para adicionar os usuários à plataforma RightScale.</span><span class="sxs-lookup"><span data-stu-id="1ff79-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) to add the users in the RightScale platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1ff79-220">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1ff79-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1ff79-221">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Rightscale.</span><span class="sxs-lookup"><span data-stu-id="1ff79-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rightscale.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1ff79-223">**Para atribuir Brenda Fernandes ao Rightscale, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1ff79-223">**To assign Britta Simon to Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="1ff79-224">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1ff79-226">Na lista de aplicativos, selecione **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-226">In the applications list, select **Rightscale**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="1ff79-228">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1ff79-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1ff79-230">Click **Add** button.</span></span> <span data-ttu-id="1ff79-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1ff79-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1ff79-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1ff79-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1ff79-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1ff79-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ff79-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1ff79-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1ff79-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1ff79-236">Testing single sign-on</span></span>

<span data-ttu-id="1ff79-237">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="1ff79-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="1ff79-238">Ao clicar no bloco do RightScale no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do RightScale.</span><span class="sxs-lookup"><span data-stu-id="1ff79-238">When you click the RightScale tile in the Access Panel, you should get automatically signed-on to your RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1ff79-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1ff79-239">Additional resources</span></span>

* [<span data-ttu-id="1ff79-240">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1ff79-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ff79-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1ff79-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

