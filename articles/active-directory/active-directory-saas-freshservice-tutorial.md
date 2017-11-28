---
title: "Tutorial: Integração do Azure Active Directory ao Freshservice | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d32775fa91d3a49da1ef55e57d1d38990fa09346
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="853c5-103">Tutorial: Integração do Azure Active Directory ao FreshService</span><span class="sxs-lookup"><span data-stu-id="853c5-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="853c5-104">Neste tutorial, você aprenderá a integrar o Freshservice ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="853c5-104">In this tutorial, you learn how to integrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="853c5-105">A integração do Freshservice ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="853c5-105">Integrating Freshservice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="853c5-106">No Azure AD, é possível controlar quem tem acesso ao Freshservice</span><span class="sxs-lookup"><span data-stu-id="853c5-106">You can control in Azure AD who has access to Freshservice</span></span>
- <span data-ttu-id="853c5-107">Você pode permitir que seus usuários façam logon automaticamente no Freshservice (logon único) com as próprias contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="853c5-107">You can enable your users to automatically get signed-on to Freshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="853c5-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="853c5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="853c5-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="853c5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="853c5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="853c5-110">Prerequisites</span></span>

<span data-ttu-id="853c5-111">Para configurar a integração do Azure AD ao Freshservice, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="853c5-111">To configure Azure AD integration with Freshservice, you need the following items:</span></span>

- <span data-ttu-id="853c5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="853c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="853c5-113">Uma assinatura habilitada para logon único do Freshservice</span><span class="sxs-lookup"><span data-stu-id="853c5-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="853c5-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="853c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="853c5-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="853c5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="853c5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="853c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="853c5-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="853c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="853c5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="853c5-118">Scenario description</span></span>
<span data-ttu-id="853c5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="853c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="853c5-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="853c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="853c5-121">Adicionando Freshservice da galeria</span><span class="sxs-lookup"><span data-stu-id="853c5-121">Adding Freshservice from the gallery</span></span>
2. <span data-ttu-id="853c5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="853c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-the-gallery"></a><span data-ttu-id="853c5-123">Adicionando Freshservice da galeria</span><span class="sxs-lookup"><span data-stu-id="853c5-123">Adding Freshservice from the gallery</span></span>
<span data-ttu-id="853c5-124">Para configurar a integração do Freshservice ao Azure AD, você precisa adicionar o Freshservice da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="853c5-124">To configure the integration of Freshservice into Azure AD, you need to add Freshservice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="853c5-125">**Para adicionar o Freshservice da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="853c5-125">**To add Freshservice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="853c5-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="853c5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="853c5-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="853c5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="853c5-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="853c5-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="853c5-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="853c5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="853c5-133">Na caixa de pesquisa, digite **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="853c5-133">In the search box, type **Freshservice**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="853c5-135">No painel de resultados, selecione **Freshservice** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="853c5-135">In the results panel, select **Freshservice**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="853c5-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="853c5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="853c5-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Freshservice com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="853c5-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="853c5-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Freshservice é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="853c5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Freshservice is to a user in Azure AD.</span></span> <span data-ttu-id="853c5-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Freshservice.</span><span class="sxs-lookup"><span data-stu-id="853c5-140">In other words, a link relationship between an Azure AD user and the related user in Freshservice needs to be established.</span></span>

