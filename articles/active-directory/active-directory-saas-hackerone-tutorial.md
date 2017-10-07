---
title: "Tutorial: integração do Azure Active Directory ao HackerOne | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Hackerone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: c9dc033e26e79a7233dcfb3899c62684d4a19652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="2c9d1-103">Tutorial: Integração do Azure Active Directory ao HackerOne</span><span class="sxs-lookup"><span data-stu-id="2c9d1-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="2c9d1-104">Neste tutorial, você aprenderá como toointegrate HackerOne com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="2c9d1-104">In this tutorial, you learn how toointegrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2c9d1-105">Integrando HackerOne com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c9d1-105">Integrating HackerOne with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2c9d1-106">Você pode controlar no AD do Azure que tenha acesso tooHackerOne</span><span class="sxs-lookup"><span data-stu-id="2c9d1-106">You can control in Azure AD who has access tooHackerOne</span></span>
- <span data-ttu-id="2c9d1-107">Você pode habilitar seu usuários tooautomatically get conectado tooHackerOne (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2c9d1-107">You can enable your users tooautomatically get signed-on tooHackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2c9d1-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2c9d1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2c9d1-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2c9d1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c9d1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2c9d1-110">Prerequisites</span></span>

<span data-ttu-id="2c9d1-111">tooconfigure integração do AD do Azure com HackerOne, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c9d1-111">tooconfigure Azure AD integration with HackerOne, you need hello following items:</span></span>

- <span data-ttu-id="2c9d1-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2c9d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2c9d1-113">Uma assinatura habilitada para logon único do HackerOne</span><span class="sxs-lookup"><span data-stu-id="2c9d1-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2c9d1-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2c9d1-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2c9d1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2c9d1-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2c9d1-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2c9d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2c9d1-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2c9d1-118">Scenario description</span></span>
<span data-ttu-id="2c9d1-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2c9d1-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="2c9d1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2c9d1-121">Adicionando HackerOne da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2c9d1-121">Adding HackerOne from hello gallery</span></span>
2. <span data-ttu-id="2c9d1-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2c9d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-hello-gallery"></a><span data-ttu-id="2c9d1-123">Adicionando HackerOne da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2c9d1-123">Adding HackerOne from hello gallery</span></span>
<span data-ttu-id="2c9d1-124">integração de saudação tooconfigure de HackerOne no AD do Azure, você precisa tooadd HackerOne da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-124">tooconfigure hello integration of HackerOne into Azure AD, you need tooadd HackerOne from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2c9d1-125">**tooadd HackerOne da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2c9d1-125">**tooadd HackerOne from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c9d1-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2c9d1-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2c9d1-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="2c9d1-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="2c9d1-133">Na caixa de pesquisa hello, digite **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-133">In hello search box, type **HackerOne**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="2c9d1-135">No painel de resultados de saudação, selecione **HackerOne**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-135">In hello results panel, select **HackerOne**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2c9d1-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2c9d1-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="2c9d1-138">Nesta seção, você configurará e testará o logon único do Azure AD com o HackerOne, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="2c9d1-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2c9d1-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em HackerOne é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HackerOne is tooa user in Azure AD.</span></span> <span data-ttu-id="2c9d1-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em HackerOne precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-140">In other words, a link relationship between an Azure AD user and hello related user in HackerOne needs toobe established.</span></span>

<span data-ttu-id="2c9d1-141">HackerOne, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-141">In HackerOne, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2c9d1-142">tooconfigure e teste de logon único do AD do Azure com HackerOne, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c9d1-142">tooconfigure and test Azure AD single sign-on with HackerOne, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2c9d1-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2c9d1-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2c9d1-145">**[Criar um usuário de teste HackerOne](#creating-a-hackerone-test-user)**  -toohave um equivalente do Britta Simon em HackerOne é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - toohave a counterpart of Britta Simon in HackerOne that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2c9d1-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2c9d1-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2c9d1-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c9d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2c9d1-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo HackerOne.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="2c9d1-150">**tooconfigure AD do Azure-logon único com HackerOne, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2c9d1-150">**tooconfigure Azure AD single sign-on with HackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c9d1-151">Em Olá portal do Azure, Olá **HackerOne** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-151">In hello Azure portal, on hello **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2c9d1-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="2c9d1-155">Em Olá **HackerOne única URL de logon e o identificador** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c9d1-155">On hello **HackerOne Single sign-on URL and Identifier** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="2c9d1-157">a.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-157">a.</span></span> <span data-ttu-id="2c9d1-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="2c9d1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="2c9d1-159">b.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-159">b.</span></span> <span data-ttu-id="2c9d1-160">Em Olá **identificador** caixa de texto, digite um URL como:`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="2c9d1-160">In hello **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="2c9d1-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-161">This value is not real.</span></span> <span data-ttu-id="2c9d1-162">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="2c9d1-163">Entre em contato com [HackerOne a equipe de suporte](mailto:support@hackerone.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-163">Contact [HackerOne support team](mailto:support@hackerone.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="2c9d1-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="2c9d1-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2c9d1-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2c9d1-168">Em Olá **HackerOne configuração** seção, clique em **configurar HackerOne** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-168">On hello **HackerOne Configuration** section, click **Configure HackerOne** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2c9d1-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="2c9d1-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="2c9d1-171">Logon o tooyour HackerOne locatário como um administrador.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-171">Sign On tooyour HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="2c9d1-172">No menu de saudação na parte superior do hello, clique hello "**configurações**."</span><span class="sxs-lookup"><span data-stu-id="2c9d1-172">In hello menu on hello top, click hello "**Settings**."</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="2c9d1-174">Navegue muito"**autenticação**"e clique em"**adicionar configurações SAML**."</span><span class="sxs-lookup"><span data-stu-id="2c9d1-174">Navigate too"**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="2c9d1-176">Em Olá **configurações SAML** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c9d1-176">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="2c9d1-178">a.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-178">a.</span></span> <span data-ttu-id="2c9d1-179">Em Olá **domínio de Email** caixa de texto, digite um domínio registrado.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-179">In hello **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="2c9d1-180">b.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-180">b.</span></span> <span data-ttu-id="2c9d1-181">Em **URL de logon único** caixas de texto, cole o valor de saudação do **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-181">In  **Single Sign On URL** textboxes, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2c9d1-182">c.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-182">c.</span></span> <span data-ttu-id="2c9d1-183">Abra o **arquivo de certificado** no bloco de notas baixado do portal do Azure, copie o conteúdo de saudação para sua área de transferência e, em seguida, cole-o toohello **certificado X509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="2c9d1-184">d.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-184">d.</span></span> <span data-ttu-id="2c9d1-185">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-185">Click **Save**.</span></span>

11. <span data-ttu-id="2c9d1-186">Na caixa de diálogo de configurações de autenticação hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c9d1-186">On hello Authentication Settings dialog, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="2c9d1-188">a.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-188">a.</span></span> <span data-ttu-id="2c9d1-189">Clique em **Executar teste**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-189">Click **Run test**.</span></span>

    <span data-ttu-id="2c9d1-190">b.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-190">b.</span></span> <span data-ttu-id="2c9d1-191">Se Olá valor Olá **Status** campo é igual a **último status do teste: criado**, entre em contato com seu [HackerOne a equipe de suporte](mailto:support@hackerone.com) toorequest uma revisão da sua configuração.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-191">If hello value of hello **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) toorequest a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="2c9d1-192">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="2c9d1-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2c9d1-193">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2c9d1-194">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2c9d1-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2c9d1-195">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2c9d1-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="2c9d1-196">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="2c9d1-198">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2c9d1-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c9d1-199">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2c9d1-201">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2c9d1-203">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2c9d1-205">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c9d1-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2c9d1-207">a.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-207">a.</span></span> <span data-ttu-id="2c9d1-208">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2c9d1-209">b.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-209">b.</span></span> <span data-ttu-id="2c9d1-210">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2c9d1-211">c.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-211">c.</span></span> <span data-ttu-id="2c9d1-212">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2c9d1-213">d.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-213">d.</span></span> <span data-ttu-id="2c9d1-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="2c9d1-215">Criação de um usuário de teste do HackerOne</span><span class="sxs-lookup"><span data-stu-id="2c9d1-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="2c9d1-216">Em seguida, você criará um usuário chamado Brenda Fernandes no HackerOne.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="2c9d1-217">O HackerOne dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="2c9d1-218">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-218">There is no action item for you in this section.</span></span> <span data-ttu-id="2c9d1-219">Quando você acessar HackerOne, um novo usuário será criado caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="2c9d1-220">Se você precisar toocreate um usuário manualmente, é necessário a equipe de suporte de certificar toocontact hello.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-220">If you need toocreate a user manually, you need toocontact hello Certify support team.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2c9d1-221">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2c9d1-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2c9d1-222">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHackerOne.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHackerOne.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="2c9d1-224">**tooassign Britta Simon tooHackerOne, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2c9d1-224">**tooassign Britta Simon tooHackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c9d1-225">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2c9d1-227">Na lista de aplicativos hello, selecione **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-227">In hello applications list, select **HackerOne**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="2c9d1-229">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="2c9d1-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-231">Click **Add** button.</span></span> <span data-ttu-id="2c9d1-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="2c9d1-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2c9d1-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2c9d1-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2c9d1-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="2c9d1-237">Testing single sign-on</span></span>

<span data-ttu-id="2c9d1-238">Por fim, você pode testar seu AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-238">Finally, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="2c9d1-239">Quando você clica em bloco HackerOne Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour HackerOne aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c9d1-239">When you click hello HackerOne tile in hello Access Panel, you should get automatically signed-on tooyour HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2c9d1-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2c9d1-240">Additional resources</span></span>

* [<span data-ttu-id="2c9d1-241">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2c9d1-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2c9d1-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2c9d1-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

