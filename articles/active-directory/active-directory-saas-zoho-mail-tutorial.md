---
title: "Tutorial: Integração do Azure Active Directory com Zoho | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Zoho."
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
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="dc023-103">Tutorial: Integração do Azure Active Directory com Zoho</span><span class="sxs-lookup"><span data-stu-id="dc023-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="dc023-104">Neste tutorial, você aprenderá como toointegrate Zoho com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="dc023-104">In this tutorial, you learn how toointegrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc023-105">Integrando Zoho com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc023-105">Integrating Zoho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dc023-106">Você pode controlar no AD do Azure que tenha acesso tooZoho.</span><span class="sxs-lookup"><span data-stu-id="dc023-106">You can control in Azure AD who has access tooZoho.</span></span>
- <span data-ttu-id="dc023-107">Você pode habilitar seu usuários tooautomatically get conectado tooZoho (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc023-107">You can enable your users tooautomatically get signed-on tooZoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="dc023-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc023-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="dc023-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dc023-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc023-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dc023-110">Prerequisites</span></span>

<span data-ttu-id="dc023-111">tooconfigure integração do AD do Azure com o Zoho, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc023-111">tooconfigure Azure AD integration with Zoho, you need hello following items:</span></span>

- <span data-ttu-id="dc023-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dc023-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc023-113">Uma assinatura habilitada para logon único do Zoho</span><span class="sxs-lookup"><span data-stu-id="dc023-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc023-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="dc023-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc023-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="dc023-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc023-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="dc023-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc023-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc023-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc023-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="dc023-118">Scenario description</span></span>
<span data-ttu-id="dc023-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="dc023-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc023-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="dc023-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc023-121">Adicionando Zoho da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="dc023-121">Adding Zoho from hello gallery</span></span>
2. <span data-ttu-id="dc023-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dc023-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-hello-gallery"></a><span data-ttu-id="dc023-123">Adicionando Zoho da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="dc023-123">Adding Zoho from hello gallery</span></span>
<span data-ttu-id="dc023-124">integração de saudação tooconfigure do Zoho no AD do Azure, você precisa tooadd Zoho da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="dc023-124">tooconfigure hello integration of Zoho into Azure AD, you need tooadd Zoho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dc023-125">**tooadd Zoho da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="dc023-125">**tooadd Zoho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc023-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="dc023-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="dc023-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="dc023-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dc023-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="dc023-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="dc023-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc023-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="dc023-133">Na caixa de pesquisa hello, digite **Zoho**, selecione **Zoho** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dc023-133">In hello search box, type **Zoho**, select **Zoho** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Zoho na lista de resultados de saudação](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dc023-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc023-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="dc023-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Zoho, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="dc023-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc023-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Zoho é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc023-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoho is tooa user in Azure AD.</span></span> <span data-ttu-id="dc023-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Zoho precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="dc023-138">In other words, a link relationship between an Azure AD user and hello related user in Zoho needs toobe established.</span></span>

<span data-ttu-id="dc023-139">No Zoho, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc023-139">In Zoho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dc023-140">tooconfigure e teste de logon único do AD do Azure com o Zoho, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc023-140">tooconfigure and test Azure AD single sign-on with Zoho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dc023-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="dc023-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dc023-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc023-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc023-143">**[Criar um usuário de teste do Zoho](#create-a-zoho-test-user)**  -toohave um equivalente do Britta Simon no Zoho é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="dc023-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - toohave a counterpart of Britta Simon in Zoho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc023-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="dc023-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc023-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="dc023-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dc023-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc023-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="dc023-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Zoho.</span><span class="sxs-lookup"><span data-stu-id="dc023-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="dc023-148">**tooconfigure AD do Azure-logon único com o Zoho, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="dc023-148">**tooconfigure Azure AD single sign-on with Zoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc023-149">Em Olá portal do Azure, Olá **Zoho** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="dc023-149">In hello Azure portal, on hello **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="dc023-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="dc023-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="dc023-153">Em Olá **Zoho domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc023-153">On hello **Zoho Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="dc023-155">a.</span><span class="sxs-lookup"><span data-stu-id="dc023-155">a.</span></span> <span data-ttu-id="dc023-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="dc023-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dc023-157">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="dc023-157">This value is not real.</span></span> <span data-ttu-id="dc023-158">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="dc023-158">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="dc023-159">Entre em contato com [equipe de suporte do cliente Zoho](https://www.zoho.com/mail/contact.html) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="dc023-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="dc023-160">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="dc023-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="dc023-162">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="dc023-162">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dc023-164">Em Olá **Zoho configuração** seção, clique em **configurar Zoho** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="dc023-164">On hello **Zoho Configuration** section, click **Configure Zoho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dc023-165">Saudação de cópia **Single Sign-On URL do serviço SAML, alterar a URL da senha e URL de logout** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="dc023-165">Copy hello **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="dc023-167">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa Zoho Mail como administrador.</span><span class="sxs-lookup"><span data-stu-id="dc023-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="dc023-168">Vá toohello **painel de controle**.</span><span class="sxs-lookup"><span data-stu-id="dc023-168">Go toohello **Control panel**.</span></span>
   
    <span data-ttu-id="dc023-169">![Painel de controle](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Painel de controle")</span><span class="sxs-lookup"><span data-stu-id="dc023-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="dc023-170">Clique em Olá **autenticação SAML** guia.</span><span class="sxs-lookup"><span data-stu-id="dc023-170">Click hello **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="dc023-171">![Autenticação SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="dc023-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="dc023-172">Em Olá **detalhes de autenticação SAML** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc023-172">In hello **SAML Authentication Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="dc023-173">![Detalhes de Autenticação SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Detalhes de Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="dc023-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="dc023-174">a.</span><span class="sxs-lookup"><span data-stu-id="dc023-174">a.</span></span> <span data-ttu-id="dc023-175">Em Olá **URL de logon** caixa de texto, colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc023-175">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="dc023-176">b.</span><span class="sxs-lookup"><span data-stu-id="dc023-176">b.</span></span> <span data-ttu-id="dc023-177">Em Olá **URL de Logout** caixa de texto, colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc023-177">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="dc023-178">c.</span><span class="sxs-lookup"><span data-stu-id="dc023-178">c.</span></span> <span data-ttu-id="dc023-179">Em Olá **alterar a URL da senha** caixa de texto, colar **alterar a URL da senha** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc023-179">In hello **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="dc023-180">d.</span><span class="sxs-lookup"><span data-stu-id="dc023-180">d.</span></span> <span data-ttu-id="dc023-181">Abra seu certificado codificado em base 64 baixado do portal do Azure no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **PublicKey** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="dc023-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="dc023-182">e.</span><span class="sxs-lookup"><span data-stu-id="dc023-182">e.</span></span> <span data-ttu-id="dc023-183">Para **Algoritmo**, selecione **RSA**.</span><span class="sxs-lookup"><span data-stu-id="dc023-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="dc023-184">f.</span><span class="sxs-lookup"><span data-stu-id="dc023-184">f.</span></span> <span data-ttu-id="dc023-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc023-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="dc023-186">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="dc023-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dc023-187">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="dc023-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dc023-188">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dc023-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dc023-189">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc023-189">Create an Azure AD test user</span></span>

<span data-ttu-id="dc023-190">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc023-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="dc023-192">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="dc023-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc023-193">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="dc023-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="dc023-195">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="dc023-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="dc023-197">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc023-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="dc023-199">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc023-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="dc023-201">a.</span><span class="sxs-lookup"><span data-stu-id="dc023-201">a.</span></span> <span data-ttu-id="dc023-202">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc023-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc023-203">b.</span><span class="sxs-lookup"><span data-stu-id="dc023-203">b.</span></span> <span data-ttu-id="dc023-204">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc023-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="dc023-205">c.</span><span class="sxs-lookup"><span data-stu-id="dc023-205">c.</span></span> <span data-ttu-id="dc023-206">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="dc023-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="dc023-207">d.</span><span class="sxs-lookup"><span data-stu-id="dc023-207">d.</span></span> <span data-ttu-id="dc023-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="dc023-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="dc023-209">Criar um usuário de teste do Zoho</span><span class="sxs-lookup"><span data-stu-id="dc023-209">Create a Zoho test user</span></span>

<span data-ttu-id="dc023-210">Ordem tooenable AD do Azure usuários toolog no Zoho Mail, eles devem ser provisionados no Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="dc023-210">In order tooenable Azure AD users toolog into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="dc023-211">No caso de saudação do Zoho Mail, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="dc023-211">In hello case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="dc023-212">Você pode usar qualquer ferramenta de criação outros Zoho Mail usuário conta ou APIs fornecidas pelo Zoho Mail tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="dc023-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail tooprovision AAD user accounts.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="dc023-213">tooprovision uma conta de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc023-213">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="dc023-214">Faça logon no tooyour **Zoho Mail** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="dc023-214">Log in tooyour **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="dc023-215">Vá muito**painel de controle \> Mail & documentos**.</span><span class="sxs-lookup"><span data-stu-id="dc023-215">Go too**Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="dc023-216">Vá muito**detalhes do usuário \> adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="dc023-216">Go too**User Details \> Add User**.</span></span>
   
    <span data-ttu-id="dc023-217">![Adicionar Usuário](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="dc023-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="dc023-218">Em Olá **adicionar usuários** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc023-218">On hello **Add users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="dc023-219">![Adicionar Usuário](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="dc023-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="dc023-220">a.</span><span class="sxs-lookup"><span data-stu-id="dc023-220">a.</span></span> <span data-ttu-id="dc023-221">Em Olá **nome** caixa de texto, tipo hello primeiro nome do usuário, como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="dc023-221">In hello **First Name** textbox, type hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="dc023-222">b.</span><span class="sxs-lookup"><span data-stu-id="dc023-222">b.</span></span> <span data-ttu-id="dc023-223">Em Olá **Sobrenome** caixa de texto, digite Olá sobrenome do usuário como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="dc023-223">In hello **Last Name** textbox, type hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="dc023-224">c.</span><span class="sxs-lookup"><span data-stu-id="dc023-224">c.</span></span> <span data-ttu-id="dc023-225">Em Olá **ID de Email** caixa de texto, id de email do tipo saudação do usuário como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="dc023-225">In hello **Email ID** textbox, type hello email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="dc023-226">d.</span><span class="sxs-lookup"><span data-stu-id="dc023-226">d.</span></span> <span data-ttu-id="dc023-227">Em Olá **senha** caixa de texto, digite a senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="dc023-227">In hello **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="dc023-228">e.</span><span class="sxs-lookup"><span data-stu-id="dc023-228">e.</span></span> <span data-ttu-id="dc023-229">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc023-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="dc023-230">proprietário de conta do Active Directory do Azure Olá receberá um email com uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="dc023-230">hello Azure Active Directory account holder will receive an email with a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="dc023-231">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dc023-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="dc023-232">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooZoho.</span><span class="sxs-lookup"><span data-stu-id="dc023-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoho.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="dc023-234">**tooassign Britta Simon tooZoho, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="dc023-234">**tooassign Britta Simon tooZoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc023-235">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="dc023-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="dc023-237">Na lista de aplicativos hello, selecione **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="dc023-237">In hello applications list, select **Zoho**.</span></span>

    ![link de Zoho Olá na lista de aplicativos Olá](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="dc023-239">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="dc023-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="dc023-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dc023-241">Click **Add** button.</span></span> <span data-ttu-id="dc023-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc023-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="dc023-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc023-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dc023-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc023-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc023-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc023-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dc023-247">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="dc023-247">Test single sign-on</span></span>

<span data-ttu-id="dc023-248">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc023-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dc023-249">Quando você clica em bloco Zoho Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Zoho aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dc023-249">When you click hello Zoho tile in hello Access Panel, you should get automatically signed-on tooyour Zoho application.</span></span>
<span data-ttu-id="dc023-250">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dc023-250">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dc023-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="dc023-251">Additional resources</span></span>

* [<span data-ttu-id="dc023-252">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="dc023-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc023-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc023-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

