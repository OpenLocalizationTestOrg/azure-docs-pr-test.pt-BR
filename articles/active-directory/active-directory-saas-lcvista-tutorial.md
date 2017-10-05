---
title: "Tutorial: Integração do Azure Active Directory ao LCVista | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o LCVista."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c19f81da495eb7116b62797d1755d312a23f3805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="5bfd8-103">Tutorial: Integração do Azure Active Directory ao LCVista</span><span class="sxs-lookup"><span data-stu-id="5bfd8-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="5bfd8-104">Neste tutorial, você aprenderá a integrar o LCVista ao Azure AD (Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5bfd8-104">In this tutorial, you learn how to integrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bfd8-105">A integração do LCVista ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="5bfd8-105">Integrating LCVista with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5bfd8-106">Você pode controlar no Azure AD quem tem acesso ao LCVista</span><span class="sxs-lookup"><span data-stu-id="5bfd8-106">You can control in Azure AD who has access to LCVista</span></span>
- <span data-ttu-id="5bfd8-107">Você pode habilitar os usuários a entrar automaticamente no LCVista (Logon Único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bfd8-107">You can enable your users to automatically get signed-on to LCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bfd8-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5bfd8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5bfd8-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bfd8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bfd8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5bfd8-110">Prerequisites</span></span>

<span data-ttu-id="5bfd8-111">Para configurar a integração do Azure AD ao LCVista, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5bfd8-111">To configure Azure AD integration with LCVista, you need the following items:</span></span>

- <span data-ttu-id="5bfd8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5bfd8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bfd8-113">Uma assinatura habilitada para logon único do LCVista</span><span class="sxs-lookup"><span data-stu-id="5bfd8-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bfd8-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bfd8-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5bfd8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bfd8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bfd8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bfd8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bfd8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5bfd8-118">Scenario description</span></span>
<span data-ttu-id="5bfd8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bfd8-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="5bfd8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bfd8-121">Adicionando o LCVista usando a galeria</span><span class="sxs-lookup"><span data-stu-id="5bfd8-121">Adding LCVista from the gallery</span></span>
2. <span data-ttu-id="5bfd8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5bfd8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-the-gallery"></a><span data-ttu-id="5bfd8-123">Adicionando o LCVista usando a galeria</span><span class="sxs-lookup"><span data-stu-id="5bfd8-123">Adding LCVista from the gallery</span></span>
<span data-ttu-id="5bfd8-124">Para configurar a integração do LCVista ao Azure AD, você precisa adicionar o LCVista da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-124">To configure the integration of LCVista into Azure AD, you need to add LCVista from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5bfd8-125">**Para adicionar o LCVista da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5bfd8-125">**To add LCVista from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5bfd8-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5bfd8-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5bfd8-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5bfd8-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5bfd8-133">Na caixa de pesquisa, digite **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-133">In the search box, type **LCVista**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="5bfd8-135">No painel de resultados, selecione **LCVista** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-135">In the results panel, select **LCVista**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5bfd8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5bfd8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5bfd8-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o LCVista, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="5bfd8-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5bfd8-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do LCVista é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LCVista is to a user in Azure AD.</span></span> <span data-ttu-id="5bfd8-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do LCVista.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-140">In other words, a link relationship between an Azure AD user and the related user in LCVista needs to be established.</span></span>

<span data-ttu-id="5bfd8-141">Essa relação de vinculação é estabelecida pela atribuição do valor de **nome de usuário** no Azure AD como o valor do **Nome de usuário** no LCVista.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LCVista.</span></span>

<span data-ttu-id="5bfd8-142">Para configurar e testar o logon único do Azure AD com o LCVista, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="5bfd8-142">To configure and test Azure AD single sign-on with LCVista, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5bfd8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5bfd8-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bfd8-145">**[Criação de um usuário de teste do LCVista](#creating-a-lcvista-test-user)** – para ter um equivalente de Brenda Fernandes no LCVista que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - to have a counterpart of Britta Simon in LCVista that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bfd8-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bfd8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5bfd8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bfd8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5bfd8-149">Nesta seção, você vai habilitar o logon único do Azure AD no Portal do Azure e configurar o logon único em seu aplicativo LCVista.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="5bfd8-150">**Para configurar o logon único do Azure AD com o LCVista, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5bfd8-150">**To configure Azure AD single sign-on with LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="5bfd8-151">No Portal do Azure, na página de integração de aplicativos do **LCVista**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-151">In the Azure portal, on the **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5bfd8-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="5bfd8-155">Na seção **Domínio e URLs do LCVista**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5bfd8-155">On the **LCVista Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="5bfd8-157">a.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-157">a.</span></span> <span data-ttu-id="5bfd8-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="5bfd8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="5bfd8-159">b.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-159">b.</span></span> <span data-ttu-id="5bfd8-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="5bfd8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="5bfd8-161">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-161">These values are not the real.</span></span> <span data-ttu-id="5bfd8-162">Atualize esses valores com o Identificador e a URL de Logon reais.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-162">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="5bfd8-163">Contate a [equipe de suporte do Cliente LCVista](https://lcvista.com/contact) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-163">Contact [LCVista Client support team](https://lcvista.com/contact) to get these values.</span></span> 

4. <span data-ttu-id="5bfd8-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="5bfd8-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5bfd8-166">Click **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="5bfd8-168">Na seção **Configuração do LCVista**, clique em **Configurar o LCVista** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-168">On the **LCVista Configuration** section, click **Configure LCVista** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5bfd8-169">Copie a **ID da Entidade SAML** e a **URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="5bfd8-169">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar o logon único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="5bfd8-171">Entre no seu aplicativo LCVista como um administrador.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-171">Sign on to your LCVista application as an administrator.</span></span>

8. <span data-ttu-id="5bfd8-172">Na seção **Configuração de SAML**, marque **Habilitar logon de SAML** e digite os detalhes como mencionado na imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-172">In the **SAML Config** section, check the **Enable SAML login** and enter the details as mentioned in below image.</span></span> 

    ![Configurar o logon único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="5bfd8-174">a.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-174">a.</span></span> <span data-ttu-id="5bfd8-175">Cole a **URL do Emissor** que você copiou do Azure AD na seção **ID da Entidade**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-175">Paste the **Issuer URL** which you have copied from Azure AD in the **Entity ID** section.</span></span> 

    <span data-ttu-id="5bfd8-176">b.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-176">b.</span></span> <span data-ttu-id="5bfd8-177">Cole a **URL do Serviço de Logon Único** que você copiou do Azure AD na seção **URL**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-177">Paste the **Single Sign-On Service URL** which you have copied from Azure AD in the **URL** section.</span></span>

    <span data-ttu-id="5bfd8-178">c.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-178">c.</span></span> <span data-ttu-id="5bfd8-179">Em Metadados (XML) que você baixou do Portal do Azure, copie o valor **X509Certificate** e cole-o na seção **Certificado x509**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-179">From Metadata (XML) which you have downloaded from Azure portal, copy the value **X509Certificate** and paste it in the **x509 Certificate** section.</span></span>

    <span data-ttu-id="5bfd8-180">d.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-180">d.</span></span> <span data-ttu-id="5bfd8-181">Na caixa de texto **Atributo de nome**, cole o valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-181">In the **First name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="5bfd8-182">e.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-182">e.</span></span> <span data-ttu-id="5bfd8-183">Na caixa de texto **Atributo de sobrenome**, cole o valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-183">In the **Last name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="5bfd8-184">f.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-184">f.</span></span> <span data-ttu-id="5bfd8-185">Na caixa de texto **Atributo de email**, cole o valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-185">In the **Email attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="5bfd8-186">g.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-186">g.</span></span> <span data-ttu-id="5bfd8-187">Na caixa de texto **Atributo de nome de usuário**, cole o valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-187">In the **Username attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="5bfd8-188">e.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-188">e.</span></span> <span data-ttu-id="5bfd8-189">Clique em **Salvar** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-189">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="5bfd8-190">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="5bfd8-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5bfd8-191">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5bfd8-192">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5bfd8-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5bfd8-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="5bfd8-194">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5bfd8-196">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5bfd8-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5bfd8-197">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bfd8-199">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bfd8-201">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bfd8-203">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5bfd8-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bfd8-205">a.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-205">a.</span></span> <span data-ttu-id="5bfd8-206">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bfd8-207">b.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-207">b.</span></span> <span data-ttu-id="5bfd8-208">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bfd8-209">c.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-209">c.</span></span> <span data-ttu-id="5bfd8-210">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5bfd8-211">d.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-211">d.</span></span> <span data-ttu-id="5bfd8-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="5bfd8-213">Criando um usuário de teste do LCVista</span><span class="sxs-lookup"><span data-stu-id="5bfd8-213">Creating a LCVista test user</span></span>

<span data-ttu-id="5bfd8-214">Nesta seção, você criará um usuário chamado Brenda Fernandes no LCVista.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="5bfd8-215">É preciso contatar a [equipe de suporte do Cliente LCVista](https://lcvista.com/contact) para adicionar os usuários no aplicativo LCVista.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-215">You need to contact [LCVista Client support team](https://lcvista.com/contact) to add the users in the LCVista application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5bfd8-216">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5bfd8-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5bfd8-217">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao LCVista.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LCVista.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5bfd8-219">**Para atribuir Brenda Fernandes ao LCVista, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5bfd8-219">**To assign Britta Simon to LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="5bfd8-220">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5bfd8-222">Na lista de aplicativos, escolha **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-222">In the applications list, select **LCVista**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="5bfd8-224">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5bfd8-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-226">Click **Add** button.</span></span> <span data-ttu-id="5bfd8-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5bfd8-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5bfd8-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bfd8-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5bfd8-232">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5bfd8-232">Testing single sign-on</span></span>

<span data-ttu-id="5bfd8-233">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="5bfd8-234">Clique no bloco LCVista no Painel de Acesso e você será redirecionado para a página de logon Organização.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-234">Click the LCVista tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="5bfd8-235">Após fazer logon com êxito, você entrará no aplicativo LCVista.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-235">After successful login, you will be signed-on to your LCVista application.</span></span> <span data-ttu-id="5bfd8-236">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="5bfd8-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5bfd8-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5bfd8-237">Additional resources</span></span>

* [<span data-ttu-id="5bfd8-238">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5bfd8-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bfd8-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5bfd8-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

