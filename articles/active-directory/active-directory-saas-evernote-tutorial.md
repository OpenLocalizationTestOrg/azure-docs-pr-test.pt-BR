---
title: "Tutorial: Integração do Azure Active Directory ao Evernote | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: be94152a84bbbeacb623d7dd8b540e3981931a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="7585d-103">Tutorial: Integração do Azure Active Directory ao Evernote</span><span class="sxs-lookup"><span data-stu-id="7585d-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="7585d-104">Neste tutorial, você aprenderá a integrar o Evernote ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7585d-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7585d-105">A integração do Evernote ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7585d-105">Integrating Evernote with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7585d-106">No Azure AD, é possível controlar quem tem acesso ao Evernote.</span><span class="sxs-lookup"><span data-stu-id="7585d-106">You can control in Azure AD who has access to Evernote.</span></span>
- <span data-ttu-id="7585d-107">Você pode permitir que seus usuários façam logon automaticamente no Evernote usando logon único com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7585d-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7585d-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7585d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7585d-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7585d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7585d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7585d-110">Prerequisites</span></span>

<span data-ttu-id="7585d-111">Para configurar a integração do Azure AD com o Evernote, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7585d-111">To configure Azure AD integration with Evernote, you need the following items:</span></span>

- <span data-ttu-id="7585d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7585d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7585d-113">Uma assinatura do Evernote habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="7585d-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7585d-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7585d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7585d-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7585d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7585d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7585d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7585d-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7585d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7585d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7585d-118">Scenario description</span></span>
<span data-ttu-id="7585d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7585d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7585d-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7585d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7585d-121">Adicionar o Evernote da galeria</span><span class="sxs-lookup"><span data-stu-id="7585d-121">Adding Evernote from the gallery</span></span>
2. <span data-ttu-id="7585d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7585d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-the-gallery"></a><span data-ttu-id="7585d-123">Adicionar o Evernote da galeria</span><span class="sxs-lookup"><span data-stu-id="7585d-123">Adding Evernote from the gallery</span></span>
<span data-ttu-id="7585d-124">Para configurar a integração do Evernote ao Azure AD, você precisará adicionar o Evernote da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7585d-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7585d-125">**Para adicionar o Evernote da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7585d-125">**To add Evernote from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7585d-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7585d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="7585d-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7585d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7585d-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7585d-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="7585d-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7585d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="7585d-133">Na caixa de pesquisa, digite **Evernote**, selecione **Evernote** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7585d-133">In the search box, type **Evernote**, select **Evernote** from result panel then click **Add** button to add the application.</span></span>

    ![Evernote na lista de resultados](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7585d-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7585d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7585d-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Evernote, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7585d-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7585d-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Evernote é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7585d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span></span> <span data-ttu-id="7585d-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Evernote.</span><span class="sxs-lookup"><span data-stu-id="7585d-138">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span></span>

<span data-ttu-id="7585d-139">No Evernote, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="7585d-139">In Evernote, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7585d-140">Para configurar e testar o logon único do Azure AD com o Evernote, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="7585d-140">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7585d-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7585d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7585d-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7585d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7585d-143">**[Criar um usuário de teste do Evernote](#create-an-evernote-test-user)** – para ter um equivalente de Brenda Fernandes no Evernote vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7585d-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - to have a counterpart of Britta Simon in Evernote that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7585d-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7585d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7585d-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7585d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7585d-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7585d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7585d-147">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Evernote.</span><span class="sxs-lookup"><span data-stu-id="7585d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="7585d-148">**Para configurar o logon único do Azure AD com o Evernote, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7585d-148">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="7585d-149">No portal do Azure, na página de integração do aplicativo **Evernote**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7585d-149">In the Azure portal, on the **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="7585d-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7585d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="7585d-153">Na seção **Domínio e URLs do Evernote**, realize as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo IDP:</span><span class="sxs-lookup"><span data-stu-id="7585d-153">On the **Evernote Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Informações de logon único de URLs e Domínio do Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="7585d-155">Na caixa de texto **Identificador**, digite a URL: `https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="7585d-155">In the **Identifier** textbox, type the URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="7585d-156">Marque **Mostrar configurações avançadas de URL** e realize a seguinte etapa se quiser configurar o aplicativo no modo iniciado pelo **SP**:</span><span class="sxs-lookup"><span data-stu-id="7585d-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Informações de logon único de URLs e Domínio do Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="7585d-158">Na caixa de texto **URL de Entrada**, digite a URL: `https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="7585d-158">In the **Sign on URL** textbox, type the URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="7585d-159">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="7585d-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="7585d-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7585d-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7585d-163">Na seção **Configuração do Evernote**, clique em **Configurar o Evernote** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="7585d-163">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7585d-164">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="7585d-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração de Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="7585d-166">Em outra janela do navegador da Web, faça logon em seu site de empresa do Evernote como administrador.</span><span class="sxs-lookup"><span data-stu-id="7585d-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="7585d-167">Acesse **'Console de Administração'**</span><span class="sxs-lookup"><span data-stu-id="7585d-167">Go to **'Admin Console'**</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="7585d-169">No **'Console de Administração'**, acesse **'Segurança'** e selecione **'Logon Único'**</span><span class="sxs-lookup"><span data-stu-id="7585d-169">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="7585d-171">Configure os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="7585d-171">Configure the following values:</span></span>

    ![Certificate-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="7585d-173">a.</span><span class="sxs-lookup"><span data-stu-id="7585d-173">a.</span></span>  <span data-ttu-id="7585d-174">**Habilitar SSO:** o SSO está habilitado por padrão (clique em **Desabilitar Logon Único** para remover o requisito de SSO)</span><span class="sxs-lookup"><span data-stu-id="7585d-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span></span>

    <span data-ttu-id="7585d-175">b.</span><span class="sxs-lookup"><span data-stu-id="7585d-175">b.</span></span> <span data-ttu-id="7585d-176">Cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure na caixa de texto **URL de solicitação HTTP SAML**.</span><span class="sxs-lookup"><span data-stu-id="7585d-176">Paste **SAML Single sign-on Service URL** value, which you have copied from the Azure portal into the **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="7585d-177">c.</span><span class="sxs-lookup"><span data-stu-id="7585d-177">c.</span></span> <span data-ttu-id="7585d-178">Abra o certificado baixado no Azure AD em um bloco de notas e copie o conteúdo, incluindo "BEGIN CERTIFICATE" e "END CERTIFICATE" e cole-o na caixa de texto **Certificado X.509**.</span><span class="sxs-lookup"><span data-stu-id="7585d-178">Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into the **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="7585d-179">d.Clique em **Salvar Alterações**</span><span class="sxs-lookup"><span data-stu-id="7585d-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="7585d-180">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="7585d-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7585d-181">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7585d-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7585d-182">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7585d-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7585d-183">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7585d-183">Create an Azure AD test user</span></span>

<span data-ttu-id="7585d-184">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7585d-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="7585d-186">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7585d-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7585d-187">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7585d-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7585d-189">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7585d-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7585d-191">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="7585d-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7585d-193">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7585d-193">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7585d-195">a.</span><span class="sxs-lookup"><span data-stu-id="7585d-195">a.</span></span> <span data-ttu-id="7585d-196">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="7585d-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7585d-197">b.</span><span class="sxs-lookup"><span data-stu-id="7585d-197">b.</span></span> <span data-ttu-id="7585d-198">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7585d-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7585d-199">c.</span><span class="sxs-lookup"><span data-stu-id="7585d-199">c.</span></span> <span data-ttu-id="7585d-200">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="7585d-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7585d-201">d.</span><span class="sxs-lookup"><span data-stu-id="7585d-201">d.</span></span> <span data-ttu-id="7585d-202">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7585d-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="7585d-203">Criar um usuário de teste do Evernote</span><span class="sxs-lookup"><span data-stu-id="7585d-203">Create an Evernote test user</span></span>

<span data-ttu-id="7585d-204">Para permitir que os usuários do Azure AD façam logon no Evernote, eles deverão ser provisionados no Evernote.</span><span class="sxs-lookup"><span data-stu-id="7585d-204">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="7585d-205">No caso do Evernote, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="7585d-205">In the case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="7585d-206">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7585d-206">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="7585d-207">Faça logon em seu site de empresa do Evernote como administrador.</span><span class="sxs-lookup"><span data-stu-id="7585d-207">Log in to your Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="7585d-208">Clique no **'Console de Administração'**.</span><span class="sxs-lookup"><span data-stu-id="7585d-208">Click the **'Admin Console'**.</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="7585d-210">No **'Console de Administração'**, acesse **'Adicionar usuários'**.</span><span class="sxs-lookup"><span data-stu-id="7585d-210">From the **'Admin Console'**, go to **‘Add users’**.</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="7585d-212">**Adicionar membros da equipe** na caixa de texto **Email**, digite o endereço de email da conta de usuário e clique em **Convidar.**</span><span class="sxs-lookup"><span data-stu-id="7585d-212">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="7585d-214">Após o envio do convite, o titular da conta do Azure Active Directory receberá um email para aceitar o convite.</span><span class="sxs-lookup"><span data-stu-id="7585d-214">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7585d-215">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7585d-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="7585d-216">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Evernote.</span><span class="sxs-lookup"><span data-stu-id="7585d-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evernote.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="7585d-218">**Para atribuir Brenda Fernandes ao Evernote, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7585d-218">**To assign Britta Simon to Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="7585d-219">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7585d-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7585d-221">Na lista de aplicativos, escolha **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="7585d-221">In the applications list, select **Evernote**.</span></span>

    ![O link do Evernote na lista de Aplicativos](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="7585d-223">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7585d-223">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="7585d-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7585d-225">Click **Add** button.</span></span> <span data-ttu-id="7585d-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7585d-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="7585d-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7585d-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7585d-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7585d-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7585d-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7585d-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7585d-231">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="7585d-231">Test single sign-on</span></span>

<span data-ttu-id="7585d-232">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7585d-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7585d-233">Ao clicar no bloco do Evernote no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo de Evernote.</span><span class="sxs-lookup"><span data-stu-id="7585d-233">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span></span> <span data-ttu-id="7585d-234">Você entrará como uma conta de Organização, mas precisará fazer logon com sua conta pessoal.</span><span class="sxs-lookup"><span data-stu-id="7585d-234">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7585d-235">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7585d-235">Additional resources</span></span>

* [<span data-ttu-id="7585d-236">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7585d-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7585d-237">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7585d-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

