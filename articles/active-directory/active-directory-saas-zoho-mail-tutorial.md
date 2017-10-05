---
title: "Tutorial: Integração do Azure Active Directory com Zoho | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: f0688cb75584ada805b944d2ef5409d66ab37339
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="f4924-103">Tutorial: Integração do Azure Active Directory com Zoho</span><span class="sxs-lookup"><span data-stu-id="f4924-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="f4924-104">Neste tutorial, você aprenderá a integrar o Zoho ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f4924-104">In this tutorial, you learn how to integrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4924-105">A integração do Zoho com o Azure AD fornece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="f4924-105">Integrating Zoho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f4924-106">Você pode controlar no Azure AD quem terá acesso ao Zoho.</span><span class="sxs-lookup"><span data-stu-id="f4924-106">You can control in Azure AD who has access to Zoho.</span></span>
- <span data-ttu-id="f4924-107">Você pode habilitar seus usuários para conexão automática no Zoho (Logon Único) com suas contas Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4924-107">You can enable your users to automatically get signed-on to Zoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f4924-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4924-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f4924-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4924-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4924-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f4924-110">Prerequisites</span></span>

<span data-ttu-id="f4924-111">Para configurar a integração do Azure AD com o Zoho, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f4924-111">To configure Azure AD integration with Zoho, you need the following items:</span></span>

