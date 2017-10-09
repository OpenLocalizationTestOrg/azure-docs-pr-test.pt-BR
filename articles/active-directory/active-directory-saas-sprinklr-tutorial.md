---
title: "Tutorial: Integração do Azure Active Directory ao Sprinklr | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="1051a-103">Tutorial: Integração do Active Directory do Azure com o Sprinklr</span><span class="sxs-lookup"><span data-stu-id="1051a-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="1051a-104">Neste tutorial, você aprenderá como toointegrate Sprinklr com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="1051a-104">In this tutorial, you learn how toointegrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1051a-105">Integrando o Sprinklr com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="1051a-105">Integrating Sprinklr with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1051a-106">Você pode controlar no AD do Azure que tenha acesso tooSprinklr</span><span class="sxs-lookup"><span data-stu-id="1051a-106">You can control in Azure AD who has access tooSprinklr</span></span>
- <span data-ttu-id="1051a-107">Você pode habilitar seu usuários tooautomatically get conectado tooSprinklr (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1051a-107">You can enable your users tooautomatically get signed-on tooSprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1051a-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1051a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1051a-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1051a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1051a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1051a-110">Prerequisites</span></span>

<span data-ttu-id="1051a-111">tooconfigure integração do AD do Azure com o Sprinklr, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1051a-111">tooconfigure Azure AD integration with Sprinklr, you need hello following items:</span></span>

- <span data-ttu-id="1051a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1051a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1051a-113">Uma assinatura habilitada para logon único do Sprinklr</span><span class="sxs-lookup"><span data-stu-id="1051a-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1051a-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1051a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1051a-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1051a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1051a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1051a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1051a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1051a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1051a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1051a-118">Scenario description</span></span>
<span data-ttu-id="1051a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1051a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1051a-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="1051a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1051a-121">Adicionando Sprinklr da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1051a-121">Adding Sprinklr from hello gallery</span></span>
2. <span data-ttu-id="1051a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1051a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-hello-gallery"></a><span data-ttu-id="1051a-123">Adicionando Sprinklr da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1051a-123">Adding Sprinklr from hello gallery</span></span>
<span data-ttu-id="1051a-124">integração de saudação tooconfigure do Sprinklr no AD do Azure, você precisa tooadd Sprinklr da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1051a-124">tooconfigure hello integration of Sprinklr into Azure AD, you need tooadd Sprinklr from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1051a-125">**tooadd Sprinklr da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1051a-125">**tooadd Sprinklr from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1051a-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1051a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1051a-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1051a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1051a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1051a-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1051a-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1051a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1051a-133">Na caixa de pesquisa hello, digite **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="1051a-133">In hello search box, type **Sprinklr**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="1051a-135">No painel de resultados de saudação, selecione **Sprinklr**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1051a-135">In hello results panel, select **Sprinklr**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1051a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1051a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1051a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Sprinklr, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1051a-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1051a-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá sprinklr é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1051a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sprinklr is tooa user in Azure AD.</span></span> <span data-ttu-id="1051a-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação sprinklr precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1051a-140">In other words, a link relationship between an Azure AD user and hello related user in Sprinklr needs toobe established.</span></span>

<span data-ttu-id="1051a-141">Sprinklr, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="1051a-141">In Sprinklr, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1051a-142">tooconfigure e teste de logon único do AD do Azure com o Sprinklr, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="1051a-142">tooconfigure and test Azure AD single sign-on with Sprinklr, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1051a-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1051a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1051a-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1051a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1051a-145">**[Criar um usuário de teste do Sprinklr](#creating-a-sprinklr-test-user)**  -toohave um equivalente de Britta Simon sprinklr é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="1051a-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - toohave a counterpart of Britta Simon in Sprinklr that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1051a-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="1051a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1051a-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="1051a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1051a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1051a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1051a-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="1051a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="1051a-150">**tooconfigure AD do Azure-logon único com o Sprinklr, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1051a-150">**tooconfigure Azure AD single sign-on with Sprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="1051a-151">Em Olá portal do Azure, Olá **Sprinklr** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="1051a-151">In hello Azure portal, on hello **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1051a-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="1051a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="1051a-155">Em Olá **Sprinklr domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1051a-155">On hello **Sprinklr Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="1051a-157">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-157">a.</span></span> <span data-ttu-id="1051a-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="1051a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="1051a-159">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-159">b.</span></span> <span data-ttu-id="1051a-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="1051a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1051a-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="1051a-161">These values are not real.</span></span> <span data-ttu-id="1051a-162">Atualize o valor de saudação com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="1051a-162">Update hello value with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1051a-163">Entre em contato com [equipe de suporte do cliente Sprinklr](https://www.sprinklr.com/contact-us/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="1051a-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="1051a-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1051a-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="1051a-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1051a-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1051a-168">Em Olá **Sprinklr configuração** seção, clique em **configurar Sprinklr** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="1051a-168">On hello **Sprinklr Configuration** section, click **Configure Sprinklr** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1051a-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="1051a-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

7. <span data-ttu-id="1051a-170">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Sprinklr como um administrador.</span><span class="sxs-lookup"><span data-stu-id="1051a-170">In a different web browser window, log in tooyour Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="1051a-171">Vá muito**administração \> configurações**.</span><span class="sxs-lookup"><span data-stu-id="1051a-171">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="1051a-172">![Administração](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="1051a-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="1051a-173">Vá muito**gerenciar parceiro \> o logon único** no painel esquerdo do hello.</span><span class="sxs-lookup"><span data-stu-id="1051a-173">Go too**Manage Partner \> Single Sign** on from hello left pane.</span></span>
   
    <span data-ttu-id="1051a-174">![Gerenciar Parceiro](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Gerenciar Parceiro")</span><span class="sxs-lookup"><span data-stu-id="1051a-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="1051a-175">Clique em **+Adicionar Logons Únicos**.</span><span class="sxs-lookup"><span data-stu-id="1051a-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="1051a-176">![Logons Únicos](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Logons Únicos")</span><span class="sxs-lookup"><span data-stu-id="1051a-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="1051a-177">Em Olá **de logon único** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1051a-177">On hello **Single Sign on** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="1051a-178">![Logons Únicos](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Logons Únicos")</span><span class="sxs-lookup"><span data-stu-id="1051a-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="1051a-179">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-179">a.</span></span> <span data-ttu-id="1051a-180">Em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="1051a-180">In hello **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="1051a-181">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-181">b.</span></span> <span data-ttu-id="1051a-182">Selecione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="1051a-182">Select **Enabled**.</span></span>

    <span data-ttu-id="1051a-183">c.</span><span class="sxs-lookup"><span data-stu-id="1051a-183">c.</span></span> <span data-ttu-id="1051a-184">Selecione **Usar novo Certificado de SSO**.</span><span class="sxs-lookup"><span data-stu-id="1051a-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="1051a-185">e.</span><span class="sxs-lookup"><span data-stu-id="1051a-185">e.</span></span> <span data-ttu-id="1051a-186">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1051a-186">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="1051a-187">f.</span><span class="sxs-lookup"><span data-stu-id="1051a-187">f.</span></span> <span data-ttu-id="1051a-188">Saudação de colar **ID da entidade SAML** valor que você copiou do Portal do Azure em Olá **Id da entidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1051a-188">Paste hello **SAML Entity ID** value which you have copied from Azure Portal into hello **Entity Id** textbox.</span></span>

    <span data-ttu-id="1051a-189">g.</span><span class="sxs-lookup"><span data-stu-id="1051a-189">g.</span></span> <span data-ttu-id="1051a-190">Saudação de colar **Single Sign-On URL do serviço SAML** valor que você copiou do Portal do Azure em Olá **URL de logon do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1051a-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="1051a-191">h.</span><span class="sxs-lookup"><span data-stu-id="1051a-191">h.</span></span> <span data-ttu-id="1051a-192">Saudação de colar **URL de logout** valor que você copiou do Portal do Azure em Olá **URL de Logout do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1051a-192">Paste hello **Sign-Out URL** value which you have copied from Azure Portal into hello **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="1051a-193">i.</span><span class="sxs-lookup"><span data-stu-id="1051a-193">i.</span></span> <span data-ttu-id="1051a-194">Para **Tipo de ID de Usuário do SAML**, selecione **A declaração contém o nome de usuário de sprinklr.com do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="1051a-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="1051a-195">j.</span><span class="sxs-lookup"><span data-stu-id="1051a-195">j.</span></span> <span data-ttu-id="1051a-196">Como **local de ID de usuário SAML**, selecione **ID de usuário está no elemento de identificador de nome de saudação do hello declaração assunto**.</span><span class="sxs-lookup"><span data-stu-id="1051a-196">As **SAML User ID Location**, select **User ID is in hello Name Identifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="1051a-197">k.</span><span class="sxs-lookup"><span data-stu-id="1051a-197">k.</span></span> <span data-ttu-id="1051a-198">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1051a-198">Click **Save**.</span></span>
       
    <span data-ttu-id="1051a-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="1051a-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="1051a-200">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="1051a-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1051a-201">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="1051a-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1051a-202">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1051a-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1051a-203">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1051a-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="1051a-204">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1051a-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1051a-206">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1051a-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1051a-207">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1051a-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1051a-209">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="1051a-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1051a-211">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1051a-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1051a-213">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1051a-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1051a-215">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-215">a.</span></span> <span data-ttu-id="1051a-216">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1051a-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1051a-217">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-217">b.</span></span> <span data-ttu-id="1051a-218">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1051a-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1051a-219">c.</span><span class="sxs-lookup"><span data-stu-id="1051a-219">c.</span></span> <span data-ttu-id="1051a-220">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="1051a-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1051a-221">d.</span><span class="sxs-lookup"><span data-stu-id="1051a-221">d.</span></span> <span data-ttu-id="1051a-222">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1051a-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="1051a-223">Criar um usuário de teste do Sprinklr</span><span class="sxs-lookup"><span data-stu-id="1051a-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="1051a-224">Faça logon no tooyour site da empresa Sprinklr como um administrador.</span><span class="sxs-lookup"><span data-stu-id="1051a-224">Log in tooyour Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="1051a-225">Vá muito**administração \> configurações**.</span><span class="sxs-lookup"><span data-stu-id="1051a-225">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="1051a-226">![Administração](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="1051a-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="1051a-227">Vá muito**gerenciar cliente \> usuários** no painel esquerdo do hello.</span><span class="sxs-lookup"><span data-stu-id="1051a-227">Go too**Manage Client \> Users** from hello left pane.</span></span>
   
    <span data-ttu-id="1051a-228">![Configurações](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="1051a-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="1051a-229">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="1051a-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="1051a-230">![Configurações](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="1051a-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="1051a-231">Em Olá **Editar usuário** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1051a-231">On hello **Edit user** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="1051a-232">![Editar usuário](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Editar usuário")</span><span class="sxs-lookup"><span data-stu-id="1051a-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="1051a-233">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-233">a.</span></span> <span data-ttu-id="1051a-234">Em Olá **Email**, **nome** e **Sobrenome** caixas de texto, informações de saudação do tipo de uma conta de usuário do AD do Azure você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="1051a-234">In hello **Email**, **First Name** and **Last Name** textboxes, type hello information of an Azure AD user account you want tooprovision.</span></span>

    <span data-ttu-id="1051a-235">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-235">b.</span></span> <span data-ttu-id="1051a-236">Selecione **Senha Desabilitada**.</span><span class="sxs-lookup"><span data-stu-id="1051a-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="1051a-237">c.</span><span class="sxs-lookup"><span data-stu-id="1051a-237">c.</span></span> <span data-ttu-id="1051a-238">Selecione **Idioma**.</span><span class="sxs-lookup"><span data-stu-id="1051a-238">Select **Language**.</span></span>

    <span data-ttu-id="1051a-239">d.</span><span class="sxs-lookup"><span data-stu-id="1051a-239">d.</span></span> <span data-ttu-id="1051a-240">Selecione **Tipo de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="1051a-240">Select **User Type**.</span></span>

    <span data-ttu-id="1051a-241">e.</span><span class="sxs-lookup"><span data-stu-id="1051a-241">e.</span></span> <span data-ttu-id="1051a-242">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="1051a-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="1051a-243">**Senha desabilitada** deve ser selecionada tooenable um toolog de usuário por meio de um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="1051a-243">**Password Disabled** must be selected tooenable a user toolog in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="1051a-244">Vá muito**função**e, em seguida, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1051a-244">Go too**Role**, and then perform hello following steps:</span></span>
   
    <span data-ttu-id="1051a-245">![Funções de Parceiro](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Funções de Parceiro")</span><span class="sxs-lookup"><span data-stu-id="1051a-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="1051a-246">a.</span><span class="sxs-lookup"><span data-stu-id="1051a-246">a.</span></span> <span data-ttu-id="1051a-247">De saudação **Global** lista, selecione **todos os\_permissões**.</span><span class="sxs-lookup"><span data-stu-id="1051a-247">From hello **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="1051a-248">b.</span><span class="sxs-lookup"><span data-stu-id="1051a-248">b.</span></span> <span data-ttu-id="1051a-249">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="1051a-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="1051a-250">Você pode usar qualquer ferramenta de criação outros Sprinklr usuário conta ou APIs fornecidas pelo Sprinklr tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1051a-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1051a-251">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1051a-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1051a-252">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSprinklr.</span><span class="sxs-lookup"><span data-stu-id="1051a-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSprinklr.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1051a-254">**tooassign Britta Simon tooSprinklr, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1051a-254">**tooassign Britta Simon tooSprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="1051a-255">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1051a-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1051a-257">Na lista de aplicativos hello, selecione **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="1051a-257">In hello applications list, select **Sprinklr**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="1051a-259">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1051a-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1051a-261">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1051a-261">Click **Add** button.</span></span> <span data-ttu-id="1051a-262">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1051a-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1051a-264">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="1051a-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1051a-265">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1051a-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1051a-266">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1051a-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1051a-267">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1051a-267">Testing single sign-on</span></span>

<span data-ttu-id="1051a-268">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="1051a-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1051a-269">Quando você clica em bloco Sprinklr Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Sprinklr aplicativo para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1051a-269">When you click hello Sprinklr tile in hello Access Panel, you should get automatically signed-on tooyour Sprinklr application For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1051a-270">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1051a-270">Additional resources</span></span>

* [<span data-ttu-id="1051a-271">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1051a-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1051a-272">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1051a-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

