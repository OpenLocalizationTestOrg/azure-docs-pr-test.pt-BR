---
title: "Tutorial: Integração do Azure Active Directory ao Egnyte | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Egnyte."
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
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="039c8-103">Tutorial: integração do Active Directory do Azure ao Egnyte</span><span class="sxs-lookup"><span data-stu-id="039c8-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="039c8-104">Neste tutorial, você aprenderá como toointegrate Egnyte com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="039c8-104">In this tutorial, you learn how toointegrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="039c8-105">Integrando o Egnyte com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="039c8-105">Integrating Egnyte with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="039c8-106">Você pode controlar no AD do Azure que tenha acesso tooEgnyte</span><span class="sxs-lookup"><span data-stu-id="039c8-106">You can control in Azure AD who has access tooEgnyte</span></span>
- <span data-ttu-id="039c8-107">Você pode habilitar seu usuários tooautomatically get conectado tooEgnyte (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="039c8-107">You can enable your users tooautomatically get signed-on tooEgnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="039c8-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="039c8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="039c8-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="039c8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="039c8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="039c8-110">Prerequisites</span></span>

<span data-ttu-id="039c8-111">tooconfigure integração do AD do Azure com o Egnyte, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="039c8-111">tooconfigure Azure AD integration with Egnyte, you need hello following items:</span></span>

- <span data-ttu-id="039c8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="039c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="039c8-113">Uma assinatura habilitada para logon único do Egnyte</span><span class="sxs-lookup"><span data-stu-id="039c8-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="039c8-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="039c8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="039c8-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="039c8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="039c8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="039c8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="039c8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="039c8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="039c8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="039c8-118">Scenario description</span></span>
<span data-ttu-id="039c8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="039c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="039c8-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="039c8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="039c8-121">Adicionando Egnyte da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="039c8-121">Adding Egnyte from hello gallery</span></span>
2. <span data-ttu-id="039c8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="039c8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-hello-gallery"></a><span data-ttu-id="039c8-123">Adicionando Egnyte da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="039c8-123">Adding Egnyte from hello gallery</span></span>
<span data-ttu-id="039c8-124">integração de saudação tooconfigure do Egnyte no AD do Azure, você precisa tooadd Egnyte da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="039c8-124">tooconfigure hello integration of Egnyte into Azure AD, you need tooadd Egnyte from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="039c8-125">**tooadd Egnyte da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="039c8-125">**tooadd Egnyte from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="039c8-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="039c8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="039c8-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="039c8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="039c8-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="039c8-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="039c8-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="039c8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="039c8-133">Na caixa de pesquisa hello, digite **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="039c8-133">In hello search box, type **Egnyte**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="039c8-135">No painel de resultados de saudação, selecione **Egnyte**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="039c8-135">In hello results panel, select **Egnyte**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="039c8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="039c8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="039c8-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Egnyte com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="039c8-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="039c8-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Egnyte é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="039c8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Egnyte is tooa user in Azure AD.</span></span> <span data-ttu-id="039c8-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Egnyte precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="039c8-140">In other words, a link relationship between an Azure AD user and hello related user in Egnyte needs toobe established.</span></span>

<span data-ttu-id="039c8-141">No Egnyte, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="039c8-141">In Egnyte, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="039c8-142">tooconfigure e teste de logon único do AD do Azure com o Egnyte, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="039c8-142">tooconfigure and test Azure AD single sign-on with Egnyte, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="039c8-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="039c8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="039c8-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="039c8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="039c8-145">**[Criar um usuário de teste do Egnyte](#creating-an-egnyte-test-user)**  -toohave um equivalente do Britta Simon no Egnyte é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="039c8-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - toohave a counterpart of Britta Simon in Egnyte that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="039c8-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="039c8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="039c8-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="039c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="039c8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="039c8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="039c8-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Egnyte.</span><span class="sxs-lookup"><span data-stu-id="039c8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="039c8-150">**tooconfigure AD do Azure-logon único com o Egnyte, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="039c8-150">**tooconfigure Azure AD single sign-on with Egnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="039c8-151">Em Olá portal do Azure, Olá **Egnyte** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="039c8-151">In hello Azure portal, on hello **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="039c8-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="039c8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="039c8-155">Em Olá **Egnyte domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="039c8-155">On hello **Egnyte Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="039c8-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="039c8-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="039c8-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="039c8-158">This value is not real.</span></span> <span data-ttu-id="039c8-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="039c8-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="039c8-160">Entre em contato com [equipe de suporte do cliente do Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="039c8-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="039c8-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="039c8-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="039c8-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="039c8-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="039c8-165">Em Olá **Egnyte configuração** seção, clique em **configurar Egnyte** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="039c8-165">On hello **Egnyte Configuration** section, click **Configure Egnyte** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="039c8-166">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="039c8-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="039c8-168">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Egnyte como um administrador.</span><span class="sxs-lookup"><span data-stu-id="039c8-168">In a different web browser window, log in tooyour Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="039c8-169">Clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="039c8-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="039c8-170">![Configurações](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="039c8-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="039c8-171">No menu de saudação, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="039c8-171">In hello menu, click **Settings**.</span></span>

   <span data-ttu-id="039c8-172">![Configurações](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="039c8-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="039c8-173">Clique em Olá **configuração** guia e, em seguida, clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="039c8-173">Click hello **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="039c8-174">![Segurança](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="039c8-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="039c8-175">Em Olá **autenticação de logon único** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="039c8-175">In hello **Single Sign-On Authentication** section, perform hello following steps:</span></span>

    <span data-ttu-id="039c8-176">![Autenticação de Logon Único](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Autenticação de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="039c8-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="039c8-177">a.</span><span class="sxs-lookup"><span data-stu-id="039c8-177">a.</span></span> <span data-ttu-id="039c8-178">Para **Autenticação de logon único**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="039c8-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="039c8-179">b.</span><span class="sxs-lookup"><span data-stu-id="039c8-179">b.</span></span> <span data-ttu-id="039c8-180">Para **Provedor de identidade**, selecione **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="039c8-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="039c8-181">c.</span><span class="sxs-lookup"><span data-stu-id="039c8-181">c.</span></span> <span data-ttu-id="039c8-182">Colar **Single Sign-On URL do serviço SAML** copiada do portal do Azure em Olá **URL de logon do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="039c8-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into hello **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="039c8-183">d.</span><span class="sxs-lookup"><span data-stu-id="039c8-183">d.</span></span> <span data-ttu-id="039c8-184">Colar **ID da entidade SAML** que você copiou do portal do Azure em Olá **ID de entidade do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="039c8-184">Paste **SAML Entity ID** which you have copied from Azure portal into hello **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="039c8-185">e.</span><span class="sxs-lookup"><span data-stu-id="039c8-185">e.</span></span> <span data-ttu-id="039c8-186">Abra seu certificado codificado em base 64 no bloco de notas que baixou do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="039c8-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="039c8-187">f.</span><span class="sxs-lookup"><span data-stu-id="039c8-187">f.</span></span> <span data-ttu-id="039c8-188">Para **Mapeamento de usuário padrão**, selecione **Endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="039c8-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="039c8-189">g.</span><span class="sxs-lookup"><span data-stu-id="039c8-189">g.</span></span> <span data-ttu-id="039c8-190">Para **Usar valor do emissor específico do domínio**, selecione **desabilitado**.</span><span class="sxs-lookup"><span data-stu-id="039c8-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="039c8-191">h.</span><span class="sxs-lookup"><span data-stu-id="039c8-191">h.</span></span> <span data-ttu-id="039c8-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="039c8-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="039c8-193">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="039c8-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="039c8-194">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="039c8-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="039c8-195">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="039c8-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="039c8-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="039c8-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="039c8-197">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="039c8-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="039c8-199">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="039c8-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="039c8-200">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="039c8-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="039c8-202">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="039c8-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="039c8-204">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="039c8-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="039c8-206">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="039c8-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="039c8-208">a.</span><span class="sxs-lookup"><span data-stu-id="039c8-208">a.</span></span> <span data-ttu-id="039c8-209">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="039c8-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="039c8-210">b.</span><span class="sxs-lookup"><span data-stu-id="039c8-210">b.</span></span> <span data-ttu-id="039c8-211">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="039c8-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="039c8-212">c.</span><span class="sxs-lookup"><span data-stu-id="039c8-212">c.</span></span> <span data-ttu-id="039c8-213">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="039c8-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="039c8-214">d.</span><span class="sxs-lookup"><span data-stu-id="039c8-214">d.</span></span> <span data-ttu-id="039c8-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="039c8-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="039c8-216">Como criar um usuário de teste do Egnyte</span><span class="sxs-lookup"><span data-stu-id="039c8-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="039c8-217">tooenable AD do Azure usuários toolog em tooEgnyte, eles devem ser provisionados no Egnyte.</span><span class="sxs-lookup"><span data-stu-id="039c8-217">tooenable Azure AD users toolog in tooEgnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="039c8-218">No caso de saudação do Egnyte, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="039c8-218">In hello case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="039c8-219">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="039c8-219">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="039c8-220">Faça logon no tooyour **Egnyte** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="039c8-220">Log in tooyour **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="039c8-221">Vá muito**configurações \> usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="039c8-221">Go too**Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="039c8-222">Clique em **adicionar novo usuário**e, em seguida, selecione o tipo de saudação do usuário que você deseja tooadd.</span><span class="sxs-lookup"><span data-stu-id="039c8-222">Click **Add New User**, and then select hello type of user you want tooadd.</span></span>
   
   <span data-ttu-id="039c8-223">![Usuários](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="039c8-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="039c8-224">Em Olá **novo usuário padrão** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="039c8-224">In hello **New Standard User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="039c8-225">![Novo Usuário Padrão](./media/active-directory-saas-egnyte-tutorial/ic787825.png "Novo Usuário Padrão")</span><span class="sxs-lookup"><span data-stu-id="039c8-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="039c8-226">a.</span><span class="sxs-lookup"><span data-stu-id="039c8-226">a.</span></span> <span data-ttu-id="039c8-227">Saudação de tipo **Email**, **nome de usuário**e outros detalhes de uma conta válida do Active Directory do Azure você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="039c8-227">Type hello **Email**, **Username**, and other details of a valid Azure Active Directory account you want tooprovision.</span></span>
   
   <span data-ttu-id="039c8-228">b.</span><span class="sxs-lookup"><span data-stu-id="039c8-228">b.</span></span> <span data-ttu-id="039c8-229">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="039c8-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="039c8-230">proprietário de conta do Active Directory do Azure Olá receberá um email de notificação.</span><span class="sxs-lookup"><span data-stu-id="039c8-230">hello Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="039c8-231">Você pode usar qualquer ferramenta de criação outros Egnyte usuário conta ou APIs fornecidas pelo Egnyte tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="039c8-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="039c8-232">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="039c8-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="039c8-233">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooEgnyte.</span><span class="sxs-lookup"><span data-stu-id="039c8-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEgnyte.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="039c8-235">**tooassign Britta Simon tooEgnyte, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="039c8-235">**tooassign Britta Simon tooEgnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="039c8-236">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="039c8-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="039c8-238">Na lista de aplicativos hello, selecione **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="039c8-238">In hello applications list, select **Egnyte**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="039c8-240">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="039c8-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="039c8-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="039c8-242">Click **Add** button.</span></span> <span data-ttu-id="039c8-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="039c8-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="039c8-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="039c8-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="039c8-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="039c8-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="039c8-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="039c8-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="039c8-248">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="039c8-248">Testing single sign-on</span></span>

<span data-ttu-id="039c8-249">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="039c8-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="039c8-250">Quando você clica em bloco Egnyte Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Egnyte aplicativo.</span><span class="sxs-lookup"><span data-stu-id="039c8-250">When you click hello Egnyte tile in hello Access Panel, you should get automatically signed-on tooyour Egnyte application.</span></span>
<span data-ttu-id="039c8-251">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="039c8-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="039c8-252">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="039c8-252">Additional resources</span></span>

* [<span data-ttu-id="039c8-253">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="039c8-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="039c8-254">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="039c8-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

