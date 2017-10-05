---
title: "Tutorial: Integração do Azure Active Directory com o Image Relay | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Image Relay."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 0bfbbaee7a74df6508584b7c8846fd07c2dc15c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="54222-103">Tutorial: Integração do Azure Active Directory com o Image Relay</span><span class="sxs-lookup"><span data-stu-id="54222-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="54222-104">Neste tutorial, você aprende a integrar o Image Relay ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="54222-104">In this tutorial, you learn how to integrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54222-105">A integração do Image Relay ao Azure AD proporciona os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="54222-105">Integrating Image Relay with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54222-106">No Azure AD, você pode controlar quem tem acesso ao Image Relay</span><span class="sxs-lookup"><span data-stu-id="54222-106">You can control in Azure AD who has access to Image Relay</span></span>
- <span data-ttu-id="54222-107">Você pode permitir que seus usuários façam logon automaticamente no Image Relay (Logon Único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="54222-107">You can enable your users to automatically get signed-on to Image Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="54222-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="54222-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="54222-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="54222-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54222-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="54222-110">Prerequisites</span></span>

<span data-ttu-id="54222-111">Para configurar a integração do Azure AD ao Image Relay, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="54222-111">To configure Azure AD integration with Image Relay, you need the following items:</span></span>

- <span data-ttu-id="54222-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="54222-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54222-113">Uma assinatura habilitada para logon único do Image Relay</span><span class="sxs-lookup"><span data-stu-id="54222-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54222-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="54222-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54222-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="54222-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54222-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="54222-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54222-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54222-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54222-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="54222-118">Scenario description</span></span>
<span data-ttu-id="54222-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="54222-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54222-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="54222-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54222-121">Adicionar o Image Relay da galeria</span><span class="sxs-lookup"><span data-stu-id="54222-121">Adding Image Relay from the gallery</span></span>
2. <span data-ttu-id="54222-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="54222-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-the-gallery"></a><span data-ttu-id="54222-123">Adicionar o Image Relay da galeria</span><span class="sxs-lookup"><span data-stu-id="54222-123">Adding Image Relay from the gallery</span></span>
<span data-ttu-id="54222-124">Para configurar a integração do Image Relay ao Azure AD, você precisará adicionar o Image Relay da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="54222-124">To configure the integration of Image Relay into Azure AD, you need to add Image Relay from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54222-125">**Para adicionar o Image Relay da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="54222-125">**To add Image Relay from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54222-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54222-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="54222-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="54222-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54222-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="54222-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="54222-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="54222-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="54222-133">Na caixa de pesquisa, digite **Image Relay**.</span><span class="sxs-lookup"><span data-stu-id="54222-133">In the search box, type **Image Relay**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="54222-135">No painel de resultados, selecione **Image Relay** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="54222-135">In the results panel, select **Image Relay**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="54222-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="54222-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="54222-138">Nesta seção, você configura e testa o logon único do Azure AD com o Image Relay com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="54222-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54222-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Image Relay é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54222-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Image Relay is to a user in Azure AD.</span></span> <span data-ttu-id="54222-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Image Relay.</span><span class="sxs-lookup"><span data-stu-id="54222-140">In other words, a link relationship between an Azure AD user and the related user in Image Relay needs to be established.</span></span>

<span data-ttu-id="54222-141">No Image Relay, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="54222-141">In Image Relay, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="54222-142">Para configurar e testar o logon único do Azure AD com o Image Relay, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="54222-142">To configure and test Azure AD single sign-on with Image Relay, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54222-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="54222-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="54222-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="54222-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54222-145">**[Como criar um usuário de teste do Image Relay](#creating-an-image-relay-test-user)** – para ter um equivalente de Brenda Fernandes no Image Relay que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54222-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - to have a counterpart of Britta Simon in Image Relay that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="54222-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="54222-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54222-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="54222-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="54222-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="54222-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="54222-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Image Relay.</span><span class="sxs-lookup"><span data-stu-id="54222-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="54222-150">**Para configurar o logon único do Azure AD com o Image Relay, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="54222-150">**To configure Azure AD single sign-on with Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="54222-151">No portal do Azure, na página de integração de aplicativos do **Image Relay**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="54222-151">In the Azure portal, on the **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="54222-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="54222-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="54222-155">Na seção **URLs e Domínio do Image Relay**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="54222-155">On the **Image Relay Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="54222-157">a.</span><span class="sxs-lookup"><span data-stu-id="54222-157">a.</span></span> <span data-ttu-id="54222-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="54222-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="54222-159">b.</span><span class="sxs-lookup"><span data-stu-id="54222-159">b.</span></span> <span data-ttu-id="54222-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="54222-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54222-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="54222-161">These values are not real.</span></span> <span data-ttu-id="54222-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="54222-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="54222-163">Entre em contato com [equipe de suporte do cliente do Image Relay](http://support.imagerelay.com/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="54222-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="54222-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="54222-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="54222-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="54222-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="54222-168">Na seção **Configuração do Image Relay**, clique em **Configurar Image Relay** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="54222-168">On the **Image Relay Configuration** section, click **Configure Image Relay** to open **Configure sign-on** window.</span></span> <span data-ttu-id="54222-169">Copie a **URL do Serviço de Logoff e a URL de Logon Único do SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="54222-169">Copy the **Sign-Out Service URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="54222-171">Em outra janela do navegador, entre em seu site de empresa do Image Relay como administrador.</span><span class="sxs-lookup"><span data-stu-id="54222-171">In another browser window, sign in to your Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="54222-172">Na barra de ferramentas na parte superior, clique na carga de trabalho **Usuários e Permissões**.</span><span class="sxs-lookup"><span data-stu-id="54222-172">In the toolbar on the top, click the **Users & Permissions** workload.</span></span>
   
    ![Configurar o logon único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="54222-174">Clique em **Criar Nova Permissão**.</span><span class="sxs-lookup"><span data-stu-id="54222-174">Click **Create New Permission**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="54222-176">Na carga de trabalho **Configurações de Logon Único**, marque a caixa de seleção **Este Grupo pode apenas entrar via logon único** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="54222-176">In the **Single Sign On Settings** workload, select the **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Configurar o logon único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="54222-178">Vá para **Configurações da Conta**.</span><span class="sxs-lookup"><span data-stu-id="54222-178">Go to **Account Settings**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="54222-180">Vá para a carga de trabalho **Configurações de Logon Único** .</span><span class="sxs-lookup"><span data-stu-id="54222-180">Go to the **Single Sign On Settings** workload.</span></span>
    
     ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="54222-182">Na caixa de diálogo **Configurações de SAML** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="54222-182">On the **SAML Settings** dialog, perform the following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="54222-184">a.</span><span class="sxs-lookup"><span data-stu-id="54222-184">a.</span></span> <span data-ttu-id="54222-185">Na caixa de texto **URL de Logon**, cole o valor da **URL de Serviço de Logon Único** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="54222-185">In **Login URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="54222-186">b.</span><span class="sxs-lookup"><span data-stu-id="54222-186">b.</span></span> <span data-ttu-id="54222-187">Na caixa de texto **URL de Logoff**, cole o valor da **URL de Serviço de Logoff Único** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="54222-187">In **Logout URL**  textbox, paste the value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="54222-188">c.</span><span class="sxs-lookup"><span data-stu-id="54222-188">c.</span></span> <span data-ttu-id="54222-189">Em **Formato da Id de Nome**, selecione **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="54222-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="54222-190">d.</span><span class="sxs-lookup"><span data-stu-id="54222-190">d.</span></span> <span data-ttu-id="54222-191">Em **Opções de Vinculação para Solicitações do Provedor de Serviço (Image Relay)**, selecione **Associação POST**.</span><span class="sxs-lookup"><span data-stu-id="54222-191">As **Binding Options for Requests from the Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="54222-192">e.</span><span class="sxs-lookup"><span data-stu-id="54222-192">e.</span></span> <span data-ttu-id="54222-193">Em **Certificado x.509**, clique em **Atualizar Certificado**.</span><span class="sxs-lookup"><span data-stu-id="54222-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="54222-195">f.</span><span class="sxs-lookup"><span data-stu-id="54222-195">f.</span></span> <span data-ttu-id="54222-196">Abra o certificado baixado no Bloco de Notas, copie o conteúdo e cole-o na caixa de texto Certificado x.509.</span><span class="sxs-lookup"><span data-stu-id="54222-196">Open the downloaded certificate in notepad, copy the content, and then paste it into the x.509 Certificate textbox.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="54222-198">g.</span><span class="sxs-lookup"><span data-stu-id="54222-198">g.</span></span> <span data-ttu-id="54222-199">Na seção **Provisionamento do Usuário Just-In-Time**, marque **Habilitar o Provisionamento do Usuário Just-In-Time**.</span><span class="sxs-lookup"><span data-stu-id="54222-199">In **Just-In-Time User Provisioning** section, select the **Enable Just-In-Time User Provisioning**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="54222-201">h.</span><span class="sxs-lookup"><span data-stu-id="54222-201">h.</span></span> <span data-ttu-id="54222-202">Selecione o grupo de permissão (por exemplo, **SSO Básico**) que tem permissão para entrar somente por meio de logon único.</span><span class="sxs-lookup"><span data-stu-id="54222-202">Select the permission group (for example, **SSO Basic**) which is allowed to sign in only through single sign-on.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="54222-204">i.</span><span class="sxs-lookup"><span data-stu-id="54222-204">i.</span></span> <span data-ttu-id="54222-205">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="54222-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="54222-206">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="54222-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="54222-207">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="54222-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="54222-208">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="54222-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="54222-209">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="54222-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="54222-210">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="54222-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="54222-212">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="54222-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54222-213">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54222-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="54222-215">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="54222-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="54222-217">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="54222-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="54222-219">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="54222-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="54222-221">a.</span><span class="sxs-lookup"><span data-stu-id="54222-221">a.</span></span> <span data-ttu-id="54222-222">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="54222-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54222-223">b.</span><span class="sxs-lookup"><span data-stu-id="54222-223">b.</span></span> <span data-ttu-id="54222-224">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="54222-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="54222-225">c.</span><span class="sxs-lookup"><span data-stu-id="54222-225">c.</span></span> <span data-ttu-id="54222-226">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="54222-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="54222-227">d.</span><span class="sxs-lookup"><span data-stu-id="54222-227">d.</span></span> <span data-ttu-id="54222-228">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="54222-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="54222-229">Criar um usuário de teste do Image Relay</span><span class="sxs-lookup"><span data-stu-id="54222-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="54222-230">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Image Relay.</span><span class="sxs-lookup"><span data-stu-id="54222-230">The objective of this section is to create a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="54222-231">**Para criar um usuário chamado Brenda Fernandes no Image Relay, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="54222-231">**To create a user called Britta Simon in Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="54222-232">Faça logon em seu site de empresa do Image Relay como administrador.</span><span class="sxs-lookup"><span data-stu-id="54222-232">Sign-on to your Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="54222-233">Acesse **Usuários e Permissões** e selecione **Criar Usuário SSO**.</span><span class="sxs-lookup"><span data-stu-id="54222-233">Go to **Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="54222-235">Insira o **Email**, o **Nome**, o **Sobrenome** e a **Empresa** do usuário que você deseja provisionar e selecione o grupo de permissões (por exemplo, SSO Básico), que é o grupo que pode entrar somente por meio de logon único.</span><span class="sxs-lookup"><span data-stu-id="54222-235">Enter the **Email**, **First Name**, **Last Name**, and **Company** of the user you want to provision and select the permission group (for example, SSO Basic) which is the group that can sign in only through single sign-on.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="54222-237">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="54222-237">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="54222-238">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="54222-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="54222-239">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Image Relay.</span><span class="sxs-lookup"><span data-stu-id="54222-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Image Relay.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="54222-241">**Para atribuir Brenda Fernandes ao Image Relay, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="54222-241">**To assign Britta Simon to Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="54222-242">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="54222-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="54222-244">Na lista de aplicativos, selecione **Image Relay**.</span><span class="sxs-lookup"><span data-stu-id="54222-244">In the applications list, select **Image Relay**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="54222-246">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="54222-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="54222-248">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="54222-248">Click **Add** button.</span></span> <span data-ttu-id="54222-249">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="54222-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="54222-251">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="54222-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="54222-252">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="54222-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="54222-253">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="54222-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="54222-254">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="54222-254">Testing single sign-on</span></span>

<span data-ttu-id="54222-255">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="54222-255">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>    

<span data-ttu-id="54222-256">Ao clicar no bloco Image Relay no Painel de Acesso, você deverá ser automaticamente conectado ao seu aplicativo Image Relay.</span><span class="sxs-lookup"><span data-stu-id="54222-256">When you click the Image Relay tile in the Access Panel, you should get automatically signed-on to your Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="54222-257">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="54222-257">Additional resources</span></span>

* [<span data-ttu-id="54222-258">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="54222-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54222-259">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54222-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