<span data-ttu-id="853c5-141">No Freshservice, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="853c5-141">In Freshservice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="853c5-142">Para configurar e testar o logon único do Azure AD com o Freshservice, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="853c5-142">To configure and test Azure AD single sign-on with Freshservice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="853c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="853c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="853c5-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="853c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="853c5-145">**[Como criar um usuário de teste do Freshservice](#creating-a-freshservice-test-user)** – para ter um equivalente de Brenda Fernandes no Freshservice que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="853c5-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - to have a counterpart of Britta Simon in Freshservice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="853c5-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="853c5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="853c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="853c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="853c5-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="853c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="853c5-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único em seu aplicativo Freshservice.</span><span class="sxs-lookup"><span data-stu-id="853c5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="853c5-150">**Para configurar o logon único do Azure AD com o Freshservice, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="853c5-150">**To configure Azure AD single sign-on with Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="853c5-151">No portal do Azure, na página de integração de aplicativos do **Freshservice**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="853c5-151">In the Azure portal, on the **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="853c5-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="853c5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="853c5-155">Na seção **URLs e Domínio do Freshservice**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="853c5-155">On the **Freshservice Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="853c5-157">a.</span><span class="sxs-lookup"><span data-stu-id="853c5-157">a.</span></span> <span data-ttu-id="853c5-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="853c5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="853c5-159">b.</span><span class="sxs-lookup"><span data-stu-id="853c5-159">b.</span></span> <span data-ttu-id="853c5-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="853c5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="853c5-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="853c5-161">These values are not real.</span></span> <span data-ttu-id="853c5-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="853c5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="853c5-163">Entre em contato com [equipe de suporte ao Cliente do Freshservice](https://support.freshservice.com/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="853c5-163">Contact [Freshservice Client support team](https://support.freshservice.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="853c5-164">Na seção **Certificado de Assinatura do SAML**, copie o valor do certificado de **IMPRESSÃO DIGITAL**.</span><span class="sxs-lookup"><span data-stu-id="853c5-164">On the **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="853c5-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="853c5-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="853c5-168">Na seção **Configuração do Freshservice**, clique em **Configurar Freshservice** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="853c5-168">On the **Freshservice Configuration** section, click **Configure Freshservice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="853c5-169">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="853c5-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="853c5-171">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Freshservice como administrador.</span><span class="sxs-lookup"><span data-stu-id="853c5-171">In a different web browser window, log in to your Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="853c5-172">No menu na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="853c5-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="853c5-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="853c5-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="853c5-174">No **Portal do Cliente**, clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="853c5-174">In the **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="853c5-175">![Segurança](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="853c5-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="853c5-176">Na seção **Segurança** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="853c5-176">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="853c5-177">![Logon Único](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="853c5-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="853c5-178">a.</span><span class="sxs-lookup"><span data-stu-id="853c5-178">a.</span></span> <span data-ttu-id="853c5-179">Ative o **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="853c5-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="853c5-180">b.</span><span class="sxs-lookup"><span data-stu-id="853c5-180">b.</span></span> <span data-ttu-id="853c5-181">Selecione **SSO do SAML**.</span><span class="sxs-lookup"><span data-stu-id="853c5-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="853c5-182">c.</span><span class="sxs-lookup"><span data-stu-id="853c5-182">c.</span></span> <span data-ttu-id="853c5-183">Na caixa de texto **URL de Logon do SAML**, cole o valor da **URL do Serviço de Logon Único do SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="853c5-183">In the **SAML Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="853c5-184">d.</span><span class="sxs-lookup"><span data-stu-id="853c5-184">d.</span></span> <span data-ttu-id="853c5-185">Na caixa de texto **URL de Logoff**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="853c5-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="853c5-186">e.</span><span class="sxs-lookup"><span data-stu-id="853c5-186">e.</span></span> <span data-ttu-id="853c5-187">Na caixa de texto **Impressão Digital do Certificado de Segurança**, cole o valor do certificado de **IMPRESSÃO DIGITAL** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="853c5-187">In **Security Certificate Fingerprint** textbox, paste the **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="853c5-188">f.</span><span class="sxs-lookup"><span data-stu-id="853c5-188">f.</span></span> <span data-ttu-id="853c5-189">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="853c5-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="853c5-190">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="853c5-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="853c5-191">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="853c5-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="853c5-192">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="853c5-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="853c5-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="853c5-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="853c5-194">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="853c5-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="853c5-196">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="853c5-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="853c5-197">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="853c5-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="853c5-199">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="853c5-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="853c5-201">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="853c5-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="853c5-203">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="853c5-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="853c5-205">a.</span><span class="sxs-lookup"><span data-stu-id="853c5-205">a.</span></span> <span data-ttu-id="853c5-206">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="853c5-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="853c5-207">b.</span><span class="sxs-lookup"><span data-stu-id="853c5-207">b.</span></span> <span data-ttu-id="853c5-208">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="853c5-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="853c5-209">c.</span><span class="sxs-lookup"><span data-stu-id="853c5-209">c.</span></span> <span data-ttu-id="853c5-210">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="853c5-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="853c5-211">d.</span><span class="sxs-lookup"><span data-stu-id="853c5-211">d.</span></span> <span data-ttu-id="853c5-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="853c5-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="853c5-213">Como criar um usuário de teste do Freshservice</span><span class="sxs-lookup"><span data-stu-id="853c5-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="853c5-214">Para permitir que os usuários do Azure AD façam logon no FreshService, eles devem ser provisionados no Freshservice.</span><span class="sxs-lookup"><span data-stu-id="853c5-214">To enable Azure AD users to log in to FreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="853c5-215">No caso do FreshService, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="853c5-215">In the case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="853c5-216">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="853c5-216">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="853c5-217">Faça logon em seu site de empresa do **FreshService** como administrador.</span><span class="sxs-lookup"><span data-stu-id="853c5-217">Log in to your **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="853c5-218">No menu na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="853c5-218">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="853c5-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="853c5-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="853c5-220">Na seção **Gerenciamento de Usuários**, clique em **Solicitantes**.</span><span class="sxs-lookup"><span data-stu-id="853c5-220">In the **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="853c5-221">![Solicitantes](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Solicitantes")</span><span class="sxs-lookup"><span data-stu-id="853c5-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="853c5-222">Clique em **Novo Solicitante**.</span><span class="sxs-lookup"><span data-stu-id="853c5-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="853c5-223">![Novos Solicitantes](./media/active-directory-saas-freshservice-tutorial/ic790819.png "Novos Solicitantes")</span><span class="sxs-lookup"><span data-stu-id="853c5-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="853c5-224">Na seção **Novo Solicitante** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="853c5-224">In the **New Requester** section, perform the following steps:</span></span>
   
    <span data-ttu-id="853c5-225">![Novo Solicitante](./media/active-directory-saas-freshservice-tutorial/ic790820.png "Novo Solicitante")</span><span class="sxs-lookup"><span data-stu-id="853c5-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="853c5-226">a.</span><span class="sxs-lookup"><span data-stu-id="853c5-226">a.</span></span> <span data-ttu-id="853c5-227">Insira os atributos **Nome** e **Email** de uma conta válida do Azure Active Directory que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="853c5-227">Enter the **First Name** and **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="853c5-228">b.</span><span class="sxs-lookup"><span data-stu-id="853c5-228">b.</span></span> <span data-ttu-id="853c5-229">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="853c5-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="853c5-230">O titular da conta do Azure Active Directory recebe um email que inclui um link para confirmar a conta antes que ela se torne ativa</span><span class="sxs-lookup"><span data-stu-id="853c5-230">The Azure Active Directory account holder gets an email including a link to confirm the account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="853c5-231">É possível usar qualquer outra ferramenta de criação da conta de usuário do FreshService ou APIs fornecidas pelo FreshService para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="853c5-231">You can use any other FreshService user account creation tools or APIs provided by FreshService to provision AAD user accounts.</span></span>
>  

![Atribuir usuário][200] 

<span data-ttu-id="853c5-233">**Para atribuir Brenda Fernandes ao Freshservice, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="853c5-233">**To assign Britta Simon to Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="853c5-234">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="853c5-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="853c5-236">Na lista de aplicativos, selecione **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="853c5-236">In the applications list, select **Freshservice**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="853c5-238">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="853c5-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="853c5-240">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="853c5-240">Click **Add** button.</span></span> <span data-ttu-id="853c5-241">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="853c5-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="853c5-243">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="853c5-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="853c5-244">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="853c5-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="853c5-245">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="853c5-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="853c5-246">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="853c5-246">Testing single sign-on</span></span>

<span data-ttu-id="853c5-247">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="853c5-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="853c5-248">Quando você clica no bloco Freshservice no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Freshservice.</span><span class="sxs-lookup"><span data-stu-id="853c5-248">When you click the Freshservice tile in the Access Panel, you should get automatically signed-on to your Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="853c5-249">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="853c5-249">Additional resources</span></span>

* [<span data-ttu-id="853c5-250">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="853c5-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="853c5-251">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="853c5-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

