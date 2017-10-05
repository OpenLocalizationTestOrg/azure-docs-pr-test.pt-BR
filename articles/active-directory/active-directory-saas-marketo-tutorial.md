---
title: "Tutorial: Integração do Azure Active Directory ao Marketo | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e146fd5a8075bc9c7ba049b25e5f301fc2645ed9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="7512a-103">Tutorial: Integração do Azure Active Directory com o Marketo</span><span class="sxs-lookup"><span data-stu-id="7512a-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="7512a-104">Neste tutorial, você aprenderá a integrar o Marketo ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7512a-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7512a-105">A integração do Marketo ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7512a-105">Integrating Marketo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7512a-106">No Azure AD, você pode controlar quem tem acesso ao Marketo</span><span class="sxs-lookup"><span data-stu-id="7512a-106">You can control in Azure AD who has access to Marketo</span></span>
- <span data-ttu-id="7512a-107">Você pode permitir que usuários façam logon automaticamente no Marketo (Logon Único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7512a-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7512a-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7512a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7512a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7512a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7512a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7512a-110">Prerequisites</span></span>

<span data-ttu-id="7512a-111">Para configurar a integração do Azure AD com o Marketo, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7512a-111">To configure Azure AD integration with Marketo, you need the following items:</span></span>

- <span data-ttu-id="7512a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7512a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7512a-113">Uma assinatura habilitada para logon único do Marketo</span><span class="sxs-lookup"><span data-stu-id="7512a-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7512a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7512a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7512a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7512a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7512a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7512a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7512a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7512a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7512a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7512a-118">Scenario description</span></span>
<span data-ttu-id="7512a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7512a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7512a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7512a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7512a-121">Adicionar o Marketo da galeria</span><span class="sxs-lookup"><span data-stu-id="7512a-121">Adding Marketo from the gallery</span></span>
2. <span data-ttu-id="7512a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7512a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-the-gallery"></a><span data-ttu-id="7512a-123">Adicionar o Marketo da galeria</span><span class="sxs-lookup"><span data-stu-id="7512a-123">Adding Marketo from the gallery</span></span>
<span data-ttu-id="7512a-124">Para configurar a integração do Marketo ao Azure AD, você precisará adicionar o Marketo da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7512a-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7512a-125">**Para adicionar o Marketo da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7512a-125">**To add Marketo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7512a-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7512a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7512a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7512a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7512a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7512a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7512a-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7512a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7512a-133">Na caixa de pesquisa, digite **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="7512a-133">In the search box, type **Marketo**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="7512a-135">No painel de resultados, selecione **Marketo** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7512a-135">In the results panel, select **Marketo**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7512a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7512a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7512a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Marketo, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7512a-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7512a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Marketo é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7512a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span></span> <span data-ttu-id="7512a-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Marketo.</span><span class="sxs-lookup"><span data-stu-id="7512a-140">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span></span>

<span data-ttu-id="7512a-141">No Marketo, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="7512a-141">In Marketo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7512a-142">Para configurar e testar o logon único do Azure AD com o Marketo, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="7512a-142">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7512a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7512a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7512a-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7512a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7512a-145">**[Criação de um usuário de teste do Marketo](#creating-a-marketo-test-user)** – para ter um equivalente de Brenda Fernandes no Marketo que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7512a-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7512a-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7512a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7512a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7512a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7512a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7512a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7512a-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo Marketo.</span><span class="sxs-lookup"><span data-stu-id="7512a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="7512a-150">**Para configurar o logon único do Azure AD com o Marketo, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7512a-150">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="7512a-151">No portal do Azure, na página de integração de aplicativos do **Marketo**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7512a-151">In the Azure portal, on the **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7512a-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7512a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="7512a-155">Na seção **Domínio e URLs do Marketo**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7512a-155">On the **Marketo Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="7512a-157">a.</span><span class="sxs-lookup"><span data-stu-id="7512a-157">a.</span></span> <span data-ttu-id="7512a-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="7512a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="7512a-159">b.</span><span class="sxs-lookup"><span data-stu-id="7512a-159">b.</span></span> <span data-ttu-id="7512a-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="7512a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7512a-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="7512a-161">These values are not real.</span></span> <span data-ttu-id="7512a-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="7512a-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="7512a-163">Entre em contato com a [equipe de suporte do Marketo](http://investors.marketo.com/contactus.cfm) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="7512a-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) to get these values.</span></span>
 
4. <span data-ttu-id="7512a-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7512a-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="7512a-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7512a-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7512a-168">Na seção **Configuração do Marketo**, clique em **Configurar Marketo** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="7512a-168">On the **Marketo Configuration** section, click **Configure Marketo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7512a-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="7512a-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="7512a-171">Para obter a Id do Munchkin do aplicativo, faça logon no Marketo usando credenciais de administrador e execute as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="7512a-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="7512a-172">a.</span><span class="sxs-lookup"><span data-stu-id="7512a-172">a.</span></span> <span data-ttu-id="7512a-173">Faça logon usando credenciais de administrador de aplicativo do Marketo.</span><span class="sxs-lookup"><span data-stu-id="7512a-173">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="7512a-174">b.</span><span class="sxs-lookup"><span data-stu-id="7512a-174">b.</span></span> <span data-ttu-id="7512a-175">Clique no botão **Admin** no painel de navegação superior.</span><span class="sxs-lookup"><span data-stu-id="7512a-175">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="7512a-177">c.</span><span class="sxs-lookup"><span data-stu-id="7512a-177">c.</span></span> <span data-ttu-id="7512a-178">Navegue até o menu Integração e clique no link do **Munchkin**.</span><span class="sxs-lookup"><span data-stu-id="7512a-178">Navigate to the Integration menu and click the **Munchkin link**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="7512a-180">d.</span><span class="sxs-lookup"><span data-stu-id="7512a-180">d.</span></span> <span data-ttu-id="7512a-181">Copie a identificação do Munchkin mostrada na tela e conclua sua URL de resposta no assistente de configuração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7512a-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="7512a-183">Para configurar o SSO no aplicativo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="7512a-183">To configure the SSO in the application, follow the below steps:</span></span>
   
    <span data-ttu-id="7512a-184">a.</span><span class="sxs-lookup"><span data-stu-id="7512a-184">a.</span></span> <span data-ttu-id="7512a-185">Faça logon usando credenciais de administrador de aplicativo do Marketo.</span><span class="sxs-lookup"><span data-stu-id="7512a-185">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="7512a-186">b.</span><span class="sxs-lookup"><span data-stu-id="7512a-186">b.</span></span> <span data-ttu-id="7512a-187">Clique no botão **Admin** no painel de navegação superior.</span><span class="sxs-lookup"><span data-stu-id="7512a-187">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="7512a-189">c.</span><span class="sxs-lookup"><span data-stu-id="7512a-189">c.</span></span> <span data-ttu-id="7512a-190">Navegue até o menu Integração e clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="7512a-190">Navigate to the Integration menu and click **Single Sign On**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="7512a-192">d.</span><span class="sxs-lookup"><span data-stu-id="7512a-192">d.</span></span> <span data-ttu-id="7512a-193">Para habilitar as configurações de SAML, clique no botão **Editar**.</span><span class="sxs-lookup"><span data-stu-id="7512a-193">To enable the SAML Settings, click **Edit** button.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="7512a-195">e.</span><span class="sxs-lookup"><span data-stu-id="7512a-195">e.</span></span> <span data-ttu-id="7512a-196">Configurações de logon único **habilitadas**.</span><span class="sxs-lookup"><span data-stu-id="7512a-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="7512a-197">f.</span><span class="sxs-lookup"><span data-stu-id="7512a-197">f.</span></span> <span data-ttu-id="7512a-198">Colar a **ID da Entidade do SAML**, na caixa de texto **ID do Emissor**.</span><span class="sxs-lookup"><span data-stu-id="7512a-198">Paste the **SAML Entity ID**, in the **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="7512a-199">g.</span><span class="sxs-lookup"><span data-stu-id="7512a-199">g.</span></span> <span data-ttu-id="7512a-200">Na caixa de texto **ID da Entidade**, insira a URL como `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="7512a-200">In the **Entity ID** textbox, enter the URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="7512a-201">h.</span><span class="sxs-lookup"><span data-stu-id="7512a-201">h.</span></span> <span data-ttu-id="7512a-202">Selecione o local da ID de usuário como **elemento do Identificador de Nome**.</span><span class="sxs-lookup"><span data-stu-id="7512a-202">Select the User ID Location as **Name Identifier element**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="7512a-204">Se o identificador de usuário não for um valor de UPN, altere o valor na guia Atributo.</span><span class="sxs-lookup"><span data-stu-id="7512a-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span></span>
   
    <span data-ttu-id="7512a-205">i.</span><span class="sxs-lookup"><span data-stu-id="7512a-205">i.</span></span> <span data-ttu-id="7512a-206">Carregue o certificado que você baixou do assistente de configuração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7512a-206">Upload the certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="7512a-207">**Salve** as configurações.</span><span class="sxs-lookup"><span data-stu-id="7512a-207">**Save** the settings.</span></span>
   
    <span data-ttu-id="7512a-208">j.</span><span class="sxs-lookup"><span data-stu-id="7512a-208">j.</span></span> <span data-ttu-id="7512a-209">Edite as configurações de redirecionamento de páginas.</span><span class="sxs-lookup"><span data-stu-id="7512a-209">Edit the Redirect Pages settings.</span></span>
   
    <span data-ttu-id="7512a-210">k.</span><span class="sxs-lookup"><span data-stu-id="7512a-210">k.</span></span> <span data-ttu-id="7512a-211">Cole a **URL do Serviço de Logon Único do SAML** na caixa de texto **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="7512a-211">Paste the **SAML Single Sign-On Service URL** in the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="7512a-212">l.</span><span class="sxs-lookup"><span data-stu-id="7512a-212">l.</span></span> <span data-ttu-id="7512a-213">Cole a **URL de Logoff** na caixa de texto **URL de Logoff**.</span><span class="sxs-lookup"><span data-stu-id="7512a-213">Paste the **Sign-Out URL** in the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="7512a-214">m.</span><span class="sxs-lookup"><span data-stu-id="7512a-214">m.</span></span> <span data-ttu-id="7512a-215">Na **URL de erro**, copie a **URL da instância do Marketo** e clique no botão **Salvar** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="7512a-215">In the **Error URL**, copy your **Marketo instance URL** and click **Save** button to save settings.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="7512a-217">Para habilitar o SSO para usuários, conclua as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="7512a-217">To enable the SSO for users, complete the following actions:</span></span>
   
    <span data-ttu-id="7512a-218">a.</span><span class="sxs-lookup"><span data-stu-id="7512a-218">a.</span></span> <span data-ttu-id="7512a-219">Faça logon usando credenciais de administrador de aplicativo do Marketo.</span><span class="sxs-lookup"><span data-stu-id="7512a-219">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="7512a-220">b.</span><span class="sxs-lookup"><span data-stu-id="7512a-220">b.</span></span> <span data-ttu-id="7512a-221">Clique no botão **Admin** no painel de navegação superior.</span><span class="sxs-lookup"><span data-stu-id="7512a-221">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="7512a-223">c.</span><span class="sxs-lookup"><span data-stu-id="7512a-223">c.</span></span> <span data-ttu-id="7512a-224">Navegue até o menu **Segurança** e clique em **Configurações de Logon**.</span><span class="sxs-lookup"><span data-stu-id="7512a-224">Navigate to the **Security** menu and click **Login Settings**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="7512a-226">d.</span><span class="sxs-lookup"><span data-stu-id="7512a-226">d.</span></span> <span data-ttu-id="7512a-227">Marque a opção **Exigir SSO** e **salve** as configurações.</span><span class="sxs-lookup"><span data-stu-id="7512a-227">Check the **Require SSO** option and **Save** the settings.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="7512a-229">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="7512a-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7512a-230">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7512a-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7512a-231">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7512a-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7512a-232">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7512a-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="7512a-233">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7512a-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7512a-235">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7512a-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7512a-236">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7512a-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7512a-238">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7512a-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7512a-240">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7512a-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7512a-242">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7512a-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7512a-244">a.</span><span class="sxs-lookup"><span data-stu-id="7512a-244">a.</span></span> <span data-ttu-id="7512a-245">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="7512a-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7512a-246">b.</span><span class="sxs-lookup"><span data-stu-id="7512a-246">b.</span></span> <span data-ttu-id="7512a-247">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7512a-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7512a-248">c.</span><span class="sxs-lookup"><span data-stu-id="7512a-248">c.</span></span> <span data-ttu-id="7512a-249">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="7512a-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7512a-250">d.</span><span class="sxs-lookup"><span data-stu-id="7512a-250">d.</span></span> <span data-ttu-id="7512a-251">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7512a-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="7512a-252">Criar um usuário de teste do Marketo</span><span class="sxs-lookup"><span data-stu-id="7512a-252">Creating a Marketo test user</span></span>

<span data-ttu-id="7512a-253">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Marketo.</span><span class="sxs-lookup"><span data-stu-id="7512a-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="7512a-254">siga estas etapas para criar um usuário na plataforma do Marketo.</span><span class="sxs-lookup"><span data-stu-id="7512a-254">follow these steps to create a user in Marketo platform.</span></span>

1. <span data-ttu-id="7512a-255">Faça logon usando credenciais de administrador de aplicativo do Marketo.</span><span class="sxs-lookup"><span data-stu-id="7512a-255">Log in to Marketo app using admin credentials.</span></span>

2. <span data-ttu-id="7512a-256">Clique no botão **Admin** no painel de navegação superior.</span><span class="sxs-lookup"><span data-stu-id="7512a-256">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="7512a-258">Navegue até o menu **Segurança** e clique em **Usuários e Funções**</span><span class="sxs-lookup"><span data-stu-id="7512a-258">Navigate to the **Security** menu and click **Users & Roles**</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="7512a-260">Clique no link **Convidar Novo Usuário** na guia Usuários</span><span class="sxs-lookup"><span data-stu-id="7512a-260">Click the **Invite New User** link on the Users tab</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="7512a-262">No assistente para Convidar Novo Usuário, preencha as informações a seguir</span><span class="sxs-lookup"><span data-stu-id="7512a-262">In the Invite New User wizard fill the following information</span></span>
   
    <span data-ttu-id="7512a-263">a.</span><span class="sxs-lookup"><span data-stu-id="7512a-263">a.</span></span> <span data-ttu-id="7512a-264">Insira o endereço de **Email** do usuário na caixa de texto</span><span class="sxs-lookup"><span data-stu-id="7512a-264">Enter the user **Email** address in the textbox</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="7512a-266">b.</span><span class="sxs-lookup"><span data-stu-id="7512a-266">b.</span></span> <span data-ttu-id="7512a-267">Insira o **Nome** na caixa de texto</span><span class="sxs-lookup"><span data-stu-id="7512a-267">Enter the **First Name** in the textbox</span></span>
   
    <span data-ttu-id="7512a-268">c.</span><span class="sxs-lookup"><span data-stu-id="7512a-268">c.</span></span> <span data-ttu-id="7512a-269">Insira o **Sobrenome** na caixa de texto</span><span class="sxs-lookup"><span data-stu-id="7512a-269">Enter the **Last Name**  in the textbox</span></span>
   
    <span data-ttu-id="7512a-270">d.</span><span class="sxs-lookup"><span data-stu-id="7512a-270">d.</span></span> <span data-ttu-id="7512a-271">Clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="7512a-271">Click **Next**</span></span>

6. <span data-ttu-id="7512a-272">Na guia **Permissões**, selecione **userRoles** e clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="7512a-272">In the **Permissions** tab, select the **userRoles** and click **Next**</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="7512a-274">Clique no botão **Enviar** para enviar o convite de usuário</span><span class="sxs-lookup"><span data-stu-id="7512a-274">Click the **Send** button to send the user invitation</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="7512a-276">Os usuários receberão a notificação de email e precisarão clicar no link e alterar a senha para ativar a conta.</span><span class="sxs-lookup"><span data-stu-id="7512a-276">User receives the email notification and has to click the link and change the password to activate the account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7512a-277">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7512a-277">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7512a-278">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao Marketo.</span><span class="sxs-lookup"><span data-stu-id="7512a-278">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Marketo.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7512a-280">**Para atribuir Brenda Fernandes ao Marketo, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7512a-280">**To assign Britta Simon to Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="7512a-281">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7512a-281">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7512a-283">Na lista de aplicativos, selecione **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="7512a-283">In the applications list, select **Marketo**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="7512a-285">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7512a-285">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7512a-287">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7512a-287">Click **Add** button.</span></span> <span data-ttu-id="7512a-288">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7512a-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7512a-290">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7512a-290">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7512a-291">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7512a-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7512a-292">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7512a-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7512a-293">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7512a-293">Testing single sign-on</span></span>

<span data-ttu-id="7512a-294">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7512a-294">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7512a-295">Quando você clica no bloco Marketo no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo do Marketo.</span><span class="sxs-lookup"><span data-stu-id="7512a-295">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7512a-296">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7512a-296">Additional resources</span></span>

* [<span data-ttu-id="7512a-297">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7512a-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7512a-298">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7512a-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

