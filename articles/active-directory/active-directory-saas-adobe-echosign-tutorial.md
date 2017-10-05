---
title: "Tutorial: Integração do Azure Active Directory com o Adobe Sign | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Adobe Sign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b413772de1af1fbb128d29b81e5831cfd6a39ab4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="dbc37-103">Tutorial: Integração do Azure Active Directory ao Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="dbc37-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="dbc37-104">Neste tutorial, você aprende a integrar o Adobe Sign ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="dbc37-104">In this tutorial, you learn how to integrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dbc37-105">A integração do Adobe Sign ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="dbc37-105">Integrating Adobe Sign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dbc37-106">No Azure AD, é possível controlar quem tem acesso ao Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="dbc37-106">You can control in Azure AD who has access to Adobe Sign</span></span>
- <span data-ttu-id="dbc37-107">É possível permitir que os usuários se conectem automaticamente ao Adobe Sign (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbc37-107">You can enable your users to automatically get signed-on to Adobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dbc37-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dbc37-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dbc37-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dbc37-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbc37-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dbc37-110">Prerequisites</span></span>

<span data-ttu-id="dbc37-111">Para configurar a integração do Azure AD ao Adobe Sign, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="dbc37-111">To configure Azure AD integration with Adobe Sign, you need the following items:</span></span>

- <span data-ttu-id="dbc37-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dbc37-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dbc37-113">Uma assinatura habilitada para logon único do Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="dbc37-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dbc37-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="dbc37-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dbc37-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="dbc37-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dbc37-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="dbc37-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dbc37-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbc37-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dbc37-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="dbc37-118">Scenario description</span></span>
<span data-ttu-id="dbc37-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="dbc37-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dbc37-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="dbc37-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dbc37-121">Adicionando o Adobe Sign por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="dbc37-121">Adding Adobe Sign from the gallery</span></span>
2. <span data-ttu-id="dbc37-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dbc37-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-the-gallery"></a><span data-ttu-id="dbc37-123">Adicionando o Adobe Sign por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="dbc37-123">Adding Adobe Sign from the gallery</span></span>
<span data-ttu-id="dbc37-124">Para configurar a integração do Adobe Sign ao Azure AD, você precisa adicionar o Adobe Sign à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="dbc37-124">To configure the integration of Adobe Sign into Azure AD, you need to add Adobe Sign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dbc37-125">**Para adicionar o Adobe Sign por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="dbc37-125">**To add Adobe Sign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dbc37-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dbc37-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dbc37-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="dbc37-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dbc37-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="dbc37-133">Na caixa de pesquisa, digite **Adobe Sign**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-133">In the search box, type **Adobe Sign**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="dbc37-135">No painel de resultados, selecione **Adobe Sign** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dbc37-135">In the results panel, select **Adobe Sign**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dbc37-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dbc37-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dbc37-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Adobe Sign, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="dbc37-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dbc37-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Adobe Sign é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbc37-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Sign is to a user in Azure AD.</span></span> <span data-ttu-id="dbc37-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="dbc37-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Sign needs to be established.</span></span>

<span data-ttu-id="dbc37-141">No Adobe Sign, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="dbc37-141">In Adobe Sign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dbc37-142">Para configurar e testar o logon único do Azure AD com o Adobe Sign, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="dbc37-142">To configure and test Azure AD single sign-on with Adobe Sign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dbc37-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="dbc37-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dbc37-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="dbc37-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dbc37-145">**[Criando um usuário de teste do Adobe Sign](#creating-an-adobe-sign-test-user)** – para ter um equivalente de Brenda Fernandes no Adobe Sign que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbc37-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - to have a counterpart of Britta Simon in Adobe Sign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dbc37-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dbc37-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dbc37-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="dbc37-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dbc37-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbc37-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dbc37-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="dbc37-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="dbc37-150">**Para configurar o logon único do Azure AD com o Adobe Sign, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="dbc37-150">**To configure Azure AD single sign-on with Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="dbc37-151">No portal do Azure, na página de integração do aplicativo do **Adobe Sign**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-151">In the Azure portal, on the **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="dbc37-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="dbc37-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="dbc37-155">Na seção **Domínio e URLs do Adobe Sign**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="dbc37-155">On the **Adobe Sign Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="dbc37-157">a.</span><span class="sxs-lookup"><span data-stu-id="dbc37-157">a.</span></span> <span data-ttu-id="dbc37-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="dbc37-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="dbc37-159">b.</span><span class="sxs-lookup"><span data-stu-id="dbc37-159">b.</span></span> <span data-ttu-id="dbc37-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="dbc37-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dbc37-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="dbc37-161">These values are not real.</span></span> <span data-ttu-id="dbc37-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="dbc37-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dbc37-163">Contate a [equipe de suporte ao Cliente do Adobe Sign](https://helpx.adobe.com/in/contact/support.html) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="dbc37-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="dbc37-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="dbc37-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="dbc37-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="dbc37-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dbc37-168">Na seção **Configuração do Adobe Sign**, clique em **Configurar o Adobe Sign** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-168">On the **Adobe Sign Configuration** section, click **Configure Adobe Sign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dbc37-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="dbc37-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="dbc37-171">Em outra janela do navegador da Web, faça logon em seu site de empresa do Adobe Sign como administrador.</span><span class="sxs-lookup"><span data-stu-id="dbc37-171">In a different web browser window, log in to your Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="dbc37-172">No menu na parte superior, clique em **Conta** e, depois, no painel de navegação do lado esquerdo, clique em **Configurações do SAML**, em **Configurações da Conta**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-172">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="dbc37-173">![Conta](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Conta")</span><span class="sxs-lookup"><span data-stu-id="dbc37-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="dbc37-174">Na seção Configuração do SAML, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="dbc37-174">In the SAML Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="dbc37-175">![Configurações do SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Configurações do SAML")</span><span class="sxs-lookup"><span data-stu-id="dbc37-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="dbc37-176">a.</span><span class="sxs-lookup"><span data-stu-id="dbc37-176">a.</span></span> <span data-ttu-id="dbc37-177">Para **Modo do SAML**, selecione **SAML Obrigatório**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="dbc37-178">b.</span><span class="sxs-lookup"><span data-stu-id="dbc37-178">b.</span></span> <span data-ttu-id="dbc37-179">Selecione **Permitir que os Administradores da Conta do EchoSign façam logon usando suas Credenciais do EchoSign**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-179">Select **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="dbc37-180">c.</span><span class="sxs-lookup"><span data-stu-id="dbc37-180">c.</span></span> <span data-ttu-id="dbc37-181">Para **Criação de Usuário**, selecione **Adicionar automaticamente os usuários autenticados por meio do SAML**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="dbc37-182">Siga em frente executando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="dbc37-182">Move on, performing the following steps:</span></span>

       <span data-ttu-id="dbc37-183">![Configurações do SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Configurações do SAML")</span><span class="sxs-lookup"><span data-stu-id="dbc37-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="dbc37-184">a.</span><span class="sxs-lookup"><span data-stu-id="dbc37-184">a.</span></span> <span data-ttu-id="dbc37-185">Cole a **ID da Entidade SAML** copiada no portal do Azure para a caixa de texto **ID da Entidade do IdP**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-185">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="dbc37-186">b.</span><span class="sxs-lookup"><span data-stu-id="dbc37-186">b.</span></span> <span data-ttu-id="dbc37-187">Cole a **URL do Serviço de Logon Único SAML** copiada no portal do Azure para a caixa de texto **URL de Logon do IdP**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into the **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="dbc37-188">c.</span><span class="sxs-lookup"><span data-stu-id="dbc37-188">c.</span></span> <span data-ttu-id="dbc37-189">Cole a **URL de Saída** copiada no portal do Azure para a caixa de texto **URL de Logoff do IdP**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-189">Paste **Sign-Out URL**, which you have copied from Azure portal into the **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="dbc37-190">d.</span><span class="sxs-lookup"><span data-stu-id="dbc37-190">d.</span></span> <span data-ttu-id="dbc37-191">Abra o arquivo de **Certificado (Base64)** baixado no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **Certificado do IdP**</span><span class="sxs-lookup"><span data-stu-id="dbc37-191">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Certificate** textbox</span></span>

    <span data-ttu-id="dbc37-192">e.</span><span class="sxs-lookup"><span data-stu-id="dbc37-192">e.</span></span> <span data-ttu-id="dbc37-193">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="dbc37-194">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="dbc37-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dbc37-195">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="dbc37-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dbc37-196">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dbc37-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dbc37-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dbc37-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="dbc37-198">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="dbc37-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="dbc37-200">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="dbc37-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dbc37-201">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dbc37-203">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="dbc37-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dbc37-205">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dbc37-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dbc37-207">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="dbc37-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dbc37-209">a.</span><span class="sxs-lookup"><span data-stu-id="dbc37-209">a.</span></span> <span data-ttu-id="dbc37-210">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dbc37-211">b.</span><span class="sxs-lookup"><span data-stu-id="dbc37-211">b.</span></span> <span data-ttu-id="dbc37-212">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="dbc37-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dbc37-213">c.</span><span class="sxs-lookup"><span data-stu-id="dbc37-213">c.</span></span> <span data-ttu-id="dbc37-214">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dbc37-215">d.</span><span class="sxs-lookup"><span data-stu-id="dbc37-215">d.</span></span> <span data-ttu-id="dbc37-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="dbc37-217">Criando um usuário de teste do Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="dbc37-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="dbc37-218">Para permitir que os usuários do Azure AD façam logon no Adobe Sign, eles devem ser provisionados no Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="dbc37-218">To enable Azure AD users to log in to Adobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="dbc37-219">No caso do Adobe Sign, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="dbc37-219">In the case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="dbc37-220">É possível usar qualquer outra ferramenta de criação da conta de usuário do Adobe Sign ou as APIs fornecidas pelo Adobe Sign para provisionar contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="dbc37-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign to provision AAD user accounts.</span></span> 

<span data-ttu-id="dbc37-221">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="dbc37-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="dbc37-222">Faça logon em seu site de empresa do **Adobe Sign** como administrador.</span><span class="sxs-lookup"><span data-stu-id="dbc37-222">Log in to your **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="dbc37-223">No menu na parte superior, clique em **Conta** e, depois, no painel de navegação do lado esquerdo, clique em **Usuários e Grupos** e, em seguida, em **Criar um novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-223">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="dbc37-224">![Conta](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Conta")</span><span class="sxs-lookup"><span data-stu-id="dbc37-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="dbc37-225">Na seção **Criar Novo Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="dbc37-225">In the **Create New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="dbc37-226">![Criar usuário](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="dbc37-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="dbc37-227">a.</span><span class="sxs-lookup"><span data-stu-id="dbc37-227">a.</span></span> <span data-ttu-id="dbc37-228">Digite o **Endereço de Email**, **Nome** e **Sobrenome** de uma conta válida do AAD que deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="dbc37-228">Type the **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="dbc37-229">b.</span><span class="sxs-lookup"><span data-stu-id="dbc37-229">b.</span></span> <span data-ttu-id="dbc37-230">Clique em **Criar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="dbc37-231">O titular da conta do Azure Active Directory recebe um email que inclui um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="dbc37-231">The Azure Active Directory account holder receives an email that includes a link to confirm the account before it becomes active.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dbc37-232">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dbc37-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dbc37-233">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="dbc37-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adobe Sign.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="dbc37-235">**Para atribuir Brenda Fernandes ao Adobe Sign, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="dbc37-235">**To assign Britta Simon to Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="dbc37-236">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="dbc37-238">Na lista de aplicativos, selecione **Adobe Sign**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-238">In the applications list, select **Adobe Sign**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="dbc37-240">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="dbc37-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dbc37-242">Click **Add** button.</span></span> <span data-ttu-id="dbc37-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dbc37-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="dbc37-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="dbc37-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dbc37-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dbc37-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dbc37-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dbc37-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dbc37-248">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="dbc37-248">Testing single sign-on</span></span>

<span data-ttu-id="dbc37-249">Quando você clicar no bloco Adobe Sign no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="dbc37-249">When you click the Adobe Sign tile in the Access Panel, you should get automatically signed-on to your Adobe Sign application.</span></span>
<span data-ttu-id="dbc37-250">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dbc37-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dbc37-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="dbc37-251">Additional resources</span></span>

* [<span data-ttu-id="dbc37-252">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="dbc37-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dbc37-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dbc37-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

