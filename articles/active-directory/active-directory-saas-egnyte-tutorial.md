---
title: "Tutorial: Integração do Azure Active Directory ao Egnyte | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 62d01333b61e73c83588d2d1701c0c300df4ab1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="2e10f-103">Tutorial: integração do Active Directory do Azure ao Egnyte</span><span class="sxs-lookup"><span data-stu-id="2e10f-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="2e10f-104">Neste tutorial, você aprenderá a integrar o Egnyte ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2e10f-104">In this tutorial, you learn how to integrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e10f-105">A integração do Egnyte ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="2e10f-105">Integrating Egnyte with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2e10f-106">Você pode controlar no Azure AD quem terá acesso ao Egnyte</span><span class="sxs-lookup"><span data-stu-id="2e10f-106">You can control in Azure AD who has access to Egnyte</span></span>
- <span data-ttu-id="2e10f-107">Você pode permitir que os usuários façam logon automaticamente no Egnyte (Logon Único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e10f-107">You can enable your users to automatically get signed-on to Egnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2e10f-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2e10f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2e10f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e10f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e10f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2e10f-110">Prerequisites</span></span>

<span data-ttu-id="2e10f-111">Para configurar a integração do Azure AD ao Egnyte, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2e10f-111">To configure Azure AD integration with Egnyte, you need the following items:</span></span>

- <span data-ttu-id="2e10f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2e10f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e10f-113">Uma assinatura habilitada para logon único do Egnyte</span><span class="sxs-lookup"><span data-stu-id="2e10f-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e10f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2e10f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e10f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2e10f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e10f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2e10f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e10f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e10f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e10f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2e10f-118">Scenario description</span></span>
<span data-ttu-id="2e10f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2e10f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e10f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="2e10f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e10f-121">Adicionando Egnyte da galeria</span><span class="sxs-lookup"><span data-stu-id="2e10f-121">Adding Egnyte from the gallery</span></span>
2. <span data-ttu-id="2e10f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2e10f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-the-gallery"></a><span data-ttu-id="2e10f-123">Adicionando Egnyte da galeria</span><span class="sxs-lookup"><span data-stu-id="2e10f-123">Adding Egnyte from the gallery</span></span>
<span data-ttu-id="2e10f-124">Para configurar a integração do Egnyte ao Azure AD, você precisará adicionar o Egnyte da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2e10f-124">To configure the integration of Egnyte into Azure AD, you need to add Egnyte from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2e10f-125">**Para adicionar o Egnyte da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2e10f-125">**To add Egnyte from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2e10f-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2e10f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2e10f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="2e10f-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2e10f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="2e10f-133">Na caixa de pesquisa, digite **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-133">In the search box, type **Egnyte**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="2e10f-135">No painel de resultados, selecione **Egnyte** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2e10f-135">In the results panel, select **Egnyte**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2e10f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2e10f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2e10f-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Egnyte com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="2e10f-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2e10f-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Egnyte é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e10f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Egnyte is to a user in Azure AD.</span></span> <span data-ttu-id="2e10f-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Egnyte.</span><span class="sxs-lookup"><span data-stu-id="2e10f-140">In other words, a link relationship between an Azure AD user and the related user in Egnyte needs to be established.</span></span>

<span data-ttu-id="2e10f-141">No Egnyte, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="2e10f-141">In Egnyte, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2e10f-142">Para configurar e testar o logon único do Azure AD com o Egnyte, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="2e10f-142">To configure and test Azure AD single sign-on with Egnyte, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2e10f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2e10f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2e10f-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2e10f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e10f-145">**[Criando um usuário de teste do Egnyte](#creating-an-egnyte-test-user)** – para ter um equivalente de Brenda Fernandes no Egnyte que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e10f-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - to have a counterpart of Britta Simon in Egnyte that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2e10f-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e10f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e10f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="2e10f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2e10f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e10f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2e10f-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Egnyte.</span><span class="sxs-lookup"><span data-stu-id="2e10f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="2e10f-150">**Para configurar o logon único do Azure AD com o Egnyte, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2e10f-150">**To configure Azure AD single sign-on with Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="2e10f-151">No portal do Azure, na página de integração de aplicativos do **Egnyte**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-151">In the Azure portal, on the **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2e10f-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="2e10f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="2e10f-155">Na seção **URLs e Domínio do Egnyte**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2e10f-155">On the **Egnyte Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="2e10f-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="2e10f-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2e10f-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="2e10f-158">This value is not real.</span></span> <span data-ttu-id="2e10f-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="2e10f-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="2e10f-160">Entre em contato com a [equipe de suporte do Cliente do Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="2e10f-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) to get this value.</span></span> 
 
4. <span data-ttu-id="2e10f-161">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="2e10f-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="2e10f-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2e10f-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2e10f-165">Na seção **Configuração do Egnyte**, clique em **Configurar Egnyte** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-165">On the **Egnyte Configuration** section, click **Configure Egnyte** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2e10f-166">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="2e10f-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="2e10f-168">Em uma janela diferente do navegador da Web, faça logon no site da empresa do Egnyte como administrador.</span><span class="sxs-lookup"><span data-stu-id="2e10f-168">In a different web browser window, log in to your Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="2e10f-169">Clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="2e10f-170">![Configurações](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="2e10f-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="2e10f-171">No menu, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-171">In the menu, click **Settings**.</span></span>

   <span data-ttu-id="2e10f-172">![Configurações](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="2e10f-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="2e10f-173">Clique na guia **Configuração** e, em seguida, clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-173">Click the **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="2e10f-174">![Segurança](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="2e10f-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="2e10f-175">Na seção **Autenticação de Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2e10f-175">In the **Single Sign-On Authentication** section, perform the following steps:</span></span>

    <span data-ttu-id="2e10f-176">![Autenticação de Logon Único](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Autenticação de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="2e10f-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="2e10f-177">a.</span><span class="sxs-lookup"><span data-stu-id="2e10f-177">a.</span></span> <span data-ttu-id="2e10f-178">Para **Autenticação de logon único**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="2e10f-179">b.</span><span class="sxs-lookup"><span data-stu-id="2e10f-179">b.</span></span> <span data-ttu-id="2e10f-180">Para **Provedor de identidade**, selecione **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="2e10f-181">c.</span><span class="sxs-lookup"><span data-stu-id="2e10f-181">c.</span></span> <span data-ttu-id="2e10f-182">Cole a **URL de Logon Único do serviço SAML** copiada do portal do Azure para o **URL de logon do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2e10f-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into the **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="2e10f-183">d.</span><span class="sxs-lookup"><span data-stu-id="2e10f-183">d.</span></span> <span data-ttu-id="2e10f-184">Cole a **ID da Entidade SAML** copiada do portal do Azure na caixa de texto **ID da entidade do provedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-184">Paste **SAML Entity ID** which you have copied from Azure portal into the **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="2e10f-185">e.</span><span class="sxs-lookup"><span data-stu-id="2e10f-185">e.</span></span> <span data-ttu-id="2e10f-186">Abra seu certificado codificado em base-64 no bloco de notas baixado do portal do Azure, copie o conteúdo dele para a área de transferência e cole-o na caixa de texto **Certificado do provedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="2e10f-187">f.</span><span class="sxs-lookup"><span data-stu-id="2e10f-187">f.</span></span> <span data-ttu-id="2e10f-188">Para **Mapeamento de usuário padrão**, selecione **Endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="2e10f-189">g.</span><span class="sxs-lookup"><span data-stu-id="2e10f-189">g.</span></span> <span data-ttu-id="2e10f-190">Para **Usar valor do emissor específico do domínio**, selecione **desabilitado**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="2e10f-191">h.</span><span class="sxs-lookup"><span data-stu-id="2e10f-191">h.</span></span> <span data-ttu-id="2e10f-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2e10f-193">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="2e10f-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2e10f-194">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2e10f-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2e10f-195">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2e10f-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2e10f-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2e10f-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="2e10f-197">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2e10f-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="2e10f-199">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2e10f-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2e10f-200">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2e10f-202">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2e10f-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2e10f-204">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e10f-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e10f-206">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2e10f-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2e10f-208">a.</span><span class="sxs-lookup"><span data-stu-id="2e10f-208">a.</span></span> <span data-ttu-id="2e10f-209">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e10f-210">b.</span><span class="sxs-lookup"><span data-stu-id="2e10f-210">b.</span></span> <span data-ttu-id="2e10f-211">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2e10f-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2e10f-212">c.</span><span class="sxs-lookup"><span data-stu-id="2e10f-212">c.</span></span> <span data-ttu-id="2e10f-213">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2e10f-214">d.</span><span class="sxs-lookup"><span data-stu-id="2e10f-214">d.</span></span> <span data-ttu-id="2e10f-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="2e10f-216">Como criar um usuário de teste do Egnyte</span><span class="sxs-lookup"><span data-stu-id="2e10f-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="2e10f-217">Para permitir que os usuários do Azure AD façam logon no Egnyte, eles deverão ser provisionados no Egnyte.</span><span class="sxs-lookup"><span data-stu-id="2e10f-217">To enable Azure AD users to log in to Egnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="2e10f-218">No caso do Egnyte, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="2e10f-218">In the case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="2e10f-219">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2e10f-219">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="2e10f-220">Faça logon no site de empresa do **Egnyte** como administrador.</span><span class="sxs-lookup"><span data-stu-id="2e10f-220">Log in to your **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="2e10f-221">Vá para **Configurações \> Usuários e Grupos**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-221">Go to **Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="2e10f-222">Clique em **Adicionar Novo Usuário**e selecione o tipo de usuário que deseja adicionar.</span><span class="sxs-lookup"><span data-stu-id="2e10f-222">Click **Add New User**, and then select the type of user you want to add.</span></span>
   
   <span data-ttu-id="2e10f-223">![Usuários](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="2e10f-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="2e10f-224">Na seção **Novo Usuário Padrão** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2e10f-224">In the **New Standard User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="2e10f-225">![Novo Usuário Padrão](./media/active-directory-saas-egnyte-tutorial/ic787825.png "Novo Usuário Padrão")</span><span class="sxs-lookup"><span data-stu-id="2e10f-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="2e10f-226">a.</span><span class="sxs-lookup"><span data-stu-id="2e10f-226">a.</span></span> <span data-ttu-id="2e10f-227">Digite o **Email**, o **Nome de usuário** e outros detalhes de uma conta válida do Azure Active Directory que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="2e10f-227">Type the **Email**, **Username**, and other details of a valid Azure Active Directory account you want to provision.</span></span>
   
   <span data-ttu-id="2e10f-228">b.</span><span class="sxs-lookup"><span data-stu-id="2e10f-228">b.</span></span> <span data-ttu-id="2e10f-229">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="2e10f-230">O titular da conta do Active Directory do Azure receberá um email de notificação.</span><span class="sxs-lookup"><span data-stu-id="2e10f-230">The Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="2e10f-231">É possível usar qualquer outra ferramenta de criação da conta de usuário do Egnyte ou as APIs fornecidas pelo Egnyte para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="2e10f-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2e10f-232">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2e10f-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2e10f-233">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Egnyte.</span><span class="sxs-lookup"><span data-stu-id="2e10f-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Egnyte.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="2e10f-235">**Para atribuir Brenda Fernandes ao Egnyte, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2e10f-235">**To assign Britta Simon to Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="2e10f-236">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2e10f-238">Na lista de aplicativos, selecione **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-238">In the applications list, select **Egnyte**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="2e10f-240">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="2e10f-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2e10f-242">Click **Add** button.</span></span> <span data-ttu-id="2e10f-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e10f-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="2e10f-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2e10f-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2e10f-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e10f-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e10f-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e10f-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2e10f-248">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="2e10f-248">Testing single sign-on</span></span>

<span data-ttu-id="2e10f-249">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="2e10f-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2e10f-250">Ao clicar no bloco do Egnyte no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo do Egnyte.</span><span class="sxs-lookup"><span data-stu-id="2e10f-250">When you click the Egnyte tile in the Access Panel, you should get automatically signed-on to your Egnyte application.</span></span>
<span data-ttu-id="2e10f-251">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e10f-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2e10f-252">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2e10f-252">Additional resources</span></span>

* [<span data-ttu-id="2e10f-253">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2e10f-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e10f-254">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2e10f-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