- <span data-ttu-id="f4924-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f4924-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4924-113">Uma assinatura habilitada para logon único do Zoho</span><span class="sxs-lookup"><span data-stu-id="f4924-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f4924-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f4924-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f4924-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f4924-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4924-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f4924-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f4924-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4924-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f4924-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f4924-118">Scenario description</span></span>
<span data-ttu-id="f4924-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f4924-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4924-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="f4924-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4924-121">Adicionar Zoho da galeria</span><span class="sxs-lookup"><span data-stu-id="f4924-121">Adding Zoho from the gallery</span></span>
2. <span data-ttu-id="f4924-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f4924-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-the-gallery"></a><span data-ttu-id="f4924-123">Adicionar Zoho da galeria</span><span class="sxs-lookup"><span data-stu-id="f4924-123">Adding Zoho from the gallery</span></span>
<span data-ttu-id="f4924-124">Para configurar a integração do Zoho com o Azure AD, você precisará adicionar o Zoho à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="f4924-124">To configure the integration of Zoho into Azure AD, you need to add Zoho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f4924-125">**Para adicionar o Zoho da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f4924-125">**To add Zoho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f4924-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f4924-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="f4924-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f4924-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f4924-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f4924-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="f4924-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f4924-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="f4924-133">Na caixa de pesquisa, digite **Zoho**, selecione **Zoho** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f4924-133">In the search box, type **Zoho**, select **Zoho** from result panel then click **Add** button to add the application.</span></span>

    ![Zoho na lista de resultados](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f4924-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4924-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f4924-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Zoho, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f4924-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f4924-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Zoho é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4924-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho is to a user in Azure AD.</span></span> <span data-ttu-id="f4924-138">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado no Zoho.</span><span class="sxs-lookup"><span data-stu-id="f4924-138">In other words, a link relationship between an Azure AD user and the related user in Zoho needs to be established.</span></span>

<span data-ttu-id="f4924-139">NoZoho, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vinculação.</span><span class="sxs-lookup"><span data-stu-id="f4924-139">In Zoho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f4924-140">Para configurar e testar o logon único do Azure AD com o Zoho, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f4924-140">To configure and test Azure AD single sign-on with Zoho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f4924-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f4924-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f4924-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f4924-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f4924-143">**[Criar um usuário de teste do Zoho](#create-a-zoho-test-user)** – para ter um equivalente de Brenda Fernandes no Zoho que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4924-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - to have a counterpart of Britta Simon in Zoho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f4924-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4924-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f4924-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="f4924-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f4924-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4924-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f4924-147">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no seu aplicativo Zoho.</span><span class="sxs-lookup"><span data-stu-id="f4924-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="f4924-148">**Para configurar o logon único do Azure AD com o Zoho, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f4924-148">**To configure Azure AD single sign-on with Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="f4924-149">No portal do Azure, na página de integração do aplicativo **Zoho**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="f4924-149">In the Azure portal, on the **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="f4924-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="f4924-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="f4924-153">Na seção **URLs e Domínio do Zoho**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f4924-153">On the **Zoho Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="f4924-155">a.</span><span class="sxs-lookup"><span data-stu-id="f4924-155">a.</span></span> <span data-ttu-id="f4924-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="f4924-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f4924-157">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="f4924-157">This value is not real.</span></span> <span data-ttu-id="f4924-158">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="f4924-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f4924-159">Entre em contato com a [equipe de suporte ao cliente do Zoho](https://www.zoho.com/mail/contact.html) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="f4924-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get this value.</span></span> 
 
4. <span data-ttu-id="f4924-160">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="f4924-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="f4924-162">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f4924-162">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f4924-164">Na seção **Configuração do Zoho** clique em **Configurar Zoho** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="f4924-164">On the **Zoho Configuration** section, click **Configure Zoho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f4924-165">Copie a **URL de Saída, a URL de Alteração de Senha e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="f4924-165">Copy the **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="f4924-167">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa Zoho Mail como administrador.</span><span class="sxs-lookup"><span data-stu-id="f4924-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="f4924-168">Vá para o **Painel de Controle**.</span><span class="sxs-lookup"><span data-stu-id="f4924-168">Go to the **Control panel**.</span></span>
   
    <span data-ttu-id="f4924-169">![Painel de controle](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Painel de controle")</span><span class="sxs-lookup"><span data-stu-id="f4924-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="f4924-170">Clique na guia **Autenticação SAML** .</span><span class="sxs-lookup"><span data-stu-id="f4924-170">Click the **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="f4924-171">![Autenticação SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="f4924-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="f4924-172">Na seção **Detalhes da Autenticação SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f4924-172">In the **SAML Authentication Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f4924-173">![Detalhes de Autenticação SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Detalhes de Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="f4924-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="f4924-174">a.</span><span class="sxs-lookup"><span data-stu-id="f4924-174">a.</span></span> <span data-ttu-id="f4924-175">Na caixa de texto **URL de Logon**, cole a **URL do Serviço de Logon Único SAML** copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4924-175">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f4924-176">b.</span><span class="sxs-lookup"><span data-stu-id="f4924-176">b.</span></span> <span data-ttu-id="f4924-177">Na caixa de texto **URL de Logoff**, cole a **URL de Saída** copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4924-177">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f4924-178">c.</span><span class="sxs-lookup"><span data-stu-id="f4924-178">c.</span></span> <span data-ttu-id="f4924-179">Na caixa de texto **Alterar URL de Senha**, cole **Alterar URL da Senha** copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4924-179">In the **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="f4924-180">d.</span><span class="sxs-lookup"><span data-stu-id="f4924-180">d.</span></span> <span data-ttu-id="f4924-181">Abra o certificado codificado em BASE-64 baixado no portal do Azure no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **PublicKey**.</span><span class="sxs-lookup"><span data-stu-id="f4924-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="f4924-182">e.</span><span class="sxs-lookup"><span data-stu-id="f4924-182">e.</span></span> <span data-ttu-id="f4924-183">Para **Algoritmo**, selecione **RSA**.</span><span class="sxs-lookup"><span data-stu-id="f4924-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="f4924-184">f.</span><span class="sxs-lookup"><span data-stu-id="f4924-184">f.</span></span> <span data-ttu-id="f4924-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4924-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="f4924-186">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="f4924-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f4924-187">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f4924-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f4924-188">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f4924-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f4924-189">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4924-189">Create an Azure AD test user</span></span>

<span data-ttu-id="f4924-190">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f4924-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="f4924-192">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f4924-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f4924-193">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f4924-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f4924-195">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="f4924-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f4924-197">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="f4924-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f4924-199">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f4924-199">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f4924-201">a.</span><span class="sxs-lookup"><span data-stu-id="f4924-201">a.</span></span> <span data-ttu-id="f4924-202">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="f4924-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f4924-203">b.</span><span class="sxs-lookup"><span data-stu-id="f4924-203">b.</span></span> <span data-ttu-id="f4924-204">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f4924-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f4924-205">c.</span><span class="sxs-lookup"><span data-stu-id="f4924-205">c.</span></span> <span data-ttu-id="f4924-206">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="f4924-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f4924-207">d.</span><span class="sxs-lookup"><span data-stu-id="f4924-207">d.</span></span> <span data-ttu-id="f4924-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f4924-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="f4924-209">Criar um usuário de teste do Zoho</span><span class="sxs-lookup"><span data-stu-id="f4924-209">Create a Zoho test user</span></span>

<span data-ttu-id="f4924-210">Para permitir que os usuários do AD do Azure façam logon no Zoho Mail, eles devem ser provisionados no Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="f4924-210">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="f4924-211">No caso do Zoho Mail, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="f4924-211">In the case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="f4924-212">É possível usar qualquer outra ferramenta de criação da conta de usuário do Zoho Mail ou APIs fornecidas pelo Zoho Mail para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="f4924-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="f4924-213">Para provisionar uma conta de usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f4924-213">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="f4924-214">Faça logon em seu site de empresa do **Zoho Mail** como administrador.</span><span class="sxs-lookup"><span data-stu-id="f4924-214">Log in to your **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="f4924-215">Vá para **Painel de Controle \> Emails e Documentos**.</span><span class="sxs-lookup"><span data-stu-id="f4924-215">Go to **Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="f4924-216">Vá para **Detalhes do Usuário \> Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="f4924-216">Go to **User Details \> Add User**.</span></span>
   
    <span data-ttu-id="f4924-217">![Adicionar Usuário](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="f4924-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="f4924-218">No diálogo **Adicionar usuários** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f4924-218">On the **Add users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="f4924-219">![Adicionar Usuário](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="f4924-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="f4924-220">a.</span><span class="sxs-lookup"><span data-stu-id="f4924-220">a.</span></span> <span data-ttu-id="f4924-221">Na caixa de texto **Nome**, digite o Nome do usuário, como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="f4924-221">In the **First Name** textbox, type the first name of user like **Britta**.</span></span>

    <span data-ttu-id="f4924-222">b.</span><span class="sxs-lookup"><span data-stu-id="f4924-222">b.</span></span> <span data-ttu-id="f4924-223">Na caixa de texto **Sobrenome**, digite o Sobrenome do usuário, como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f4924-223">In the **Last Name** textbox, type the last name of user like **Simon**.</span></span>

    <span data-ttu-id="f4924-224">c.</span><span class="sxs-lookup"><span data-stu-id="f4924-224">c.</span></span> <span data-ttu-id="f4924-225">Na caixa de texto **ID de Email** digite a identificação do email do usuário, como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="f4924-225">In the **Email ID** textbox, type the email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="f4924-226">d.</span><span class="sxs-lookup"><span data-stu-id="f4924-226">d.</span></span> <span data-ttu-id="f4924-227">Na caixa de texto **Senha** digite a senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="f4924-227">In the **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="f4924-228">e.</span><span class="sxs-lookup"><span data-stu-id="f4924-228">e.</span></span> <span data-ttu-id="f4924-229">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4924-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="f4924-230">O titular da conta do Active Directory do Azure receberá um email com um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="f4924-230">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f4924-231">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4924-231">Assign the Azure AD test user</span></span>

<span data-ttu-id="f4924-232">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Zoho.</span><span class="sxs-lookup"><span data-stu-id="f4924-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="f4924-234">**Para atribuir Brenda Fernandes ao Zoho, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f4924-234">**To assign Britta Simon to Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="f4924-235">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f4924-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f4924-237">Na lista de aplicativos, escolha **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="f4924-237">In the applications list, select **Zoho**.</span></span>

    ![O link do Zoho na lista de Aplicativos](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="f4924-239">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f4924-239">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="f4924-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f4924-241">Click **Add** button.</span></span> <span data-ttu-id="f4924-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f4924-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="f4924-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f4924-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f4924-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f4924-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f4924-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f4924-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f4924-247">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="f4924-247">Test single sign-on</span></span>

<span data-ttu-id="f4924-248">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="f4924-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f4924-249">Quando você clicar no bloco Zoho no Painel de Acesso, deverá conectar automaticamente no seu aplicativo Zoho.</span><span class="sxs-lookup"><span data-stu-id="f4924-249">When you click the Zoho tile in the Access Panel, you should get automatically signed-on to your Zoho application.</span></span>
<span data-ttu-id="f4924-250">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f4924-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f4924-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f4924-251">Additional resources</span></span>

* [<span data-ttu-id="f4924-252">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f4924-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f4924-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f4924-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

