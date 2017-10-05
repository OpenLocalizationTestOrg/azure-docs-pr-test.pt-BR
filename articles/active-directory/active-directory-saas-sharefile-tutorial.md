---
title: "Tutorial: integração do Azure Active Directory com o Citrix ShareFile | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: b85680104fe4f33638c559b2a12483a2312a4476
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="79453-103">Tutorial: integração do Azure Active Directory ao Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="79453-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="79453-104">Nesse tutorial, você aprenderá a integrar o Citrix ShareFile ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="79453-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79453-105">A integração do Citrix ShareFile ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="79453-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="79453-106">No Azure AD, é possível controlar quem tem acesso ao Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="79453-106">You can control in Azure AD who has access to Citrix ShareFile.</span></span>
- <span data-ttu-id="79453-107">Você pode permitir que seus usuários façam logon automaticamente no Citrix ShareFile usando logon único com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79453-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="79453-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="79453-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="79453-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79453-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79453-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="79453-110">Prerequisites</span></span>

<span data-ttu-id="79453-111">Para configurar a integração do Azure AD ao Citrix ShareFile, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="79453-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span></span>

- <span data-ttu-id="79453-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="79453-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79453-113">Uma assinatura habilitada para logon único do Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="79453-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79453-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="79453-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79453-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="79453-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79453-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="79453-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79453-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79453-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79453-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="79453-118">Scenario description</span></span>
<span data-ttu-id="79453-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="79453-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79453-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="79453-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79453-121">Adicionar o Citrix ShareFile por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="79453-121">Add Citrix ShareFile from the gallery</span></span>
2. <span data-ttu-id="79453-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="79453-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-the-gallery"></a><span data-ttu-id="79453-123">Adicionar o Citrix ShareFile por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="79453-123">Add Citrix ShareFile from the gallery</span></span>
<span data-ttu-id="79453-124">Para configurar a integração do Citrix ShareFile com o Azure AD, você precisa adicionar o Citrix ShareFile, por meio da galeria, à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="79453-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79453-125">**Para adicionar o Citrix ShareFile da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="79453-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79453-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79453-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="79453-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="79453-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="79453-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="79453-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="79453-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79453-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="79453-133">Na caixa de pesquisa, digite **Citrix ShareFile**, selecione **Citrix ShareFile** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79453-133">In the search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button to add the application.</span></span>

    ![Citrix ShareFile na lista de resultados](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="79453-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="79453-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="79453-136">Nesta seção, você vai configurar e testar o logon único do Azure AD com o Citrix ShareFile, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="79453-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79453-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Citrix ShareFile é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79453-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span></span> <span data-ttu-id="79453-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="79453-138">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span></span>

<span data-ttu-id="79453-139">No Citrix ShareFile, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="79453-139">In Citrix ShareFile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="79453-140">Para configurar e testar o logon único do Azure AD com o Citrix ShareFile, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="79453-140">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79453-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="79453-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="79453-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="79453-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79453-143">**[Criar um usuário de teste do Citrix ShareFile](#create-a-citrix-sharefile-test-user)** – para ter um equivalente de Brenda Fernandes no Citrix ShareFile que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79453-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="79453-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79453-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79453-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="79453-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="79453-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="79453-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="79453-147">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="79453-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="79453-148">**Para configurar o logon único do Azure AD com o Citrix ShareFile, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="79453-148">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="79453-149">No Portal do Azure, na página de integração do aplicativo **Citrix ShareFile**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="79453-149">In the Azure portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="79453-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="79453-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="79453-153">Na seção **URLs e Domínio do Citrix ShareFile**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="79453-153">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="79453-155">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="79453-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79453-156">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="79453-156">This value is not real.</span></span> <span data-ttu-id="79453-157">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="79453-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="79453-158">Entre em contato com a [equipe de suporte ao cliente do Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="79453-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) to get this value.</span></span> 

4. <span data-ttu-id="79453-159">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="79453-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="79453-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="79453-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79453-163">Na seção **Configuração do Citrix ShareFile**, clique em **Configurar Citrix ShareFile** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="79453-163">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="79453-164">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="79453-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="79453-166">Em outra janela do navegador da Web, faça logon em seu site de empresa do **Citrix ShareFile** como administrador.</span><span class="sxs-lookup"><span data-stu-id="79453-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="79453-167">Na barra de ferramentas na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="79453-167">In the toolbar on the top, click **Admin**.</span></span>

9. <span data-ttu-id="79453-168">No painel de navegação à esquerda, selecione **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="79453-168">In the left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="79453-169">![Administração de Conta](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Administração de Conta")</span><span class="sxs-lookup"><span data-stu-id="79453-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="79453-170">Na página **Configuração de Logon Único/SAML 2.0** em **Configurações Básicas**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="79453-170">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>
   
    <span data-ttu-id="79453-171">![Logon Único](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="79453-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="79453-172">a.</span><span class="sxs-lookup"><span data-stu-id="79453-172">a.</span></span> <span data-ttu-id="79453-173">Clique em **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="79453-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="79453-174">b.</span><span class="sxs-lookup"><span data-stu-id="79453-174">b.</span></span> <span data-ttu-id="79453-175">Na caixa de texto **ID da Entidade/Emissor do IDP**, cole o valor da **ID da Entidade SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="79453-175">In **Your IDP Issuer/ Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="79453-176">c.</span><span class="sxs-lookup"><span data-stu-id="79453-176">c.</span></span> <span data-ttu-id="79453-177">Clique em **Alterar** ao lado do campo **Certificado X.509** e carregue o certificado baixado no portal Azure.</span><span class="sxs-lookup"><span data-stu-id="79453-177">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure portal.</span></span>
    
    <span data-ttu-id="79453-178">d.</span><span class="sxs-lookup"><span data-stu-id="79453-178">d.</span></span> <span data-ttu-id="79453-179">Na caixa de texto **URL de Logon**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="79453-179">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="79453-180">e.</span><span class="sxs-lookup"><span data-stu-id="79453-180">e.</span></span> <span data-ttu-id="79453-181">Na caixa de texto **URL de Logoff**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="79453-181">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="79453-182">Clique em **Salvar** no portal de gerenciamento do Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="79453-182">Click **Save** on the Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="79453-183">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="79453-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="79453-184">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="79453-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="79453-185">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79453-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="79453-186">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="79453-186">Create an Azure AD test user</span></span>

<span data-ttu-id="79453-187">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="79453-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="79453-189">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="79453-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79453-190">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79453-190">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="79453-192">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="79453-192">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="79453-194">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="79453-194">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="79453-196">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="79453-196">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="79453-198">a.</span><span class="sxs-lookup"><span data-stu-id="79453-198">a.</span></span> <span data-ttu-id="79453-199">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="79453-199">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79453-200">b.</span><span class="sxs-lookup"><span data-stu-id="79453-200">b.</span></span> <span data-ttu-id="79453-201">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="79453-201">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="79453-202">c.</span><span class="sxs-lookup"><span data-stu-id="79453-202">c.</span></span> <span data-ttu-id="79453-203">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="79453-203">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="79453-204">d.</span><span class="sxs-lookup"><span data-stu-id="79453-204">d.</span></span> <span data-ttu-id="79453-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="79453-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="79453-206">Criar um usuário de teste do Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="79453-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="79453-207">Para permitir que os usuários do Azure AD façam logon no Citrix ShareFile, eles devem ser provisionados no Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="79453-207">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="79453-208">No caso do Citrix ShareFile, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="79453-208">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="79453-209">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="79453-209">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="79453-210">Faça logon em seu locatário do **Citrix ShareFile** .</span><span class="sxs-lookup"><span data-stu-id="79453-210">Log in to your **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="79453-211">Clique em **Gerenciar Usuários \> Gerenciar Página Inicial dos Usuários \> + Criar Funcionário**.</span><span class="sxs-lookup"><span data-stu-id="79453-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="79453-212">![Criar Funcionário](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Criar Funcionário")</span><span class="sxs-lookup"><span data-stu-id="79453-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="79453-213">Na seção **Informações Básicas**, execute as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="79453-213">On the **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="79453-214">![Informações Básicas](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Informações Básicas")</span><span class="sxs-lookup"><span data-stu-id="79453-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="79453-215">a.</span><span class="sxs-lookup"><span data-stu-id="79453-215">a.</span></span> <span data-ttu-id="79453-216">Na caixa de texto **Endereço de Email**, digite o endereço de email de Brenda Fernandes como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="79453-216">In the **Email Address** textbox, type the email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="79453-217">b.</span><span class="sxs-lookup"><span data-stu-id="79453-217">b.</span></span> <span data-ttu-id="79453-218">Na caixa de texto **Nome**, digite o **nome** do usuário como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="79453-218">In the **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="79453-219">c.</span><span class="sxs-lookup"><span data-stu-id="79453-219">c.</span></span> <span data-ttu-id="79453-220">Na caixa de texto **Sobrenome**, digite o **sobrenome** do usuário como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="79453-220">In the **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="79453-221">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="79453-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="79453-222">O titular da conta do Azure AD receberá um email e seguirá um link para confirmar sua conta antes de se tornar ativo. Você pode usar quaisquer outras ferramentas de criação de conta de usuário do Citrix ShareFile ou APIs fornecidas pelo Citrix ShareFile para provisionar contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79453-222">The Azure AD account holder will receive an email and follow a link to confirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="79453-223">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="79453-223">Assign the Azure AD test user</span></span>

<span data-ttu-id="79453-224">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="79453-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix ShareFile.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="79453-226">**Para atribuir Brenda Fernandes ao Citrix ShareFile, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="79453-226">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="79453-227">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="79453-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="79453-229">Na lista de aplicativos, selecione **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="79453-229">In the applications list, select **Citrix ShareFile**.</span></span>

    ![O link do Citrix ShareFile na lista de Aplicativos](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="79453-231">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="79453-231">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="79453-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="79453-233">Click **Add** button.</span></span> <span data-ttu-id="79453-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="79453-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="79453-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="79453-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="79453-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="79453-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79453-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="79453-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="79453-239">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="79453-239">Test single sign-on</span></span>

<span data-ttu-id="79453-240">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="79453-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="79453-241">Quando você clica no bloco Citrix ShareFile. no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="79453-241">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span></span>
<span data-ttu-id="79453-242">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79453-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="79453-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="79453-243">Additional resources</span></span>

* [<span data-ttu-id="79453-244">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="79453-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79453-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="79453-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

