---
title: "Tutorial: integração do Azure Active Directory com o ClickTime | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: 0e0123a40d52dfd7a2e29c29cb2239e979089ca9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="60c82-103">Tutorial: integração do Active Directory do Azure ao ClickTime</span><span class="sxs-lookup"><span data-stu-id="60c82-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="60c82-104">Neste tutorial, você aprenderá a integrar o ClickTime ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="60c82-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60c82-105">A integração do ClickTime ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="60c82-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="60c82-106">Você pode controlar no Azure AD quem tem acesso ao ClickTime</span><span class="sxs-lookup"><span data-stu-id="60c82-106">You can control in Azure AD who has access to ClickTime</span></span>
- <span data-ttu-id="60c82-107">É possível permitir que seus usuários façam logon automaticamente no ClickTime (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="60c82-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60c82-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="60c82-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="60c82-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="60c82-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60c82-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="60c82-110">Prerequisites</span></span>

<span data-ttu-id="60c82-111">Para configurar a integração do Azure AD com o ClickTime, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="60c82-111">To configure Azure AD integration with ClickTime, you need the following items:</span></span>

- <span data-ttu-id="60c82-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="60c82-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60c82-113">Uma assinatura do ClickTime habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="60c82-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60c82-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="60c82-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60c82-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="60c82-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60c82-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="60c82-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60c82-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60c82-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60c82-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="60c82-118">Scenario description</span></span>
<span data-ttu-id="60c82-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="60c82-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60c82-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="60c82-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60c82-121">Adicionando ClickTime da galeria</span><span class="sxs-lookup"><span data-stu-id="60c82-121">Adding ClickTime from the gallery</span></span>
2. <span data-ttu-id="60c82-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="60c82-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-the-gallery"></a><span data-ttu-id="60c82-123">Adicionando ClickTime da galeria</span><span class="sxs-lookup"><span data-stu-id="60c82-123">Adding ClickTime from the gallery</span></span>
<span data-ttu-id="60c82-124">Para configurar a integração do ClickTime com o Azure AD, você precisará adicionar o ClickTime à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="60c82-124">To configure the integration of ClickTime into Azure AD, you need to add ClickTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60c82-125">**Para adicionar o ClickTime por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="60c82-125">**To add ClickTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60c82-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="60c82-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="60c82-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="60c82-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="60c82-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="60c82-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="60c82-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="60c82-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="60c82-133">Na caixa de pesquisa, digite **ClickTime**, selecione **ClickTime** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="60c82-133">In the search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button to add the application.</span></span>

    ![ClickTime na lista de resultados](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="60c82-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="60c82-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="60c82-136">Nesta seção, você configurará e testará o logon único do Azure AD com o ClickTime, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="60c82-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="60c82-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ClickTime é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60c82-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span></span> <span data-ttu-id="60c82-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no ClickTime.</span><span class="sxs-lookup"><span data-stu-id="60c82-138">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span></span>

<span data-ttu-id="60c82-139">No ClickTime, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="60c82-139">In ClickTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="60c82-140">Para configurar e testar o logon único do Azure AD com o ClickTime, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="60c82-140">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60c82-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="60c82-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="60c82-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="60c82-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60c82-143">**[Criar um usuário de teste do ClickTime](#create-a-clicktime-test-user)** – para ter um equivalente de Brenda Fernandes no ClickTime que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60c82-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="60c82-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60c82-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60c82-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="60c82-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="60c82-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="60c82-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="60c82-147">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo ClickTime.</span><span class="sxs-lookup"><span data-stu-id="60c82-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="60c82-148">**Para configurar o logon único do Azure AD com o ClickTime, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="60c82-148">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="60c82-149">No Portal do Azure, na página de integração do aplicativo **ClickTime**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="60c82-149">In the Azure portal, on the **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="60c82-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="60c82-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="60c82-153">Na seção **Domínio e URLs do ClickTime**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="60c82-153">On the **ClickTime Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="60c82-155">a.</span><span class="sxs-lookup"><span data-stu-id="60c82-155">a.</span></span> <span data-ttu-id="60c82-156">Na caixa de texto **Identificador**, digite uma URL como: `https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="60c82-156">In the **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="60c82-157">b.</span><span class="sxs-lookup"><span data-stu-id="60c82-157">b.</span></span> <span data-ttu-id="60c82-158">Na caixa de texto **URL de Resposta** , digite uma URL nos seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="60c82-158">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="60c82-159">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="60c82-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="60c82-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="60c82-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="60c82-163">Na seção **Configuração do ClickTime**, clique em **Configurar o ClickTime** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="60c82-163">On the **ClickTime Configuration** section, click **Configure ClickTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="60c82-164">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="60c82-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="60c82-166">Em outra janela do navegador da Web, faça logon em seu site de empresa do ClickTime como administrador.</span><span class="sxs-lookup"><span data-stu-id="60c82-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="60c82-167">Na barra de ferramentas na parte superior, clique em **Preferências** e em **Configurações de Segurança**.</span><span class="sxs-lookup"><span data-stu-id="60c82-167">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="60c82-168">Na seção de configuração de **Preferências de Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="60c82-168">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="60c82-169">![Configurações de segurança](./media/active-directory-saas-clicktime-tutorial/tic777280.png "as configurações de segurança")</span><span class="sxs-lookup"><span data-stu-id="60c82-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="60c82-170">a.</span><span class="sxs-lookup"><span data-stu-id="60c82-170">a.</span></span>  <span data-ttu-id="60c82-171">Selecione **Permitir** a entrada usando o SSO (Logon Único) com **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="60c82-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="60c82-172">b.</span><span class="sxs-lookup"><span data-stu-id="60c82-172">b.</span></span> <span data-ttu-id="60c82-173">Na caixa de texto **Ponto de Extremidade de Provedor de Identidade**, cole a **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="60c82-173">In the **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="60c82-174">c.</span><span class="sxs-lookup"><span data-stu-id="60c82-174">c.</span></span>  <span data-ttu-id="60c82-175">Abra o **certificado codificado em Base 64** baixado no Portal do Azure no **Bloco de notas**, copie o conteúdo e cole-o na caixa de texto **Certificado X.509**.</span><span class="sxs-lookup"><span data-stu-id="60c82-175">Open the **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="60c82-176">d.</span><span class="sxs-lookup"><span data-stu-id="60c82-176">d.</span></span>  <span data-ttu-id="60c82-177">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="60c82-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="60c82-178">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="60c82-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="60c82-179">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="60c82-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="60c82-180">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="60c82-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="60c82-181">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="60c82-181">Create an Azure AD test user</span></span>
<span data-ttu-id="60c82-182">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="60c82-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="60c82-184">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="60c82-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60c82-185">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="60c82-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="60c82-187">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="60c82-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="60c82-189">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="60c82-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60c82-191">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="60c82-191">In the **User** dialog box, perform the following steps:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60c82-193">a.</span><span class="sxs-lookup"><span data-stu-id="60c82-193">a.</span></span> <span data-ttu-id="60c82-194">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="60c82-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60c82-195">b.</span><span class="sxs-lookup"><span data-stu-id="60c82-195">b.</span></span> <span data-ttu-id="60c82-196">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="60c82-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60c82-197">c.</span><span class="sxs-lookup"><span data-stu-id="60c82-197">c.</span></span> <span data-ttu-id="60c82-198">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="60c82-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="60c82-199">d.</span><span class="sxs-lookup"><span data-stu-id="60c82-199">d.</span></span> <span data-ttu-id="60c82-200">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="60c82-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="60c82-201">Criar um usuário de teste do ClickTime</span><span class="sxs-lookup"><span data-stu-id="60c82-201">Create a ClickTime test user</span></span>

<span data-ttu-id="60c82-202">Para permitir que os usuários do Azure AD façam logon no ClickTime, eles devem ser provisionados no ClickTime.</span><span class="sxs-lookup"><span data-stu-id="60c82-202">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="60c82-203">No caso do ClickTime, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="60c82-203">In the case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="60c82-204">É possível usar qualquer outra ferramenta de criação da conta de usuário do ClickTime ou as APIs fornecidas pelo ClickTime para provisionar as contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60c82-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span></span>

<span data-ttu-id="60c82-205">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="60c82-205">**To provision a user account, perform the following steps:**</span></span>
1. <span data-ttu-id="60c82-206">Faça logon em seu locatário do **ClickTime** .</span><span class="sxs-lookup"><span data-stu-id="60c82-206">Log in to your **ClickTime** tenant.</span></span>
2. <span data-ttu-id="60c82-207">Na barra de ferramentas na parte superior, clique na **Empresa** e em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="60c82-207">In the toolbar on the top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="60c82-208">![Pessoas](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="60c82-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="60c82-209">Clique em **Adicionar Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="60c82-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="60c82-210">![Adicionar pessoa](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Adicionar pessoa")</span><span class="sxs-lookup"><span data-stu-id="60c82-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="60c82-211">Na seção Nova Pessoa, execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="60c82-211">In the New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="60c82-212">![Pessoas](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="60c82-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="60c82-213">a.</span><span class="sxs-lookup"><span data-stu-id="60c82-213">a.</span></span>  <span data-ttu-id="60c82-214">Na caixa de texto **nome completo**, digite o nome completo do usuário, por exemplo, **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="60c82-214">In the **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="60c82-215">b.</span><span class="sxs-lookup"><span data-stu-id="60c82-215">b.</span></span>  <span data-ttu-id="60c82-216">Na caixa de texto **endereço de email**, digite o endereço de email do usuário, por exemplo, **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="60c82-216">In the **email address** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="60c82-217">Se quiser, defina propriedades adicionais do novo objeto pessoa.</span><span class="sxs-lookup"><span data-stu-id="60c82-217">If you want to, you can set additional properties of the new person object.</span></span>
   
    <span data-ttu-id="60c82-218">c.</span><span class="sxs-lookup"><span data-stu-id="60c82-218">c.</span></span>  <span data-ttu-id="60c82-219">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="60c82-219">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="60c82-220">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="60c82-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="60c82-221">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao ClickTime.</span><span class="sxs-lookup"><span data-stu-id="60c82-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClickTime.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="60c82-223">**Para atribuir Brenda Fernandes ao ClickTime, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="60c82-223">**To assign Britta Simon to ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="60c82-224">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="60c82-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="60c82-226">Na lista de aplicativos, selecione **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="60c82-226">In the applications list, select **ClickTime**.</span></span>

    ![O link do ClickTimne na lista de Aplicativos](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="60c82-228">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="60c82-228">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202] 

4. <span data-ttu-id="60c82-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="60c82-230">Click **Add** button.</span></span> <span data-ttu-id="60c82-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="60c82-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="60c82-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="60c82-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="60c82-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="60c82-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="60c82-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="60c82-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="60c82-236">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="60c82-236">Test single sign-on</span></span>

<span data-ttu-id="60c82-237">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="60c82-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60c82-238">Ao clicar no bloco do ClickTime no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo do ClickTime.</span><span class="sxs-lookup"><span data-stu-id="60c82-238">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span></span>
<span data-ttu-id="60c82-239">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="60c82-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60c82-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="60c82-240">Additional resources</span></span>

* [<span data-ttu-id="60c82-241">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="60c82-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60c82-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="60c82-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

