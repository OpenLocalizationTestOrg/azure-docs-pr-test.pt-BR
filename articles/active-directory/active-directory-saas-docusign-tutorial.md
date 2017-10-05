---
title: "Tutorial: integração do Azure Active Directory com o DocuSign | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 29c99fdf39d366df90abc070f7b836320935035c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="cddf3-103">Tutorial: integração do Active Directory do Azure com o DocuSign</span><span class="sxs-lookup"><span data-stu-id="cddf3-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="cddf3-104">Neste tutorial, você aprende a integrar o DocuSign ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="cddf3-104">In this tutorial, you learn how to integrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cddf3-105">A integração do DocuSign ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="cddf3-105">Integrating DocuSign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cddf3-106">No Azure AD, é possível controlar quem tem acesso ao DocuSign</span><span class="sxs-lookup"><span data-stu-id="cddf3-106">You can control in Azure AD who has access to DocuSign</span></span>
- <span data-ttu-id="cddf3-107">É possível permitir que os usuários se conectem automaticamente ao DocuSign (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cddf3-107">You can enable your users to automatically get signed-on to DocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cddf3-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cddf3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cddf3-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cddf3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cddf3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cddf3-110">Prerequisites</span></span>

<span data-ttu-id="cddf3-111">Para configurar a integração do Azure AD ao DocuSign, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="cddf3-111">To configure Azure AD integration with DocuSign, you need the following items:</span></span>

- <span data-ttu-id="cddf3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cddf3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cddf3-113">Uma assinatura habilitada para logon único do DocuSign</span><span class="sxs-lookup"><span data-stu-id="cddf3-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cddf3-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cddf3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cddf3-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cddf3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cddf3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cddf3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cddf3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cddf3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cddf3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cddf3-118">Scenario description</span></span>
<span data-ttu-id="cddf3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cddf3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cddf3-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="cddf3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cddf3-121">Adicionando o DocuSign por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="cddf3-121">Adding DocuSign from the gallery</span></span>
2. <span data-ttu-id="cddf3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cddf3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-the-gallery"></a><span data-ttu-id="cddf3-123">Adicionando o DocuSign por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="cddf3-123">Adding DocuSign from the gallery</span></span>
<span data-ttu-id="cddf3-124">Para configurar a integração do DocuSign ao Azure AD, é necessário adicionar o DocuSign à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="cddf3-124">To configure the integration of DocuSign into Azure AD, you need to add DocuSign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cddf3-125">**Para adicionar o DocuSign por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cddf3-125">**To add DocuSign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cddf3-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cddf3-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cddf3-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cddf3-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cddf3-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cddf3-133">Na caixa de pesquisa, digite **Docusign**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-133">In the search box, type **DocuSign**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="cddf3-135">No painel de resultados, selecione **DocuSign** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cddf3-135">In the results panel, select **DocuSign**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cddf3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cddf3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cddf3-138">Nesta seção, você configura e testa o logon único do Azure AD com o DocuSign, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cddf3-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cddf3-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do DocuSign é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cddf3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DocuSign is to a user in Azure AD.</span></span> <span data-ttu-id="cddf3-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do DocuSign.</span><span class="sxs-lookup"><span data-stu-id="cddf3-140">In other words, a link relationship between an Azure AD user and the related user in DocuSign needs to be established.</span></span>

<span data-ttu-id="cddf3-141">Essa relação de vínculo é estabelecida com a atribuição do valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no DocuSign.</span><span class="sxs-lookup"><span data-stu-id="cddf3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in DocuSign.</span></span>

<span data-ttu-id="cddf3-142">Para configurar e testar o logon único do Azure AD com o DocuSign, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="cddf3-142">To configure and test Azure AD single sign-on with DocuSign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cddf3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cddf3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cddf3-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cddf3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cddf3-145">**[Criando um usuário de teste do DocuSign](#creating-a-docusign-test-user)** – para ter um equivalente de Brenda Fernandes no DocuSign que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cddf3-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - to have a counterpart of Britta Simon in DocuSign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cddf3-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cddf3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cddf3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="cddf3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cddf3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cddf3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cddf3-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo DocuSign.</span><span class="sxs-lookup"><span data-stu-id="cddf3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="cddf3-150">**Para configurar o logon único do Azure AD com o DocuSign, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cddf3-150">**To configure Azure AD single sign-on with DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="cddf3-151">No portal do Azure, na página de integração do aplicativo **DocuSign**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-151">In the Azure portal, on the **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cddf3-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="cddf3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="cddf3-155">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="cddf3-155">On the **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="cddf3-157">Na seção **Configuração do DocuSign** do portal do Azure, clique em **Configurar o DocuSign** para abrir a janela Configurar logon.</span><span class="sxs-lookup"><span data-stu-id="cddf3-157">On the **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** to open Configure sign-on window.</span></span> <span data-ttu-id="cddf3-158">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="cddf3-158">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="cddf3-160">Em outra janela do navegador da Web, faça logon no **portal de administração do DocuSign** como administrador.</span><span class="sxs-lookup"><span data-stu-id="cddf3-160">In a different web browser window, login to your **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="cddf3-161">No menu de navegação à esquerda, clique em **Domínios**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-161">In the navigation menu on the left, click **Domains**.</span></span>
   
    ![Configurando o logon único][51]

7. <span data-ttu-id="cddf3-163">No painel direito, clique em **Solicitar Domínio**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-163">On the right pane, click **Claim Domain**.</span></span>
   
    ![Configurando o logon único][52]

8. <span data-ttu-id="cddf3-165">Na caixa de diálogo **Solicitar um domínio**, na caixa de texto **Nome de Domínio**, digite o domínio de sua empresa e clique em **Solicitar**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-165">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="cddf3-166">Verifique o domínio e confira se o status está ativo.</span><span class="sxs-lookup"><span data-stu-id="cddf3-166">Make sure that you verify the domain and the status is active.</span></span>
   
    ![Configurando o logon único][53]

9. <span data-ttu-id="cddf3-168">No menu à esquerda, clique em **Provedores de Identidade**</span><span class="sxs-lookup"><span data-stu-id="cddf3-168">In menu on the left side, click **Identity Providers**</span></span>  
   
    ![Configurando o logon único][54]
10. <span data-ttu-id="cddf3-170">No painel direito, clique em **Adicionar Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-170">In the right pane, click **Add Identity Provider**.</span></span> 
   
    ![Configurando o logon único][55]

11. <span data-ttu-id="cddf3-172">Na página **Configurações do Provedor de Identidade** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cddf3-172">On the **Identity Provider Settings** page, perform the following steps:</span></span>
   
    ![Configurando o logon único][56]

    <span data-ttu-id="cddf3-174">a.</span><span class="sxs-lookup"><span data-stu-id="cddf3-174">a.</span></span> <span data-ttu-id="cddf3-175">Na caixa de texto **Nome** , digite um nome exclusivo para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="cddf3-175">In the **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="cddf3-176">Não use espaços.</span><span class="sxs-lookup"><span data-stu-id="cddf3-176">Do not use spaces.</span></span>

    <span data-ttu-id="cddf3-177">b.</span><span class="sxs-lookup"><span data-stu-id="cddf3-177">b.</span></span> <span data-ttu-id="cddf3-178">Cole a **ID da Entidade SAML** na caixa de texto **Emissor do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-178">Paste **SAML Entity ID** into the **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="cddf3-179">c.</span><span class="sxs-lookup"><span data-stu-id="cddf3-179">c.</span></span> <span data-ttu-id="cddf3-180">Cole a **URL do Serviço de Logon Único SAML** na caixa de texto **URL de Logon do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-180">Paste **SAML Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="cddf3-181">d.</span><span class="sxs-lookup"><span data-stu-id="cddf3-181">d.</span></span> <span data-ttu-id="cddf3-182">Cole a **URL de Saída** na caixa de texto **URL de Logoff do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-182">Paste **Sign-Out URL** into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="cddf3-183">e.</span><span class="sxs-lookup"><span data-stu-id="cddf3-183">e.</span></span> <span data-ttu-id="cddf3-184">Selecione **Assinar Solicitação AuthN**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="cddf3-185">f.</span><span class="sxs-lookup"><span data-stu-id="cddf3-185">f.</span></span> <span data-ttu-id="cddf3-186">Para **Enviar solicitação AuthN por**, selecione **POST**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="cddf3-187">g.</span><span class="sxs-lookup"><span data-stu-id="cddf3-187">g.</span></span> <span data-ttu-id="cddf3-188">Em **Enviar solicitação de logoff por**, selecione **GET**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="cddf3-189">Na seção **Mapeamento de Atributo Personalizado** , escolha o campo que você deseja mapear com a Declaração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cddf3-189">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span></span> <span data-ttu-id="cddf3-190">Neste exemplo, a declaração **emailaddress** é mapeada com o valor de **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-190">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="cddf3-191">Esse é o nome de declaração padrão do Azure AD para a declaração de email.</span><span class="sxs-lookup"><span data-stu-id="cddf3-191">It is the default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="cddf3-192">Use o **Identificador de usuário** apropriado para mapear o usuário do Azure AD para o mapeamento de usuário do DocuSign.</span><span class="sxs-lookup"><span data-stu-id="cddf3-192">Use the appropriate **User identifier** to map the user from Azure AD to DocuSign user mapping.</span></span> <span data-ttu-id="cddf3-193">Selecione o campo adequado e insira o valor apropriado com base nas configurações de sua organização.</span><span class="sxs-lookup"><span data-stu-id="cddf3-193">Select the proper Field and enter the appropriate value based on your organization settings.</span></span>
          
    ![Configurando o logon único][57]

13. <span data-ttu-id="cddf3-195">Na seção **Certificado do Provedor de Identidade**, clique em **Adicionar Certificado** e, depois, carregue o certificado baixado no portal do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cddf3-195">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Configurando o logon único][58]

14. <span data-ttu-id="cddf3-197">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-197">Click **Save**.</span></span>

15. <span data-ttu-id="cddf3-198">Na seção **Provedores de Identidade**, clique em **Ações** e em **Pontos de Extremidade**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-198">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Configurando o logon único][59]
 
16. <span data-ttu-id="cddf3-200">Na seção **Exibir Pontos de Extremidade do SAML 2.0** do **portal de administração do DocuSign**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cddf3-200">In the **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform the following steps:</span></span>
   
    ![Configurando o logon único][60]
   
    <span data-ttu-id="cddf3-202">a.</span><span class="sxs-lookup"><span data-stu-id="cddf3-202">a.</span></span> <span data-ttu-id="cddf3-203">Copie a **URL de Emissor do Provedor de Serviço** e, em seguida, cole-a na caixa de texto **Identificador** na seção **Domínio e URLs do DocuSign** do portal do Azure seguindo o padrão: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="cddf3-203">Copy the **Service Provider Issuer URL**, and then paste into the **Identifier** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="cddf3-204">b.</span><span class="sxs-lookup"><span data-stu-id="cddf3-204">b.</span></span> <span data-ttu-id="cddf3-205">Copie a **URL de Logon do Provedor de Serviço** e, em seguida, cole-a na caixa de texto **URL de Logon** na seção **Domínio e URLs do DocuSign** do portal do Azure seguindo o padrão: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="cddf3-205">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="cddf3-207">c.</span><span class="sxs-lookup"><span data-stu-id="cddf3-207">c.</span></span>  <span data-ttu-id="cddf3-208">Clique em **Fechar**</span><span class="sxs-lookup"><span data-stu-id="cddf3-208">Click **Close**</span></span>
    
17. <span data-ttu-id="cddf3-209">No portal do Azure, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-209">On the Azure portal, click **Save**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="cddf3-211">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="cddf3-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cddf3-212">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="cddf3-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cddf3-213">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cddf3-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cddf3-214">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cddf3-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="cddf3-215">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cddf3-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cddf3-217">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cddf3-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cddf3-218">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cddf3-220">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cddf3-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cddf3-222">Na parte superior da caixa de diálogo, clique em **Adicionar** para abrir a caixa de diálogo **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cddf3-224">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cddf3-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cddf3-226">a.</span><span class="sxs-lookup"><span data-stu-id="cddf3-226">a.</span></span> <span data-ttu-id="cddf3-227">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cddf3-228">b.</span><span class="sxs-lookup"><span data-stu-id="cddf3-228">b.</span></span> <span data-ttu-id="cddf3-229">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cddf3-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cddf3-230">c.</span><span class="sxs-lookup"><span data-stu-id="cddf3-230">c.</span></span> <span data-ttu-id="cddf3-231">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cddf3-232">d.</span><span class="sxs-lookup"><span data-stu-id="cddf3-232">d.</span></span> <span data-ttu-id="cddf3-233">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="cddf3-234">Criando um usuário de teste do DocuSign</span><span class="sxs-lookup"><span data-stu-id="cddf3-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="cddf3-235">O aplicativo dá suporte ao **provisionamento de usuário Just-In-Time** e, após a autenticação, os usuários são criados no aplicativo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cddf3-235">Application supports **Just in time user provisioning** and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cddf3-236">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cddf3-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cddf3-237">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao DocuSign.</span><span class="sxs-lookup"><span data-stu-id="cddf3-237">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to DocuSign.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cddf3-239">**Para atribuir Brenda Fernandes ao DocuSign, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cddf3-239">**To assign Britta Simon to DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="cddf3-240">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cddf3-242">Na lista de aplicativos, selecione **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-242">In the applications list, select **DocuSign**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="cddf3-244">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cddf3-246">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cddf3-246">Click **Add** button.</span></span> <span data-ttu-id="cddf3-247">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cddf3-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cddf3-249">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cddf3-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cddf3-250">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cddf3-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cddf3-251">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cddf3-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cddf3-252">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cddf3-252">Testing single sign-on</span></span>

<span data-ttu-id="cddf3-253">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="cddf3-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cddf3-254">Quando você clicar no bloco do DocuSign no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo DocuSign.</span><span class="sxs-lookup"><span data-stu-id="cddf3-254">When you click the DocuSign tile in the Access Panel, you should get automatically signed-on to your DocuSign application.</span></span>
<span data-ttu-id="cddf3-255">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cddf3-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cddf3-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cddf3-256">Additional resources</span></span>

* [<span data-ttu-id="cddf3-257">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cddf3-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cddf3-258">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cddf3-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="cddf3-259">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="cddf3-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

